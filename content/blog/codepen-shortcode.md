---
title: Adding a Codepen Shortcode to Hugo
date: 2018-04-24 12:36:17 -0400
tags:
- hugo

---
Shortcodes allow you to add external content to a blog post in a user friendly way. Someone's tweet, an instagram photo, forms, and so on. Instead of a long ugly snippet of JavaScript, you can paste one line of clean shortcode. Hugo has [built in shortcode support](https://gohugo.io/content-management/shortcodes/), and adding a custom shortcode is super easy.

<!--more-->

I thought I would be in trouble when Google found no obvious solution for a Codepen & Hugo shortcode. Fortunately, this git repo had [just what I was looking for](https://github.com/jorinvo/hugo-shortcodes/blob/master/shortcodes/pen.html). As stated in Hugo's [docs on custom shortcodes](https://gohugo.io/templates/shortcode-templates/), simply create a file at `layouts/shortcodes/name.html` where `name` is the name of the shortcode you want to add.

Once the `name.html` file is created, copy the code from the repo above into it an save. Then, simply add a pen your posts with:

`{{</* pen id="Gflmy" */>}}`


And that's it. Nice. Demo below.

{{< pen id="apJdaY" height="200" >}} 

**Related**: Shortcodes execute even when they are wrapped in markdown code tags, or indented with 4 lines. The only way I was able to show how I embed a pen above was to escape was to use `</* pen id="Gflmy" */>` in between the opening and closing `{{}}`