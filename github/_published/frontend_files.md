<!-- -*-Markdown-*- -->

We spend a lot of time optimizing the front end experience at GitHub.  With that said, our asset (css, javascript, images) packaging and serving has evolved to be the best setup I've seen out of any web application I've worked on in my life.

Originally, I was going to package what we have up into a plugin, but realized that much of our asset packaging is specific our particular app architecture and [choice of deployment strategy](http://github.com/blog/470-deployment-script-spring-cleaning).  If you haven't read up on our deployment recipe ***read it now***.  I cannot stress enough how awesome it is to have 14 second no downtime deploys. In any case, you can find the relevant asset bundling code in [this gist](http://gist.github.com/238291)

### Benefits of our asset bundling

* Users never have to wait while the server generates bundle caches, ever. With default Rails bundling, each time you deploy, each request until your server generates the bundle has to wait for the bundle to finish. This makes your site pause for about 30s after each deploy.
* We can use slower asset minifiers (such as YUI or Google Closure) without consequence to our users.
* Adding new stylesheets or javascripts is as easy as creating the file. No need to worry about including a new file in every layout file.
* Because we base our ASSET_ID off our git modified date, we can deploy code updates without forcing users to lose their css/js cache.
* We take full advantage of image caching with SSL while eliminating the unauthenticated mixed content warnings some browsers throw.

Our asset bundling is comprised of several different pieces:

1. A particular css & js file structure
2. Rails helpers to include css & js bundles in production and the corresponding files in development.
3. A rake task to bundle and minify css & javascript as well as the accompanying changes to deploy.rb to make it happen on deploy
4. Tweaks to our Rails environment to use smart ASSET_ID and asset servers

### CSS & JS file layout

Our file layout for CSS & JS is detailed in the [README](http://gist.github.com/238291#file__readme.md) for Javascript, but roughly resembles something like this:

    public/javascripts
    |-- README.md
    |-- admin
    | |-- date.js
    | `-- datePicker.js
    |-- common
    | |-- application.js
    | |-- jquery.facebox.js
    | `-- jquery.relatize_date.js
    |-- dev
    | |-- jquery-1.3.2.js
    | `-- jquery-ui-1.5.3.js
    |-- gist
    | `-- application.js
    |-- github
    | |-- _plugins
    | | |-- jquery.autocomplete.js
    | | `-- jquery.truncate.js
    | |-- application.js
    | |-- blob.js
    | |-- commit.js
    `-- rogue
        |-- farbtastic.js
        |-- iui.js
        `-- s3_upload.js

I like this layout because:

* It allows me to namespace specific files to specific layouts (gist, github.com, iPhone, admin-only layouts, etc) **and** share files between apps (common).
* I can lay out files however I want within each of these namespaces, and reorganize them at will.

Some might say that relying on including everything is bad practice -- but remember that web-based javascript is almost exclusively onDOMReady or later. That means that there is no dependency order problems. If you run into dependency order issues, you're writing javascript wrong.

### Rails Helpers

To help with this new bundle strategy, I've created some Rails helpers to replace your standard `stylesheet_link_tag` and `javascript_include_tag`.  Because of the way we bundle files, it was necessary to use custom helpers. As an added benefit, these helpers are much more robust than the standard Rails helpers.

Here's the code:

<script src="http://gist.github.com/238291.js?file=bundle_helper.rb"></script>

Our `application.html.erb` now looks something like this:

    <%= javascript_dev ['jquery-1.3.2', "#{http_protocol}://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"] %>
    <%= javascript_bundle 'common', 'github' %>

This includes jQuery and all javascript files under `public/javascripts/common` and `public/javascripts/github` (recursively).  Super simple and we probably won't need to change this for a very long time.  We just add files to the relevant directories and they get included magically.

For pages that have heavy javascript load, you can still use the regular `javascript_include_tag` to include these files (we keep them under the `public/javascripts/rogue` directory).

### Bundle rake & deploy tasks

The `javascript_bundle` and `stylesheet_bundle` helpers both assume that in production mode, there'll be a corresponding bundle file.  Since we are proactively generating these files, you need to create these manually on each deploy.

<script src="http://gist.github.com/238291.js?file=bundle.rake"></script>

Throw this into `lib/tasks/bundle.rake` ***and the corresponding YUI & Closure jars*** and then run `rake bundle:all` to generate your javascript.  You can customize this to use the minifying package of your choice.

To make sure this gets run on deploy, you can add this to your deploy.rb:

<script src="http://gist.github.com/238291.js?file=deploy.rb"></script>

### Tweaks to production.rb

The last step in optimizing your asset bundling for deploys is to tweak your production.rb config file to make asset serving a bit smarter.  The relevant bits in our file are:

<script src="http://gist.github.com/238291.js?file=production.rb"></script>

There's three important things going on here.

**First—** If you hit a page using SSL, we serve all assets through SSL.  If you're on Safari, we send all CSS & images non-ssl since Safari doesn't have a mixed content warning.

It is of note that many people [suggest serving CSS & images non-ssl to Firefox](http://37signals.com/svn/posts/1431-mixed-content-warning-how-i-loathe-thee).  This was good practice when Firefox 2.0 was standard, but now that Firefox 3.0 is standard (and obeys cache-control:public as it should) there is no need for this hack.  Firefox does have a mixed content warning (albeit not as prominent as IE), so I choose to use SSL.

**Second—** We're serving assets out of 4 different servers.  This fakes browsers into downloading things faster and is generally good practice.

**Third—** We're hitting the git repo on the server (note our deployment setup) and getting a sha of the last changes to the `public/stylesheets` and `public/javascripts` directory.  We use that sha as the ASSET_ID (the bit that gets tacked on after css/js files as ?sha-here).

This means that if we deploy a change that only affects `app/application.rb` we don't interrupt our user's cache of the javascripts and stylesheets.

### Conclusion

What all of this adds up to is that our deploys have almost no frontend consequence unless they intend to (changing css/js). This is **huge** for a site that does dozens of deploys a day. All browser caches remain the same and there isn't any downtime while we bundle up assets.  It also means we're not afraid to deploy changes that may only affect one line of code and some minor feature.

All of this is not to say there isn't room for improvement in our stack.  I'm still tracking down some SSL bugs, and always trying to cut down on the total CSS, javascript and image load we deliver on every page.