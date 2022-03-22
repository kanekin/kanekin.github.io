+++
date = "2022-03-21T16:36:01+01:00"
draft = false
image = ""
showonlyimage = false
title = "Missing Tutorial for Swift UI (Network and MVVM): Introduction"
+++




#### TL;DR:

We will make this app. 
![kinema record image](/img/article/swiftui-network-requests/kinema-record.jpeg)


### What is this article?

A iOS native app development tutorial with Swift UI, MVVM, Network. The app makes network calls to [TMDB](https://www.themoviedb.org/) API to demonstrate the flow of fetching data and update the UI on a Swift UI app.

### Target audience

- People with prior programming experience but not on the iOS platform.
    - Finished apple's official Swift UI tutorial and want to take it one step further.
- iOS Developers who have been primarily working on apps supporting iOS 12 and below, who didn't get to explore Swift UI.
- iOS Developers who haven't gotten their hands on new async/await features available from iOS 15 onwards.

### What you will learn

- Swift UI
- MVVM
- Network 
  - Error handling
  - Logging
  - Mocking data
  - Combine based vs Async based vs Closure
- Async Image loading

## Who would benefit by reading this article?

### 1. You are new to iOS:

Apple's official tutorial is a beautiful interactive tutorial. But it doesn't include handling network calls. If you are not an experienced iOS Developer, the network is possibly the first real headache. For instance, you might have to face the following problems:
- Concurrency
- Error handling
- Dynamically loading content
- Authentication + Persisting token

You might say it's not hard. I have seen many mistakes in the production code base of consumer-facing apps. The network is like veins running through the app. Most of interesting feature will most likely depends on your network layer. It would be painful if you have to refactor network layer later.

### 2. You haven't worked with SwiftUI:

The lifecycle of UIs is significantly different from UIKit. Reactive way of handling data (Binding UI with variables that represents the state of the app using Combine) seems to be the way to go in SwiftUI. If you didn't work with RxSwift, this article might give you a good glance at how data flows in SwiftUI apps between UI and the network layer.

### 3. You haven't worked with async/await features (iOS 15.0+):

Since the introduction of Combine (iOS 13: 2019), Combine-based API from `URLSession`. (`.dataPublisher { ... }`) became a popular option to build the network layer with. However Apple introduced another new API on `URLSession` in 2021 utilising `async/await`. In this article, I will be mainly using the new async/await based API from URLSession.
(I will also discuss why I prefer using async/await for network calls as well)



## Why am I writing this article?

There are many iOS articles out there. Why do we need more?

Until recently I was an iOS developer who didn't get to work with the latest features such as SwiftUI, Combine and async/await. The project that I have been working on needed to support iOS 12 and below. When I started to pick up the latest iOS tooling, I was overwhelmed by the many choices available. Network on iOS in 2022 especially has three valid choices using URLSessions, namely `.dataTask`, `.dataTaskPublisher`, `.data`. I found it difficult to decide which one to use even though I had years of iOS development experience.

Second, there are a lot of articles already but most of them are focused on single-page examples. It doesn't demonstrate the features in a multi-page environment. I think for beginners, it is still difficult to derive how things can be wired together when expanding the app from a single page app into a multi-page app where you have to manage the lifecycle of the views, passing dependency, handle errors, manage asynchronous image loading, persist authentication tokens.

Thirdly, Network is one of the essential parts of the app and yet usually a layer that is written once at the early stage of the app development and used for a long time. Even if you have years of professional experience working on large projects, you could have missed an opportunity to write your own network layer. 

Therefore, I thought I can provide some values by writing a series of articles that provides examples that are relevant in real-world development and I explain the motivations of the choices I make. That is being said, it is based on my opinion. You can disagree with me and I am open to feedback.

## What will not be discussed

I would like to avoid discussing the reasoning of app architecture in this article. I am aware that there are many different approaches and opinions around it. I have seen opinions like MVVM is not necessary and redundant, VIPER is better, MVP is great, let's go back to MVC, etc. After years of experience, I concluded that any app architecture works is fine.  I am a firm believer of delivering meaningful features is more important than using the most sophisticated app architecture. Nothing is perfect, is it? Therefore let's get pragmatic and get things done!

## What are we making?

An App that can fetch data from TMDB API. Features of the app includes:

- Login
- Display a list of movies 
- Display a details of a movie

It will look like this:

![kinema record gif](/img/article/kinema-record.gif)

## Table of Content

- Build a list view and details view with async/await based network calls
- Error handling
- Mocking data
- Comparison between closure, Combine, async/await APIs
- Login page 

  
  