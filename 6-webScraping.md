---
layout: default
title: 6-Web Scraping
nav: true
---

# Getting Data by Scraping the Web
- Web scraping, web harvesting, or web data extraction is data scraping used for extracting data from websites. OpenRefine can be used to extract data from websites, then immediately cleaned and prepared for analysis. We'll be modeling one method of using OpenRefine to scrape Craigslist. A more detailed tutorial can be found on the the Programming Historian - [Fetch and Parse Data with OpenRefine](https://programminghistorian.org/en/lessons/fetch-and-parse-data-with-openrefine)

## Tutorial
- Create new project from Clipboard
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
