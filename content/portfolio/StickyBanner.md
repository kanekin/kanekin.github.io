+++
image = "img/portfolio/stickybanner.gif"
showonlyimage = false
draft = false
date = "2022-17-19T17:30:00+01:00"
title = "Hobby: Gesture Dismissible Sticky Banner with Swift UI"
weight = 5
+++

Interactive Banner in Swift UI. You can snap up to dismiss.

<!--more-->

![snappy banner gif](/img/portfolio/stickybanner.gif)

It looks just like iOS native notification banner. To my surprise (and for many others I believe), there is no standard component that can be launched within the app and customizable. There are many tutorials on how to make a banner, snackbar on Swift UI. But I couldn't find an example which allows the interactions like a native notification banner, such as snap up to dismiss or bounding back to the original position when you drag it down.

I wanted to have a truly iOS native notification banner like experience. I fiddled around and this is what I came up with. 