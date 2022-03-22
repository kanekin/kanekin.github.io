+++
date = "2022-03-22T10:45:45+01:00"
draft = true
image = ""
showonlyimage = false
title = "Missing Tutorial for Swift UI (Network and MVVM): List View with Network Request "
+++

__This is a part of a tutorial series: Missing Tutorial for Swift UI (Network and MVVM).__

#### Table of Content
- List View with Simple GET request
- Details View with error handling
- Login View with POST request
- Which API should we be using URLSession?

## List View with Simple GET request
The first part of the tutorial is to make a list view where you can see a list of movies by fetching movie data from TMDB API. 

### Objectives and Disclaimer
In this tutorial, we will focus primarily on network requests. We will fetch data from TMDB API and update the UI based on the response. 

Please note that I am not going to explain the details of how to construct the views, as Apple's official tutorial covers the topic. They have done a much better job than I could ever do. 

If you haven't followed Apple's tutorial, I highly recommend following that first. It will take approx one hour to complete and covers the fundamentals of SwiftUI, so please be encouraged to jump there first. This tutorial covers the step after Apple's tutorial.

### Create an App and Add Folder structure
First step is of course to create an app. It's a step covered in many tutorials, so I will be brief.

Step 1: Select Template:
![step 1](/img/article/swiftui-network-requests/select-template.png)

Step 2: Provide product name:
![step 2](/img/article/swiftui-network-requests/create-project.png)

Step 3: Create Folder strutures
Let's lay down the folder structure so that we don't have to be bothered with it later in this tutorial.

First, create 2 Groups on the top level of the project:
- Features: 
    - This is where each screen and related files will be located
- Common: 
    - This is where common component will be placed such as network, data and extension

Second, in the `Features` group, create `MovieList` group. This is where all the UI related files will be placed.

Thirdly, in the `Common` group, create `Data`, `Network` group.

Your project structure should look like this:

![step 3](/img/article/swiftui-network-requests/folder-structure.png "This is the title attribute {width='100' height='75' style='border: 1px solid red;`}")

### Get API key to hit TMDB API
In this tutorial series, we will be using TMDB API. In order to hit their endpoint, you will need to have a API Key. You can follow the instruction on this page (https://www.themoviedb.org/documentation/api).

### Defining Data
Let's define the data which we build the app with. In this tutorial, we will be using [get popular movies endpoint](https://developers.themoviedb.org/3/movies/get-popular-movies). 

- Create `TMDBResponse` file in `Common/Data`.
- Place the following code:

```
struct TMDB {
    
    struct Response {
        struct Movies: Decodable {
            let page: Int
            let results: [Movie]
        }

        struct Movie: Decodable, Identifiable {
            let id: Int
            let title: String
            let releaseDate: String
            let originalLanguage: String
            let voteAverage: Double
            let posterPath: String
            
            enum CodingKeys: String, CodingKey {
                case id
                case title
                case releaseDate = "release_date"
                case originalLanguage = "original_language"
                case voteAverage = "vote_average"
                case posterPath = "poster_path"
            }
        }
    }
}
```