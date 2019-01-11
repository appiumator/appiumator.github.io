---
title: Cross functioning
author: GG
layout: post
---
It is not easy to answer for a future of QA engineering. Some people say that this position has to extinct because there is bo need for testing. 
Personally I doubt it very much. In high demanding world of IT I cant imagine any software without QA. So what else? Well some others say that QA will 
need to be more flexible and have to adapt new skills especially in coding to be able to fix the bugs. For this moment I am now facing this new chellange.

<h3>1. Lack of resources.</h3>

It is a fact that the QAs are in inbalance to developers in a dev team. There are finacial reasons behind this I believe. 
But this situation may lead to some kind of bottleneck in production. To keep CD a testing process might be incomplete which causes reducing of quality. 
So how to avoid losing quality when hiring new testers is not possible and all known tools have been already used? The answerd might be a cross functional team.


<h3>2.Cross functional development team</h3>

What is this cross functional team? In simple words it means that testers can help devs in some simple tasks and devs can do some testig.
 At the end of a day we all have got a common goal - to develop the best quality products.
In real world I can bet with you that devs will try to do not test no matter what. This atitude can be even stronger when your tests are in 
different languange than a product application code. They will try to cover themselves by job describtion which might be vary in diffwrent companies. 
In mine everyone has the same duty - to develop applications. The low level agreements are between employee and employer. We've been thinking how to work around this impass for 3 past months

<h3>3.The way to success.</h3>
.
<quote>“Be the change that you wish to see in the world.”</quote>

― Mahatma Gandhi

It is much easier to convnince devs to help with tests when the main application and tests are in the same languange. If there are differences then someone needs to learn new language
But no one wants to do something more than is ment to be doing apart from the regular duty. That is why we QAs needs to make a step forward and follow the main application source language code.
In my team we made a decission to start writing tests in JavaScript as the main application is purely font end. At the beginning devs said that they will help with PR and make sure the code is in
the best possible JS standards. As an exchange we offered in future when we will be skilled in JS enought to fix simple bugs. They also said they will not write the tests anyway.
Me and my QA partner decided to go this way anyway. 
At the beginning it wasn't easy at all. JS environment is completely different than Python. There is a lot dependencies which needs to be met to run tests based on selenium. After two weeks of failing
team decided to assign one of the devs to establish a decent test base with all libraries and dependencies required to write e2e front end testing. That was the best what could happen. Assigned developer
who was the greatest opponent to write tests beloved that and said after esstablishing the base he will write tests when testers will be overworked because tests are much more interesting than heoriginally thought.

<h3>4. Conclusion.</h3>

Right now my first e2e test in JS is in PR. We are now deciding if we should follow the coding standards which are in use in my team when coding in JS but the logic is ready. We we'll see how things go but 
I am very optimistic about what is going to happen.

 <center><a href="https://appiumator.github.io/2018/12/25/expansion.html">Previous post - "Expansion." </a> </center>

 
