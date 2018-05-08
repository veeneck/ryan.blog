+++
date = "2018-05-07T20:06:53-04:00"
draft = true
tags = ["web", "hugo"]
title = "Add Jazzy Docs to Hugo"

+++
I'm still riding this wave of excitement for static sites and free hosting, so the next step for me was to build my code documentation right into my Hugo sites instead of a separate standalone instance on Github Pages.

<!--more-->

![](/uploads/2018/05/08/Screen Shot 2018-05-07 at 8.09.19 PM.png)

The implementation is quite simple, so I'm just documenting it here for reference. I just grab [Jazzy](https://github.com/realm/jazzy), my favorite documentation tool. Next, utilize Hugo's [static directory](https://gohugo.io/content-management/static-files/) by configuring Jazzy to output there. In the `config.yml` file for the project, include:

    output: /path/to/hugo/site/static/ProjectName

Once that is set up build jazzy with:

    cd /path/to/xcode/project/ProjectName
    jazzy --config config.yml

Jazzy will run, and our docs are generated.

### Bonus

As I was setting this up, I tripped across these 3 items:

1. Set `clean: yes` in `config.yml` to delete the old files each time the docs are generated.
2. Jazzy support for custom themes is great, and I definitely recommend using it. I had to build twice sometimes for updates to appear -- not sure if it is a cache issue in the browser or in Jazzy.
3. Avoid hard errors in Jazzy by setting the Swift version: `swift_version: 4.1`

Once everything is running smoothly, I recommend [using Automator](http://localhost:1313/blog/automating-workspaces-on-macos/) or a post commit hook to generate the docs effortlessly.