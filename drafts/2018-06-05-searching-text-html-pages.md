---
layout: post
title:  "Locating plain text in HTML pages"
date:   2018-06-05
author: francesco
category: algorithm
---

[SciLite][1] is a Europe PMC tool that allows biological terms or relations, such as diseases, chemicals or protein interactions, to be highlighted for readers on abstracts and full text articles . These annotations are identified by text mining algorithms, developed by a variety of text mining groups.

The main challenge for Scilite tool is locating plain text annotations in HTML pages. The challenges derive from the nature of HTML pages. Below is a list of the major challenges we faced and the solutions adopted to mitigate them.

 1. **The pages contain HTML tags obviously.** Consider the page https://europepmc.org/articles/PMC1215513 and click on the "Gene Function" checkbox on the right hand side of the page to see the sentence highlighted. 
 [![Annotation containing HTML tags][image_PMC1215513]][image_PMC1215513]
***Figure 1**: Annotation containing HTML tags*  
The problem is caused by the sub tag that it is surrounding the v inside the world Nav1.7. Therefore if you search for an exact match of the plain sentence into the HTML page, that will not be found. The solution adopted was to search for a regular expression built including an optional HTML tag between any two characters of the annotation text. The disadvantage of this approach is that this type of search is much more demanding from a computational point of view than an exact match search. Therefore, we decided to adopt this regular expression search only for sentence-based annotations where the chance of having HTML tags is much higher than named entity annotations composed usually only by one or two words.
 
 2. **HTML encodes some special characters.** An example is the character >: it is encoded as &gt; inside the HTML page. Consider the page http://europepmc.org//abstract/MED/28385055 and click on the "Gene Disease Open Targets" checkbox. 
 [![Annotation containing HTML encoded characters][image_MED28385055]][image_MED28385055]
***Figure 2**: Annotation containing HTML encoded characters*   
The text of the annotation contains the character >. The solution adopted was to encode the annotation text as it would appear in an HTML page and then perform an exact match search.
 
 3. **There is a lack of correspondence between the text of the annotation and text inside the HTML page.** Consider the page http://europepmc.org/articles/PMC3558359 and click on the "Gene Function" checkbox.
 [![Annotation containing Greek characters][image_PMC3558359]][image_PMC3558359]
***Figure 3**: Annotation containing Greek characters* 
The original annotation text is "Our results revealed a direct interaction between PRL-3 and integrin beta1 and characterized Y783 of integrin beta1 as a bona fide substrate of PRL-3, which is negatively regulated by integrin alfa1." The problem is that the Greek letters alfa and beta are represented in two different ways in the page and in the annotation text. A solution to this problem is applying a fuzzy match approach that is discussed later.
 
## Fuzzy Match Strategy ##
 
 The fuzzy match approach we used to solve some of the problems described above is based on the open source Javascript library [Fuse.js][2] . Internally it uses the [Levenshtein distance][3] to compute the similarity score between two strings. This score is computed as the minimum number of single-character edits (insertions, deletions or substitutions) required to change one word into the other
 

## Conclusions ##

Searching plain text in HTML pages presents many challenges due to the nature of HTML rendering (tags, encoding, mismatch characters). An approach to solve them is to introduce techniques to apply some sort of fuzzy matching. However, those techniques can be demanding from performance point of view especially if the HTML pages are long and the number of annotations to locate is big. Therefore, it is necessary to carefully balance accuracy of results and performance deciding when it is  appropriate to apply those strategies.


  [1]: https://europepmc.org/Annotations
  [2]: http://fusejs.io/
  [3]: https://en.wikipedia.org/wiki/Levenshtein_distance
  [4]: https://github.com/Tessmore/sbd
  [image_PMC1215513]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_PMC1215513.png
  [image_MED28385055]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_MED28385055.png
  [image_AGRIND605699789]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_AGRIND605699789.png
  [image_PMC3558359]: {{ site.baseurl }}/images/posts/locating-text-html-pages/fuzzy_match_PMC3558359.png
