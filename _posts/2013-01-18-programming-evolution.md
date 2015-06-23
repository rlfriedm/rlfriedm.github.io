---
layout: post
title:  "Programming Evolution"
date:   2013-01-18 16:52:37
categories: python pygame evolution simulation
---

The potential to artificially mimic evolution has interested me for quite some time. I have always been interested in biology and the ways in which it is possible to study biological behavior using computer simulations. Studying evolutionary processes through the use of programming is particularly fascinating to me; a simulation can select for certain traits that are unlikely to be observed in nature (as well as those that are) and also it can be sped up to allow for a more efficient way to study evolutionary processes.

The most interesting resource I have found on the topic of evolutionary simulation is a study conducted in 1994 by [Karl Sims](http://www.karlsims.com/) called, "Evolving Virtual Creatures."&nbsp;This study seems to be one of the best examples of using virtual creatures to examine evolution. Creatures were initially generated using genetic algorithms to determine both morphology and neural systems. Following this, the virtual creatures were placed into a number of different virtual world environments that were designed to result in selection for certain behaviors (i.e. swimming, walking, etc.). After a certain amount of time, each creature was given a fitness value based on its level of success in the behavior that was being tested for. Creatures with high fitness values relative to the rest of the population were selected to survive and reproduce. Following this procedure, over time through sexual reproduction with random gene mutations, many interesting creatures increasingly well adapted to their environments evolved.

The video below illustrates the fascinating results of this study. Creatures were evolved for everything from being the fastest on land to being the fastest to grab a green cube. In the green cube scenario, the creature closest to the cube at the end of the simulation was declared the winner. Many different strategies to acquire the cube evolved, such as an arm to reach out and grab it and a two armed technique which involved swiping the cube from the side and then moving the cube over to a second arm in order to hold it. Others yet developed a strategy that involved preventing their opponents from acquiring the cube versus trying to acquire it themselves.

<iframe src="http://archive.org/embed/sims_evolved_virtual_creatures_1994" height="480" width="640" frameborder="0"></iframe>

This study and other research I did on the topic inspired me to try to create my own simulation of evolution. My simulation is currently a work in progress. I am using Python with the Pygame graphics library in order to implement a very basic simulation of evolution due to natural selection (based on the organisms’ abilities to acquire food). Currently my “organisms” consist of two different colored squares (male and female). These organisms have three different important traits: speed, size, and how often they switch directions while moving around the screen. Organisms start out with a certain amount of health and their health decreases over time. If an organism’s health goes down to zero, the organism dies.

>![image](http://media.tumblr.com/76f79983b81e4257d1b491961c23788f/tumblr_inline_mgt5b0usUr1renss6.png)
>
> Organisms with randomly generated traits moving around a screen with randomly spawned food.

As of now, I am in the process of implementing reproduction. By selecting for the top food acquiring organisms (and therefore the most evolutionary fit) in each generation and allowing them to reproduce, I believe that certain trends will become apparent. I plan to update my progress on this simulation in the near future.

>![image](http://media.tumblr.com/bf55804862d639fe9ab08b75ecb1068f/tumblr_inline_mgt5doHkc91renss6.png)
>
> The last four remaining organisms from this simulation. As organisms decrease in health their color fades.