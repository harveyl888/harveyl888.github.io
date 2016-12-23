---
layout: article
title: "R-Notebooks Collapse Button"
excerpt: "Adding an open/collapse button to an R Notebook"
categories: blog
created: 2016-12-20
comments: false
share: false
ads: false
---

I've taken to using R Notebooks for many of the tasks that I used to write in R Markdown.  Advantages are that code chunks can be executed independently, leading to easier management and debugging, and that the output is still a usable document.  
There are times, however, when I would like to include a large table or multiple plots but don't want them to take up too much of the output document.  For tables this can easily be accomplished using a datatable but for more complex tables or multiple plots placing them in a collapsible div attached to a button works well.  In the code chunk below, formattable is used to format the iris dataset.

```r
library(htmltools)
library(formattable)
HTML('<div class="row">
        <div class="col-md-12">
          <button type="button" class="btn btn-warning btn-sm code-folding-btn" data-toggle="collapse" data-target="#table_iris" aria-expanded="false">
            <span>Iris Data</span>
          </button>
        </div>
      </div>
<div id="table_iris" class="collapse">')
as.htmlwidget(formattable(iris,
                          list(Sepal.Length = color_tile("white", "lightpink"),
                          Sepal.Width = color_tile("white", "lightgreen"),
                          Petal.Length = color_tile("white", "lightpink"),
                          Petal.Width = color_tile("white", "lightgreen"))), 
                          width = '30%')
HTML('</div>')
```

![R Notebook collapsible](/images/post-images/r-notebook-collapse.png){:class="img-responsive"}