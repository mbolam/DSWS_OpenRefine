---
layout: default
title: 6-Reconciliation
nav: true
---

# Enhancing with Data from Other Sources
- Vocabulary reconciliation is a process where automated systems use terms from unstandardized metadata to search controlled vocabularies and return URIs.
- OpenRefine has built in tools to reconcile data with [Wikidata](https://www.wikidata.org/)
- Other data services can be added

## OpenRefine's Wikidata Service
- Reconciling the university names
  - `Reconcile` > `Start reconciling...`
  - choose `Wikidata Reconciliation for OpenRefine (en)`
  - choose `universities` and `Auto-match candidates with high confidence`
  - matches some automatically, but often requires some manual review

- Extract the Wikidata id
  - `Edit column` > `Add column based on this column...`
  - name column: wikidata_id
  - cell.recon.match.id

## Adding more data based on extracted dataset
- OpenRefine 2.8 added querying and extracting tools
  - Select `matched` from the judgement facet
  - `Edit column` > `Add columns from reconciled values`
  - Add located at street address, student count, country, official website, inception, mascot, Carnegie Classification of Institutions of Higher Education (etc.)
- Geographic Coordinates for places
  - place of birth > `Edit column` > `Add columns from reconciled values`
  - Add coordinate location

## Other data services
- Users can set up their own data services or use other existing data services.
- Some sample services are available at the [OpenRefine Wiki - Reconcilable Data Sources](https://github.com/OpenRefine/OpenRefine/wiki/Reconcilable-Data-Sources) and at [http://refine.codefork.com/](http://refine.codefork.com/).
- Reconciliation can be taxing on host servers and data sources. Documentation for hosting your own service are available at and on the [conciliator GitHub](https://github.com/codeforkjeff/conciliator).
