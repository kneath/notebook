# Let's make the web better

I tried very hard to keep my mouth shut on this whole Flash vs the iPad thing.  But I decided that instead of arguing why we should or should not kill off Flash, I'd try to explain some of the modern challenges of "ditching flash" as it may be -- and why I think we're at least a decade off from being able to do so.

## Arguing against Flash is dumb

You're probably wrong and at best it's unproductive.  Spend your time trying to make existing technologies a better alternative than Flash, don't sit around bashing Flash. You just look dumb.

## So what problem are we trying to solve?

It's always a good idea to think about what problems you're trying to solve before you start proposing solutions.  On one hand: we have a miracle plugin (Flash) that has been responsible for almost all innovation on the web in the past decade (think about it: streaming video, scalable vectors, animation, persistent network connections, OS integration -- Flash pioneered it all and at nearly 100% penetration). On the other hand: Flash is and always will be a second class citizen -- less performant than native implementations.

In past decade, leaps in Javascript performance along with the rise of technologies like SVG, Canvas, and Ajax have offered opportunities to replace Flash under specific circumstances. Just for reference: I remember not five years ago Flash was *required* to fade an image.

But it's important to note that we still don't have viable solutions for many problems: most notably streaming video.  This is because **browser manufacturers have been extraordinarily lazy and the W3C is incapable of leading the web.**

### Streaming Video

Let's not kid ourselves: the big issue here is streaming video. HTML5 does have a specification for a `<video>` element -- but without a common video format (ogg or h.264), this element is no more than a tech demo that works in very specific Browser + Operating System + Video Provider combination.

At best, current `<video>` examples ([YouTube](http://youtube.com/html5), Vimeo) replace one proprietary player (Flash) with another (Safari/Quicktime). h.264 is no more open than FLV and codecs cannot be implemented in open source browsers like Firefox and Chromium.  It's true that h.264 has declared they won't be charging for online video licensing.... for now. But one day in the future, they have all the rights to demand royalties from every publisher for any video posted online (this should scare you).

The problem boils down to this: browser manufacturers seem unwilling to cooperate and the W3C seems incapable of creating a spec that provides a solution for the future.  The end result is a non-solution stalemate. The only path to the future that sees `<video>` replacing Flash is if one of the following scenarios plays out:

1. Everyone in the world uses Safari/Chrome/Proprietary and h.264 licensing remains free.
2. All video providers encode their videos at least twice **and** one of the two scenarios plays out:
  * Internet Explorer (all versions) usage drops close to 0%
  * Internet Explorer chooses to implement `<video>` using h.264 or ogg

This is not a solution.

## Who can solve this problem?

So now we've identified the problems we're facing: what can we do to fix it?  You'll notice none of my scenarios for `<video>` taking over had anything to do with Adobe making any actions. This is why it doesn't make sense to bash Adobe -- their actions are of no consequence.  The people we need to be complaining to are **browser manufacturers**. We need browser manufacturers to create better tools than Adobe has. And so far they have failed.

### Simplify

Things that are extremely simple in Flash are still horribly convoluted in browsers.  Let's try creating a scalable button with a gradient and a dropshadow:

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

This is so far beyond unacceptable I don't even know where to start. And don't get me started on the [state of rendering](http://www.flickr.com/photos/kneath/3388433187/) or curse words like "Opera" and "Linux".

Just for a minute, imagine we lived in a magical world where browser manufacturers cared. We might have syntax like this:

    a.button{
      text-shadow:1px 1px 1px #fff;
      background: gradient(linear, top, #fff, #d8d8d8);
      border-radius:3px;
      box-shadow: 0 0 3px rgba(0, 0, 0, 0.4);
    }
    a.button:hover{
      text-shadow:-1px -1px 1px #3168a3;
      background: gradient(linear, top, #00bbf0, #006add);
      box-shadow: 0 0 3px rgba(0, 98, 148, 1.0);
    }
    a.button:active{
      background: gradient(linear, top, #006add, #00bbf0);
    }

Sad part? I'm not even making up any syntax or browser features.  Just twenty minutes of collaboration between the Gecko and Webkit teams would have unified the syntax. Add in a little reality (The W3C will never ship a spec, don't expect them to) and you can drop all the proprietary `-webkit` and `-moz` bits.

*Politics* have prevented making developers lives easier. No more, no less.

### Catch up

Just the other day I noticed that Chrome gives you upload progress when you upload files from HTML forms.  This is the first browser to my knowledge that does this.  Flash has supported file upload progress (and other things like selection of multiple files, folders, etc) since before I can remember -- but it took until 2010 for someone to implement upload progress in a browser!

There's numerous other little bits where Flash is just way ahead -- clipboard integration, cross-domain requests, automatic upgrading, font embedding, image scaling... the list goes on and on. If Flash has been able to do these things as a **third party** -- why the hell haven't browser manufacturers done it?

### Take notice how important the internet is

I'm not here to say that keeping up with Flash in a performant and reliable fashion is going to be easy for browser manufacturers. But let's face it: the internet is one of the most important things to happen to the human race in a long time.

Browser development is big money and big exposure.  The only browser developer I know of that gets this is Google.  A little over a year into the game and they're *destroying* other manufacturers who have been around for more than a decade.  They get how important this is and they're doing something about it.

## I want to say the future is bright...

It's 2010 and I really wish I could look back at a post I wrote about HTML5 & CSS3 [back in 2007](http://warpspire.com/features/html5-css3/) and say I was wrong.  But here we are 2+ years later and the only difference is that instead of saying "iPhone" I should have said "iPhone and other devices to use MobileWebkit."

The bottom line: Flash is still the best tool for the job. The only way to replace Flash isn't to point out Flash's flaws, but rather to create tools that are a better option.

If you give me a better option for streaming video that doesn't include "fuck *those* users" or "well it works on *my* machine" I'm happy to use it. But the truth is Flash has the best solution out there -- and I'll keep using it until it isn't.