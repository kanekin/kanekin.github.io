+++
image = "img/portfolio/filterablemap.gif"
showonlyimage = false
date = "2016-11-05T19:44:32+05:30"
title = "Tiqets: Filterable Map"
draft = false
weight = 4
+++

Filterable items on map component.
A common iOS UI pattern can be found in many apps. 
<!--more-->

<p><img src="/img/portfolio/filterablemap.gif" width="300"/></p>

This type of pattern can be found in many apps, such as TooGoodToGo, OneFit/ClassPass, Felyx, GO, CHECK, SnappCar, Sixt Sharing, MyWheels and etc.
## Dynamically deployable filters

What is unique about the map filters we implemented at Tiqets is that new filters can be introduced without releasing a new version of the mobile app itself. 

We abstracted the filters and the list items so that we could introduce a new set of filters by the backend change alone. We were able to quickly A/B test the filters that are more useful for users. 
Combined with the analytics data, we could see which filters were more useful for the users and optimize the map UI.

## My role in this project
- Designed the backend response
- Documented and coordinated the development with a backend developer and an Android developer 
- Implemented the Map and filter UI on the iOS app