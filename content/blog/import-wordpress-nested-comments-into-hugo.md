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

1. Code your actual Hugo templates
2. Finalize your design
3. See the data structure
4. Finally, import the data

By doing it this way, when you finally import your Wordpress comments it will become 100% clear whether or not you imported the data correctly.

The [Staticman starter guide](https://staticman.net/docs/) is perfect, so follow it step by step. It is fairly easy to get a basic form submitting to your Github repo. I only encountered two minor problems along the way.

    error: GITHUB_READING_FILE

This is a simple one. You forgot to commit your staticman.yml file to master on Github. An understandable mistake when working locally. Next up:

    error: MISSING_CONFIG_BLOCK

This one took me forever to fix, which means it was a super obvious mistake. It means Staticman can't read your config file. In my case, the URL I had the form POST to was wrong. I left a third `}` at the end of my Hugo template, which added `%7D` to the end of the URL. Look for errors along those lines if you see the code above.

### Code Your Hugo Templates

NetworkHobo has the [best guide on importing comments](https://networkhobo.com/2017/12/30/hugo---staticman-nested-replies-and-e-mail-notifications/), so definitely start there. Everything I have implemented piggybacks off of that content, so I won't be repeating it in this article. However, there were a few additional limitations that I came across with the templates.

1. **Nesting more than one deep.**

This is the biggest change I made to the NetworkHobo guide. I wanted to allow for unlimited nesting. To do that, each template had to be modified and set up in a recursive way. Here is the general concept:

    Single.html loops over every comment and includes comment-display.html
    |---- comment-display.html displays the comment, and then includes comment-replies.html
    	  |---- comment-replies.html searches for replies matching the parent_id, and if found calls comment-display.html
    		    |---- loops until that reply has no more children

Take a second to process that, and then have a look at the 3 related snippets below.