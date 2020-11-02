---
layout: post
title:  "Europe PMC <em>Text-annotator</em> is now open source"
date:   2020-11-02
author: ['dayane', 'zhan']
category: literature_data_integration
summary: A new open source tool for annotating Europe PMC articles.
---

<style type="text/css" scoped>
  a img {
    border: 2px solid #ccc;

  }
</style>

## Introducing *Text-annotator*

Europe PMC has open-sourced *Text-annotator*, a JavaScript library to locate and annotate plain text in HTML. 
The annotation process includes:

1. **Search**: Search for a piece of plain text in the HTML; on finding it, store its location identified by an index and then return the index for later annotation.<!--more-->
1. **Annotate**: Annotate the found text given its index.  <br/><br/>
In order to annotate a piece of text, two steps, search and annotate, are taken. The idea of splitting the annotation process into the two steps is to allow more flexibility, e.g., the user can search for all pieces of text first and then annotate them later as required. *Text-annotator* can be used in the browser or the Node.js server.

## How is *Text-annotator* used in Europe PMC? 

The *Text-annotator* has been used in [Europe PMC](https://europepmc.org) in the following features: 

### Article title highlighting

When searching in Europe PMC, the search term will be highlighted in the title of articles displayed in the search result page. 

[![Search example][image4]][image4]
<small style="display:block;text-align:center;"><a href="https://europepmc.org/search?query=p53">https://europepmc.org/search?query=p53</a></small>


### Snippets

*Text-annotator* also supports the snippets, which are highlights from the article matching the searched query. 

[![Snippets example][image5]][image5]
<small style="display:block;text-align:center;"><a href="https://europepmc.org/article/MED/33121131">https://europepmc.org/article/MED/33121131</a></small>

Every search result displays two snippets, separated by an ellipsis. The following shows the snippets in an article returned for a search term ‘cancer’

[![Search result snippets example][image1]][image1]
<small style="display:block;text-align:center;"><a href="https://europepmc.org/search?query=cancer">https://europepmc.org/search?query=cancer</a></small>

### SciLite
The *Text-annotator* was also used for the development of [SciLite](http://blog.europepmc.org/2020/09/announcing-new-version-of-scilite.html), a tool for highlighting biological entities, such as genes/proteins, accession numbers, protein interactions, diseases, gene-disease relationship, in the full text of life sciences articles in Europe PMC. This function combines the two steps of *Text-annotator*, search and annotation. SciLite currently provides access to over 1.3 billion annotations in articles. 

[![Scilite example][image2]][image2]
<small style="display:block;text-align:center;"><a href="https://europepmc.org/article/PMC/PMC6423025">https://europepmc.org/article/PMC/PMC6423025</a></small>

### Linkback
When using SciLite, the highlighted term will provide a popup window with the name of the annotation provider and a link to the data resource. The feature that allows users to get the linkback to this annotation via the ‘Share’ option also is supported by *Text-annotator*. 

[![Linkback example][image3]][image3]
<small style="display:block;text-align:center;"><a href="http://europepmc.org/article/PMC/PMC6423025#europepmc-b1865e80dfcfdd5d919150aaa56e7b0b">http://europepmc.org/article/PMC/PMC6423025#europepmc-b1865e80dfcfdd5d919150aaa56e7b0b</a></small> 

The source code for *Text-annotator* is available on [Gitlab](https://gitlab.ebi.ac.uk/literature-services/public-projects/text-annotator). We welcome feedback and hope that you find it useful! Check out some of the other projects we've open-sourced at [GitLab](https://gitlab.ebi.ac.uk/literature-services/public-projects) and [Github](https://github.com/EuropePMC).

For more information, contact [helpdesk@europepmc.org](mailto:helpdesk@europepmc.org).

  [image1]: {{site.baseurl}}/images/posts/text-annotator-open-source/image1.png
  [image2]: {{site.baseurl}}/images/posts/text-annotator-open-source/image2.png
  [image3]: {{site.baseurl}}/images/posts/text-annotator-open-source/image3.png
  [image4]: {{site.baseurl}}/images/posts/text-annotator-open-source/image4.png
  [image5]: {{site.baseurl}}/images/posts/text-annotator-open-source/image5.png