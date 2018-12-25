---
title: Swollen Samsung
author: GG
layout: post
---

Some say no pain no gain - This is what happened to our Samsung:

<a href="#" class="image fit"><img src="/assets/images/samsung.png" alt="XCode" /></a>

I know that keeping mobiles plugged in for too long can damage the battery but this is something I didn't expect. It got swollen like bitten by hornet. But to be fair I had with this Samsung some problems before. I used to love this model (A3 2017) when I was using it for manual testing. It's nicely shaped, quick but the bad things started after software updating to Android 7 and in our specs this should remain as Android 5. I remember I blocked auto updates but still it managed to happen somehow. So we had to perform a downgrade which is never a great thing for a mobile phone. After that whole system slowed down critically and become absolutely useless. I send it back to service desk and guys managed to apply a different version of android 5. That helped a bit but still I had a feeling that this phone won't last for too long. And here we are - swollen battery.

We found some solution in the internet for this situation .

<h3>1. Arduino</h3>

<a href="https://www.testdevlab.com/blog/2016/08/how-to-create-programmatically-switchable-usb-hub/">https://www.testdevlab.com/blog/2016/08/how-to-create-programmatically-switchable-usb-hub/</a>

That sounds great but if you are not skilled in micro soldering then I doubt you will choose this solution. Arduino is just microcontroller which needs some adapting for our needs. If you feel like you are master of DIY - do it definitely! You are not going to find any better solution.

<h3>2. Switchable hub</h3>

<a href="https://www.yepkit.com/products/ykush">https://www.yepkit.com/products/ykush/</a>
 
Well this looks optimistic - is reasonably cheap and give us the control over the hub from the computer which allows us to write some scripts which will switch on and off power when it's needed. I must say actually this is my favourite solution so fair.

<h3>3. Timer Switch</h3>

<a href="https://www.ebay.com/bhp/timer-switch">https://www.ebay.com/bhp/timer-switch</a>

This is the cheapest option - You can get it just like for free. Just set a time when power should be switched off and put blues brothers sun glasses on. I am just a bit worried how it will be affecting the battery status. There are different devices plugged in and we feed them within the same rigorous time frame. I think it is possible to get some conclusion what is the best window for all of the devices but this needs some testing.

<h3>4. Just switch off the power on your USB HUB</h3>

A budget solution - no costs at all. And this is where I started. So I tested it. Outcome was is that devices still get some juice from the USB port in PC but it's definitely enough for 4 devices. LG G6 was fine - It has the smallest screen and performance so I expected this to live long. IPhone looked like be draining most of the juice for some reason because the battery was nearly 100% all the time. The problem was with Xiaomi - The battery was getting lower and lower to be finally dead after the week of time (which actually is  a great note but for unplugged phone, not for constant charging!). I need to add also that Samsung is in service now for battery replacing and was not included into set for this test. Also which is weird Jenkins failed to communicate with the devices - there was an error  with 'unknown device' message. But when I was running my tests from command line all was fine. Anyway as a final conclusion I can say one thing - this is a dead end solution.

I will keep you posted about the next solutions. You can share in comments what you are doing to keep your mobiles well during testing.


<center><a href="https://appiumator.github.io/2018/11/15/jenkins-plugins.html">Previous post - "Jenkins plugins."</a><a href="https://appiumator.github.io2018/11/23/expansion.html">Next post - "Expansion"</a></center>

