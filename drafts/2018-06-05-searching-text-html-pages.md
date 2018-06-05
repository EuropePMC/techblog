---
layout: post
title:  "Locating plain text in HTML pages"
date:   2018-06-05
author: francesco
category: documentation
---

[SciLite][1] is a Europe PMC tool that allows biological terms or relations, such as diseases, chemicals or protein interactions, to be highlighted for readers on abstracts and full text articles . These annotations are identified by text mining algorithms, developed by a variety of text mining groups.

The main challenge for Scilite tool is locating plain text annotations in HTML pages. The challenges derive from the nature of HTML pages. Below is a list of the major challenges we faced and the solutions adopted to mitigate them.


 
 
 
 
 
 
 
  [1]: https://europepmc.org/Annotations
  [2]: http://fusejs.io/
  [3]: https://en.wikipedia.org/wiki/Levenshtein_distance
  [4]: https://github.com/Tessmore/sbd
  [image_PMC1215513]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_PMC1215513.png
  [image_MED28385055]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_MED28385055.png
  [image_AGRIND605699789]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_AGRIND605699789.png
  [image_PMC3558359]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_fuzzy_match_PMC3558359.png