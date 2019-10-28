---
layout: default
title: 4-Cleaning
nav: true
---

# Cleaning Data with OpenRefine

## About the Data

In this demo we are going to play with a data about University endowments harvested from Wikipedia—so it is very *messy*! Since we are trying to demonstrate a lot of features, some of the steps will be very “destructive” to the data (but our original data is still safe).

Download <a href="images/universityData.csv" target="\_blank">`universityData.csv`</a>

> The university endowment demo data is from the Enipedia OpenRefine Tutorial.

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

## Creating a project
  - Projects can be created from data on your computer, data on the web, pasting into the clipboard, connecting to a database, or linking to Google Sheets.
  - As a reminder. OpenRefine never over writes your original data, and information is *not* sent over the Internet!
  - OpenRefine can accept a variety of data types, including CSV/TSV/\*SV, line-based text files, fixed-width field text files, JSON files, RDF files, XML files, and Excel files. I have found that simple \*SV files tend to work the best.
  - OpenRefine data preview page will attempt to identify the file-type, and the available options will vary based on that file-type. For our University Data, OpenRefine correctly identified it as TSV, even though the file extension said ".csv"
  - When satisfied with the data, click the "Create Project>>" button.

## Navigating OpenRefine
  - Data manipulation happens through pull-down menus associated with each column.
  - OpenRefine only displays a few fields at a time - it is acting as a preview of the data, but the actions taken are on all cells in a column.
  - You can adjust the number of visible fields and navigate forward/backward through the pages of data.

## Text Filters
  - Text filters can be used to isolate specific rows that contain the text. They can be used to quickly isolate rows for further manipulation.
  - The dialog box allows for case-sensitive filters and regular expressions.
  - Regular expressions can be very powerful for querying data, but a bit outside the scope of this workshop. I regularly use a regular expression to find rows that do not have the word:  ^((?!Pennsylvania).)\*$

## Facets
  - Creating and using facets is one of the most powerful features of OpenRefine. Facets can be used to learn more about your data, discover inconsistencies, and select subsets of data for review and cleaning.
  - Many types of facets can be created, depending on the data type of the field - text, numeric, timeline, scatterplot. Additionally, there is a list of custom facets built for specific uses, like duplicates, text length, errors, and empty strings. Finally, users can create their own facets using the custom facet builder.
  - This workshop will focus mostly on text facets, because our data is not great for demonstrating the others.

## Editing Data

## Transforming Data

## Mass Cleaning

## Clustering

## Creating New Columns

## Splitting Columns

## Removing Duplicate Rows

## Manipulating Data Types

## Interacting with Rows

## Exporting a Project or Data Sets

## Automating Workflows

## Fetching Data from a URL



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

**Even More**
  - Star / Flag & remove rows
  - create new column with transform `length(value)`, numeric facet
  - deduplicate
    - sort by, permanent reorder
    - blank down / fill down
  - fetch URLs
    - basic geo code lookup using [Open Street Maps Nominatim API](https://nominatim.openstreetmap.org/) ([Nominatim Usage Policy](https://operations.osmfoundation.org/policies/nominatim/))
      - create URLs that point at the Nominatim API -- add column based on "country" column: `"https://nominatim.openstreetmap.org/search?format=json&email=mbolam@gmail.com&app=google-refine&q=" + escape(value, 'url')`
      - grab JSON from the API using "Add column by fetching URLs" on newly created column
      - parse JSON using "Add column based on this column" `with(value.parseJson()[0], pair, pair.lat + ',' + pair.lon)`

## Exploring and Cleaning Data

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
