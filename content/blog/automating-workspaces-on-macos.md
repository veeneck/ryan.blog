+++
date = "2018-05-01T00:21:37+00:00"
draft = true
tags = ["productivity"]
title = "Automating Workspaces on macOS"

+++
I now have 4 side projects in motion along with personal tasks like finance and communication. For the first time, my go to workspace solution of mission control and spaces doesn't cut it. Between Xcode, multiple terminal windows running, Photoshop, Mail, Photos, Sketch, and so on I finally felt overwhelmed. It's time for a new solution.

<!--more-->

I'm sure plenty of people have scripts to handle common tasks, but I've never needed it. Jumping from one project to the next has been a couple of windows at most. But, in this new web development world, [things get complicated fast](http://ryancampbell.blog/blog/a-lot-changes-in-six-years/). So, I wanted a solution that would close all windows, and reopen the relevant windows to exact positions in specific spaces with one keystroke. I was hoping [Workspaces](http://www.apptorium.com/workspaces) would do the trick, but it does not have enough features. So, I rolled my own with automator. Final product below:

<div style='position:relative;padding-bottom:57%'><iframe src='https://gfycat.com/ifr/WanJoyousAmericanalligator' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div>

Link to automator basics and then jump into specifics and then point out my specific scripts.

### Run Multiple Terminal Commands

text

### Jump To A Specific Space

Link to macOS spaces, then article on keystrokes for spaces:

[http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/](http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/ "http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/")

Then AppleScript of a space switch

Note the bug that requires keycde: [https://discussions.apple.com/thread/7891341](https://discussions.apple.com/thread/7891341 "https://discussions.apple.com/thread/7891341")

Credit: 	[https://www.quora.com/Are-there-any-scripts-to-automate-rotation-of-desktops-for-Mac-Spaces](https://www.quora.com/Are-there-any-scripts-to-automate-rotation-of-desktops-for-Mac-Spaces "https://www.quora.com/Are-there-any-scripts-to-automate-rotation-of-desktops-for-Mac-Spaces")

### Moom to the Rescue

Show how to save a snapshot in moom

Then show help docs which show what automator supports.

Then automator code.

### Changing Desktop Image

Ignore this actions input to change background when switching spaces

### Other Notes

Codekit doesn't like Moom because it resizes on its own

hot_exit:false needed for sublime

Note - click off app before switching or else open app won’t close

Changing Icons: [http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/](http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/ "http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/") to change app icons

key codes if you need them: [https://eastmanreference.com/complete-list-of-applescript-key-codes/](https://eastmanreference.com/complete-list-of-applescript-key-codes/ "https://eastmanreference.com/complete-list-of-applescript-key-codes/")

### Other Examples

Open finder window

Open Fork with given folder

Open Safari with URL

Open a second tab in safari