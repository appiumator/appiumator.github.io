---
title: Introduction
author: GG
layout: post
---

<h3>1. Reason.</h3>

By living in 21st century our lives are a way different than they ware before. Over the years of constant development in sharing informations it is now unbreakable standard of our lives to posses information via internet.
Thanks to some smart guys in companies like Apple or Samsung we are now able to do in anytime anywhere by using mobiles. This fact pushed the IT companies to adapt to this trends and most of modern web apps are now responsive and fully accesable via mobile phones. 
This very convinient way made a great impact in a way of designing apps. To make sure such a great market demands are reachable there is a great chellange for QA lads, to achive the best possible product quality as it it possible. How to achive it?

We need to answer a most important question - how we wanna make sure that our app is fully working on every mobile OS and every mobile. Well, the best solution would be to test it one by one on every availiable on a availiable on market model of mobile phone. 
Sounds hecktig, doesn't it? Let's try to find some other way.

<h3>2. Idea.</h3>

Let's state then - we need some automation to achive this great goal. How we gonna do it? There are two ways. We can simulate environments, and then probably we we'll cover more possible devices but IMHO that approach does not gives me enough confidance in term of reliability when working with simulators.
 I believe it is better to cover the most popular devices and OS and make a good assumption that behaviour of application will be the same on other models(kind of equivalent classes method) and make a tests on selected real devices. I did it in my project and I can sign under this solution with both hands(and other precious parts of body).

In my project I am using 4 mobiles, one IPhone with latest IOS version, and three mobiles with android OS versions as follows 5, 6 , 7. That gives me a good picture of how the app can look like when some block will be viewing it on his mobile.

<h3>3. Solutions.</h3>

The next question is how we can automate mobile tests? TBH it is easier than can be imagined. The most important thing is to choose correct for your needs test tool which will be a great tool in QA's hand but not become a great friend with no benefits(then it is not a friend any more in this case, correct?). 
First of all we need something which will allow us to use existing tests written in one of the most popular programming languages availiable plus additionally if it is a frontend App it will support a Selenium Webdriver. Second thing is which needs to be doable is to select a mobile easy enought to don't get crazy while running tests.
 And the last condition is to run tests remotely to make sure that you are not the only person in who can run the test. So what's gonna be the best tool to get this requirements done? There are two answers:

<dl>
		<dt>Solution 1</dt>
		<dd>
			<p>Go to cloud solutions. I don't want to link here to any service which provides this solution. It's easy to google. That is a great way if you have got some spare money to spent or your boss is very open-minded. But be sure this solutions is not cheap. If that's is not a problem for you, you are not gonna find this blog as interesting, rather waste of time. I did not have this money to proof my concept of automating tests for mobile devices so I jumped straight to second solution.</p>
		</dd>
		<dt>Solution 2</dt>
		<dd>
			<p>Create your own platform. Considering 3 AC I stated above my choice was easy - I decided to use Appium framework. And this decision redifined my testing that they became fascinating like never before.</p>
		</dd>
</dl>


If You got so far in reading this article that means I have got your interest. I promise to take care of this gift and describe as easy and detailed as possible how to run the automated tests using Appium for real devices. Shall we... ?

<center><a href="https://appiumator.github.io/2018/10/19/first-mobile-test-on-android.html">Next post - "First mobile test on android device"</a></center>