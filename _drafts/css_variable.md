---
layout: article
title: "Using CSS Variables with Shiny"
excerpt: "How to change a CSS variable in a shiny app"
categories: blog
created: 2018-07-13
comments: false
share: false
ads: false
---

**Note - this method does not work with Internet Explorer**

CSS variables are a powerful way to make wholesale changes to the style throughout an entire document.  They are set using a custom notation `--variable_name` and accessed throughout the document using `var(--variable_name)`.  With a little javascript these variables can be used in Shiny apps and updated as needed.  The example below contains three files: a shiny app (app.R), the CSS styling (style.css) and the associated javascript functions which update the CSS variables (var\_change.css).  The CSS and javascript files are stored in the www folder.

### app.R

```r
library(shiny)

intial_size <- 20
intial_color <- 'orange'

server <- function(input, output, session) {
  
  session$sendCustomMessage("col_change", intial_color)
  session$sendCustomMessage("size_change", intial_size)
  
  observeEvent(input$but1, {
    session$sendCustomMessage("col_change", "green")
  })
  
  observe({
    session$sendCustomMessage("size_change", input$sld1)
  })
}

ui <- fluidPage(
  tags$head(
    tags$link(rel = "stylesheet", type = "text/css", href = "style.css"),
    tags$script(src="var_change.js")
  ),
  actionButton('but1', 'change color'),
  sliderInput('sld1', 'change size', value = 20, min = 1, max = 100, step = 1),
  h1("Heading 1"),
  h2("Heading 2"),
  h3("Heading 3")
)

shinyApp(ui, server)
```

### style.css
```css
:root {
  --heading-color: black;
  --heading-size: 12px;
}

h1 {
  color: var(--heading-color);
  font-size: var(--heading-size);
}

h2 {
  color: var(--heading-color);
}

h3 {
  color: var(--heading-color);
}
```

### var\_change.js
```javascript
Shiny.addCustomMessageHandler("col_change", col_change);
Shiny.addCustomMessageHandler("size_change", size_change);

function col_change(x) {
  document.documentElement.style.setProperty('--heading-color', x);
}

function size_change(x) {
  document.documentElement.style.setProperty('--heading-size', x + "px");
}
```