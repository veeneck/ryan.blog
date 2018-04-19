---
title: "Publishing a Decentralized Blog"
date: 2018-04-17T12:24:17-04:00
draft: false
---

The promising aspect of Beaker is that all web technologies work as expected. The fact that visting a site is as simple as creating an `index.html` and placing `dat` instead of `http` in front of the URL is a great start. The trickier aspect is teaching yourself to think in terms of a static, shared infrastructure instead of a central one. No database means that a static CMS is needed to manage the blog. 

<!--more--> 

Before getting into my process, it is helpful to read these first:

- [So you want to decentralize your website](dat://tmcw.hashbase.io/2017/07/20/decentralize-your-website.html)
- [How I Publish taravancil.com](dat://taravancil.com/blog/how-i-publish-taravancil-com/)
- [Deploying a Modern, Secure Staitc Site](dat://tomjwatson.com/blog/deploying-a-modern-static-site/)

Now, my process:

2. Create Hugo site
3. dat . to create decentral site and syn changes with dat
4. Push to Github
5. Github syncs to Netlify and site is updated
6. Problems: No great UI...NetflyGUI exists but still needs works. [Siteleaf](https://www.siteleaf.com) feels like a good compromise because Jekyll / not locked in, but still paid and limited.
7. Too hard for non techies.

Need to figure out:

2. Do Beaker sites only live on Beaker or any browser that supprots dats?

### User Interface

[Siteleaf](https://www.siteleaf.com) - hosted, not what I'm lloking for
[Publii](https://getpublii.com) - local, exactly what I'm looking for but communty doesn't seem active so not sure if it will stick around
[Grav](https://getgrav.org) - Myabe exactly what I need? Appears more active than Publii TBD
Netlify GUI - Works with premade themes they offer, but does it work with custom HUGO theme?

