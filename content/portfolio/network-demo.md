+++
date = "2022-03-29T14:59:42+02:00"
draft = false
image = "img/portfolio/kinema-record.jpeg"
showonlyimage = false
title = "Network Demo with Swift UI and MVVM"
+++

An app to demonstrate how network calls can be implemented in a SwiftUI/MVVM app.
<!--more-->

![Thumbnail](/img/portfolio/kinema-record.jpeg)

## Motivations

Apple's introductory tutorial is a great starting point to learn about SwiftUI (https://developer.apple.com/tutorials/swiftui). However, it doesn't cover many things that an app in a production app would need:

- Network calls
  - Being able to communicate with many endpoints without code duplication
  - Concurrency
    - Network calls that depend on the other calls' results
  - Error handling
- Logging
- Navigation
- Test

When I tried to extend my app after finishing the Apple's Swift UI tutorial, I still had to make many decisions about how to organize the codebase. It could be useful for myself and other people who are new to SwiftUI if I implement the app with network calls with a more realistic app architecture with basic tests and logging.

## Disclaimer

The main purpose of the app is to demostrate how an app can be structured. It is not an app with a full functionality.

## Features

- Login (You can login with a TMDB account. You can create an accout at: https://www.themoviedb.org/signup)
- Logout
- Display a list of popular films
- Display a details of a movie
  - browse casts
  - browse crew

## Demo video:
Click to play:
<p>
<a href="https://youtu.be/Ny4RI_iajjA">
<img src="/img/portfolio/video-thumbnail.png"  width="200" /> 
</a>
</p>

## Github repo

Source code available at: https://github.com/kanekin/NetworkDemo