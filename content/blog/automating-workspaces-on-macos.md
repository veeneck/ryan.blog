+++
date = "2018-05-01T00:21:37Z"
tags = ["productivity"]
title = "Automating Workspaces on macOS"

+++
I now have 4 side projects in motion along with personal tasks like finance and communication. For the first time, my go to workspace solution of mission control and spaces doesn't cut it. Between Xcode, multiple terminal windows running, Photoshop, Mail, Photos, Sketch, and so on I finally felt overwhelmed. It's time for a new solution.

<!--more-->

I'm sure plenty of people have scripts to handle common tasks, but I've never needed it. Jumping from one project to the next has been a couple of windows at most. But, in this new web development world, [things get complicated fast](http://ryancampbell.blog/blog/a-lot-changes-in-six-years/). So, I wanted a solution that would close all windows, and reopen the relevant windows to exact positions in specific spaces with one keystroke. I was hoping [Workspaces](http://www.apptorium.com/workspaces) would do the trick, but it does not have enough features. So, I rolled my own with automator. Final product below:

<div style='position:relative;padding-bottom:57%'><iframe src='https://gfycat.com/ifr/WanJoyousAmericanalligator' frameborder='0' scrolling='no' width='100%' height='100%' style='position:absolute;top:0;left:0;' allowfullscreen></iframe></div>

If you're unfamiliar with Automator, [this tutorial](https://www.raywenderlich.com/58986/automator-for-mac-tutorial-and-examples) can bring you up to speed. It basically runs a sequence of commands in order to automate tedious tasks. Here is the output from the gif above.

![](/uploads/2018/05/01/Screen Shot 2018-04-30 at 3.03.42 PM.png)

One of the options in Automator is to run an AppleScript, which I ended up using the most. It's just more efficient to put in a couple of lines of code instead of 2 or 3 workflow actions. Below are the snippets I used most.

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

Next up, I've always like to organize my apps into different spaces. I prefer just a few apps per space, and to keep them all related. To get this AppleScript to work, you have to first [enable keystrokes on your spaces](http://osxdaily.com/2011/09/06/switch-between-desktops-spaces-faster-in-os-x-with-control-keys/). Once verified, go ahead and add this script.

    on run {input, parameters}
    	delay 1
    	tell application "System Events" to key code 20 using control down
    	delay 1
    	return input
    end run

Notice that the script above uses keycde 20 instead of "3". There a[ppears to be a bug where you have to use key codes](https://discussions.apple.com/thread/7891341) instead of a string of the key specifically when switching spaces.

### Resizing Windows

This was a tricky one. [Resizing windows](https://www.labnol.org/software/resize-mac-windows-to-specific-size/28345/) is possible with AppleScript, but it would be tedious. Fortunately, I discovered the [Moom](https://manytricks.com/moom/) (a window manager) has snapshots which save the layout of any space you tell it to. You also provide a custom name for the snapshot. In this case, the name is `Web Dev Build & Commit`. To make it better, they added AppleScript support for snapshots, so that you can trigger a snapshot from a script. Once I automate all of my windows, the final step is to run this snippet:

    on run {input, parameters}
    	
    	tell application "Moom"
    		delay 1
    		arrange windows according to snapshot named "Web Dev Build & Commit"
    		delay 1
    	end tell
    	
    	return input
    end run

Also, if you open Moom and then go to Help->AppleScript they have a list of all commands they support. Good stuff.

### Changing Desktop Image

I like to change the desktop color and image often, and this automates that process. Depending on what I'm working on, the desktop will change. Automator has a built in action for `Get Specified Finder Items` and then `Set Desktop Picture` so no AppleScript is needed.

I did hit one bug though: When switching spaces after changing the desktop background, I would get a hard crash. To avoid this, I had to check `Ignore this action's input` under Options for the change space task.

### Open In App

Opening directly in an application like Fork for version control is simple. It's worth noting the syntax for the path uses colons (:) instead of forward slashes (/) in this case.

    on run {input, parameters}
    	
    	tell application "Fork"
    		open "path:to:project"
    	end tell
    	
    	return input
    end run

### Open URL and Tabs in Safari

Opening Safari to a specific URL is straightforward.

    on run {input, parameters}
    	
    	do shell script "open -a Safari 'http://localhost:1313'"
    	
    	return input
    end run

Opening in tabs is simple once Safari is open:

    on run {input, parameters}
    	
    	tell front window of application "Safari"
    		set newTab to make new tab
    		set the URL of newTab to "http://google.com"
    		set the current tab to newTab
    	end tell
    	
    	return input
    end run

It also appears [form input is possible](http://www.cubemg.com/how-to-fill-out-forms-on-websites-with-applescript/), so my next step may be automating login on certain sites.

### Open Finder to a Directory

Fairly simple task of just getting the directory open in Finder. This will open in the current Finder window if you have one open, or a new window if you don't.

    on run {input, parameters}
    	
    	tell application "Finder"
    		reopen
    		set the target of the front Finder window to (POSIX file "/path/to/project/")
    	end tell
    	
    	return input
    end run

### Close Fork Tabs

Quit all applications is convenient, but some applications like to remember where they were last open. Fork, for example, will reopen with the new repository and all of the previous repositories, which gets cluttered. So, before calling the quit all applications workflow, I run this to close each for tab individually.

    on run {input, parameters}
    	
    	if application "Fork" is running then
    		activate application "Fork"
    		tell application "System Events"
    			tell process "Fork"
    				repeat 3 times
    					keystroke "w" using command down
    				end repeat
    			end tell
    		end tell
    	end if
    	
    	return input
    end run

### Other Notes

While configuring all of this, I ran into these oddities:

1. Codekit doesn't like Moom since it resizes on launch. I had to manually position the size of the window that sits next to Codekit.
2. Sublime Text opens all recently used projects by default. In user defaults, set `hot_exit:false` to prevent this.
3. Before running the Automator application that you created, click onto the desktop. Quit all apps won't work if one of your current apps has focus.
4. Consider changing your newly create app by [giving it a custom icon](http://www.idownloadblog.com/2016/06/20/customizing-app-icons-on-mac-os-x-el-capitan/ ).
5. [Here is handy list of key codes](https://eastmanreference.com/complete-list-of-applescript-key-codes/) that you may need.