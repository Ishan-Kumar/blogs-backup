## Confused about the best automation tool to learn/implement?

So you just started in testing, and are now 

- confused about where should I start to learn from?
- confused on whether I should choose cypress because it is gaining a lot of traction in the market?

Also, some of the common queries I encounter while mentoring: 

- What will be the biggest automation testing tools in the coming years?
- What is the best tool one should learn to be an automation engineer?
- Is Selenium still relevant in UI Automation?

Beginners are often confused with these similar questions and conclude many things wrong. I was at the same place when I started. And now I realize how wrong I was then and how we do not see the ever-changing dynamics of technology in the industry. Hence, I thought to write about my experience and what I have observed in all these years of working in the industry.

Let me first start with:

So, **which is the best tool in the market again?**

Well to start with, I believe that things aren't going to be very different from what we are already seeing in the last 3-4 years from a tools perspective.

So, in that regard,

Number 1? Frontend Top test tool? Free? Matured as hell ??

Surprise Surprise

.

.

.

it's [Selenium](https://www.selenium.dev/).

And AFAIK, Selenium isn't going anywhere for the next few years at least.

Like Test community already seeing it since the last couple of years, Selenium is evolving and clubbing around with many tools and techniques. And my take is that of course, you might see various improvised libraries here and there but under the hood, it is going to exist for long. 

Framework & Tools support in the market?

Yeah sure, there are many and the community is growing like crazy. To name a few tool we have in the arsenal:

- Cucumber
- Serenity
- Robotium
- Katalon Studio
- TestNg
- Junit ..etc
And we will see more in the coming years for sure.

I want to stress here that we must understand that these tools are nothing but features developed either the top of the existing selenium library or in support of it. 

And apart from the above, we have different tools for different test categories and these right now are in boom already.

Some of these tools are:


- Rest Assured/ Jackson etc for API automation
- Blazemeter, Jmeter (performance tools)
- Sikuli (Image comparison based UI Automation tool)

Some Bonus Entry :) :

1. [Site speed](https://www.sitespeed.io/) (awesome website performance tool):

2. [Gauge](https://gauge.org/index.html)

3. [Taiko](https://taiko.gauge.org/)

4. [Botium](https://www.botium.ai/) (to test bots)

5. [Locust](https://locust.io/) Python based code alternative of jmeter

6. [Goose](https://www.tag1consulting.com/blog/jmeter-vs-locust-vs-goose) Rust based performance tool

My Point?

Take a good look at the above tools and you will realize how rapidly the dynamics of testing are changing in the industry.

So, in essence, you would not want to be a tool-specific engineer i.e selenium engineer or a cucumber engineer per se. Instead, you would want to be an Automation Engineer having sound knowledge of the basic test development principles and components, which you can use to automate things based on the requirements using the tool of your choice, and that my friends should be the way to go.

In today's era, from Low-level testing at the very early stage of development to creating the end to end UI test solutions, we now are looking to automate things at every level & degree in our applications. So in that sense, the entire industry is moving more towards incorporating test frameworks in CI/CD techniques using various cloud technologies like docker, Kubernetes, AWS, digital ocean, GitLab, etc. So whatever you develop it should be CLI executable first.

Application implementation and deployments are moving more towards [microservices](https://microservices.io/) based architecture techniques.


The key here is to build fast, test fast, fix fast, and ship fast.

So yeah. Not exactly tool-wise, but the way we test and deploy things, I think we are getting more mature and testing dynamics are really changing a lot under the HUD. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1624789195525/TF43dn8sJ.png)



So before I finish, I want to emphasize that intent of this post is not to give you insights on the exact latest trends but to elaborate on the point that technology is ever-changing and if you are pursuing to be an automation engineer or if is in search for a tool to automate your product "which is the best tool?" is the wrong question. A lot depends on the product under test's business logic and what do we want to achieve with it?

*We should instead work on the basic principles of Automation. New tools will emerge every time but the things under the hood are going to remain more or less the same. There is best for everything in the market and focusing on requirements instead will give you the best ROI*.

Keep learning, it's a never-ending cycle :).