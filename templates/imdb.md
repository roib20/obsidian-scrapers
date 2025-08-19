---
<%*
// Request a web page to speed up execution time
let page = await tp.obsidian.request(await tp.system.clipboard())
let doc = new DOMParser().parseFromString(page,"text/html")

let title = await tp.user.imdb('title', tp, doc)
-%>
url: "<% tp.user.imdb('url', tp, doc) %>"
watched:
 - "[[<% tp.date.now("YYYY-MM-DD") %>]]"
my-rating: 0
imdb-rating: <% tp.user.imdb('imdbRating', tp, doc) %>
duration: <% tp.user.imdb('duration', tp, doc) %>
year: <% tp.user.imdb('published', tp, doc) %> 
type: <% tp.user.imdb('type', tp, doc) %>
genres: <% tp.user.imdb('genresQuotesListLink', tp, doc) %>
keywords: <% tp.user.imdb('keywordsQuotesListLink', tp, doc) %>
cast: <% tp.user.imdb('starsQuotesListLink', tp, doc) %>
countries: <% tp.user.imdb('countriesQuotesListLink', tp, doc) %>
creators: <% tp.user.imdb('creatorsQuotesListLink', tp, doc) %>
directors: <% tp.user.imdb('directorsQuotesListLink', tp, doc) %>
---
# <% title %> (<% await tp.user.imdb('published', tp, doc) %>)

## My Review



## Image

![](<% tp.user.imdb('image', tp, doc) %>)

## Description

<% tp.user.imdb('description', tp, doc) %>

<%*
let filename = title + " (" + await tp.user.imdb('published', tp, doc) + ")"
// Remove prohibited characters
filename = filename.replace(/[/\:*?<>|""]/g, "")
// Rename a note
await tp.file.move(filename)
-%>
