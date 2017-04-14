---
layout: article
title: "goalTracker"
excerpt: "Keep track of goals"
categories: codes
created: 2017-04-13
modified: 2017-04-13
comments: false
share: false
ads: false
image: 
  teaser: code-images/goalTracker.png
---

goalTracker is an R-based shiny app and flexdashboard which allows easy tracking and updating of goals.  The goal tracking structure is defined by a series of main goals, each of which can contain a number of subgoals. The subgoals can be timebound, in which a start and end date are required, or not. They can also be tagged as *new* or *priority* and have an associated percent completed.  Data can be stored in a local sqlite or external mysql database.  

I use this to track my work-related goals via RStudio Connect. Both the shiny app and flexdashboard markdown reside on RStudio Connect and connect to a database residing on an external server.  Working in this way, I can run a daily update of the flexdashboard to display any progress or changes made to the goals - it becomes almost realtime tracking. 

Code can be found at [goalTracker](https://github.com/harveyl888/goalTracker)
