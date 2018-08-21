---
layout: default
title: 4-Cleaning
nav: true
---

# Demo: Navigating OpenRefine and Basic Data Cleaning

In this demo we are going to play with a data about University endowments harvested from Wikipedia—so it is very *messy*!

Download <a href="images/universityData.csv" target="_blank">`universityData.csv`</a>

> The university endowment demo data is from the [Enipedia OpenRefine Tutorial](http://enipedia.tudelft.nl/wiki/OpenRefine_Tutorial).

The data fields are
- university
- endowment
- numFaculty
- numDoctoral
- country
- numStaff
- established
- numPostgrad
- numUndergrad
- numStudents

# Navigating OpenRefine

**Creating a project**
  - check character encoding, options
  - Refine never over writes your original data, it creates a copy!
  - information is *not* sent over internet

**Manipulating columns**
  - text filter
  - faceting
  - edit cells / facets
  - transform, `value.unescape('url')`, find & replace, `value.replace("old","new")`
  - undo/redo
  - clustering
  - split into multiple columns
  - combine columns (*tricky* because combining blank cells results in an error)
    - facet by blank, combine only non-empty cells
    - transform, `value + " " + cells["col 2"].value`
  - remove / reorder columns

**Exporting a project or a data set**
  - OpenRefine project
  - many formats!
  - templating
  - export is always a new copy of data, never alters original!

**Automating tasks**
  - Undo/Redo copy `Extract` to txt file (use text editor, not Word)
  - create new project with original file
  - Undo/Redo paste saved extract into `Apply`

**More!**
	- Star / Flag & remove rows
	- create new column with transform `length(value)`, numeric facet
	- deduplicate
		- sort by, permanent reorder
		- blank down / fill down
  - fetch URLs
    - basic geo code lookup, `"http://maps.google.com/maps/api/geocode/json?sensor=false&address=" + escape(value, "url")
  with(value.parseJson().results[0].geometry.location, pair, pair.lat +", " + pair.lng)`

# Exploring and Cleaning Data

**Cleaning the simple stuff**
  - a lot of options in the drop-down menus
  - get rid of white space
    - `Edit cells` > `Common transforms`
  - `Edit cells` > `Transform...` is very powerful
  - GREL = General Refine Expression Language
  - GREL [documentation](https://github.com/OpenRefine/OpenRefine/wiki/General-Refine-Expression-Language) and [recipes](https://github.com/OpenRefine/OpenRefine/wiki/Recipes) are available on the OpenRefine wiki.

**Sample GREL Recipes**
- Clean-up character encoding problems
  - `value.unescape("url")`
- Replace string in cells
  - `value.replace("Pittsburgh", "Pittsburg")`
  - `value.replace("~", "").replace(",", "").replace("-", "")`
- Remove duplicate comma separated entries in a cell
  - `value.split(", ").uniques().join(", ")`
- Convert number with text to number
  - `toNumber(value.replace(" million", ""))*1000000`

**Splitting, faceting, and clustering**
  - multi-valued fields can be a barrier to data cleaning
    - `Edit cells` > `Split multi-valued cells...`
    - record view vs. row view
    - `Facet` > `Text facet`
    - manual cleaning and clustering
    - `Edit cells` > `Join multi-valued cells`
