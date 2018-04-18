---
title: "Publishing a Decentralized Blog"
date: 2018-04-17T12:24:17-04:00
draft: true
---

The promising aspect of Beaker is that all web technologies work as expected. The fact that visting a site is as simple as creating an `index.html` and placing `dat` instead of `http` in front of the URL is a great start. The trickier aspect is teaching yourself to think in terms of a static, shared infrastructure instead of a central one. No database means that a static CMS is needed to manage the blog. 

<!--more--> 

Before getting into my process, it is helpful to read these first:

- [So you want to decentralize your website](dat://tmcw.hashbase.io/2017/07/20/decentralize-your-website.html)
- [How I Publish taravancil.com](dat://taravancil.com/blog/how-i-publish-taravancil-com/)
- [Deploying a Modern, Secure Staitc Site](dat://tomjwatson.com/blog/deploying-a-modern-static-site/)

Now, my process:

1. Create decentral site
2. Create Hugo site
3. Copy public directory over from Hugo to decentral
4. Push to Github
5. Github syncs to Netlify
6. Problems: No great UI...NetflyGUI exists but still needs works. [Siteleaf](https://www.siteleaf.com) feels like a good compromise because Jekyll / not locked in, but still paid and limited.
7. Too hard for non techies.

Need to figure out:

1. Auto copy from hugo build to Beaker site
2. Do Beaker sites only live on Beaker or any browser that supprots dats?
3. Pus to github and lock github to netlify
4. Does netlify CMS work with any HUGO repo, or only their predefined themes?