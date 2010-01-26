# The birth of a new feature

I've been pretty quiet around here lately, but that's because I've been spending so much time enjoying [my new job](http://warpspire.com/tipsresources/personal/joining-github/).  One of the best things about the new gig is how little bureaucracy there is.  There's few secrets in the land of GitHub -- ask us what we're working on and we'll let you know.  So I thought it might be interesting to write about how we're building a new feature.

## What feature?

The feature is pretty broad: **code review**. In fact it's hard to call it a feature because it's not really something we can add to a checklist.  Code review is a process that takes many tools to complete.

The thing is, GitHub offers many code review tools as is.  Pull requests notify developers when they have branches ready to merge, issues give you a tool to discuss & track bugs & merge status, and commit/line comments allow you to discuss the code.

But none of this really worked with the flow I was used to.

## GitHub makes git better

Ever since I joined GitHub, [Ryan Tomayko](http://rtomayko) and myself have been talking about how we wish there was a view showing the combination of `git cherry` and `git diff master...` in GitHub.  These two commands have been insanely useful in the past for code reviews.  For example, if you're in a branch called `new-feature` and you run `git cherry -v master` it will show you all *unique* commits in this branch compared to master. Basically what you'd be merging in:

    main_site(new-feature) % git cherry -v master
    + 733e176ea97cfdaf77eb01724ce3abce7adeacb8 Add in context switching widget
    + e859dc59c3bb5147a633a93d8fdc5accb2518ca6 Fake a contexted click-thru page
    + 501123dbc0e3cc942938df513b27fb2fa076897d Add in some descriptive text
    + 7d5acf63df5cd8decb3e63f0eebc9cad19cf8fe8 Improve copy for contexted pages

This is awesomely useful.  It doesn't matter how many times you merge `master` back into `new-feature` -- `git cherry` shows you the unique work to the branch.  Next up is `git diff master...`  which shows you a diff of the unique changes to the `new-feature` branch.

So these two commands give you *why* the branch was created (commit messages) and *how* the branch affects the existing code.  These are the two principle things I want to see when I review someone's branch/changes. But GitHub is about making git *better* - and the output for these commands is fairly ugly.

## Specs are dead, just ship it

We'd been talking about this in campfire for a while, but we were distracted by other issues.  One night I whipped up a quick & dirty comp in Photoshop:

<div class="figure"><img src="/images/posts/code-review/initial_comp.gif" alt="Initial Comp" /></div>

A day or so later, Scott slammed together some code that got the feature off the ground by listing the output of cherry.  Ryan hopped in and cleaned things up to get them to a usable state.  Pretty much at that point we launched the feature to admins only.  At a certain point, I realized that I was using it every day, so we cranked out some simple caching and [let the public in](http://github.com/sinatra/sinatra/compare/0.9.x...master) (assuming you know how to construct the URLs, this works everywhere)

<div class="figure"><img src="/images/posts/code-review/compare_view_now.gif" alt="Compare View right now" /></div>

If you're ever planning out a big feature, I suggest you just start shipping bits of it.  This compare view is not what I had in mind for code review, and it's not complete, but it's a dart thrown in the right direction -- and most importantly it's the minimum viable product (launch early, launch often, even after you're launched).

## Brainstorm, dump & sketch it out

<div class="figure right"><img src="/images/posts/code-review/ramblings.gif" alt="Ramblings" /></div>

I'm a big fan of talking your problems out.  So the past week I've been bugging everyone in campfire with endless messages about where to go with everything.  We even discussed in person quite a bit to figure out where we wanted to go.  After this I just started dumping out all my ideas to our wiki (see screenshot right).

It's really important to dump out your ideas after a brainstorming session.  Doesn't matter if your medium is text, photoshop, omnigraffle or a sketchbook -- just get the ideas out of your brain and onto a shareable medium.