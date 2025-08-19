---
<%*
// Request a web page to speed up execution time
let page = await tp.obsidian.request(await tp.system.clipboard())
let doc = new DOMParser().parseFromString(page,"text/html")

let title = await tp.user.imdb('title', tp, doc)
-%>
url: "<% tp.user.imdb('url', tp, doc) %>"
my-watch-dates:
 - "[[<% tp.date.now("YYYY-MM-DD") %>]]"
my-rating: 0
imdb-rating: <% tp.user.imdb('imdbRating', tp, doc) %>
duration: <% tp.user.imdb('duration', tp, doc) %>
year: <% tp.user.imdb('published', tp, doc) %> 
type: <% tp.user.imdb('type', tp, doc) %>
genres: [<% tp.user.imdb('genresQuotes', tp, doc) %>]
keywords: [<% tp.user.imdb('keywordsQuotes', tp, doc) %>]
cast: [<% tp.user.imdb('starsQuotes', tp, doc) %>]
countries: [<% tp.user.imdb('countriesQuotes', tp, doc) %>]
creators: [<% tp.user.imdb('creatorsQuotes', tp, doc) %>]
directors: [<% tp.user.imdb('directorsQuotes', tp, doc) %>]
---
# <% title %> (<% await tp.user.imdb('published', tp, doc) %>)

## My Review



## Image

![](<% tp.user.imdb('image', tp, doc) %>)

## Description

<% tp.user.imdb('description', tp, doc) %>

## Genres

<% tp.user.imdb('genresLinks', tp, doc) %>

## Keywords

<% tp.user.imdb('keywordsLinks', tp, doc) %>

## Cast

<% tp.user.imdb('starsLinks', tp, doc) %>

## Countries

<% tp.user.imdb('countriesLinks', tp, doc) %>

## Creators

<% tp.user.imdb('creatorsLinks', tp, doc) %>

## Directors

<% tp.user.imdb('directorsLinks', tp, doc) %>

<%*
let filename = title + " (" + await tp.user.imdb('published', tp, doc) + ")"
// Remove prohibited characters
filename = filename.replace(/[/\:*?<>|""]/g, "")
// Rename a note
await tp.file.move(filename)
-%>
