---
title: Running test by jenkins
author: GG
layout: post
---

Alright folks now you can be very much exited! Now you know how to run your tests on mobile devices, no matter what OS is on board, for a time saving you can run them paralelly and even see the reports of it in a nice and easy readable way!
How cool is that? Well, not so much TBH.
Let's be honest - in 2018 CI is everything. No one really runs tests by hand for too long. That can quickly became to be very boring. Also it might be time consuming if you have got more than one product to maintain with your team.
I decided to upload all my tests on jenkins very quickly. But what I thougt will be piece of cake then became pain in the a**.
Also by this moment it might be great to dedicate some testing machine responsible for your test. It should contain all enviromental setting which I explained in my previous post required to run tests on mobile devices. Obviously the devices should be plugged into that machine as well.
What is also important this machine should be rechable by your computer. To make sure you can call it to run your tests simply try to ping it with the IP address of this machine from your command line. If all network configuration is fine then you should see ping responses showing up in your terminal.
To run your tests remotely from your machine all what needs to be done you need to edit your code where you create a appium webdriver so :

<pre>
	<code>

		mobile_driver.Remote('http://<address_ip_of_your_testing_machine>:<appium_port>/wd/hub', {caps})
		
	</code>
</pre>

OK let's get back to Jenkins. I hope you know what Jenkins is. If no, then please read the official website <a href="https://jenkins.io/">https://jenkins.io/</a>. You gonna find all information how to run your Jenkins server and how to install all usefull plugins. Which plugins I personally perefer will explained in some future post.
If I good remember I had some problems with enviromental variables but I can't really tell how I managed to fix this issues - all information can be googled.
OK so what do we need to make sure Jenkins will manage your tests? Well to make sure any tester or Jenkins can run tests it is important to be make every tests will be using unique Appium instance. Otherwise tests will clash and throw errors.
That approach should avoid a lot of problems just on the start. But how to do this? Well I found some implementation in java language with some external dependencies how to run appium server but as you already know I write my tests in Python and I did not like this solution.
Shortly I decided to implement my own way of creating Appium instance just before creating webdriver and then to kill it shortly after the test is finished. The answer is in this line of code:

<pre>
	<code>
 
		subprocess.Popen(<your_command>, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
	
	</code>
</pre>
 
 Subproces Popen opens a terminall for you. Shell = true allows you to use it as a shell command line stdout=subprocess.PIPE hides what is displayed in the terminal. It is important because what is appium should not be bothering you. All what we should be focused is test results that's why we skip appium logs.
 But don't worry - if something will go wrong then errors from appium will still be shown in tests results.
 
 Then in your after_all method you should mention this line:
 
<pre>
	<code>
  
		subprocess.send_signal(signal.SIGINT)
	
	</code>
</pre>

 This line will simply close the terminal and kill the appium server - exactly like ctrl + C.
 
 Great! Everything looks easy. Feeling great excitement to see my test managed by Jenkins I pointed my job on Jenkins to github repository and then troubles began. Simply everytime when I ran my tests paralelly on seperate devices an ugly error come up on the first attempt:
 
<pre>
	<code>
 
		ECONNREFUSED - Connection refused by server
		
	</code>
</pre>
 
 What the heck is this now?! I have never seen such an error while running my tests. I was fighting over the week whith this crap. After a lot of new wrinkles appeered on my face I found out that this happens because I was running my appium instances using the same port.
 So I had to implement some mechanism which will distinct every appium server by port. This is what I implemented:
 
<pre>
	<code>
 
		 APPIUM = {
			"LG": "appium -p {appium_port} --chromedriver-port {chrome_port}",
			"XIAOMI": "appium -p {appium_port} --chromedriver-port {chrome_port}",
			"SAMSUNG": "appium -p {appium_port} --chromedriver-port {chrome_port}",
			"IPHONE": "appium -p {appium_port} --chromedriver-port {chrome_port}"
		}
		
	</code>
</pre>

So basically I decided to cast the free system port to appium start up command and then to make sure also chromedriver will not clash on other tests I made this port unique as well. Great - nearly there!
But how to say which system port is currently not listining? This is what I invented:

<pre>
	<code>

		def get_free_port():
			port = randint(1000, 9999)
			while try_port(port) is False:
				port = randint(1000, 9999)
			return port


		def try_port(port):
			result = False
			check_port = 'lsof -i :{0}'.format(port)
			process = subprocess.Popen(check_port, shell=True, stdout=subprocess.PIPE)
			output = None
			for trial in range(5):
				try:
					time.sleep(1)
					output = str(process.stdout.readline())
					if 'COMMAND  PID' in output:
						break
				except:
					time.sleep(1)
			process.send_signal(signal.SIGINT)
			if 'COMMAND  PID' not in output:
				result = True
		return result
		
	</code>
</pre>

In this approach I get a random port and then by using lsof commaind I will see if anything is listining at this port. If nothing is listining then nothing will show up in console logs and port is free. If not then code will try again and again.
I also repeat this procedute for appium test internaly by setting systemPort appium dependency.

<pre>
	<code>

		TestCapabilities.CAPS.get(context.platform).update({"systemPort": system_port})
		
	</code>
</pre>
 
After this I have never seen this bloody error again.
And this is actually all you need. Or to be more precise that is what I thought is enough to enjoy my mobile tests being managed by Jenkins. I could not be more wrong :) Shortly I ran on more error but in next posts I will explain how I dealt with them.
As ussually all presented implementation can be found on my <a href="https://github.com/appiumator/appmation1/branches">GitHub!</a> profile.
 
