---
title: Jenkins plugins
author: GG
layout: post
---
My developmnent team ( 5 front end devs + 2 QA) is responsible for 8 projects at the moment. It's impossible to maintain so much code without automation and CI.
That is why I focuse so much on Jenkins. As I promised in some of the previous posts I will share today with you my favourite Jenkins plugins which I can't really live without honestly.
Unfortunatelly I can't share with you screenshots from the jobs I created due to my contract limitations so I will use screenshots from official plugin docs.

<h3>1. Naginator.</h3>

When you need to put some parameters to your tests you will propobly use multi-job task. This is very convinience way of running whole reggresion by one click and see output sorted by the test parameter.
Naginator plugin gives you te possibilit to rerun failed configurations. It is very important especially in e2e testing. There is plenty of things which are difficult to predict which can fail our tests.
And still it does not mean that our tests are poor quality - simply many things can be a bit lagged and load a bit slower than ussually and our reggresion must fail. The solution for this is to retry job.
But question is if we really want to repeat whole regression for one test? Not really. And this is why Naginator came to live! you can simply schedulle to retry only failed configurations as many times you want
with timeout so long as you want. Really time-saving chap! More details can be found on <a href="https://wiki.jenkins.io/display/JENKINS/Naginator+Plugin"> https://wiki.jenkins.io/display/JENKINS/Naginator+Plugin</a>.
Highly recommended!

<h3>2. Display Console Output.</h3>

Personally I think to get to the real stacktrace of the code we need to go too deep trough the job structures. I want my error throw out now! That is why I am using Display Console Output
This plugin inputs the console output just on the single job main view. It is really usefull. You can find more information on 
<a href="https://wiki.jenkins.io/display/JENKINS/Display+Console+Output+Plugin"> https://wiki.jenkins.io/display/JENKINS/Display+Console+Output+Plugin</a>. 
<a href="#" class="image fit"><img src="{{ 'assets/images/display-console-output-plugin_75.png' | relative_url }}" alt="XCode" /></a>

<h3>3.Console Tail.</h3>

I believe a realiable and quick answer for the question what have failed is a key in our job. That is why I found another plugin related with console output. This one works great with multi-job tasks.
Simply prints the job console output straight on the multi-job view. I know exactly which configurations with which parameter have failed so I can tell which part of my regression is down. By clicking on
link in this console output I am redirected straight to the single job which got failed and with Display Console Output plugin I have got full view of the situation very quickly. See  
<a href="https://wiki.jenkins.io/display/JENKINS/Console+Tail+Plugin"> https://wiki.jenkins.io/display/JENKINS/Console+Tail+Plugin</a>. for more details.
<a href="#" class="image fit"><img src="{{ 'assets/images/tail.png' | relative_url }}" alt="XCode" /></a>

<h3>3.Dashboard view.</h3>

When you need to maintain many projects in the same time you want to keep your jenkins jobs within some kind of folders. Otherwise you will end up with a list of reggresions and health checks and after
a few days you will see that this is not so easy to find exactly this job you currently need. The answer for this problem is in Dashboard view plugin. It allows to group your job and keep them in seperate
tabs. To find the regression you need to run currently is a piece of cake now.

<a href="https://wiki.jenkins.io/display/JENKINS/Dashboard+View"> https://wiki.jenkins.io/display/JENKINS/Dashboard+View</a>. for more details.
<a href="#" class="image fit"><img src="{{ 'assets/images/dashboard.png' | relative_url }}" alt="XCode" /></a>

<h3>4.Build monitor plugin.</h3>

Recently my team is working also on our own tools for github monitoring and also for jenkins monitoring. Despite this for a long time we ware using plugin implemented by Jan Molak which is called
Build Monitor. This simple plugin uses Jenkins API to get job statuses and displays them in very nice and readable form with a live update. When you need to be sure no failure will go happen without
your attention it is another must have plugin on your list. I used to put my health checks and reggresions on this monitor and then when I get to my job I could see straight if something failed.
Thanks Jan for this!
<a href="https://wiki.jenkins.io/display/JENKINS/Build+Monitor+Plugin"> https://wiki.jenkins.io/display/JENKINS/Build+Monitor+Plugin</a>. for more details.
<a href="#" class="image fit"><img src="{{ 'assets/images/monitor.png' | relative_url }}" alt="XCode" /></a>

<h3>5. Configuration slicing.</h3>

How many times I was editing n-number of simmilar jobs and adding some single change like timeout or naming pattern change and I forgot about one of the builds and caused another problems....
Never again such ridiculus cases. I decided to find something which will allow me for some kind of bulk change for my jobs. There is some way to get this by editing something via API but
I thought there must be a better way and my QA partner found for us this - Configuration Slicing Plugin. You can't edit every single parameters of your jobs by this but still many of them
can be sorted by simple click and you can be sure you did not forget about any build. If you ask me I would say is a graet tool if you've got to maintain many projects at once.

<a href="https://wiki.jenkins.io/display/JENKINS/Configuration+Slicing+Plugin"> https://wiki.jenkins.io/display/JENKINS/Configuration+Slicing+Plugin</a>. if you want to know more.
<a href="#" class="image fit"><img src="{{ 'assets/images/slice.png' | relative_url }}" alt="XCode" /></a>

<h3>6. Backup plugin.</h3>

When I was setting up Jenkins from scratch by the first time I was playing around with some commands found on stacktrace and I went one step to far once day. There was a command which removed
whole jenkins folder from a hard drive. I was literally pissed. Then I Product Owner said some 'words of wisdom': "People generraly can be classified by this who make backups and who don't.
The intresting fact is that in some moment people decide to change the team and joins this who make backup." After this I became another great example of person who joined people making backup.
And because there is so many great plugins for Jenkins available then there must be something which will creates beautifull backups for me and don't bother me with it. And I found - Backup plugin. Really a
misterius name isn't it? Of course is not - It is doing exactly what the name suggests it could. In a few words it basically makes the backups with whole configuration and jobs you are created with all settigs.
Backup files can be stored in any specified direction so command 'remove folder' should not cause a disaster any more. You can set the frequancy how often a backup should be created 
Again <a href="https://wiki.jenkins.io/display/JENKINS/Backup+Plugin"> https://wiki.jenkins.io/display/JENKINS/Configuration+Slicing+Plugin</a>. for some more. Highly recommended as well!


And that's pretty much it. I hope you will find something usefull in this set of plugins which will help you to track bugs. For me this is absolute must have. Also if you want you can share some
plugins you recommend for test automation which didn't get to this list this time and are your live-saver on yor project in commends below the post.
See you next time!

 <center><a href="https://appiumator.github.io/2018/11/13/platform-check.html">Previous post - "Platform checks."   </a> <a href="https://appiumator.github.io2018/11/23/swollen-samsung.html">Next post - "Swollen Samsung"</a></center>

 
