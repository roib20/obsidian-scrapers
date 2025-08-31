---
<%*
// Request a web page to speed up execution time
let page = await tp.obsidian.request(await tp.system.clipboard())
let doc = new DOMParser().parseFromString(page,"text/html")

let title = await tp.user.goodreads('title', tp, doc)
-%>
url: "<% tp.user.goodreads('url', tp, doc) %>"
isbn: <% tp.user.goodreads('isbn', tp, doc) %>
published: <% tp.user.goodreads('published', tp, doc) %>
pages: <% tp.user.goodreads('pageCount', tp, doc) %>
ratings: <% tp.user.goodreads('rating', tp, doc) %>
authors: <% tp.user.goodreads('authorsQuotesListLink', tp) %>
genres: <% tp.user.goodreads('genresQuotesListLink', tp, doc) %>
cover: "<% tp.user.goodreads('cover', tp, doc) %>"
---

# <% title %> - <% tp.user.goodreads('authors', tp) %>

!['<% title %>' Cover](<% tp.user.goodreads('cover', tp, doc) %>)

## Description

<% tp.user.goodreads('description', tp, doc) %>

<%* 
let filename = title + " - " + await tp.user.goodreads('authors', tp)
// Remove prohibited characters
filename = filename.replace(/[/\:*?<>|""]/g, "")
// Rename a note
await tp.file.move(filename)
-%>
