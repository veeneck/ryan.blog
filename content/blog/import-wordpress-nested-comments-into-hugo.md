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

**Nesting more than one deep.**

This is the biggest change I made to the NetworkHobo guide. I wanted to allow for unlimited nesting. To do that, each template had to be modified and set up in a recursive way. Here is the general concept:

    Loop over comments and call dislay.
    |---- Display comment and call replies.
    	  |---- Finds replies, calls display.
    		    |---- Loops until no replies.

Take a second to process that, and then have a look at the 3 related snippets below. We'll start with the base template file, and then jump into each nested call.

    <ol>
    {{ range $index, $comments := $commentsForPost }}
        {{ if not .reply_to }}
            {{ partial "comment-display.html" (dict "entryId_parent" $entryId "SiteDataComments_parent" $.Site.Data.comments "parentId" ._id "parentName" .name "context" .) }} 
        {{ end }}
    {{ end }}
    </ol>

<p style="text-align:right"><small><i>single.html</i></small></p>

Starting with the post display, loop over all comments that aren't replies and start a thread. For each comment, call `comment-display` and pass in the data about the comment.

    <li>
    <p>{{ $.context.body | markdownify }}</p>
    </li>
    
    {{ partial "comment-replies" (dict "entryId_parent" $.entryId_parent "SiteDataComments_parent" $.SiteDataComments_parent "parentId" $.context._id "parentName" .name "context" $.context) }}

<p style="text-align:right"><small><I>comment-display.html</i></small></p>

This simplified version of `comment-display` simply renders the comment in a list element and then outside of the list calls `comment-replies`.

    <ul class="children">
    {{ range $index, $comments := (index $.SiteDataComments_parent $.entryId_parent ) }}
      {{ if eq .reply_to $.parentId }}
         	{{ partial "comment-display.html" (dict "entryId_parent" $.entryId_parent "SiteDataComments_parent" $.SiteDataComments_parent "parentId" ._id "parentName" .name "context" .) }} 
      {{ end }}
    {{ end }}
    </ul>

<p style="text-align:right"><small><I>comment-replies.html</i></small></p>

Each nested thread is a brand new `ul`. Every single comment is looped over again to see if any match the `$.parentId`. If a match is found, `comment-display` is called and the match is rendered. If that match has its own children, it will enter this loop and render them out.

**Displaying Comment Count**

Because the data is organized in a way that each post has it's own folder with only the relevant comments in it, looping over everything is not slow unless you're running a mega site. So, comment count is an easy grab both on the blog post and on any list pages where you want to preview comment count for the reader.

I made a partial for comment count with this code:

    {{ $entryId := .File.BaseFileName }}
    {{ $commentsForPost := index $.Site.Data.comments $entryId }}
    {{ $.Scratch.Set "comment_count" "0 comments" }}
    {{ with $commentsForPost }}
    	{{ $count := len $commentsForPost }}
    	{{ if eq $count 1 }}
    		{{ $.Scratch.Set "comment_count" (printf "%s" (print 1 " comment")) }}
    	{{ else }}
    		{{ $.Scratch.Set "comment_count" (printf "%s" (print $count " comments")) }}
    	{{ end }}
    {{ end }}

From there, you can call `$.Scratch.Get "comment_count"` to render the count.

**Custom Gravatars**