---
layout: post
title:  "Locating plain text in HTML pages"
date:   2018-06-05
author: francesco
category: documentation
---

[SciLite][1] is a Europe PMC tool that allows biological terms or relations, such as diseases, chemicals or protein interactions, to be highlighted for readers on abstracts and full text articles . These annotations are identified by text mining algorithms, developed by a variety of text mining groups.

The main challenge for Scilite tool is locating plain text annotations in HTML pages. The challenges derive from the nature of HTML pages. Below is a list of the major challenges we faced and the solutions adopted to mitigate them.

 1. **The pages contain HTML tags obviously.** Consider the page https://europepmc.org/articles/PMC1215513 and click on the Gene Function checkbox on the right hand side of the page to see the sentence highlighted. 
***Figure 1**: Annotation containing HTML tags*  
The problem is caused by the sub tag that it is surrounding the v inside the world Nav1.7. Therefore if you search for an exact match of the plain sentence into the HTML page, that will not be found. The solution adopted was to search for a regular expression built including an optional HTML tag between any two characters of the annotation text. The disadvantage of this approach is that this type of search is much more demanding from a computational point of view than an exact match search. Therefore, we decided to adopt this regular expression search only for sentence-based annotations where the chance of having HTML tags is much higher than named entity annotations composed usually only by one or two words.
 
 
 
 
 
 
 
  [1]: https://europepmc.org/Annotations
  [2]: http://fusejs.io/
  [3]: https://en.wikipedia.org/wiki/Levenshtein_distance
  [4]: https://github.com/Tessmore/sbd
  [image_PMC1215513]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_PMC1215513.png
  [image_MED28385055]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_MED28385055.png
  [image_AGRIND605699789]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_AGRIND605699789.png
  [image_PMC3558359]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_fuzzy_match_PMC3558359.png