# SQL Injection Attack Module
A short module on SQL Injection Attacks with exercises on the OWASP Juice Shop and remediation and observation with DataDog agent.

## Introduction
SQL Injection is one of the top attacks performed on web applications today. Though it has been around since the late 1990's and can easily be avoided, it still prevails. 

An SQL Injection attack happens when the attacker enters malicious code or a query into an unvalidated form, such as username and password. Becasuse the form data is not validated, the SQL database can accept what is entered into the form as a command to be executed. 

The _OWASP Top Ten Website_ defines and describes SQL Injection as follows:


> _SQL Injection is when an attacker enters a malicious or malformed query to either retrieve or tamper data from a database. And in some cases, log into accounts._

 (Note: OWASP stands for the Open Web Application Security Project) 

 This type of attack can reveal usernames and passwords, as well as allowing the attacker to login as admin or any other user.

## Module Overview
In this module you will learn what a SQL injection is, how to perform one and what the results can be. You'll also see how DataDog's agent can prevent and alert you of such an attack.

This module is intended for an IT professional, with a curiosity about AppSec. Your role might be Developer, SRE, QA, or Engineer. 

First, we will open Docker and install a common vulnerability website for us to hack called the OWASP Juice Shop. Next, we will perform an SQL injection on the OWASP Juice Shop using a well known tool called Burp Suite. Next, we will look at the results of our injection, the consequences. Finally, we'll build a Docker container with the OWASP Juice shop plus the DataDog agent installed to see how this tool can prevent and give visibility into the attack.

For brevity this module does not include  installing or using Docker, the use of a Command Line Interface or give an overview of Burp Suite. Links to resources on Docker and Burp Suite are provided for your own learning outside the module. Docker is required to complete this module.

## Assumptions
The ideal learner is  familiar with the command line interface (CLI).  Docker basics are required to run the scenario.  If you do not have experience with Docker, here are a few links on installing Docker and a quick how-to on how to get Docker up and running.

* [Get Docker](https://docs.Docker.com/get-Docker/)
* [Getting started with Docker](https://docs.Docker.com/get-started/)

## Required Tools
1. Access to a Shell or Command Line Interface
2. Firefox or web browser of choice
3. Docker
4. Burp Suite community edition
5. OWASP JuiceShop Website (which we will retrieve in and install via Docker)
6. DataDog account (sign up for a free trial  [here](https://www.datadoghq.com))
7. Something to take notes with
8. A curious mind!
***
## Step 1:  Install and run the OWASP Juice Shop Image in Docker
Open your shell or command line interface. From here we will use Docker to get the image for the OWASP  Juice Shop to load into our container.



**Note:** There is a companion video located in the GitHub folder called Docker.mp4. It may be handy to have this open while performing this step.

<video width="320" height="240" controls>
  <source src=(/assets/) type="video/mp4">
</video>

https://user-images.githubusercontent.com/15679125/175845793-35ef4c95-3ef5-4abf-93a5-fc542ea61aa1.mp4



From your command line, enter the following commands:
>`docker pull bkimminich/juice-shop`
(this pulls the Docker image into our local environment)

>`docker run --rm -p 3000:3000 bkimminich/juice-shop` (BTW, that is an _r_ and _m_ after the two dashes. This actually runs the image)

Now that the OWASP Juice Shop is running, open up Firefox or your web browser of choice and enter the following URL to access the OWASP Juice Shop:

>http://localhost:3000 (on macOS and Windows browse to http://192.168.99.100:3000 if you are using Docker-machine instead of the native Docker installation)

The OWASP Juice Shop is one of many applications made to practice hacking in a safe environment without offending anyone or breaking any laws. Feel free to poke around and look at the various aspects of this site.

## Step 2: Install and run Burp Suite Community Edition

Burp Suite is a leading tool in the cyber security toolkit. It has many features for web security testing. We will be focusing on intercepting data entered into a web form and then passing back our own unique response to the server.


Start by downloading Burp Suite from this URL:
https://portswigger.net/burp/releases/professional-community-2022-5-1?requestededition=community&requestedplatform=
[![Burp Suite Download](/assets/images/burp-suite-download.png)](https://portswigger.net/burp/releases/professional-community-2022-5-1?requestededition=community&requestedplatform=)
> Note: Mac OS file should look like: _burpsuite_community_macos_x64_v2022_5_1.dmg_

> Windows file should look like: _burpsuite_community_windows-x64_v2022_5_1.exe_

> Linux file should look like: _burpsuite_community_linux_v2022_5_1.sh_

Once downloaded run the installer for your operating system.

This module will only touch on basic usage of Burp Suite. If you'd like to learn more or take an introductory course on Burp Suite, you can find that [here](https://portswigger.net/burp/documentation/desktop/getting-started/intercepting-http-traffic). 

We’ll be guiding you step by step on what to do in Burp Suite for this exercise, so don't worry.

Once Burp Suite is downloaded and installed, go ahead and run the application. At first launch you will likely be prompted about the project. Leave *Temporary project* selected and hit **Next**.
On the next screen leave *Use Burp defaults* and hit **Start Burp**.

Once running it should look something like this:

![Burp Suite](/assets/images/burp-suite.png)
>Note: For your convenience, a video titled Burp Suite.mp4, walking through the attack itself is provided in the GitHub folder. Feel free to have that open and running as you perform steps 3 and 4.
![Burp Suite Video](/assets/video/Burp%20Suite.mp4)

## Step 3: Perform SQL Injection attack on OWASP Juice Shop and Login as Admin

Go ahead and close whatever browser you have the OWASP Juice Shop open.

With Burp Suite open you’ll likely be on the Dashboard.

Navigate to the Proxy tab and click on the Open Browser button. This will open Burp Suite’s own Chromium browser for us to access the OWASP Juice Shop. Enter the URL in for the OWASP Juice Shop in the browser:

>http://localhost:3000 (on macOS and Windows browse to http://192.168.99.100:3000 if you are using Docker-machine instead of the native Docker installation)

It’s handy to have the browser window with the OWASP Juice Shop on one side of your screen and Burp Suite on the other side.

In the OWASP Juice Shop click on the Account menu and select **Login** from the drop down.

At the login in screen enter the lowercase letter _a_ for both the username and password, but do not press the login button yet.

Back in Burp Suite turn intercept on by clicking the button that says ***Intercept is off***

Now in the OWASP Juice Shop click the **Login** button and notice what happens in the Burp Suite window.

>Question: What is the last bit of code or text starting at line 20 in Burp Suite?

>Answer:

In the Burp Suite window find where the email and the two _a_'s you entered are.

Change the “a” next to email with: `‘or 1=1--` and press the **Forward** button above to forward onto the server. Since we only needed to intercept that one entry, go ahead and turn intercept off by clicking on the ***Intercept is on*** button.

Notice the OWASP Juice Shop’s response

>Question: What is the email address of the Admin account on the OWASP Juice Shop?
Answer:

**Congratulations!** You are now logged in as the Admin account on the OWASP Juice Shop!

You may be wondering why this worked? In short, it worked because:

1. The character `'` closes the brackets in the SQL query
2. `'OR'` in a SQL statement will return true if either side of it is true. Because  1=1 is always true, the entire statement is true. This will tell the server that the email is valid, and log us into user id 0, which just so happens to be the administrator account.
3. The `-- `character is used in SQL to comment out data, any restrictions on the login will no longer work because they are perceived as a comment. 

## Step 4: Perform SQL Injection attack on OWASP Juice Shop and Login as user Bender





