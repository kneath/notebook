# Let's make the web better

I tried very hard to keep my mouth shut on this whole Flash vs the iPad thing.  But I decided that instead of arguing why we should or should not kill off Flash, I'd try to explain some of the modern challenges of "ditching flash" as it may be -- and why I think we're at least a decade off from being able to do so.

## Arguing against Flash is dumb

You're probably wrong and at best it's unproductive.  Spend your time trying to make existing technologies a better alternative than Flash, don't sit around bashing Flash. You just look dumb.

## So what problem are we trying to solve?

It's always a good idea to think about what problems you're trying to solve before you start proposing solutions.  On one hand: we have a miracle plugin (Flash) that has been responsible for almost all innovation on the web in the past decade (think about it: streaming video, scalable vectors, animation, persistent network connections -- Flash pioneered it all and at nearly 100% penetration). On the other hand: Flash is and always will be a second class citizen -- most importantly, less performant than native implementations.

In past decade, we've seen the rise of viable alternatives to Flash under certain circumstances: long-polling AJAX connections, SVG, Canvas, leapfrogs in Javascript performance, etc.

But it's important to note that we still don't have viable solutions for many problems: notably scalable interfaces and streaming video.  This is because **browser manufacturers have been extraordinarily lazy and the W3C is incapable of leading the web.**

### Streaming Video

HTML5 does have a specification for a `<video>` element -- but without a common video format (ogg or h.264), this element is no more than a tech demo that works in very specific browser & OS combinations.

At best, current `<video>` examples ([YouTube](http://youtube.com/html5), Vimeo) replace one proprietary player (Flash) with another (Safari). h.264 is no more open than FLV, and codecs cannot be implemented in open source browsers like Firefox and Chromium.

To make the web better, **we need to have a standard streaming video solution that works in OSS browsers (Firefox, Chromium, Mobile Webkit) *and* proprietary browsers (Safari, Chrome).**

Browser manufacturers seem unwilling to cooperate and the W3C seems incapable of creating a spec that provides a solution for the future.  The end result is a non-solution. There only path to the future that sees `<video>` replacing Flash is if one of the following scenarios plays out:

1. Everyone in the world uses Safari/Chrome
2. All video providers encode their videos at least twice and either:
  * Internet Explorer usage drops close to 0%
  * Internet Explorer chooses to implement `<video>` using h.264 or ogg

I don't see this as a solution.

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