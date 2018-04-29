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

But hey, we don't have to browser test as much. Example hamburger menu. Then talk about things like [https://webkit.org/blog/7929/designing-websites-for-iphone-x/](https://webkit.org/blog/7929/designing-websites-for-iphone-x/ "https://webkit.org/blog/7929/designing-websites-for-iphone-x/") and other challenges. Nice to see things like CSS Breakpoints (link) in a SASS function (link)

### Codepen Helps

Both in finding snippets, and forcing yourself to clean and test code before posting snippets. In turn, this increases the desire to separate CSS into different files for typography, forms, etc. Just doing one simple task slowly, methodically, and correctly sets the stage for a better project.

### Codekit Still Does The Job (JQuery Too!)

Integrate it into Hugo, compiles sass just fine. Nice to see JQuery hasn't gone out of style. I'd still use Prototype if I could. Webpack is painful.

And while we're talking about old tools, Google Fonts is still wonderful.

### Scrolling is Easier

[https://css-tricks.com/scroll-fix-content/](https://css-tricks.com/scroll-fix-content/ "https://css-tricks.com/scroll-fix-content/") is a catch all, but a simpler way is fixed position on mobile and css sticky on web. Always a pain in the ass that looked glitchy in the JS days. Smooth scrolling even feels better. [https://css-tricks.com/snippets/jquery/smooth-scrolling/](https://css-tricks.com/snippets/jquery/smooth-scrolling/ "https://css-tricks.com/snippets/jquery/smooth-scrolling/")

### Flexbox Rocks & Doesn't

OK, it mostly does. Allows you to change position of things using order (link, newsletter example), generally fixes div soup and float issue. Won't autoscale an image inside, unless it is in a figure ([https://stackoverflow.com/questions/43759448/image-doesnt-scale-inside-flexbox](https://stackoverflow.com/questions/43759448/image-doesnt-scale-inside-flexbox "https://stackoverflow.com/questions/43759448/image-doesnt-scale-inside-flexbox"))

### Animation is a Thing

animate when in viewport. jQuery script

### Mailing Lists Can Be Static

General note on trend of static. Solve mailing list by using Zapier an dMailchimp. will follow up with article.

----

That about sums it up.