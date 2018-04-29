+++
date = "2018-04-29T19:29:30+00:00"
draft = true
title = "A Lot Changes in Five Years"
undefined = ["charity"]

+++
I recently offered to create a website for a local charity, and then it hit me -- I haven't made a website in five years. Sure, I made this site and got on the [decentralized bandwagon](http://ryancampbell.blog/blog/i-m-late-to-the-jamstack-party/), but I haven't done something from scratch in some time. Especially on the design and responsive front. Now that I'm finished, I thought it may be useful to share my notes.

<!--more-->

Screenshot of finished in monitor, tablet and iPhone.

### The Design Process

Compare screenshots before and after. Explain how it sucks.

### Responsive Sucks

For a second, I was so happy because everything seems to be supported by every browser. The days of old IE testing are over. The holy grail has been obtained. Wrong. Instead, every annoyance with browser testing has now been transferred one-to-one with an annoyance of responsive design.

I dipped my feet into the responsive design pool with a simple task in mind -- build a hamburger menu. This is great starting point since it mainly applies to portrait mobile and anything larger than that. Here is the end result (resize your browser to see).

{{< pen id="odLvQz" height="400" >}}

[This pen by Brad Frost](https://codepen.io/bradfrost/pen/sHvaz) helped me navigate the waters. I was happy with how the implementation went until I realized that every single design decision will have to be combed over and designed for 4+ screen sizes. Ugh. Then, [some devices have specific considerations](https://webkit.org/blog/7929/designing-websites-for-iphone-x/). Double Ugh.

I took this approach to [manage CSS breakpoints with a Sass mixin](https://css-tricks.com/media-queries-sass-3-2-and-codekit/). I now see the date of 2012 on that article. Where has the time gone? Anyway, so far it's still working fine. Is there a better solution now?

### Codepen Helps

Fortunately, with all of this CSS/responsive nonsense, [Codepen](http://codepen.io) is a huge help. I wasn't uncommon for me to have 3 pens open at any given time while working through issues. But an unexpected benefit was in creating my own pens. It forced me to clean up the code before "publishing" it. 

Cleaning up the code naturally made we want to set up Sass. Before I knew it, I had files for [typography](https://devinhunt.github.io/typebase.css/), forms, constants, layout along with section specific CSS. I mention that to point out that just doing one simple task slowly, methodically, and correctly sets the stage for a better project.

### Codekit Still Does The Job (JQuery Too!)

Integrate it into Hugo, compiles sass just fine. Nice to see JQuery hasn't gone out of style. I'd still use Prototype if I could. Webpack is painful.

And while we're talking about old tools, Google Fonts is still wonderful.

### Scrolling is Easier

[https://css-tricks.com/scroll-fix-content/](https://css-tricks.com/scroll-fix-content/ "https://css-tricks.com/scroll-fix-content/") is a catch all, but a simpler way is fixed position on mobile and css sticky on web. Always a pain in the ass that looked glitchy in the JS days. Smooth scrolling even feels better. [https://css-tricks.com/snippets/jquery/smooth-scrolling/](https://css-tricks.com/snippets/jquery/smooth-scrolling/ "https://css-tricks.com/snippets/jquery/smooth-scrolling/")

embed gif

### Flexbox Rocks & Doesn't

OK, it mostly does. Allows you to change position of things using order (link, newsletter example), generally fixes div soup and float issue. Won't autoscale an image inside, unless it is in a figure ([https://stackoverflow.com/questions/43759448/image-doesnt-scale-inside-flexbox](https://stackoverflow.com/questions/43759448/image-doesnt-scale-inside-flexbox "https://stackoverflow.com/questions/43759448/image-doesnt-scale-inside-flexbox"))

### Animation is a Thing

animate when in viewport. jQuery script, link to example.

also link to css that animated hamburger menu above

### Mailing Lists Can Be Static

General note on trend of static. Solve mailing list by using Zapier an dMailchimp. will follow up with article.

---

That about sums it up.