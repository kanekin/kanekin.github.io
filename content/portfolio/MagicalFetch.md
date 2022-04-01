+++
draft = false
image = "img/portfolio/magicalfetch.jpg"
date = "2016-11-05T19:56:17+05:30"
title = "Tiqets: Magical Tickets Fetch"
showonlyimage = false
weight = 6
+++

Tickets are automatically available right after installation. It's magic!
<!--more-->

Tiqets is an app where a user can purchase a ticket for cultural venues such as museums and tourist attractions. One of the common problems among any consumer-facing app is that sometimes users can not figure out how to use the app.

I think the Tiqets app is a fairly simple app. You purchase a ticket in the app and you have the ticket in a minute. That's it! Show the ticket in the app at the venue and everything is done fast.

However, we have another path that many users go through. That is when a user purchases a ticket on a web browser and installs the app afterwards. In this scenario, a user has to authenticate himself in order to get the ticket on the app as he ordered the ticket outside of the app. Perhaps the order took place on a different device from the mobile app where he wants to get the ticket. 

Even though it's relatively straightforward steps, still many things could go wrong. For example, the Email address can be incorrectly filled when purchasing the ticket. And believe me, it happens much more often than you would think. In such an unhappy path, the only option the user had was to contact customer service. The user was expecting to finish the entire process within a few minutes but suddenly they have to call somebody now. That is a nightmare. Tiqets is meaningless if the customer journey is not fast, simple, and pleasant. 

That is why Tiqets mobile team worked on the magical tickets fetch functionality. We built a system where we send the confirmation message with a magical fetch URL in email or SMS. When you click the URL, we will make sure that you will have the ticket you ordered as soon as you install and launch the app.  

But what if the user doesn't have the app when clicking the URL in the confirmation message? Surely, the URL doesn't result in getting the ticket in the app, right? That's the magical part!  You will still get the ticket as soon as you install and launch the app. The URL can navigate the users to the AppStore if they don't have the app yet. And we detect the trace of url on the launch, so that the app can fetch the ticket. This was difficult to achieve but we made it work. 

I can not reveal how it exactly works in the nutshell, but it was an amazing improvement for the user's journey. We reduced the contact rate to our customer service drastically. 

## My role in this project
- Experiment/Research the magical trick on iOS
- Implemented the logic on the launch to detect the purchase on install and fetch the ticket from the backend.