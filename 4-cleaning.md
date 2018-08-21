---
layout: default
title: 4-Cleaning
nav: true
---

# Demo: Digital Mitford Data

In this demo we are going to play with a data set extracted from [Digital Mitford](http://digitalmitford.org/). The original data was a [TEI](http://www.tei-c.org/index.xml) encoded index of names used on the site. The <listPerson sortKey="histPersons"> node was extracted into a TSV file for simplicity.

Download <a href="images/histPerson_data.tsv" target="_blank">`histperson.tsv`</a>

The data fields are
- xml id
- gender
- name
- occupation
- viaf id

# Navigating OpenRefine

- Creating a project
  - check character encoding, options
  - Refine never over writes your original data, it creates a copy!
  - information is *not* sent over internet

- Manipulating columns
  - renaming and removing columns
  - changing column order
  - collapsing columns

- Exporting a project or a data set
  - OpenRefine project
  - many formats!
  - templating
  - export is always a new copy of data, never alters original!

- Automating tasks
  - Undo/Redo copy `Extract` to txt file (use text editor, not Word)
  - create new project with original file
  - Undo/Redo paste saved extract into `Apply`

# Exploring and Cleaning Data

- Cleaning the simple stuff
  - a lot of options in the drop-down menus
  - get rid of white space
    - `Edit cells` > `Common transforms`
  - `Edit cells` > `Transform...` is very powerful
  - GREL = General Refine Expression Language
  - GREL [documentation](https://github.com/OpenRefine/OpenRefine/wiki/General-Refine-Expression-Language) and [recipes](https://github.com/OpenRefine/OpenRefine/wiki/Recipes) are available on the OpenRefine wiki.

- Splitting, faceting, and clustering
  - multi-valued fields can be a barrier to data cleaning
    - `Edit cells` > `Split multi-valued cells...`
    - record view vs. row view
    - `Facet` > `Text facet`
    - manual cleaning and clustering
    - `Edit cells` > `Join multi-valued cells`
