---
title: Publishing a Decentralized Blog
date: 2018-04-17 12:24:17 -0400
tags:
- decentralized
- hugo

---
The promising aspect of Beaker is that all web technologies work as expected. The fact that visting a site is as simple as creating an `index.html` and placing `dat` instead of `http` in front of the URL is a great start. The trickier aspect is teaching yourself to think in terms of a static, shared infrastructure instead of a central one. No database means that a static CMS is needed to manage the blog.

<!--more-->

<mark>**!! Update:** This post is still relevant, but I now have an [alternate workflow for when I want to use a GUI](http://ryancampbell.blog/blog/forestry---hugo---netlify/). Read them both!</mark>

Before getting into my process, it is helpful to read these first:

* [So you want to decentralize your website](dat://tmcw.hashbase.io/2017/07/20/decentralize-your-website.html)
* [How I Publish taravancil.com](dat://taravancil.com/blog/how-i-publish-taravancil-com/)
* [Deploying a Modern, Secure Staitc Site](dat://tomjwatson.com/blog/deploying-a-modern-static-site/)

Now, my process is similar to the above. I'm documenting for myself as much as anything. It's easy to walk away from something for a few weeks and then completely forget a step.

### Picking a Static CMS

I don't have a strong preference on this. I just knew I wanted something fresh and with momentum. [Hugo](http://gohugo.io) seems to satisy those needs, and it gives me a chance to play with Go. For now, I just started with a [theme](https://themes.gohugo.io), and I'll tailor it to my needs as I go along. Following the [quickstart guide](http://gohugo.io/getting-started/quick-start/) was enough to get me to a Hello World state.

### Populating the Site

By now, we've already lost all non tech users. That's OK, and I'll address a GUI later. For us techies, creating content is fairly straightforward.

1. Open the entire site directory in your [favorite editor](https://www.sublimetext.com).
2. Jump to the directory in terminal, and create a new post using: `hugo new blog/first-post.md`
3. Open the newly created `.md` file in your editor and write your post.
4. Back in terminal, type `hugo` in the parent directory to generate the static files.
5. Verify the entire site was created in the `/public` directory.

_Note_: When you run `hugo` to build the site, it [won't delete any existing files](http://gohugo.io/getting-started/usage/#deploy-your-website) in the `/public` directory. It's best to delete everything in that directory before regenerating the site, but be sure permanent folders like .well-known stay in place.

### Publishing the Decentralized Site

Creating a `.dat` is much easier than I expected it would be. Simply navigate to the `/public` directory in terminal and type `dat .`. That will convert the directory into a dat archive, and give it a unique address. When it runs, the output will be similar to:

    dat v13.10.0
    dat://38e18e7e5ddace84f0cad2d55056aa27acede9acd71df787324e1d48f5882567
    Sharing dat: 82 files (1.8 MB)

If you paste the `dat://` URL into Beaker, you should see your site.

To take it a step further, you can create a free [Hashbase](http://hashbase.io) account and upload your dat archive to them. They will generate a URL like [dat://blog-rpc.hashbase.io/](dat://blog-rpc.hashbase.io/), which makes sharing a link to your site much cleaner. **Bonus**: Hashbase also hosts your site on https, so you can stop here if you don't want a custom domain for your site.

### Publishing the Standard Site

In my case, I did want to use a custom domain, so I had to pick a static site host. The most familiar one is Github pages, but [Netlify](https://www.netlify.com) seems to be the popular one right now. Netlify will sync with your Github account, and display a specified directory from the respository. After pushing my entire Hugo directory to Github, adding that repo to my free Netlify account, and telling Netfliy that `public` is the directory I wish to display, the process is as simple as:

1. Commit any new files.
2. Push the commit to master.

That's it. That's how the live site is updated.

### Using a Domain with a dat://

It would be even better if `dat://ryancampbell.blog` resolved to my site. Two things need to happen for Beaker to recognize your domain name and use it with a `dat://` prefix.

First, [create a well-known file](https://github.com/beakerbrowser/beaker/wiki/Authenticated-Dat-URLs-and-HTTPS-to-Dat-Discovery). To do this:

1. Add a new folder named `.well-known` in your `/public` directory.
2. Add a file named `dat` inside of the `.well-known` folder.
3. Paste your `dat://` long URL into the newly created file and save.
4. Push these changes to Github, which in turn will sync to Netlify.

Once you've verified that `https://yourdomain/.well-known/dat` exists and doesn't give a 404, you're set. Notice that URL uses `https`. If you don't have SSL enabled on your site, it is required for this to work. Fortunately, that is easy. Just log in to Netlify and add SSL under your domains. They generate a free [Let's Encrypt](https://letsencrypt.org) certificate for you in one click.

### GUI?

Overall, I love this workflow. Everytime I add a post, it takes three terminal commands to build the site and push it to both `dat://` and `http://`. Everything is fast, easy to debug locally, and well documented. To take it a step further, I'm excited by the idea of merging a pull request to instantly change a live blog. In comparison to this, a GUI feels slow and outdated.

At the same, we need GUI's. By we, I mean the world. I was looking for modern static CMS GUI's and came across some interesting ideas. [Siteleaf](https://www.siteleaf.com) is beautiful, but I don't want something hosted. [Publii](ttps://getpublii.com) and [Grav](https://getgrav.org) run locally, but neither felt like it had the support that Hugo has. [NetlifyCMS](https://www.netlifycms.org) appears to be the most promising because it works with multiple static site generators including Hugo. It lacks features, but has active development. Keep an eye on the space -- this problem should be resolved soon.