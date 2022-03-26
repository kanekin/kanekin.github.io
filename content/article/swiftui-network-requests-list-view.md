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

### Get API key to hit TMDB API
Before we jump into anything, let's get API key on TMDB. In this tutorial series, we will be using TMDB API. In order to hit their endpoint, you will need to have a API Key. You can follow the instruction on this page (https://www.themoviedb.org/documentation/api).


## Step 1: Display List of Movies with a static data

First let's aim to the point where we have a functioning UI with static data. Basically, we want to get to the point where Apple's official Swift UI tutorial leaves you. But we will already take one step further by utilising ViewModel. Once we have this foundation done, we can focus on diving into the details of network requests.
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

![step 3](/img/article/swiftui-network-requests/folder-structure.png)

### Defining Data
Let's define the data which we build the app with. In this tutorial, we will be using [get popular movies endpoint](https://developers.themoviedb.org/3/movies/get-popular-movies). 

- Create `TMDBResponse` file in `Common/Data`.
- Place the following code:

```swift
struct Movies: Decodable {
    let page: Int
    let results: [Movie]
}

extension Movies {
    struct Movie: Decodable, Identifiable {
        let id: Int
        let title: String
        let releaseDate: String
        let voteAverage: Double
        let posterPath: String
        
        enum CodingKeys: String, CodingKey {
            case id
            case title
            case releaseDate = "release_date"
            case voteAverage = "vote_average"
            case posterPath = "poster_path"
        }
    }
}
```

`Movies` is the struct corresponding to the response on `/movie/popular` endpoint. 
`Movie` is the struct that is contained in `results` attribute of `Movies` struct.
Both structs omits the attributes listed in API docs for the sake of the simplicity of this tutorial.

You might be wondering what is `Decodable`? `Decodable` is a protocol that enables us to convert our app-specific object into another format of data, such as JSON. It is a part of Swift standard library, so you don't have to import any libraries.

You can decode the object into data just like this:
```swift
let data = getPopular() // Psuedo code: Suppose getPopular() will returning a Data
let movies = try JSONDecoder().decode(Movies.self, from: data)
```


### Define the UI and ViewModel

Next we are going define the UI and ViewModel. 
- Create the two files in `Features/MovieList` 
    - `MovieListScreen` file
    - `MovieListViewModel` file
- Create `Features/MovieList/Subviews` folder
    - And create `MovieListCell` file

`Features` folder should be looking like this now:

![folder after ui files](/img/article/swiftui-network-requests/folder-structure-with-movie-list-files.png)

Once it's there, place these code into the files:

`MovieListScreen.swift`
```swift
import SwiftUI

struct MovieListScreen: View {
    @ObservedObject var viewModel: MovieListViewModel
    
    var body: some View {
        List(viewModel.movies) { movie in
            MovieListCell(movie: movie)
                .padding(.init(top: 8.0, leading: 0.0, bottom: 8.0, trailing: 0.0))
        }
        .listStyle(.plain)
        .onAppear {
            viewModel.load()
        }
    }
}
```

`MovieListViewModel.swift`
```swift
import Foundation
import Combine

class MovieListViewModel: ObservableObject {
    @Published var movies: [Movies.Movie] = []

    func load() {
        // Mock data for now. We will replace this with network requests.
        movies = [
            .init(
                id: 1,
                title: "Movie title",
                releaseDate: "12 Mar, 2022",
                voteAverage: 8.6,
                posterPath: "/74xTEgt7R36Fpooo50r9T25onhq.jpg"
            ),
            .init(
                id: 2,
                title: "Movie title 2",
                releaseDate: "12 Mar, 2022",
                voteAverage: 4.6,
                posterPath: "/74xTEgt7R36Fpooo50r9T25onhq.jpg"
            )
        ]
    }
}
```


`MovieListCell.swift`
```swift
struct MovieListCell: View {
    var movie: Movies.Movie
    
    var body: some View {
        HStack(spacing: 12.0) {
            VStack(alignment: .leading, spacing: 8.0) {
                Text(movie.title)
                    .font(.title2)
                    .fontWeight(.bold)
                HStack {
                    Image(systemName: "star.fill")
                        .foregroundColor(.yellow)
                    Text(String.init(format: "%.1f", movie.voteAverage))
                        .fontWeight(.semibold)
                }
                Text(movie.releaseDate)
            }
            
        }
        .frame(maxWidth: .infinity, minHeight: 100, alignment: .leading)
    }
}

struct MovieListCell_Previews: PreviewProvider {
    static var previews: some View {
        VStack {
            MovieListCell(
                movie: .init(
                    id: 1,
                    title: "Movie title",
                    releaseDate: "12 Mar, 2022",
                    originalLanguage: "Spanish",
                    voteAverage: 8.6,
                    posterPath: "/74xTEgt7R36Fpooo50r9T25onhq.jpg"
                )
            )
        }
        .previewLayout(.sizeThatFits)
    }
}
```

And finally replace the code in `ContentView.swift` with:
```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        MovieListScreen(viewModel: MovieListViewModel())
    }
}

struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        ContentView()
    }
}
```

You can already build and run the app on your simulator. You should see a list of two movies on the screen.

![movie list 1](/img/article/swiftui-network-requests/movie-list-1.png)

Let's briefly go through how these files are related:
- `MovieListScreen` shows a list of `MovieListCell`.
- `MovieListScreen` observes changes in `MovieListViewModel`

It might look magical on how `MovieListScreen` gets updated when `MovieListViewModel` is updated. This is enabled by a framework called `Combine`, Apple's reactive framework. 

In a short summary, notice the three keywords:
- `ObservableObject`
- `@Published` 
- `@ObservedObject`

![combine diagram](/img/article/swiftui-network-requests/combine-diagram.png)

When a class is marked as `ObservableObject` and has properties marked as `@Published`, the following relationship is established.
1. `ObservableObject` will emit an event whenever change occurs to a `@Published` properties.
2. Swift UI holding a reference to the changing instance marked as `@ObservedObject` will receive the event and reevaluate the `body`.

> **_NOTE_**: Under the nutshell, Swift compiler will synthesize an `objectWillChange` publisher that emits the changed value before any of the properties marked as `@Published`. `ObservableObject` will make sure that the view gets invalidated whenever it receives `objectWillChange` event.

### Implement Network layer in a ugly way
At this point, we have a working UI which lists the movies. We already have a working pipeline where UI will be automatically updated every time `movies` in `MovieListViewModel` gets updated. The only missing part is the part that actually fetch the data from the endpoint. The focus of the tutorial.

When you place the following code in `MovieListViewModel`, it actually starts to work:
```swift
class MovieListViewModel: ObservableObject {
    @Published var movies: [Movies.Movie] = []
    
    func load() {
        Task {
            do {
                movies = try await getPopularMovies()?.results ?? []
            } catch {
                print(error)
            }
        }
    }
   
    private func getPopularMovies() async throws -> Movies? {
        guard var urlComponents = URLComponents(string: "https://api.themoviedb.org/3/movie/popular") else {
            return nil
        }
        urlComponents.queryItems = [ URLQueryItem(name: "api_key", value: "<YOUR_API_KEY>") ]
        
        guard let url = urlComponents.url else { return nil }
        var request = URLRequest(url: url)
        let (data, response) = try await URLSession.shared.data(for: request)
        return try JSONDecoder().decode(Movies.self, from: data)
    }
}
```



#### Identifying the moving parts in Network requests

There are a few things that we need to take it into account:
- We want to be able to add required HTTP headers, parameters, and body flexibly depending on which endpoint we are sending the request.
- Network requests need to be asynchrnous call, so that it won't block the main thread which causes the UI to get stuck during animation.
- Each network calls have a set of routine tasks, such as check for network error, check for status code in the response and decode the data into the specific type.
- We want to avoid duplicated code because we have to be able to send requests to many different endpoints.

I remember that I was overwhelmed by the challenges when I had to write the network layer for the first time. My approach was to rely on an external library. And many full fledged iOS developers still rely on a third-party library. Although it is understandable when you are not fully familiar with the swift or iOS, the better approach is to use [`URLSession`](https://developer.apple.com/documentation/foundation/urlsession) which is a part of [`Foundation` framework](https://developer.apple.com/documentation/foundation).
