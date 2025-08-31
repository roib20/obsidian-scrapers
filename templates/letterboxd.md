---
<%*
// Request a web page to speed up execution time
let page = await tp.obsidian.request(await tp.system.clipboard())
let doc = new DOMParser().parseFromString(page,"text/html")

let title = await tp.user.letterboxd('title', tp, doc)
let altTitle = await tp.user.letterboxd('altTitle', tp, doc)
-%>
aliases: <%* altTitle == "" ? tR += '["' + title + '"]' : tR += '["' + title + '", "' + altTitle + '"]' %>
url: "<% tp.user.letterboxd('url', tp, doc) %>"
imdb-url: <% tp.user.letterboxd('imdbUrl', tp, doc) %>
tmdb-url: <% tp.user.letterboxd('tmdbUrl', tp, doc) %>
rating: <% tp.user.letterboxd('rating', tp, doc) %>
runtime: <% tp.user.letterboxd('runtime', tp, doc) %>
year: <% tp.user.letterboxd('published', tp, doc) %> 
genres: <% tp.user.letterboxd('genresQuotesListLink', tp, doc) %>
directors: <% tp.user.letterboxd('directorsQuotesListLink', tp, doc) %>
studios: <% tp.user.letterboxd('studiosQuotesListLink', tp, doc) %>
countries: <% tp.user.letterboxd('countriesQuotesListLink', tp, doc) %>
languages: <% tp.user.letterboxd('languagesQuotesListLink', tp, doc) %>
writers: <% tp.user.letterboxd('writersQuotesListLink', tp, doc) %>
cast: <% tp.user.letterboxd('castShortQuotesListLink', tp, doc) %>
cover: "<% tp.user.letterboxd('image', tp, doc) %>"
---

# <% tp.user.letterboxd('title', tp, doc) %>

## Poster

!['<% title %>' Poster](<% tp.user.letterboxd('image', tp, doc) %>)

## Description

<% tp.user.letterboxd('description', tp, doc) %>

<%* 
let filename = title
// Remove prohibited characters
filename = filename.replace(/[/\:*?<>|""]/g, "")
// Rename a note
await tp.file.move(filename)
-%>
