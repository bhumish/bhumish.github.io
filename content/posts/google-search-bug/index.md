---
title: "A weird Google-search bug"
date: 2013-02-13
draft: false
tags: ["google", "search", "bug", "algorithm", "search-engine", "quora"]
categories: ["technology", "bugs", "search-engines"]
description: "Analysis of a peculiar Google search bug that returns inappropriate results for contradictory search queries, discovered through Quora discussions"
---

Last month, it was asked on quora –

> What does `[-4^(1/4)"]` mean and why is it connected to porn?

Still today, if you search for that equation on Google, it returns results with xxx titles. Some more contradictory search equations which return same type of results are

```
"1 2" -1
"1 2" -2
```

The explanation of the equation `-4^(1/4)"` is given as – we are asking Google to return pages containing a 1 next to a 4, but which do not contain a 4.

A Google engineer related with the search quality, justifies that this should return zero results, because it is impossible to satisfy both requirements. However, we have uncovered a bug that causes some web pages to "match" these contradictory queries. Since these are the only results that "match" the query, they are the results that get shown.

Its really a bizarre bug in the Google search, which needs to be fixed soon. Though its not affecting many of its users, it is benefiting the porn websites in getting higher ranks.