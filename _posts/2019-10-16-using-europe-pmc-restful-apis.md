---
layout: post
title:  "PDBe integrates Europe PMC APIs"
date:   2019-10-16
author: ['dayane', 'nurul']
category: literature_data_integration
summary: PDBe exposes literature metadata by integrating Europe PMC REST APIs
---

## PDBe exposes literature metadata by integrating Europe PMC REST APIs

[PDBe](https://www.ebi.ac.uk/pdbe/), a member of the Worldwide Protein Bank, is a European resource that maintains a free and publicly available archive of macromolecular structures. The public can easily find information on protein structure and metadata associated with protein structure. PDBe also exposes enriched metadata from other sources such as publications and citations, which are retrieved through Europe PMC APIs.
<!--more-->

By integrating knowledge from Europe PMC open-access publications, PDBe provides entries with 3D macromolecular structures in context with literature highlighting the impact of a given structure on scientific research. The first step in the integration process is to map the PDB IDs to PubMed IDs (e.g PDB "1cbs" has "PMID7704533" as its primary publication). The second step is to use the Europe PMC REST API [GET /search](https://europepmc.org/RestfulWebService#!/Europe32PMC32Articles32RESTful32API/search) request to retrieve the publications by PMID, which will populate a PDBe page with fields such as publication DOI, title, authorList, journal and abstract.

[![Illustration showing how the webservices response becomes text on a webpage in PDBe][image_1]][image_1]
<small style="display:block; text-align: right;">***Figure 1**: [Europe PMC's search API response](https://www.ebi.ac.uk/europepmc/webservices/rest/search?query=7704533&resultType=core&cursorMark=*&pageSize=25&format=json) becomes [a page on PDBe](https://www.ebi.ac.uk/pdbe/entry/pdb/1cbs/)*</small>

PDBe also retrieves citation counts through the Europe PMC REST API [GET /citations](https://europepmc.org/RestfulWebService#!/Europe32PMC32Articles32RESTful32API/citations) request for each PMID. The response is manipulated in order to display the number and links to reviews and experimental articles citing a given publication.

[![Illustration showing how the webservices response becomes text on a webpage in PDBe][image_2]][image_2]
<small style="display:block; text-align: right;">***Figure 2**: [Europe PMC's citations API response](https://www.ebi.ac.uk/europepmc/webservices/rest/MED/7704533/citations?page=1&pageSize=25&format=json) becomes [a page on PDBe](https://www.ebi.ac.uk/pdbe/entry/pdb/1cbs/citations)*</small>

The integration of Europe PMC APIs in PDBe web services was very simple. Once we knew what data we were interested in, we just needed to use the correct API endpoint with the corresponding parameters to populate PDBe database with data gleaned from the response. This data is then used for PDBe pages and PDBe REST API providing richer context to protein structure records.

[image_1]: {{site.baseurl}}/images/posts/using-europe-pmc-restful-apis/Blog_image01.png
[image_2]: {{site.baseurl}}/images/posts/using-europe-pmc-restful-apis/Blog_image02.png
