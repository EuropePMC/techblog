---
layout: post
title:  "Europe PMC project for eLife Innovation Sprint"
date:   2019-08-20
author: maria
category: literature_data_integration
summary: Europe PMC will participate in the 2019 eLife Innovation Sprint with a proposal to improve the discoverability of relevant scientific preprints.
---

## How to find the perfect preprint

The [eLife Innovation Sprint](https://sprint.elifesciences.org/) is a yearly collaborative hackathon for developers, designers, researchers, technologists, science communicators, and everyone enthusiastic about open science. The premise of the Sprint is simple &ndash; the current science publishing system is slow, inefficient and insanely expensive. What we need are open science ideas that could be turned into prototypes to address the challenges we face in science publishing. All Sprint outputs have to be openly available, use open-source licenses for code and software, and permissive licenses (such as CC-BY) for other content.

This year the Europe PMC team will participate in the Sprint with a proposal to improve the discoverability of relevant scientific preprints. [Dayane Araujo](https://www.ebi.ac.uk/about/people/dayane-rodrigues-araujo) (Technical Outreach Officer) and [Michael Parkin](https://www.ebi.ac.uk/about/people/michael-parkin) (Data Scientist) will be working on a tool to sort through ~80,000 life science preprints, and they need your help.

<!--more-->

## Project idea

Considering how the acceptance of preprints in the biomedical field has increased, how do researchers come across relevant preprints when looking for what is new in their scientific field? Preprints rarely have associated keywords to make filtering easier. The majority of preprints lack full-text available for deep indexing. Since preprints appear hot-off-the-press, they often don’t accumulate many citations, and are not associated with journal impact factors, commonly used as a proxy for scientific quality. This makes it harder to decide what preprint to read next. 

What if there was a tool to find and sort preprints by topic? The tool could visualise which preprints have been commented on, most read, and/or most downloaded, to help with the selection process. Such a tool would help improve preprint discoverability. 

[Europe PMC](https://europepmc.org/), a database of research literature, indexes preprints from multiple sources, in addition to traditional journal publications. We will use the [Europe PMC Annotations API](https://europepmc.org/AnnotationsApi) to retrieve text-mined biological concepts from preprint abstracts, sorting preprints into categories. We will track preprint reviews linked to preprints in Europe PMC. Additionally, we will use Crossref and other sources to retrieve comments, number of downloads, social media mentions, and other associated metrics.
Our resulting open source package will help select preprints by topic, and display comments, recommendations, and associated preprint metrics. This package could be re-used by preprint servers to provide topic streams, by preprint journal clubs and recommendation platforms to select content for review, and by researchers to simplify preprint discovery process. 

## How can you help

This project will benefit from team members with experience using REST APIs, particularly Crossref event data service. It will be essential to get user insights from those reading, posting and commenting on preprints, as well as those selecting preprints for journal clubs. 

If you would like to help us take preprints to the next level, [please get in touch with Dayane](mailto:dayane@ebi.ac.uk).  And for all participants at the eLife Innovation Sprint 2019 interested in preprinting &ndash; we look forward to working together!
 
