# Let's make the web better

I tried very hard to keep my mouth shut on this whole Flash vs the iPad thing.  But I decided that instead of arguing why we should or should not kill off Flash, I'd try to explain some of the modern challenges of "ditching flash" as it may be.

## Arguing against Flash is dumb

You're probably wrong and at best it's unproductive.  Spend your time trying to make existing technologies a better alternative than Flash, don't sit around bashing Flash. You just look dumb.

## So what problems are we trying to solve?

People say we should ditch Flash for HTML5.  This statement is terribly ambiguous, so we should remind ourselves what we want to replace:

* Streaming video
* Streaming audio
* Scalable interfaces (pixel independent interfaces)
* Animated vectors
* Rich interfaces (for simplicity's sake, use flash games as an example)

Unfortunately HTML5, as a specification does not solve any of these problems.  Luckily web developers and browser manufacturers learned long ago that the W3C is incompetent at best, so we *do* have some partial solutions.

### Streaming Video

HTML5 does have a specification for a `<video>` element. Unfortunately W3C didn't have the balls to put browser manufacturers in their place, so there isn't a common video format.  This means that things like [YouTube's](http://youtube.com/html5) program really don't work hardly anywhere. Try loading it up in Firefox, or Chromium -- you'll notice none of it works.

We have to remember than h.264 is still proprietary (it isn't "open") -- so at the end of the day, we're just replacing one proprietary player (Flash Player) for another (Safari's or Google's).

What's this mean in the long run? People on linux machines will likely never be able to see h.264 videos.  People on iPhones will be able to play videos, but people on Android phones will not (depending on what licensing the particular manufacturer ships with).

To make the web better, **we need to have a standard streaming video solution that works in OSS browsers (Firefox, Chromium, Mobile Webkit) *and* proprietary browsers (Safari, Chrome).**

### Streaming Audio

My hope is that streaming audio is the one place that we can reliably ditch Flash in the next decade.  There aren't nearly as many licensing issues blocking us from accomplishing our goals.  So I think on the audio front, we're actually pretty good.

### Scalable interfaces

As the web moves away from "regular" computers and onto devices like the iPad where resolution is relative, we're going to need to solve the scalable interface problem.  Pixels aren't really pixels on the iPad, iPhone, Android, etc.

So, we'll need a solution to create simple graphics (borders, curves, shadows, gradients, etc) with CSS.  If you think that the current state of these CSS properties is sufficient, *you are mistaken.*  For example, let's make a simple button:

    a.button{
      text-shadow:1px 1px 1px #fff;
      background: -moz-linear-gradient(top, #fff, #d8d8d8);
      background: -webkit-gradient(linear, left top, left bottom, from(#fff), to(#d8d8d8));
      -moz-border-radius:3px;
      -webkit-border-radius:3px;
      -moz-box-shadow: 0 0 3px rgba(0, 0, 0, 0.4);
      -webkit-box-shadow: 0 0 3px rgba(0, 0, 0, 0.4);
    }
    a.button:hover{
      text-shadow:-1px -1px 1px #3168a3;
      background: -moz-linear-gradient(top, #00bbf0, #006add);
      background: -webkit-gradient(linear, left top, left bottom, from(#00bbf0), to(#006add));
      -moz-box-shadow: 0 0 3px rgba(0, 98, 148, 1.0);
      -webkit-box-shadow: 0 0 3px rgba(0, 98, 148, 1.0);
    }
    a.button:active{
      background: -moz-linear-gradient(top, #006add, #00bbf0);
      background: -webkit-gradient(linear, left top, left bottom, from(#006add), to(#00bbf0));
    }

This is so far beyond unacceptable I don't even know where to start.  `border-radius` showed up in Firefox 1.0 and here we are in 2010 still typing out `-moz-border-radius`.  The Webkit team and Gecko team are so full of themselves they can't spend a week deciding how to support gradient syntax. Don't even mention Opera & IE to me or I'll explode. And don't get me started on the [state of rendering](http://www.flickr.com/photos/kneath/3388433187/) either.

To make the web better, **we need reliable, standard ways of creating simple scalable graphics.**