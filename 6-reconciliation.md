---
layout: default
title: 6-Reconciliation
nav: true
---

# Enhancing with Data from Other Sources

**Reconciling from other data sources**
- Vocabulary reconciliation is a process where automated systems use terms from unstandardized metadata to search controlled vocabularies and return URIs.
- OpenRefine has built in tools to reconcile data with [Wikidata](https://www.wikidata.org/)
- Other data services can be added

**OpenRefine's Wikidata Service**
- Reconciling the names
  - `Reconcile` > `Start reconciling...`
  - choose `Wikidata Reconciliation for OpenRefine (en)`
  - choose `human` and `Auto-match candidates with high confidence`
  - matches some automatically, but often requires some manual review
- OpenRefine 2.8 added querying and extracting tools
  - Select `matched` from the judgement facet
  - `Edit column` > `Add columns from reconciled values`
  - Add country of citizenship, occupation, place of birth, place of death, place of burial, and VIAF ID
  - `Add Property` filter to include date of birth and date of death
- Review the results of your reconciliation
  - date of birth > `Facet` > `Timeline facet`
- Extract the Wikidata id
  - `Edit column` > `Add column based on this column...`
  - name column: wikidata_id
  - cell.recon.match.id

**Adding more data based on extracted dataset**
- Geographic Coordinates for places
  - place of birth > `Edit column` > `Add columns from reconciled values`
  - Add coordinate location

**Compare the collected and extracted VIAF ids**
- Clean up collected VIAF ids
  - `Facet` > `Customized facets` > `Facet by blank`
  - On rows view, choose `false` to select rows with viaf ids
  - `Filter` - regex: ^(?!http://).+
  - Transform cells to remove final "/" temporarily - value.replace(/\/$/, "")
  - Transform cells to apply final "/" because that is what VIAF expects - value+"/"
- Make extracted VIAF id numbers into VIAF URLs
  - `Edit column` > `Add column based on this column...`
  - name column: viaf_url
  - "http://http://viaf.org/viaf/" + value + "/"
- Build a facet to compare the two columns
  - value == cells["viaf id"].value

**Other data services**
- Users can set up their own data services or use other existing data services.
- Some sample services are available at the [OpenRefine Wiki - Reconcilable Data Sources](https://github.com/OpenRefine/OpenRefine/wiki/Reconcilable-Data-Sources) and at [http://refine.codefork.com/](http://refine.codefork.com/).
- Reconciliation can be taxing on host servers and data sources. Documentation for hosting your own service are available at and on the [conciliator GitHub](https://github.com/codeforkjeff/conciliator).
