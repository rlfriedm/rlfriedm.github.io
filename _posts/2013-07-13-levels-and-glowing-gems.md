---
layout: post
title:  "Levels and Glowing Gems!"
date:   2013-07-13 16:52:37
---

It’s time for another update on the game with working title, Musical Platforms! Since the last post there have been some new additions to the game. There are now levels and a convenient way for me to make them! I didn’t want to have to hard code the locations of all the objects in the game, so I decided to use a pretty simple technique to set up my levels. I have a GameLevel class and this class sets up a level based on an image consisting of black, red, blue, and green colors.&nbsp; I modified an already existing imageToCSV function which originally took black and white images and turned them into a comma separated string of 1s and 0s (indicating black and white pixels respectively). Now this function looks for red, green, and blue color values in addition to black and white and labels them with 2s, 3s, and 4s in the comma separated string. This can also easily be modified to include more colors when I need to represent more game objects

From here I have a function that creates the actual game map from the string of numbers that represents the image. This function creates instances of objects based on their representative colors’ locations in the string. For instance, if 10 black pixels appear in a row then a platform is created based on the location of those pixels as represented by the string. This method makes it easy to create and edit levels using an image editing program (I use [Gimp](http://www.gimp.org/)).

In addition to the ability to create and easily edit levels, there is also a new way to get from level to level. There is now a glowing sparkly gem in every level that the player must find to complete the level and move on to the next. When the player hits this gem the screen flashes and all the music that the player has created by moving around the level up until this point is played back rapidly. The speed and the general way this happens will definitely be tweaked, but the general concept is there.

> ![image](http://media.tumblr.com/0abf144f7ee05ddb346a41b6a3bca35b/tumblr_inline_mprcz2ZR6C1qz4rgp.png)
> 
> The gem!

I’m currently thinking of more ideas as far as gameplay and also story. One thing I want to do soon is to create some sort of enemy in the game. I also want to give the player the ability to, in some form, “throw” his light to illuminate other parts of the map (in a certain range).

Below is a video showing some of the new things:

<p>
<div class="auto-resizable-iframe">
	<div>
		<iframe width="640" height="390" id="youtube_iframe" src="https://www.youtube.com/embed/0pcT8nKD2vs" frameborder="0"></iframe>
	</div>
</div>
</p>



(Arrow keys to move, space bar to jump. Note: there are only 4 levels currently and the game loops back to the beginning after the 4th level)