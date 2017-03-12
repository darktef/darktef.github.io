---
layout: post
title: Location-based time tracking with Geofency, Zapier and Toggl
category: productivity
tags: time-tracking automation geofence
---

I am a huge procrastinator, always stayed up the whole night to finish up the project or prepare the test when the deadline is tomorrow. After the project or test past, I spent another full day to sleep and recover. As I am getting older, and graduated from the college, I realized that it should not be the way how life works.  

<!--more-->

I started wondering, where I spent all the time, if I was not doing anything productive before the deadline. I could always crush the task the night before, which means the task should just take 24 hours at most to finish. What if I have a better vision on how long a specific task gonna take me to finish, will it become easier for me to finish the task first before anything else.  

It is the starting point of my journey on productivity management, plus a little automation. Automation will reduce the friction on doing productivity management and help me to stick to whatever rule I come up with down the road.  

This post will focus on developing location-based time tracking with apps and services.  

### Toggl

Toggl is a popular choice for time tracking. I have never used it before I started my first job as a web developer. I was geeky, but not geeky enough to start using the IT-guy-recommended web services.   

I really like its easy of use, the weekly-report feature and the updated dashboard design, despite its inconsistency across different platforms and mysterious authorizations within our team. I continued using it even the whole company switch to a custom-made time-record dashboard.   

Inspired by the [burn down chart](https://en.wikipedia.org/wiki/Burn_down_chart) and [Cortex](https://www.relay.fm/cortex), I started using it for my personal time tracking.  

![burn-down-chart](https://upload.wikimedia.org/wikipedia/commons/0/05/SampleBurndownChart.png)
<p class='credit-author'>Credit by Wiki</p>  

Toggl has a really nice [API](https://github.com/toggl/toggl_api_docs) doc for you to start to manipulate anything without even open the real Toggl App. This opens up a lots more possibility for integrating toggl in your workflow.  

### Geofency

I already forgot when I started using [Geofency iOS](http://www.geofency.com/). Tons of data is lost with my previous phone. It is probably the first try to monitor how I spend my time. I am usually lazy and relaxed at home, but more productive at library or coffee shop. Location is a pretty good indicator of my productivity in general.  

The app tracks every location I have been and how long I stayed. Though there is a little accuracy issue, user could set specific locations to be more monitored, and enlarge the monitoring radius to overcome the accuracy problem. The app also ships with the statistical part. It calculates the total time spent at certain location daily, weekly and monthly, and creates a distribution graph, showing how time is spent at different locations every day.   

<amp-img width="260" height="463" src="/assets/images/posts/geofency.png"></amp-img>

The best part is the app allow user to create webhook whenever he/she enter or exit certain location. Click into the location you would like to manipulate, and tap into the webhook. Now you unlocks the possibility to do anything you want, with the help of Zapier.   

<amp-img width="260" height="463" src="/assets/images/posts/geofency_webhook.png"></amp-img>

In my specific use case, I integrate with Zapier and Toggl to enable the location-based time tracking.  

### Zapier

[IFTTT(IF This Than That)](https://ifttt.com/) is the first well-known name doing some sort of automation for normal user. I started using it back in 2015, but did not experiment a lots with it. Some of the applets(the workflow) I used back then is not sticky and powerful enough for me to become an active user. I was still impressed with the idea, and felt like seeing the first light of automation for a normal user.   

Only until recently, Cortex and some random posts mentioned Zapier, and claimed that Zapier could do much more than IFTTT, especially the ability to connect two apps/services together. For example, you could send a message in Slack, and it will create a todo in Todoist automatically. How awesome is that! A normal day is made of some productive activities and lots of inevitable chore. One simple solution to boost productivity is just to reduce as much chore as possible, either by automation or by hiring somebody to do it for you.  

Being as ~~poor~~ geeky as me, I chose the first route.  

It is almost impossible for Geofency to communicate directly with Toggl due to the fact that Geofency could only send fixed data in webhook. Thus, I have to use Zapier as the middleman to connect two apps.  

The basic flow is as follow:  

<amp-img width="280" height="583" src="/assets/images/posts/zapier_flow.png"></amp-img>  

Toggle could not stop the current entry without providing the id of current time entry. The workaround is to start another time entry, then the current time entry will stop automatically.  

### Conclusion

There you go, now you have your own location-based time tracking. Zapier's free plan could only do 2 Zaps and 100 tasks every month, I might want to figure out a way to create this kind of interface by myself. We will see what happens down the road. 

Have fun coding/tweaking!
