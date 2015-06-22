---
layout: post
title:  "Generating Haiku - Poems Uncontrolled"
date:   2013-03-13 16:52:37
categories: haiku python
---


It has been a while since my last post (approximately 3 months) and the semester is now coming to a close. I finally had time this past weekend to work on something non-class related (though I probably should have been studying for finals). This summer I will be working on a research project at Hamilton dealing with [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis),&nbsp;so I decided to spend a bit of time researching [natural language processing](http://en.wikipedia.org/wiki/Natural_language_processing) (NLP). From this, I decided a neat thing to do would be to write a program to generate (mostly) random&nbsp;haiku&nbsp;with the help of the [Natural Language Toolkit ](http://nltk.org/)(NLTK) for Python.

The first thing I did was to generate a giant Python dictionary consisting of syllable counts as keys and lists of words with that syllable count as values. To do so, I processed the [CMU dictionary](http://www.speech.cs.cmu.edu/cgi-bin/cmudict) to get each word’s syllable count and then added it to my new Python dictionary under the correct syllable count key. I decided to exclude proper names and any non-English words to make the&nbsp;haiku&nbsp;read better. To do so I used a module from NLTK called wordnet. I called wordnet.synsets(word) for each word from the CMU dictionary; this finds all English synonyms for a word. Therefore, if the word was a name or not in English, then the result of this evaluated to false and it&nbsp;did not get included in my syllable dictionary.

Following this, I saved this dictionary using the module Pickle so I would only have to construct the syllable dictionary once. &nbsp;Then I wrote a program that uses this dictionary to create entirely random&nbsp;haiku. This generated&nbsp;haiku&nbsp;with the 5, 7, 5 syllable line pattern and I actually had some interesting results. A few of the best are as follows:

> unprofessional
>
> radioactivity
>
> exterminated
 
> skilled monogamy
>
> nondiscriminatory
>
> invigorated
 
> x. undiagnosed    <- seemed like something out of sci-fi
>
> denationalization
>
> immortalizing

As you can probably see, most of the best entirely random&nbsp;haiku&nbsp;were ones with shorter lines (meaning less individual words). I did generate&nbsp;haiku&nbsp;with up to 4 words for the 5 syllable lines and up to 6 for the 7 syllable lines, but most of these did not flow very well. Here is an interesting example with more words created before I added in the English word checking:

> ink impersonates&nbsp;
> 
> captain luhr noell iwerks pub&nbsp;
> 
> bumbly staccato&nbsp;

At this point I wanted to try to make it so that the program would be more likely to generate lines consisting of words that flowed well together. From my brief foray into NLP and NLTK I remembered collocations and bigrams. [Collocations](http://en.wikipedia.org/wiki/Collocation) are sequences of words that occur together often and bigrams are pairs of words. I wanted my&nbsp;haiku&nbsp;to consist of frequently used bigram collocations interspersed with the more random words from my initial haiku creation system. I did this similarly to the way that I created the initial syllable look up dictionary; I created a dictionary of syllable count keys paired with a list of lists consisting of common bigrams with that syllable count total (the sum of the syllables in each word in the bigram). I used my original syllable dictionary to&nbsp;look up&nbsp;the syllable counts for the words in each bigram.

To find common bigrams I used NLTK and the included [Brown](http://icame.uib.no/brown/bcm.html) and [Gutenberg](http://www.gutenberg.org/) Corpuses. This could be easily modified to increase bigram diversity by simply creating another bigram syllable dictionary for another corpus. Like before, I stored these new Python dictionaries using the Pickle module so they would only ever need to be created once. Each dictionary took more than 5 minutes to create so this is definitely a necessity. Plus, it would be silly to process giant text corpuses every time you wanted to generate&nbsp;haiku.

I then modified my initial haiku creating program to add in bigrams. To see exactly how this was done you can view my code on [Github](https://github.com/rlfriedm/HaikuGenerator), but basically if the number of syllables required is greater than 1 then there is a ~67% chance that the program will use a bigram instead of a random word (~33% chance of one from either of the bigram dictionaries). I also wanted to include the possibility to have completely random words instead of just&nbsp;haiku&nbsp;consisting of bigrams entirely, so I left in a ~33% chance for a word to be chosen from the original syllable dictionary. And also, if a 1 syllable word is required to construct the line, then clearly the bigram dictionary would not be useful (there are no 1 syllable bigrams).

I’ve included a voice recording of me reading some of my favorite&nbsp;haiku&nbsp;produced this way and here are the texts listed below:

<iframe src="https://w.soundcloud.com/player/?url=http%3A%2F%2Fapi.soundcloud.com%2Ftracks%2F92043148" width="100%" height="166" frameborder="no"></iframe>

As you can probably see, there are some phrases that actually make sense within these&nbsp;haiku. The more I generate the more interesting ones I seem to come across. Since I can generate 1,000 new ones in under a second, I have endless haiku to read!

I plan to continue improving this program to possibly incorporate trigrams (3 commonly used together words) and also to give some control over the&nbsp;haiku&nbsp;themes. I can see this second part being done using NLTK to find words commonly associated with a given word and then building the haiku around that. Say for instance that you wanted to generate a haiku about snow, the word snow could be looked up and found to be associated with: penguins, ice, cold, icicle, etc. And then with that list a themed haiku could be generated.

As mentioned earlier, all the code for this project can be found on my [Github](https://github.com/rlfriedm/HaikuGenerator) account. A few final notes: it took me this long to realize that the plural form of haiku is haiku! I have been writing "haikus" for far too long. And also, the title subscript, poems uncontrolled, was actually from one of the generated haiku (rather fitting if I don't say so myself).