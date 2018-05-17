+++
date = "2018-05-17T07:01:09-04:00"
draft = true
tags = ["web", "jamstack", "hugo"]
title = "Import Wordpress Nested Comments into Hugo"

+++
I'm currently in the process of converting my most [complex Wordpress site](http://battleofbrothers.com) into a Hugo site, and comments proved to be one of the greater challenges. My approach went from screw comments, to let's use Disqus, to no let's do this right and use a static comment system.

<!--more-->

As you begin the same migration, I'm sure that you'll come to the same conclusion. The entire Disqus ecosystem feels complex, dated and bloated which contradicts the fresh feel of starting over using a static site. Combined with their user tracking and lack of ownership over the comments, a static comment system becomes the only acceptable option. Enter [Staticman](https://staticman.net).

Below I've documented some of the more interesting hurdles I encountered both in implementing Staticman and importing Wordpress comments.

### Get Staticman Working First

First up, I'd recommend getting Staticman comments working locally before attempting the import. This allows you to:

* See the data structure
* Code your actual Hugo templates
* Finalize your design

By doing it this way, when you finally import your Wordpress comments it will become 100% clear whether or not you imported the data correctly.