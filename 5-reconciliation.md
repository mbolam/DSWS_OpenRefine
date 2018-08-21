---
layout: default
title: 5-Reconciliation
nav: true
---

# Enhancing with Data from Other Sources

- Reconciling from other data sources
  - Vocabulary reconciliation is a process where automated systems use terms from unstandardized metadata to search controlled vocabularies and return URIs.
  - OpenRefine has built in tools to reconcile data with [Wikidata](https://www.wikidata.org/)
  - Other data services can be added

- OpenRefine's Wikidata Service
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
