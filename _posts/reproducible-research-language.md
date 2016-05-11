---
title: Disseminating Reproducible Research is Fundamentally a Language and Communication Problem
author: roger
layout: post
---

Just about 10 years ago, I wrote the [first](http://www.ncbi.nlm.nih.gov/pubmed/16510544) of many articles about the importance of reproducible research. Since that article, one of the points I've tried to make is that they key issue to resolve was one of tools and infrastructure. The point being that, at the time, it was difficult to answer the question "What should I do if I desperately want to make my work reproducible?" Back then, even if you could convince a clinical researcher to use R and LaTeX to create a [Sweave](https://en.wikipedia.org/wiki/Sweave) document (!), it was not immediately obvious where they should host the document, code, and data files.

Much has happened since then. We now have knitr and Markdown for live documents (as well as iPython notebooks and the like). We also have GitHub and the like, which provide free code sharing repositories. With the recent announcement of the [Journal of Open Source Software](http://www.arfon.org/announcing-the-journal-of-open-source-software), posting code on GitHub can now be recognized within the current system of credits and incentives. Finally, the number of data repositories has grown providing more places for researchers to deposit their files (if it's not appropriate for GitHub). 

So, is the tools and infrastructure problem solved? I'd say yes. One thing that has become clear is that disseminating reproducible research is **no longer a software problem**. At least in R land, building live documents that can be executed by others is straightforward and not too difficult to pick up. For other languages there many equivalent (if not better) tools for writing documents that mix code and text. For this kind of thing, there's just no excuse anymore. Could things be optimized a bit for some edge cases? Sure, but the tools are prefectly fine for the vast majority of use cases. 

But now there is a bigger problem that needs to be solved, which is that **we do not have an effective way to communicate data analyses**. One might think that publishing the full code and datasets is the perfect way to communicate a data analysis, but in a way, it is too perfect. That approach can  provide too much information. I find the following analogy useful for discussing this problem.

