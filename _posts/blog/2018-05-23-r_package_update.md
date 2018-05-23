---
layout: article
title: "R 3.5.0 Package Update"
excerpt: "Working with user and system libraries"
categories: blog
created: 2018-05-23
comments: false
share: false
ads: false
---

After our IT colleagues updated R to version 3.5.0 I found that I have many packages duplicated between the system library and my user library.  This short piece of code lists all packages with their version for all libraries.  It helps identify those that can be removed from the user library or updated.

```r
library(plyr)

df.all <- as.data.frame(installed.packages()[,c(1:4, 16)], stringsAsFactors = FALSE)
df.split <- split.data.frame(df.all, df.all$LibPath)
df.wide <- join_all(df.split, by = 'Package')
names(df.wide) <- c('Package', paste0(rep(c('libpath_', 'version_', 'priority_', 'built_'), length(df.split)), rep(seq(length(df.split)), each = 4)))

df.user <- df.wide[!is.na(df.wide$libpath_2),]

```