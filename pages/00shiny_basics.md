---
layout: page
title: Interactive DataViz
---

Getting Started
---------------

If you haven't done it yet, install Shiny.

``` r
install.packages("shiny")
```

To load our first Shiny application, use the file tab in RStudio to navigate to the folder named LA\_circulation and open the file app-1.R. Here's a listing of the code:

``` r
library(shiny)

# Define UI for app that draws a histogram ----
ui <- fluidPage(

  # App title ----
  titlePanel("Hello Shiny!"),

  # Sidebar layout with input and output definitions ----
  sidebarLayout(

    # Sidebar panel for inputs ----
    sidebarPanel(

      # Input: Slider for the number of bins ----
      sliderInput(inputId = "bins",
                  label = "Number of bins:",
                  min = 1,
                  max = 50,
                  value = 30)

    ),

    # Main panel for displaying outputs ----
    mainPanel(

      # Output: Histogram ----
      plotOutput(outputId = "distPlot")

    )
  )
)


# Define server logic required to draw a histogram ----
server <- function(input, output) {

  # Histogram of the number monthly circulations at Los Angeles libraries
  # over a 24 month period
  # with requested number of bins
  # This expression that generates a histogram is wrapped in a call
  # to renderPlot to indicate that:
  #
  # 1. It is "reactive" and therefore should be automatically
  #    re-executed when inputs (input$bins) change
  # 2. Its output type is a plot
  output$distPlot <- renderPlot({

    x    <- faithful$waiting
    bins <- seq(min(x), max(x), length.out = input$bins + 1)

    hist(x, breaks = bins, col = "#75AADB", border = "white",
         xlab = "Waiting time to next eruption (in mins)",
         main = "Histogram of waiting times")

    })

}
# Run the application 
shinyApp(ui = ui, server = server)
```

\#Structure of a Shiny application
----------------------------------

-   in the subsequent lessons we'll use the same data, but add widgets and formatting to build a more useful and informative application

Lesson 1

> This lesson was derived from RStudio [Lesson 1: Welcome to Shiny](https://shiny.rstudio.com/tutorial/written-tutorial/lesson1/)
