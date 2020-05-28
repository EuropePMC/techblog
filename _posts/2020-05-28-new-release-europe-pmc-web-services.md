---
layout: post
title:  'New release: Europe PMC Web Services 6.3'
date:   2020-01-28
author: ['dayane', 'mohamed']
category: literature_data_integration
summary: A new Europe PMC Web Services release
---
Today Europe PMC released Web Services version 6.3, updating its SOAP and RESTful APIs. Programmatic users can now find more fields available in the core response of these services

## Multiple author affiliations

In the previous version, author affiliations were a single value. The new version 6.3 includes a list of multiple affiliations.

<!--more-->
Example:

    <authorList>
        <author>
            <fullName>Wei W</fullName>
            <firstName>Wei</firstName>
            <lastName>Wei</lastName>
            <initials>W</initials>
            <authorAffiliationsList>
                <authorAffiliation>
                    Department of Orthopaedics, The 1st Affiliated Hospital of Harbin Medical University, Harbin, China.
                </authorAffiliation>
                <authorAffiliation>
                    Department of Orthopaedics, Harbin 242 Hospital, Harbin, China.
                </authorAffiliation>
            </authorAffiliationsList>
        </author>
    </authorList>

## Datalinks tags

Articles now also contain data links tags, which can be used to retrieve data links using a tag parameter.

Example:

    <dataLinksTagsList>
        <dataLinkstag>altmetrics</dataLinkstag>
        <dataLinkstag>supporting_data</dataLinkstag>
    </dataLinksTagsList>

Check the [Articles RESTful API](https://europepmc.org/RestfulWebService) page to find more information on Europe PMC data links.

## Publication status

Retrieving the status of the article is now also possible. The new field ‘Publication status’ indicates, for example, if a given article is published or ahead of print.

The possible values for publication status are:

<dl>
  <dt>received</dt>           <dd>date manuscript received for review</dd>
  <dt>accepted</dt>          <dd>accepted for publication</dd>
  <dt>epublish</dt>          <dd>published electronically by publisher</dd>
  <dt>ppublish</dt>          <dd>published in print by publisher</dd>
  <dt>revised</dt>          <dd>article revised by publisher/author</dd>
  <dt>pmc</dt>          <dd>article first appeared in PubMed Central</dd>
  <dt>pmcr</dt>         <dd>article revision in PubMed Central</dd>
  <dt>pubmed</dt>          <dd>article citation first appeared in PubMed</dd>
  <dt>pubmedr</dt>          <dd>article citation revision in PubMed</dd>
  <dt>aheadofprint</dt>      <dd>epublish, but will be followed by print</dd>
  <dt>premedline</dt>        <dd>date into PreMedline status</dd>
  <dt>medline</dt>          <dd>date made a MEDLINE record</dd>
  <dt>other</dt><dd></dd>
</dl>

Example:

    <publicationStatus>ppublish</publicationStatus>

Let us know your thoughts and questions regarding this new release. Contact [helpdesk@europepmc.org](mailto:helpdesk@europepmc.org) or post on the [Europe PMC developer forum](https://groups.google.com/a/ebi.ac.uk/forum/#!forum/epmc-webservices).
