---
title: Platform check
author: GG
layout: post
icon: fa-lightbulb
icon-style: regular
---

<h3>1. Maintaining the platform</h3>

If you got so far that it means that you are very much convinced (as I am) that it is absolute MUST HAVE on every development project with mobile support to automate mobile testing.
But as every tool also this might be out of order. And I can bet this moment will happen exactly when you gonna neeed it most. So how to avoid this? We need to write some health checks.
As my project is growing and I expect to get more teams using my platform within company it is good to create some kind of security which will prevent concurrent builds from running on the same device
at the same time. I have found out that when two test will hit the same appium instance at once then appium gets totally crazy and simply does not know which call should be served.
Webdriver requests keep comming from both tests and whenever appium tries to complete one of them the other one is stopping it from it. As a result appium gets into endless loop when none of
this two tests are going to be handled. And this is one of the health checks - to establish if mobile is currently in use and no tests should be triggered at the moment or we are good to go.
Second health check should tell us about the real platform condition - if the connection between computer and mobiles is stable. Unfortunatelly the only way to do it currently is to init appium driver.
If the driver will get created with no errors then connection is stable. Otherwise there is something wrong. And basically that's it. Sounds easy doesn't it?

<h3>2. Device availiability check.</h3>

I have to confess to you that I did not get any working solution for the first problem. I found a way to read android console logs via ADB but when I set up a jenkins job then I realize that many times there
are still some appium logs in mobile processes so my check was giving me some fake results. Which is worse to get IOs logs you need to jailbreak the device and then you gonna lose your warranty. Anyway
due to fact that no other team is using my platform and I and my collegue are the only users then I decided to leave this check for now. The best workaround I found so far is to setup postponing jobs on Jenkins.
There is an option to select if some other jobs are currently running then postpone this one until other are finished. And this solution is doing a job very well.


<h3>3. Platform condition check.</h3>

Happily I managed to implement platform condition check more successfully than previous one. As I said before - idea was simple - to init appium driver. Let's see my implementation:

 <pre><code>

appium_port = get_free_port()
appium_params = APPIUM.get(device).format(appium_port)
process = subprocess.Popen(appium_params, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
time.sleep(4)
system_port = get_free_port()
CAPS.get(device).update({"systemPort": system_port})
eval(ENV.get(device).format(port=appium_port, caps=CAPS.get(device)))

  </code></pre>

To make sure the code is working we need to trigger it for all devices. The best way to do it setup Jenkins job. And this is where I got disappointed again. Apparentely while running the tests for all devicess
at the same time another error occured - <code> [Errno 61] Connection refused </code>. I also discovered that the same error appears also for my tests in a first attempt. Then, my tests pass but in a first
try they fail with the same error. I found out that this error comes from urlib which is part of selenium which is part of appium. It happens when connetion is distrupted somehow. I could not find the answer
why is that. I decided to try-catch it and try again. In the second implementation I have got to this:

  <pre><code>
for trial in range(7):
    try:
        eval(ENV.get(device).format(port=appium_port, caps=CAPS.get(device)))
        print('{0} STABLE>>>>>>>>>'.format(device))
        process.send_signal(signal.SIGINT)
        break
    except Exception as e:
        for error in APPIUM_WD_ERROR_MSG:
            if error in e.msg:
                print('{error} occured while checing {device}  I am trying again!'.format(error=error, device=device))
                time.sleep(randint(1, 5))
        else:
            process.send_signal(signal.SIGINT)
            if 'Unknown device or simulator UDID' in e.msg:
                raise ValueError('{0} is taken out from the platform'.format(device))
            else:
                raise ValueError('UNKNOWN ERROR OCCURED WHILE CHECKING {0}: '.format(device) + e.msg)

else:
    print("Unstable devices {0}".format(device))
    process.send_signal(signal.SIGINT)
    raise ValueError('{0} is connected but after 7 attempts {0} is not answering'.format(device))
   </code></pre>

To make sure my tests are now stable I have added the same try for my environment.py. Luckily I havn't seen this error any more. 
And that's it for this time. My checks are triggered by Jenkins periodically, tests are now fully stable. 
As ussually you can found my code on <a href="https://github.com/appiumator/appmation1">GitHub!</a> profile.

<center><a href="https://appiumator.github.io/2018/11/04/running-test-by-jenkins.html"><<<Previous post - "Running test by jenkins"</a></center>