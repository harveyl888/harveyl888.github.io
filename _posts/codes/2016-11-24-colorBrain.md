---
layout: article
title: "colorBrain"
excerpt: "colorBrain R code"
categories: codes
created: 2016-11-24
modified: 2016-11-24
comments: false
share: false
ads: false
image: 
  teaser: code-images/colorBrain.png
---

colorBrain is a proof-of-concept code.  It arose from a conversation with a colleague at 5:00 pm on a Friday and was implemented within 2 hours.  The conversation went along the lines of "We generally represent biological data using barcharts with error bars but this is not always the best way to illustrate the information.  Is there a better way?"  I thought about this for a while and decided to write some code using R to map biological response using geomapping - afterall if we can represent our system by a segmented graphic, we can use a simple GIS (geographic information system) to display the data.  This was my first foray into geomapping.  
In the example on github dummy data were used to color-code parts of a brain.  The image was sketched with polygons using [qgis](http://www.qgis.org/en/site/) and saved as a shapefile.  The maptools package was used within R to project the data onto the image.  
The cool thing about this was that I could use R in conjunction with Shiny to create a working app quickly.  From initial conception of the idea to a working app took less than 2 hours.  I like to think of this as rapid prototyping for programming.  
[colorBrain](https://github.com/harveyl888/colorBrain)
