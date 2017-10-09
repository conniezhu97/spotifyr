---
title: "spotifyr"
author: "RCharlie"
date: "September 9, 2017"
output: html_document
---

## Overview
spotifyr is a quick and easy wrapper for pulling track audio features from Spotify's Web API in bulk. By automatically batching API requests, it allows you to enter an artist's name and retrieve their entire discography in seconds, along with Spotify's audio features and track/album popularity metrics. You can also pull song and playlist information for a given Spotify User (including yourself!).

## Installation
```r
devtools::install_github('charlie86/spotifyr')
```

## Authenication
You'll have to set up a Dev account with Spotify to access their Web API [here](https://developer.spotify.com/my-applications/#!/applications). This will give you your `Client ID` and `Client Secret`. Once you have those, you can pull your access token into R with `get_spotify_access_token`. 

The easiest way to authenticate is to set your credentials to the System Environment variables `SPOTIFY_CLIENT_ID` and `SPOTIFY_CLIENT_SECRET`. The default arguments to `get_spotify_access_token` (and all other functions in this package) will refer to those. Alternatively, you can set them manually and make sure to explicitly refer to your access token in each subsequent function call.

```r
Sys.setenv(SPOTIFY_CLIENT_ID = 'xxxxxxxxxxxxxxxxxxxxx')
Sys.setenv(SPOTIFY_CLIENT_SECRET = 'xxxxxxxxxxxxxxxxxxxxx')

access_token <- get_spotify_access_token(client_id = Sys.getenv('SPOTIFY_CLIENT_ID'), client_secret = Sys.getenv('SPOTIFY_CLIENT_SECRET'))
```

## Usage
### What was The Beatles' favorite key?

```r
library(spotifyr)
```

```
## Warning: package 'dplyr' was built under R version 3.4.2
```


```r
beatles <- get_artist_audio_features('the beatles')
```

```
## Error in overscope_eval_next(overscope, expr): object 'artist_uri' not found
```

```r
count(beatles, key_mode, sort = T)
```

```
## Error in group_vars(x): object 'beatles' not found
```

### What's the most danceable Joy Division song?

```r
joy <- get_artist_audio_features('joy division')
```

```
## Error in overscope_eval_next(overscope, expr): object 'artist_uri' not found
```

```r
joy %>% 
 arrange(-danceability) %>% 
 select(track_name, danceability) %>% 
 head(10)
```

```
## Error in eval(lhs, parent, parent): object 'joy' not found
```
