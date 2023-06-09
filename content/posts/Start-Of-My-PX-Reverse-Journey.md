---
title: "Start of My PX Reverse Journey"
featured_image: "/images/analysis.png"
date: 2023-06-08T14:09:01-04:00
draft: false
---
So, I decided to start my RE journey by reverse engineering Perimeter X. Currently, I am working on the site grubhub.com and have also checked out a site called airtable.com. Mind you, I have heard about many anti-bots but never brought myself to actually attempt reversing them. From PX to Cloudflare, Shape, and other services like Akamai and Kasada, they have always interested me. It's from both an egotistical perspective and pure curiosity about how they work and whether I can reverse engineer them to bypass their protections. I have always loved the idea of bypassing security. I'm not sure why. The greatness it is to reverse engineer the anti-bots of multimillion-dollar companies is, at the very least, a very nice feeling.

Anyways, enough about me and on to my findings for the day. I set out on this journey to learn completely on my own, without referencing others' work, especially when it comes to PX reverse engineering. All findings documented on my journey have been discovered by me through hours of analysis. This is my journey documented. I'm not here to teach anyone reverse engineering, nor am I here to guide anyone, as I am not experienced enough to be a teacher of any sort, and I've just started, lmao, If you have some itch about something I said being wrong or incorrect, please do educate me as im trying to learn, otherwise again this is my journey so I will not get everything right first try. But I will make an effort to make what I'm saying and found understandable.

#### Analyzing PX Scripts And Request Payloads

- ##### PX Scripts Location

The Perimeter X scripts (and really any scripts) are located in the Sources tab of the Chrome DevTools in your browser.

![PX Script Location](/images/pxscriptloc.png)


- ##### Taking a Look At Request Payloads And Responses

So, of course, being my first time doing this, I didn't really know what to do. But, of course, I figured that I need to look at the requests because, well, this is a website, and requests are how data is sent and received. So, I open up the Network tab in Chrome DevTools and begin looking at the requests.

<p align="center">
  <img src="/images/grubhubreq.png" />
</p


Let's actually dissect what is important and what isn't. The first request is simply the **GET** request that's made when you load up the page on Grubhub. We can ignore everything else until we get to a request named "collector". This is the first request made by Perimeter X, and it is the request that is sent multiple times, interacting and communicating with PX. The payload changes each time, but some things stay static from the first request all the way to the end.

<p align="center">
  <img src="/images/collector.png" />
</p

This is a POST request to the endpoint `https://sensor.grubhub.com/O97ybH4J/xhr/api/v2/collector`. `https://sensor.grubhub.com` is the endpoint/domain that Grubhub uses to communicate with PX.

<p align="center">
  <img src="/images/payload.png" />
</p

What I discovered from looking at the PX Scripts is that the appId is unique to each website. It is essentially an identifier to verify that the request is coming from a PX certified user. 😉

This is the PX App ID for Grubhub:

<p align="center">
  <img src="/images/appId.png" />
</p

And this is the PX App ID for airtable.com:

<p align="center">
  <img src="/images/airtableappid.png" />
</p

As you can see, they are essentially the same thing. However, note that both of these are at different versions (as shown by the license copyright date), so the script will not be the same. But as for this part of the script, not much has changed.

- #### Final Analysis for the Day

Overall, this was the conclusion I came to after my first few hours (2 hours) of looking at the interaction between Grubhub and PX.

<p align="center">
  <img src="/images/analysis.png" />
</p

Again, I apologize if this wasn't the most comprehensive analysis, but this is for my learning experience and to document my journey. Thank you for reading!


