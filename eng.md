*Editor's note: This post is ≈3,000 words. It covers many different aspects of
perceived performance of mobile websites as well as practical solutions to 
speeding up your site. TL;DR: it's not about how fast your site is; it's about 
how fast your users think it is.*

![A Beginner's Guide to Perceived Performance][1]

Building well-designed websites on mobile devices is slowly becoming easier and
easier. Whatever the method (responsive, adaptive, etc.), if you know what you'
re doing, crafting a good-looking site is not a problem.

But your clients, just like ours, may still be asking for that app-like
experience. And creating such experiences remains a challenge.

Most of the time, when people say something is *‘app-like’* or that it feels **

Native apps are fast. Animations are rendered smoothly; buttons respond
immediately when you press them, and there’s never any question as to whether 
something is loading.

**Getting your site to feel native means doing everything you can to get your
site to perform as quickly as possible.**

Improving performance is a really hot topic right now, and for good reason.
Until very recently, the web has been trending towards slower and heavier sites.
And there’s an argument that it’s impossible to make a performant web app.

This was the reason [Facebook said they had to move to a native app][2]. They
just couldn’t get the speed or interactions where they wanted them, at least 
with the resources they had.

Despite what Facebook thinks, it’s not impossible to build performant
websites. It may not be easy, but it’s not out of our grasp. We just have to 
work a little bit harder to make it happen. Technically, we’ve got the power to 
make our sites feel faster, more modern, and overall better experiences.

### Perceived Performance vs. Actual Performance

While improving actual performance is important, it turns out it doesn’t
really mean that much to the end user unless they can actually sense the 
improvement.

At An Event Apart in Seattle earlier this year, Luke Wroblewski told a 
[story about his mobile app, Polar][3]. He explained that his team worked hard
to improve the amount of time it takes to load new polls.

At the same time, they introduced a short spinner to show users when polls were
loading. Feedback immediately started pouring in about how loading new polls 
felt so much slower than before, despite the fact that it was actually much 
faster. Polar quickly released a patch removing the spinner, and people were 
impressed by how much faster polls loaded.

This is a great example of the importance of perceived performance. It doesn’
t matter how fast your site is if it doesn’t feel fast. In the case of the 
spinner, it just drew the user’s attention to the fact that they were waiting 
instead of distracting them from it.

**As designers and developers, our goal shouldn’t just be to create the
fastest site mathematically; it should also be to create the fastest site 
experientially.**

All that matters is how the user perceives the speed of your site. Any actual
speed increase is just a topper on an already well-decorated cake. I would argue
that perceived performance is more important than actual performance gains. But 
that doesn’t mean you shouldn’t be working on actual performance as well.

So, enough with the explanations. What can you do to improve perceived
performance on your site right now?

**Here are four techniques you can start implementing immediately.**

### 1. Add Touch States to Your Buttons

One of the easiest ways to improve perceived performance on your site is by
enabling the active state on mobile.

**You see, any time a visitor taps on a button on your site, she has to wait
250ms before it even looks like anything happened**.

Browsers put that timeout in there so they can make sure the user didn’t mean
to do something else (like zoom in or scroll). So they wait one quarter of a 
second to see what else the user does and, if it’s nothing, they act on that 
initial tap. And when the action finally does happen, it just highlights with a 
grey overlay and then goes through.

This is a terrible experience. The Nielsen Group performed a study which showed
that anything taking more than
[100ms to respond makes the user feel like they’re waiting][4] — and all
they’re trying to do is move through your site.

However, the majority of mobile sites, including some of the ones I've built,
don't address this perceived performance issue. Designers usually leave the 
default touch state as-is on links or buttons.

**To make your site feel faster, you need to make your buttons respond
immediately to a user's touch and give that user a great visual indication that 
something is happening.**

There is a great property on the web for showing when a button or link is
clicked; it’s the`:active` state. We use it all the time for desktop browsers
.

Unfortunately, neither iOS nor Android respect this property when a link or
button is tapped on mobile. To enable those active states, you need to add a 
simple event to the page with JavaScript:

    document.addEventListener("touchstart", function(){}, true)
    

Then, you'll want to use CSS to add active states to our buttons and remove the
tap highlight:

    -webkit-tap-highlight-color: rgba(,,,);
    

With both of those properties in place and active states set on your buttons,
they’ll immediately feel like they respond faster even though they actually 
respond at the same speed. You’re just giving your users immediate feedback for 
their actions instead of making them wait 250ms to see if anything happened.

![Without Touch States][5]
##### Without Touch State ([code][6]) 

![Withough Touch States][7]
##### With Touch State ([code][6]) 

**However, if you want to make them actually respond immediately, you can go
one step further.**

Using a JavaScript function called `fasttap` or `fastclick`, you can fully
remove that 250ms delay from your buttons. This, along with the active states, 
will make your websites feel speedy as heck.

For more information on `fasttap`, read [this article by Google][8] or, for a
ready-made implementation, check out[this repo on Github][9].

### 2. Use Momentum Scrolling

Have you tried creating a scrollable container on your mobile site and been
stuck with the slow, non-responsive scrolling that’s enabled by default?

You’re in luck! Android 3+ and iOS 5+ implemented a new property called 
`overflow-scrolling` that enables momentum scrolling. And it works beautifully
.

![Without Momentum Scrolling][10]
##### No Momentum Scrolling ([code][11]) 

![With Momentum Scrolling][12]
##### With Momentum Scrolling ([code][13]) 

This momentum scrolling *feels* native because it *is* native. All you need to
do is add this property to your scrolling containers:

    -webkit-overflow-scrolling: touch;
    

There is one issue with this property, however. It will disable the ability to
tap the status bar on the top of your iPhone to scroll back to the top of the 
page. This bug has been around for a while, and it doesn’t seem to be fixed even
in the[latest version of Mobile Safari on iOS 7][14].

One way to get around this is to create a class that adds 
`overflow-scrolling: touch` to the container and then use JavaScript to only
apply that class when that container is visible.

On Android 4, you don’t even need this property. Every scrollable container
has momentum scrolling.

On older versions of Android, you have a couple of options. My favourite one is
to detect momentum scrolling support with Modernizr and alter your layout to 
have the container overflow visibly. If that’s not an option, there are a few 
JavaScript libraries you can try instead. Filament Group’s[Overthrow][15] and
[iScroll][16] work pretty well.

### 3. Create Performant Animations

One of the most noticeable differences between websites and apps is the use of
animations.

Apps have been able to to take full advantage of the hardware graphic
acceleration present in all modern devices for years now. On the web, developers
have been making do with JavaScript-based animations, which are slow on weaker 
mobile CPUs.

But now, with mobile browser support being what it is, you can make great use
of hardware-accelerated CSS3 animations in your projects.

**This is an awesome way to add some of that visual pizazz that all of our
favourite apps have been flaunting for years.**

Not so fast, though! For animations to feel native, you have to make sure that
your animations aren't slow or choppy, which can be quite difficult.

Allen Pike of Steamclock Software wrote [a great article in 2011][17] about the
joy animations provide users and how non-performant animations can have a huge 
impact on how an app feels.

Interestingly, he wrote this article about native app development. This makes
it a perfect article for us to follow in our mission to create native-feeling 
animations on the web.

In the article, he lays out what he calls a "timeline of perception":

**1. Animations Should Move at 60fps.** This means that each frame should take
[~16ms to complete][18]. That’s the bare minimum to feel native and smooth.
60fps is the speed that all iOS’s built-in animations run at; it’s why scrolling
on an iPhone feels so much better than on an Android device (although Google has
made great improvements in this space recently). You should attempt to get all 
animations that are directly related to a user’s interaction moving at this 
speed.

**2. Everything Else Should Respond in Under 100ms.** That number is the mental
barrier after which things feel slow. Anything under 100ms feels essentially 
instantaneous to the user.

**3. If it Absolutely has to Take Longer than 100ms, it Should Definitely
Respond Within 1000ms.** Allen suggests that anything that takes this amount of
time should give the user some indication that something is happening. Like a 
spinner or a progress bar.

But, as we learned earlier with the Polar example, focusing the user’s
attention on the wait may actually do more harm than good. I’ll cover a 
different method for dealing with this in a bit.

**4. Anything That Takes Longer than a Second** is probably bad, and you should
feel bad.

Okay, so knowing all of that, you may be wearing your keyboard as a hat and
contemplating a career change — since when did building for the web mean you had
to worry about things like animation timing?

**Don’t worry, there are some great resources that make this stuff a lot
easier!**

The first one is a new library by the fine folks at HTML5 Boilerplate, 
[Effeckt.css][19]. Their goal is to create a library of common transitions and
animations that perform at 60fps. While it’s not quite done yet, a lot of them 
are working pretty well, and I highly recommend using them and tweaking them to 
suit your project.

Another great library is [Topcoat][20]. Built by the web team at Adobe, this is
a CSS component library built with performance in mind. This library is filled 
to the brim with excellent components that run extremely smoothly. Because 
performance is their main goal, every single one of the components is
[benchmarked so you can see exactly how it performs][21].

Topcoat and Effeckt.css actually go hand in hand. Topcoat contributes directly
to the Effeckt.css repo, and both play very nicely together.

**Next, I mentioned earlier that I’d talk about a method for avoiding
spinners when possible.**

One of my preferred methods for avoiding spinners on waits longer than 100ms
but shorter than, say, 250ms — where a spinner will actually do more harm than 
good — is to hide it behind an animation.

For instance, if you’re Ajaxing in content, try animating the content’s
container so that it shrinks up and then grows back to fit the new content. A 
short animation like this will distract the user from the wait — instead of 
staring at a spinner they’re simply waiting for a short animation to finish. 
They may not even realize the new content wasn’t there to begin with.

Of course, repetitive animations that take a long time to complete can be
annoying too, so make sure you when you use these techniques sparingly. That’s 
good advice for most animations.

### 4. Take Advantage of Natural Gestures

One thing apps seem to have over the web is their ability to harness gestures
that seem to come naturally to people on touch devices.

App creators have recognized the power that gestures hold and are quickly
capitalizing on it.

Look at [Mailbox][22] or [Clear][23] for great examples of this. These apps use
simple gestures that take advantage of the biggest differentiator of the mobile 
device, the ability to directly touch objects on screen.

Most websites, however, only rely on tapping objects. Designers avoid
implementing other gestures, leaving users feeling like second-class citizens.

**We need to start thinking about developing websites directly for the device.
If a user's device allows for gestures, why not use them?**

Of course, there’s just one little problem: mobile operating systems have
this nasty little habit of hijacking gestures in the browser for their own '
nefarious' means.

For example, apps like Facebook have been using edge swipes on the left and
right edges of the screen to open up navigation. However, on the web, this 
interaction is out of bounds as Chrome uses it to switch between tabs and the 
new version of Mobile Safari in iOS 7
[uses it to go forward and back through history][14].

Okay, so those gestures are pretty much off limits. Which ones can and should
you use? Here are four:

#### Gesture #1. Side-to-Side Swiping

Even though the edges are out, side-to-side swiping is still a great gesture.
You just have to be careful not to have it too close to the edge of the screen.

This gesture is best used to move through a set of objects, in something like a
photo carousel or a list of tabs.

#### Gesture #2. Pull-to-Refresh

Pull-to-refresh is another gesture that people just seem to *get*. There are a
bunch of great JavaScript libraries that make it easy to integrate this feature.
The one I’ve used before is[Hook.js][24].

#### Gesture #3. Long Press

There’s a useful property called `-webkit-touch-callout: none;` that will
disable the default long press action in Mobile Safari. If you want to disable 
it on Android, however, it’s a[bit more work][25].

Long press gesture can be used for actions such picking up an item (e.g.
reordering items in a list) or showing more options (e.g. social sharing
).

#### Gesture #4. Pinch-Zoom

Everyone understands pinch-zoom. Most people when they encounter a photo on the
web will try to pinch-zoom in to see it in greater detail.

This is another situation where the browser hijacks a gesture but, in this case
, it’s actually not so bad.

Whether you’re locking the viewport from zooming or not, sometimes you don’
t want the whole page to zoom when a user pinches. To take over those multitouch
gestures, you can use the small but awesome[Hammer.js][26] library. This
library has a bunch of built in gestures you can use or you can create your own.

A great example of this is the pinch-zoom for images on the 
[imgur.com mobile website][27]. Check out what swiping does while you’re
there.

Just remember, if you’re using a gesture, make sure it’s one that either
feels natural or makes sense for the user to do.

### Conclusion

My hope is that one day there won’t need to be a distinction between native
and web. We’re not there yet but the more we work to make all of our websites*
feel* like they were designed for the user, the sooner that day will arrive.

**I think the recent trend towards focusing on performance is fantastic but we
have to remember that our users aren’t machines.**

They don’t care about how many requests your website makes or how fast the
screen repaints. But they do care about what those things impact — their 
perception of performance.

**Focus on making sure your site looks and acts like it’s as fast as possible
. There’s no point in making the fastest site ever if the user doesn’t notice.
**

If you have any more tips for improving perceived performance, please post in
the comments.

 [1]: img/perceived-performance.png
 [2]: http://www.infoq.com/news/2012/09/Facebook-HTML5-Native
 [3]: http://www.lukew.com/ff/entry.asp?1797
 [4]: http://www.nngroup.com/articles/response-times-3-important-limits/
 [5]: img/notapstate.gif
 [6]: http://codepen.io/mobify/full/ulwqf
 [7]: img/tapstate.gif
 [8]: http://developers.google.com/mobile/articles/fast_buttons
 [9]: http://github.com/ftlabs/fastclick
 [10]: img/nooverflowscroll.gif
 [11]: http://codepen.io/mobify/full/LueFn
 [12]: img/overflowscroll.gif
 [13]: http://codepen.io/mobify/full/vLcky
 [14]: http://www.mobify.com/blog/designing-for-ios-7/
 [15]: http://filamentgroup.github.io/Overthrow/
 [16]: http://cubiq.org/iscroll-4
 [17]: http://www.allenpike.com/2011/providing-joy-at-60-fps/
 [18]: http://speakerdeck.com/jaffathecake/rendering-without-lumps
 [19]: http://github.com/h5bp/Effeckt.css
 [20]: http://topcoat.io/
 [21]: http://bench.topcoat.io/
 [22]: http://mailboxapp.com
 [23]: http://www.realmacsoftware.com/clear/
 [24]: http://usehook.com/

 [25]: http://stackoverflow.com/questions/3413683/disabling-the-context-menu-on-long-taps-on-android
 [26]: http://eightmedia.github.io/hammer.js/
 [27]: http://imgur.com/gallery/U6HYTnm