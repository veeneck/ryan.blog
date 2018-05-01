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

If you're unfamiliar with Automator, [this tutorial]() can bring you up to speed. One of the options in Automator is to run an AppleScript, which I ended up using the most. It's just more efficient to put in a couple of lines of code instead of 2 or 3 workflow actions. Below are the snippets I used most.

### Run Multiple Terminal Commands

With almost every project I need to open terminal. For websites, terminal runs localhost. For game development, terminal runs Jazzy docs. So, it is common to both want to be in the directory of the folder, and trigger some sort of action. Here is how I run a Hugo server automatically:

    on run {input, parameters}
    	
    	tell application "Terminal"
    		do script "cd /path/to/project" & ";hugo server -D"
    		delay 0.5
    	end tell
    	
    	return input
    end run

### Jump To A Specific Space

Next up, I've always like to organize my apps into different spaces. I prefer just a few apps per space, and to keep them all related. To get this AppleScript to work, you have to first enable keystrokes on your spaces. Once verified, go ahead and add this script.

    on run {input, parameters}
    	delay 1
    	tell application "System Events" to key code 20 using control down
    	delay 1
    	return input
    end run

Link to macOS spaces, then article on keystrokes for spaces:

[http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/](http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/ "http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/")

Then AppleScript of a space switch

Note the bug that requires keycde: [https://discussions.apple.com/thread/7891341](https://discussions.apple.com/thread/7891341 "https://discussions.apple.com/thread/7891341")

Credit: 	[https://www.quora.com/Are-there-any-scripts-to-automate-rotation-of-desktops-for-Mac-Spaces](https://www.quora.com/Are-there-any-scripts-to-automate-rotation-of-desktops-for-Mac-Spaces "https://www.quora.com/Are-there-any-scripts-to-automate-rotation-of-desktops-for-Mac-Spaces")

### Resizing Windows

This was a tricky one. Resizing windows is possible with AppleScript, but it would be tedious. Fortunately, I discovered the Moom (a window manager) has snapshots which save the layout of any space you tell it to. To make it better, they added AppleScript support for snapshots, so that you can trigger a snapshot from a script. Once I automate all of my windows, the final step is to run this snippet:

    on run {input, parameters}
    	
    	tell application "Moom"
    		delay 1
    		arrange windows according to snapshot named "Web Dev Build & Commit"
    		delay 1
    	end tell
    	
    	return input
    end run

Show how to save a snapshot in moom

Then show help docs which show what automator supports.

Then automator code.

### Changing Desktop Image

Ignore this actions input to change background when switching spaces

### Open In App

    on run {input, parameters}
    	
    	tell application "Fork"
    		open "path:to:project"
    	end tell
    	
    	return input
    end run

### Open URL and Tabs in Safari

    on run {input, parameters}
    	
    	do shell script "open -a Safari 'http://localhost:1313'"
    	
    	return input
    end run

### Open Finder to a Directory

    on run {input, parameters}
    	
    	tell application "Finder"
    		reopen
    		set the target of the front Finder window to (POSIX file "/path/to/project/")
    	end tell
    	
    	return input
    end run

### Other Notes

Codekit doesn't like Moom because it resizes on its own

hot_exit:false needed for sublime

Note - click off app before switching or else open app won’t close

Changing Icons: [http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/](http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/ "http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/") to change app icons

key codes if you need them: [https://eastmanreference.com/complete-list-of-applescript-key-codes/](https://eastmanreference.com/complete-list-of-applescript-key-codes/ "https://eastmanreference.com/complete-list-of-applescript-key-codes/")