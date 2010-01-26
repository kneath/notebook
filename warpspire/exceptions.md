# Exception Monitoring

Modern websites have bugs. This isn't a debatable point, it's the reality of building web applications.  Your users are going to do things you never thought possible (How in the hell did you get a `\r` in your filename, sir?) and it's going to cause unexpected things to happen.  The trick isn't to try and stop these exceptions, but to deal with them in an intelligent manner.

## You don't have to fix every exception

Many web developers treat every exception like some kind of treasure hunt. They'll spend hours tracking down an exception that gets sent off to their email, not realizing that this exception was caused by an edge case user who fixed his problem with a page reload.

Some exceptions are okay.  Does it really matter if a script testing for exploits in Wordpress is hitting your rails app and causing exceptions? Probably not.  Learn to let some exceptions go. They're just not worth your time.

## Don't fix, monitor

Once you've set yourself free of the need to fix every exception, you can start to do something far more useful: monitor the rate of exceptions for interestingness.  Let's take the following graph:

![Sample Exception Graph](http://share.kyleneath.com/captures/haystack_graph-20100110-151207.gif)

This graph is not interesting.  Many developers would look at it and freak out that there were around 50-100 exceptions happening an hour.  But remember, we're not worried about the hard numbers. We're looking for *interesting trends*.

I encourage all developers to graph their exceptions.  With a quick glance it's easy to see whether something is bad or not (especially after big deploys).