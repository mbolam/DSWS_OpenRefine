---
layout: default
title: 5-Web Scraping
nav: true
---

# Getting Data by Scraping the Web

- Create new project from Clip board
  - paste in `https://pittsburgh.craigslist.org/search/sss`
  - this will only pull the data from the first page of results; you'd have to do some query manipulation to get more results back.
  - you can perform a search to get a subset of this data
- create column by fetching url, named "search"
- on "search" column:
  - create column based on called "links", using transform to get only the \<a\> with class="hdrlnk", `forEach(value.parseHtml().select("a.hdrlnk"),e,e.htmlAttr("href")).join(" ; ")`
- remove the first column and "search" column
- on "links" column:
  - split multivalued cells on `;`
- add column by fetching url, named "ads"
  - this can be slow, as OpenRefine goes to the web and queries Craigslist and pulls back results pages. For the workshop, "star" a couple, then facet by star.
- on "ads" column:
  - get title: add column based on "ads" named "title", grabbing span class="postingtitletext", `value.parseHtml().select("head")[0].select("title")[0].htmlText()`
  - get price: `value.parseHtml().select("h2.postingtitle")[0].select("span.price")[0].htmlText()`
  - get category: `value.parseHtml().select("header")[0].select("li.category")[0].htmlText()`

Etc!
