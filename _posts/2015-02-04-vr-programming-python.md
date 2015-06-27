---
layout: post
title:  "Virtual Reality Programming in Real-Time with Python"
date:   2015-02-04 16:52:37
---

Over the past few weeks I've been working on creating a Python virtual reality programming environment. I've been using the Unity Game Engine and have embedded IronPython within in order to be able to access Unity functionality through Python. The reason I'm using Python for this is that the eventual intention for this project is that it will be a way for people new to programming to be able to learn in an interactive (virtual) environment where they can see how what they write or change about code actually changes the objects around them. I think Python is the best language to start off with for a large number of reasons, so I really wanted to use it within my VR programming environment.&nbsp;

Here's a video of the project in its current state right now:
<p>
<div class="auto-resizable-iframe">
	<div>
		<iframe width="640" height="390" id="youtube_iframe" allowfullsreen="yes" src="https://www.youtube.com/embed/Bgx0IF7K61U?feature=oembed&amp;enablejsapi=1&amp;origin=https://safe.txmblr.com&amp;wmode=opaque" frameborder="0"></iframe>
	</div>
</div>
</p>

If you already know Unity, it is actually pretty much fully functional in its current state. The objects you can see me creating in the demo are actually instances of Python classes from another Python file that is being loaded into the Python environment when the program starts. The Python classes (in the video the Cube and Tree classes) create and store Unity objects. Each class also has an update function and a C# script is calling each instances' update function within the overall Unity update loop (allowing for the animation you see). Also shown in the video is that when you look at an object it will display the most recent variable name it is assigned to. This can be turned on and off, but for the main purpose of this project will be important in helping to teach about variable assignment, instances, and object orientation in general. 