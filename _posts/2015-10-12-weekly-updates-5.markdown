---
layout: post
title:  "Weekly Update #5"
date:   2015-10-12 05:27:00
categories: Newsletter
author: Shubham Bansal
---

Happy Monday!! Hope you all had an amazing weekend.

Here is a quick update about some of the improvements we made to [DomReactor](https://domreactor.com) this past week. Also, here are some interesting articles to get your week started. I hope you enjoy them as much as we did.  


#### **What we are reading this week**

**[The Internet of Things. And Testing.](http://blog.domreactor.com/ideas/2015/10/06/iot-and-testing.html?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta">(4 min read)</span>  
Andrew Antal, our CEO, wrote a candid post about "Internet of things" and testing in general. As more devices are connected and new platforms are brought on, handling the consistency of that experience will be a pretty big problem. DomReactor might be a great first step to that.

**[Ludicrously Fast Page Loads - A Guide for Full-Stack Devs](http://www.nateberkopec.com/2015/10/07/frontend-performance-chrome-timeline.html?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta">(22 min read)</span>  
Your website is slow, but the backend is fast. How do you diagnose performance issues on the frontend of your site? We'll discuss everything involved in constructing a webpage and how to profile it at sub-millisecond resolution with Chrome Timeline, Google's flamegraph-for-the-browser.

**[Accidental Leadership](http://wildbit.com/blog/2015/10/09/accidental-leadership?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta">(3 min read)</span>  
"The biggest challenge for us was to remove the predefined baggage that came with separating responsibilities, and making sure we were clear that company strategy was always a joint effort." - Natalie Nagale

**[Lessons from the Woman Who Built Squarespace’s Customer Care Team from 1 to 184](http://firstround.com/review/lessons-from-the-woman-who-built-squarespaces-customer-care-team-from-1-to-370/?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta">(10 min read)</span>  
Superb customer care translates into great word of mouth. The trust of your customer is not only what’s at stake; it’s the potential conviction of each customer’s network, too.

**[Notes on Startup Engineering Management for Young Bloods](http://whilefalse.blogspot.com/2015/10/notes-on-startup-engineering-management.html?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta">(8 min read)</span>  
Put one foot in front of the next. Keep going. Be open-minded. Be curious. Read about what other people are doing. Make friends who are running tech at other companies. Be kind to yourself, even if you fail. You have the power to make the world better for all of those people on your team. Use it responsibly.

**[The Fear of Failure Can Be Paralyzing](http://www.paperplanes.de/2015/10/5/the-fear-of-failure.html?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta">(5 min read)</span>  
When you step into unknown territory, the paralysis is a natural thing to happen. When you don't know what's going to happen, the simplest thing for us is to stay away from taking the plunge. I know this feeling very well, and I'm finding myself faced with it again right now. It gets even harder when it stops just being you, and when other people’s income and supporting their families is on the line.

**[An employee handbook built for inclusion ](https://github.com/clef/handbook?utm_source=DomReactor+Weekly+Updates)** <span class="post-meta"></span>  
Clef just open sourced their entire company handbook. The document includes Benefits and Perks, Employment Policies, Onboarding Documents, Hiring Documents and pretty much everything you need to run a company. Kudos to them for being so transparent.  

#### **What we shipped this week**  

**<u>Fix reactions that have no associated report (Bug)</u>**  
We found an issue around reactions that were either still running or didn't have an associated report. If such a test existed, the dashboard page was not loading and threw an error. That has been fixed now and dashboard will load irrespective of the status of the the reactions on the page.

**<u>Generate a shareable token for every reaction (Bug)</u>**  
Shareable token was not getting created when the reaction was kicked off. This resulted in an invalid link getting generated for sharing reactions. However, we have fixed this issue so that the shareable token gets created properly and a valid link to share a reaction is generated.

Happy Testing,  
Your friends at DomReactor

