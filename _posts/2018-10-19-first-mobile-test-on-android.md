---
title: First mobile test on android device
author: GG
layout: post
icon: fa-lightbulb
icon-style: regular
---

<h3>1. Appium - what is it?</h3>


Before we get to the point, let's stop for a while to talk about Appium itself.


Appium is a free open source project. The whole idea is to create a stable bridge between mobile and computer without coding in SDK or recompiling your app. Requirements? Pretty low: Android SDK, XCode. And this is the only real limitation  - to use XCode you need Mac OS if you want to run your tests on IOS devices. As IMHO to get a full cover it is a must have to run tests on IOS so I will create a guide with usage of Mac OS. However running appium on Android device looks exactly the same on Windows so everyone no matter of what OS is using can follow this article. OK let's ROCK!


Here we go. At first we need to install some additional staff. Let's start from scratch then. We need to install Node.js. To do this open your command line and type <code>brew install node</code> (but not with sudo!). After a few moments as a happy user of Node.js let's install appium by hiting <code>npm install -g appium</code> (but not with sudo!). This command will install the latests stable version of appium. For now it is 1.9.1. What is the most important for us, since 1.8.0 appium is able to run tests parallel which is a milestone in mobile tests automation. 

Alright so we have got node, appium and to make installing easy let's install some health check by typing <code>npm install -g appium-doctor</code>. Now type <code>appium-doctor</code> and see what else do we need. Most likely appium-doctor diagnosed missing java, android sdk, and the latest Xcode version. So the next step is to install from official website latest JAVA SDK and adding it to JAVA_HOME to PATH. To verify if java is succesfully added to PATH type <code>echo &JAVA_HOME</code> and in response you should see the path you set in your PATH. Run your appium-doctor again and you should see that this dependency is met now. Let's move on and install android SDK. It is also recommended to use the latest version and add ANDROID_HOME to PATH. Again to verify you configured your PATH correctly type <code>echo &ANDROID_HOME</code> and check if responded path is correct. Run appium-doctor again and see if dependecies are met. As a last point is to make sure you have got latest XCODE installed. To do it, go to AppStore and find XCODE and press UPDATE. Now we can check appium-doctor for the last time and all dependecies should be green now. Congratulation! You have just configured Appium!

 
<h3>2. Let's do some coding then!</h3>


I usually code my tests in python, so for the example I will use ready solutions which I implemented in this language. Before we start we need to install client by running <code>pip install appium-python-client</code>.

There are few mandatory appium capabilities which needs to be specified while running tests. I pass them as a dictionary when create driver.

 <pre><code>
{% highlight python %}
    CAPS_ANDROID = {

        'platformName': 'Android', # this tells appium what platform you want to test

        'platformVersion': '7.1.2', # this as you have already guessed tells what OS version is installed on the device

        'deviceName': 'Android', # as a name you can type whatever

        'browserName': 'Chrome', # for Android Devices the supported browser is Chrome, for IPhone - Safari

        'clearSystemFiles': True, # it's not mandatory but it is very wise to clear a workspace after test

        'automationName': 'UiAutomator2', # there are two automators implemented in Appium but this one is the letest child and supports latest OS and parallel testing and works quicker than previous

        "udid": "", # that is the uniqe for every mobile idetificator which we need to obtain in a sec

    }
{% endhighlight %}
  </code></pre>

Now let's focus on missing udid. To obtain it we need to use a tool which got installed with Android SDK automatically - ADB. Please make sure you have connected via USB cable your mobile corretly. We need to go to command line and type <code>adb devices</code>. As a response we can see:

  <pre><code>

List of devices attached

YOGAA1BBB412    device

   </code></pre>

And now all we need to do is to copy 'YOGAA1BBB412' and pass it as udid in our CAPS.

 

Let's get back to coding. The line which creates webdriver is the same as for Selenium. So in practice we use:

   <pre><code>

from appium import webdriver

 

webdriver.Remote('http://127.0.0.0:4726/wd/hub', {})".format(CAPS_ANDROID)

    </code></pre>

In general appium driver is an extention of selenium webdriver so that is why all commands works in the same way. In this case we are creating Remote driver and as server we are passing IP address with specific port (remember this port as we will be hiting this in a while) and with capabilities set above. The rest remains the same as you are ussually working with Selenium Webdriver.

 

<h3> Run Appium server.</h3>	

Let's go to command line. In the easiest case we can just simply type appium and we we'll see fully working appium server listening on some default port. But for a future reference we can distinct it now by port we have already declared when calling webdriver - 4726. So we type <code>appium -p 4726</code> and we can see Appium Welcome message:

 <pre><code>

(node:16139) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.

[Appium] Welcome to Appium v1.8.0

[Appium] Non-default server args:

[Appium]   port: 4726

[Appium] Appium REST http interface listener started on 0.0.0.0:4726

 </code></pre>

The last line is most important - tells us that we started a server on local machine listining at specified port.

 

Now we get back to the code. Let's say we run a simple test which we'll open Google and search for 'Appium'. For the implementation I leave you a free will but an example can be found on my <a href="https://github.com/appiumator/appmation1">GitHub!</a> profile.

And here we go. If everything went fine, when we start our tests we should see the great movement in appium instance. First what's gonna happen is that ADB will install Appium client on our mobile which will allow it to oparate a browser. Oh, by the way - Chrome browser MUST be installed on the device. Then appium will do some basic checks and will open a browser, hit the google.com url and type the phrase. After all we'll close the browser and Wuala! First Mobile test passed!


<center><a href="https://appiumator.github.io/2018/10/08/introduction.html">Previous post - "Introduction"   </a> <a href="https://appiumator.github.io/2018/10/20/paralellAndIphoneTesting.html">Next post - "Parallel and IPhone testing"</a></center>