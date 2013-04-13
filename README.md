## Information

### themoviedb

A Ruby wrapper for the [The Movie Database API](http://docs.themoviedb.apiary.io/).

Provides a simple, easy to use interface for the Movie Database API.

Get your API key [here](https://www.themoviedb.org/account).

## Getting started

```ruby
gem install themoviedb
```

## Configuration

```ruby
Tmdb::Api.key("KEY_HERE")
```

## Resources

Current available resources:
* Company
* Movie
* Collection
* People

## Example

```ruby
Tmdb::Movie.find("batman")
Tmdb::Collection.find("spiderman")
Tmdb::People.find("samuel jackson")
Tmdb::Company.find("lucas")
```

## Search

### Usage

resources => person, movie, collection, company

```ruby
@search = Tmdb::Search.new
@search.resource('person') # determines type of resource
@search.query('samuel jackson') # the query to search against
@search.fetch # makes request
```


## Configuration

Get the system wide configuration information. Some elements of the API require some knowledge of this configuration data. The purpose of this is to try and keep the actual API responses as light as possible.
This method currently holds the data relevant to building image URLs as well as the change key map.
To build an image URL, you will need 3 pieces of data. The base_url, size and file_path. Simply combine them all and you will have a fully qualified URL. 
Here’s an example URL: http://cf2.imgobject.com/t/p/w500/8uO0gUM8aNqYLs1OsTBQiXu0fEv.jpg

```ruby
configuration = Tmdb::Configuration.new
configuration.base_url
configuration.secure_base_url
configuration.poster_sizes
configuration.backdrop_sizes
configuration.profile_sizes
configuration.logo_sizes
```

## Detail

Every movie example documented below uses the movie Fight Club (id 550) while every person uses Brad Pitt (id 287). These are only used as examples to show what a real world request looks like.

### Movie

```ruby
movie = Tmdb::Movie.detail(550)
movie.adult => false
movie.backdrop_path => "/8uO0gUM8aNqYLs1OsTBQiXu0fEv.jpg"
movie.belongs_to_collection => nil
movie.budget => 63000000
movie.genres => [{"id"=>28, "name"=>"Action"}, {"id"=>18, "name"=>"Drama"}, {"id"=>53, "name"=>"Thriller"}]
movie.homepage => ""
movie.id => 550
movie.imdb_id => "tt0137523"
movie.original_title => "Fight Club"
movie.overview => "A ticking-time-bomb insomniac and a slippery soap salesman channel primal male aggression into a shocking new form of therapy. Their concept catches on, with underground \"fight clubs\" forming in every town, until an eccentric gets in the way and ignites an out-of-control spiral toward oblivion."
movie.popularity => 7.4
movie.poster_path => "/2lECpi35Hnbpa4y46JX0aY3AWTy.jpg"
movie.production_companies => [{"name"=>"20th Century Fox", "id"=>25}, {"name"=>"Fox 2000 Pictures", "id"=> 711}, {"name"=>"Regency Enterprises", "id"=>508}]
movie.production_countries => [{"iso_3166_1"=>"DE", "name"=>"Germany"}, {"iso_3166_1"=>"US", "name"=>"United States of America"}]
movie.release_date => "1999-10-14"
movie.revenue => 100853753
movie.runtime => 139
movie.spoken_languages => [{"iso_639_1"=>"en", "name"=>"English"}]
movie.status => "Released"
movie.tagline => "How much can you know about yourself if you've never been in a fight?"
movie.title => "Fight Club"
movie.vote_average => 8.8
movie.vote_count => 234
```
Get the latest movie id.
```ruby
Tmdb::Movie.latest
```
Get the list of upcoming movies. This list refreshes every day. The maximum number of items this list will include is 100.
```ruby
Tmdb::Movie.upcoming
```
Get the list of movies playing in theatres. This list refreshes every day. The maximum number of items this list will include is 100.
```ruby
Tmdb::Movie.now_playing
```
Get the list of popular movies on The Movie Database. This list refreshes every day.
```ruby
Tmdb::Movie.popular
```
Get the list of top rated movies. By default, this list will only include movies that have 10 or more votes. This list refreshes every day.
```ruby
Tmdb::Movie.top_rated
```

Get the alternative titles for a specific movie id.
```ruby
Tmdb::Movie.alternative_titles(22855)
```

Get the images (posters and backdrops) for a specific movie id.
```ruby
Tmdb::Movie.images(22855)
```

Get the cast information for a specific movie id.
```ruby
Tmdb::Movie.casts(22855)
```

Get the plot keywords for a specific movie id.
```ruby
Tmdb::Movie.keywords(22855)
```

Get the release date by country for a specific movie id.
```ruby
Tmdb::Movie.releases(22855)
```

Get the trailers for a specific movie id.
```ruby
Tmdb::Movie.trailers(22855)
```

Get the translations for a specific movie id.
```ruby
Tmdb::Movie.translations(22855)
```

Get the similar movies for a specific movie id.
```ruby
Tmdb::Movie.similar_movies(22855)
```

Get the lists that the movie belongs to.
```ruby
Tmdb::Movie.lists(22855)
```

Get the changes for a specific movie id.
```ruby
Tmdb::Movie.changes(22855)
```

h3. Company
#company = Tmdb::Company.detail(1)
#puts company.id
#puts company.description
#puts company.homepage
#puts company.logo_path
#puts company.name
#puts company.parent_company
#puts Tmdb::Company.movies(1)

h3. Collection
#collection = Tmdb::Collection.detail(51845)
#puts collection.id
#puts collection.backdrop_path
#puts collection.parts
#puts collection.poster_path
#puts collection.name
#puts Tmdb::Collection.images(51845)

h3. People
#people = Tmdb::People.detail(1)
#puts people.id
#puts people.name
#puts people.place_of_birth
#puts people.also_known_as
#puts people.adult
#puts people.biography
#puts people.birthday
#puts people.deathday
#puts people.homepage
#puts people.profile_path
#puts Tmdb::People.popular
#puts Tmdb::People.latest
#puts Tmdb::People.credits(1)
#puts Tmdb::People.images(1)
#puts Tmdb::People.changes(1)