---
title: Challenges faced while creating this blog. 
author: Soubhik Rakshit
date: 2020-05-14 16:00:00 -0400
categories: [Tutorial]
tags: [jekyll]
sticky: true
---

> Its all fun and games until you try to compile a file with Unix style line endings in Linux.

**Some thoughts**

* Most of the time spent in getting this site up and running was in creating the [**Tags**](tabs/tags/) and [**Categories**](tabs/categories/) pages.
* The problem was with the extraction of `tags` and `categories`.
* This issue was hard to debug as certain `tags` and `categories` links were broken. After spending some embarrassingly large amount of time, I finally understood that this was due to compiling strings with Unix style line endings in Linux.
* One thing I learnt from this : `dos2unix` is of great help in fixing these errors.
* I will keep adding my experience of developing this site in this page.