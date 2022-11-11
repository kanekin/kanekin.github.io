+++
draft = false
image = "img/portfolio/magicalfetch.jpg"
date = "2019-04-05T19:56:17+05:30"
title = "Tiqets: Magical Tickets Fetch"
showonlyimage = false
weight = 6
+++

Tickets are automatically available right after installation. It's magic!
<!--more-->

Tiqets is an app where users can purchase tickets for cultural venues such as museums and tourist attractions. One of the common problems among any consumer-facing app is that sometimes users need help figuring out how to use the app.

Tiqets app is a relatively simple app. You purchase a ticket in the app, and you have the ticket in a minute. That's it! Show the ticket in the app at the venue, and everything is done fast.

However, we have another path that many users go through. That is when a user purchases a ticket on a web browser and installs the app afterward. In this scenario, a user must authenticate himself to get the ticket on the app as he ordered the ticket outside the app. Perhaps the order took place on a different device from the mobile app where he wanted to get the ticket. 

Even though it's relatively straightforward, many things could go wrong. For example, the Email address can be incorrectly filled in when purchasing the ticket. That cannot happen? Believe me, it happens much more often than you would think. In such an unhappy path, the only option that the user had was to contact customer service. The user was expecting to complete the entire process within a few minutes. Now, suddenly they have to call somebody. That is a nightmare. Tiqets is only meaningful if the customer journey is fast, simple, and pleasant. 

That is why Tiqets mobile team worked on the magical tickets fetch functionality. We built a system where we send the confirmation message with a magic fetch URL in email or SMS. When you click the URL, we will ensure that you have the ticket you ordered as soon as you install and launch the app.  

But what if the user doesn't have the app when clicking the URL in the confirmation message? The URL doesn't result in getting the ticket in the app, right? That's the magical part! You will still get the ticket as soon as you install and launch the app. The URL can navigate the users to the AppStore if they still need to get the app. And we detect the trace of the URL on the launch, so the app can fetch the ticket. This wasn't easy to achieve, but we made it work. 

## My role in this project
- Experiment/Research the magical trick on iOS
- Implemented the logic on the launch to detect the purchase on install and fetch the ticket from the backend.