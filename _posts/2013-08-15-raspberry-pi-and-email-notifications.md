---
layout: post
title:  "The Raspberry Pi and Email Notifications"
date:   2013-08-15 16:52:37
categories: raspberry pi email python
---

This past holiday season I received a [Raspberry Pi](http://raspberrypi.org/‎). The Raspberry Pi is a tiny credit-card sized Linux based computer developed with the intention of making computers, and thus programming, more accessible to kids. The Pi is extremely inexpensive ($25-$35) and surprisingly powerful. Currently there are two varieties of the Pi: The Model A and the Model B (the one I have). The Model B has 512MB of RAM (versus the A’s 256MB) as well as an extra USB port and an Ethernet port. To get a general idea of the Pi's power, according to the Raspberry Pi [website](http://www.raspberrypi.org/faqs), the Pi has graphical capabilities approximately equivalent to the original Xbox.

> My Raspberry Pi in action&nbsp;
> 
> ![image](http://media.tumblr.com/3eda5cedcff2827e40ed8c49b92381e6/tumblr_inline_mrldc38k4b1qz4rgp.jpg)

People have been doing really interesting things with the Pi in addition to using it for learning both in and outside of the classroom. Some examples are: using beets to make music with touch, an automatic [DeviantArt](http://www.deviantart.com/) powered picture frame, using it to control robots, and much more. If interested, [treehugger.com](http://treehugger.com) has compiled a list of [20 awesome projects](http://www.treehugger.com/slideshows/gadgets/20-awesome-projects-raspberry-pi-microcomputers/) completed using the Raspberry Pi.

I had not actually experimented much with mine until a few weekends ago.&nbsp;I always had the idea that I might use the Pi as a way to run some sort of program 24/7; it doesn't take much power and it is a great way to have something running without having to leave the desktop/laptop running all the time. The idea I came up with was to have it run a program that would send me text messages whenever I got an email Gmail classifies as “important”. I wanted to do this for a number of reasons, most importantly because I don’t have a smartphone and during the school year I tend to miss out on important emails. Having the Pi running this program all the time will let me receive my email messages on the go when I’m not near a computer.&nbsp; Gmail does already offer a similar email [SMS](http://en.wikipedia.org/wiki/Short_Message_Service) notification service; however this limits the messages to 160 characters. I wanted to be able to receive longer emails on the go than the Gmail service would offer.

After writing a program to do this on my laptop (with intentions of transferring it over to the Pi) I realized that it would be much easier to do so then and in the future if I could work on my Pi completely remotely. Having it connected to my TV via HDMI and connecting it to a mouse and keyboard worked fine, but I had way too many wires on my desk and since the Pi is tiny and independent, it made more sense to interact with it remotely. The first thing I did was to enable Secure Shell (SSH) on the Pi so that I could access it by SSH from my desktop. At this point, using [PuTTY](http://www.putty.org/) (a SSH client), I was able to remotely connect to and control the Pi from its command line. Also, using [WinSCP](http://winscp.net/eng/index.php) it was then possible to transfer files over via SSH. The last thing I did to enable me to interact totally remotely with the Pi was to set up a remote desktop for the Pi’s GUI using [TightVNC](http://www.tightvnc.com/). At this point I had total control over the Pi from my desktop and I moved the Pi to its current home away from the desk. It’s pretty cool having only two things plugged into the Pi (power and Ethernet) and being able to control it and even see its desktop from my main computer. If anyone with a Pi happens across this post and is looking for the best way to do all of the above, check out [this really helpful tutorial](http://www.howtogeek.com/141157/how-to-configure-your-raspberry-pi-for-remote-shell-desktop-and-file-transfer/all/).

> The Raspberry Pi's desktop
> 
> ![image](http://media.tumblr.com/fe9720922b4a61160f8e015252a907b0/tumblr_inline_mrldnf3V5q1qz4rgp.jpg)

Now I will go into a bit more detail about the actual email to SMS notifier program. Initially I started out by writing some functions to check for new mail and then notify via SMS of new important mail. However, I quickly realized that it made more sense to create a SMS Notifier class to make the program more adaptable. This class has three methods: start, checkMail, and notify. Each new instance of this class is initialized with five parameters: the username of the Gmail account to be checked, its password, the rest time to wait before checking for more mail, the maximum number of texts the notifier will send, and the SMS address for the phone the messages are being sent to (i.e.: 1234567890@vtext.com).

When the start method is called on a notifier, the notifier starts checking for mail and will do so until the program is manually exited. It waits a specified period of time before calling the checkMail function again to check for more new emails (I usually have it check every 60 seconds). The checkMail method checks to see if there are new email messages that Gmail has classified as important. It is set up so that it will not mark any emails as read (even after it notifies the user about them). This is a personal preference but can easily be switched. Then, for each new message it finds, the plain text from the email is extracted and stored as a string. Next, the sender and subject are extracted and the notify method is called with these fields combined into one big string (sender, subject, and message) as a parameter. The notify method sets up the connection to Gmail to send the SMS message(s) from the user’s email account. From here, the function breaks the message down into 160 (or less) character parts and these are sent as SMS messages (text messages) to the specified SMS phone address up to the user’s specified maximum number of 160 character texts.

Here is an example use of the class:

{% highlight python %}
notifier = Email_SMS_Notifier(yourGmailUsername, yourGmailPassword, 60, 3, yourSMSAddress)
notifier.start()
{% endhighlight %}

If you would like to look at the code yourself and/or are in need of a good Gmail text message notification system, check out my code [here](https://github.com/rlfriedm/Email_SMS_Notifier).&nbsp;