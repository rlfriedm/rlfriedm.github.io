---
layout: post
title:  "Quine-Tastic!"
date:   2013-02-05 16:52:37
---

This semester I am taking a course called Principles of Programming Languages. For our first lab assignment we were tasked with writing a self-reproducing program in our language of choice. Self-reproducing programs, or [quines](http://en.wikipedia.org/wiki/Quine_(computing) "quines"), take no input and output themselves exactly. We had to come up with a non-trivial solution to the problem (which meant not just retrieving and outputting the source code). I chose to write my program in Python because it seemed to be the best choice in terms of the ease of string manipulation.

My first solution involved using a list and appending string representations of all the lines of code to that list. My thought process behind this method was that by using a list I would be able to print out all of the items in the list (the strings representing the program’s code) and then modify these strings to print out the lines in which they were appended to the list using for loops. While I did end up getting this method working, I wasn’t satisfied with the length of the program so I&nbsp;decided to approach it slightly differently.

My final solution ended up as:
{% highlight python %}
text="text=print text[:5]+chr(34)+text[0:]+chr(34); print text[5:]"
print text[:5]+chr(34)+text[0:]+chr(34); print text[5:]
{% endhighlight %}

This solution simply consists of a string representation of the entirety of the program’s functional code followed by the functional code itself. Printing different slices of the text string allowed me to output the line&nbsp;where the text variable is defined followed by the rest of the program.

Being able to directly run the output of a program is something new and interesting to me. This past week we were actually assigned to write another program whose output could be run. The assignment was to write a program in Perl to create C++ Makefiles for a given directory. While Perl isn’t my favorite language, mainly due to its lack of readability, I do appreciate its usefulness (and the fact that I won’t have to manually write a C++ Makefile for quite some time!). &nbsp;