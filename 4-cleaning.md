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

{% include figure.html file="openRefineDataPreview.jpg" alt="openrefine data preview" width="100%" %}

## Navigating OpenRefine
  - Data manipulation happens through pull-down menus associated with each column.
  - OpenRefine only displays a few fields at a time - it is acting as a preview of the data, but the actions taken are on all cells in a column.
  - You can adjust the number of visible fields and navigate forward/backward through the pages of data.
  - Data manipulation happens through pull-down menus associated with each column.

{% include figure.html file="openRefineMenuSelect.jpg" alt="openrefine menu select" width="100%" %}

## Text Filters
  - Text filters can be used to isolate specific rows that contain the text. They can be used to quickly isolate rows for further manipulation.
  - The dialog box allows for case-sensitive filters and regular expressions.
  - Regular expressions can be very powerful for querying data, but a bit outside the scope of this workshop. I regularly use a regular expression to find rows that do not have the word:  ^((?!Pennsylvania).)\*$

## Facets
  - Creating and using facets is one of the most powerful features of OpenRefine. Facets can be used to learn more about your data, discover inconsistencies, and select subsets of data for review and cleaning.
  - Many types of facets can be created, depending on the data type of the field - text, numeric, timeline, scatterplot. Additionally, there is a list of custom facets built for specific uses, like duplicates, text length, errors, and empty strings. Finally, users can create their own facets using the custom facet builder.
  - This workshop will focus mostly on text facets, because our data is not great for demonstrating the others.

## Editing Data
  - OpenRefine is great for making the same change throughout a column of data. An individual cell can be selected and edited, and all other cells matching that cell can be automatically updated.
  - Using facets, the text of the facet can be modified, updating all of the cells with that same data.

## Transforming Data
  - OpenRefine includes some basic "Common Transforms", including trimming and collapsing whitespace, change the text case, and converting cells to different datatypes.
  - Additionally, you can write your own tranforms using the General Refine Expression Language (GREL). GREL is incredibly powerful, and we are going to look at a few examples:
      - Clean-up character encoding problems
          - `value.unescape("url")`
      - Add to a string
          - `value + " random thing"`
      - Replace string in cells
          - `value.replace("Pittsburgh", "Pgh")`
          - `value.replace("~", "").replace(",", "").replace("-", "")`
      - Remove duplicate comma separated entries in a cell
          - `value.split(", ").uniques().join(", ")`
      - Convert number with text to number
          - `toNumber(value.replace(" million", ""))*1000000`
  - This is just the basics. GREL [documentation](https://github.com/OpenRefine/OpenRefine/wiki/General-Refine-Expression-Language) and [recipes](https://github.com/OpenRefine/OpenRefine/wiki/Recipes) are available on the OpenRefine wiki.

## Clustering
  - OpenRefine includes a set of text clustering algorithms. The different algorithms are best suited for different types of applications, but I have found that navigating through the different options helps considerably when attempting to normalize data.
  - Learn more about the text clustering algorithms - [Clustering In Depth](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth) - on the OpenRefine wiki.

## Creating New Columns

## Splitting Columns

## Removing Duplicate Rows

## Working with Different Data Types

## Interacting with Rows


## Exporting a Project or Data Sets

## Undo / Redo
 - OpenRefine has powerful undo and redo capabilities. The Undo/Redo link provides the entire project history, and allows you to step back/forward to any step in the process.

## Automating Workflows
  - The actions in the Undo/Redo tab can also be saved to create workflows. If you are regularly performing the same actions on a data set, then it might be helpful to save the process and reuse it each time you open the data set.

## Fetching Data from a URL


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
