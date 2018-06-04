---
layout: page
title: DataViz and GGPLOT2 Basics
---

User interface
--------------

Our circulation statistics application needs a user interface. One of Shiny's strengths is the way in which it handles basic page layout for you without requiring you to write html and css. Let's take a look at our application with all but the basic Shiny structure stripped out.

    library(shiny)

    # Define UI ----
    ui <- fluidPage(
      
    )

    # Define server logic ----
    server <- function(input, output) {
      
    }

    # Run the app ----
    shinyApp(ui = ui, server = server)

As you'd expect, the code in the ui section is what controls the layout of the user interface. The fluidPage function in Shiny builds a web page that automatically resizes to your browser window dimensions. To build a user interface, we add code elements as a comma-separated list of parameters passed to the fluidPage function. These code elements can be text items, formatting functions, or widget functions. Basically what these functions do is write the html and javascript that display information or accept input from the user. Lets look at our ui code again to see what this means and then make some modifications.

    # Define UI for application that draws a histogram
    ui <- fluidPage(
       
       # Application title
       titlePanel("Los Angeles Library Monthly Circulation Data"),
       
       # Sidebar with a slider input for number of bins 
       sidebarLayout(
          sidebarPanel(
             sliderInput("bins",
                         "Number of bins:",
                         min = 1,
                         max = 50,
                         value = 30)
          ),
          
          # Show a plot of the generated distribution
          mainPanel(
             plotOutput("distPlot")
          )
       )
    )

In our interface, there are seven function calls. Can you find them?

The function call sliderInput is one of many widget functions available in Shiny. We'll explore more of these in the next lesson. For now, let's just concern ourselves with how to add text elements to the existing panels. To see how this works, we'll add some placeholder text to the sidebarPanel and mainPanel sections. Examine the code below, then add the same modifications to your application.

       # Sidebar with a slider input for number of bins 
       sidebarLayout(
          sidebarPanel(
             "This is a a side bar panel",
             sliderInput("bins",
                         "Number of bins:",
                         min = 1,
                         max = 50,
                         value = 30)
          ),
          
          # Show a plot of the generated distribution
          mainPanel(
             "This is a main panel",
             plotOutput("distPlot")
          )

### Text formating

Be sure to include the comma after the quoted text and you can add as many comma-separated elements as you need. Generally, you'll want to format the code with html and Shiny allows you to do this in two ways. The cleanest way is to use one of the functions below that share the same name as their equivalent html tag. For example if you wanted to format the words "This is a a side bar panel" in a bold font, you write it like this: `strong("This is a a side bar panel")`.

| Function | Tag        | Description                                      |
|----------|------------|--------------------------------------------------|
| p        | `<p>`      | A paragraph of text                              |
| h1       | `<h1>`     | A first level header                             |
| h2       | `<h2>`     | A second level header                            |
| h3       | `<h3>`     | A third level header                             |
| h4       | `<h4>`     | A fourth level header                            |
| h5       | `<h5>`     | A fifth level header                             |
| h6       | `<h6>`     | A sixth level header                             |
| a        | `<a>`      | A hyper link                                     |
| br       | `<br>`     | A line break (e.g. a blank line)                 |
| div      | `<div>`    | A division of text with a uniform style          |
| span     | `<span>`   | An in-line division of text with a uniform style |
| pre      | `<pre>`    | Text ‘as is’ in a fixed width font               |
| code     | `<code>`   | A formatted block of code                        |
| img      | `<img>`    | An image                                         |
| strong   | `<strong>` | Bold text                                        |
| em       | `<em>`     | Italicized text                                  |
| HTML     |            | Directly passes a character string as HTML code  |

I also mentioned second way of adding formatting and that's done by wrapping a string of valid html in the HTML() function. In other words, `strong("This is a a side bar panel")` could also be written as `HTML("<strong>This is a a side bar panel</strong")`. This makes it possible to do more complex html formatting when needed. To practice these methods, add h1 tags to the text we added to the sidebar and main panels using the h1() function in one and the HTML() function in the other.

### Images

Images can be added to panels as well. In the examples folder, you'll find a file called rstudio.png. In order to use this in you application, you will need to copy it to a folder called www in your application folder. Create the folder, copy the file and then add the following as the last element in your mainPanel:

`img(src = "rstudio.png", height = 140, width = 400)`

> This lesson was derived from RStudio [Lesson 2: Build a user interface](https://shiny.rstudio.com/tutorial/written-tutorial/lesson2/)
