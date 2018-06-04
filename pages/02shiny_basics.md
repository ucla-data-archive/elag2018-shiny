---
layout: page
title: DataViz and GGPLOT2 Basics
---

Widgets
-------

In it's current state, our application isn't particularly useful because it lumps data from multiple months and libraries together. In this lesson we'll add additional widgets to allow our application to filter the data and display the results for a specific library.

To accomplish this, we'll add a widget that allows a user to select a specific library. Our dataset actually contains data for approximately 90 libraries, but for convenience we'll limit choices to a predetermined list of ten libraries.

You can find the code chunk below in the project folder in the file library\_select\_list.R. Open that file then copy and paste the following code into your application immediately preceding the sliderInput function. Be sure to separate the two function calls with a comma.


    selectInput(inputId = "library", 
                label = "Choose a library:",
                choices =  c("Lancaster",
                           "Diamond Bar",
                           "Rowland Heights",
                           "West Covina",
                           "Angelo M. Iacoboni",
                           "La Crescenta",
                           "East Los Angeles",
                           "Hacienda Heights",
                           "Rosemead",
                           "West Hollywood"), 
                selected = "Lancaster")
                           

Before we use this new input to change the plot, let's add some code to tell the application to display in the main panel what we selected from the list. To do this, we need to add two more sections of code. First, we have to add something to the ui section to tell the application *where* to display the text. We'll do that by adding the following line to mainPanel.

    textOutput("selected_var")

Note that "selected\_var" isn't the literal text that will be printed. This is because the textOutput function uses this string as an identifer to content that will be created in the server function and assigned to the output object.

We'll add the next piece of code to the server function to *generate* the content for "selected\_var". You may paste it immediately after the closing parentheses on the renderPlot function in the server section. There should **not** be a comma separating the two function calls.

     output$selected_var <- renderText({ 
       paste("You have selected", input$library)
       })
       

Our code already contains another render function, renderPlot. This table provides a quick overview of all of the render functions in Shiny.

| Function        | Desscription                                        |
|-----------------|-----------------------------------------------------|
| renderPlot      | Plot Output                                         |
| renderText      | Text Output                                         |
| renderPrint     | Printable Output                                    |
| renderDataTable | Table output with the JavaScript library DataTables |
| renderImage     | Image file output                                   |
| renderTable     | Table Output                                        |

### Reactive expressions

Now when we run the application and make choices from the list, the text should change in the main panel. In this section, we'll use the selected value to actuall change the plot.

In order to filter our data in response to a user input, we need to use what's called a reactive expression. Reactive expressions are required when an application manipulates data in response to user inputs. In the earlier version of our application, we were modifying a parameter to the plot, namely bin numbers, and not the underlying data.

The following code demonstrates how we define and then use a reactive expression with a plot created by ggplot. There is some critical syntax in these expressions that will break your code if not used correctly, so let's spend a little time talking about them.

    libstats <- reactive({circstats %>% filter(`Library Name` == input$library)})
    output$distPlot <- renderPlot({
      ggplot(data=libstats(), aes(Circulation)) + geom_histogram(bins=input$bins)
    })

Now, modify your code and see if it works. You'll need to add the reactive expression and modify the appropriate parameters in ggplot.

#### Challenge:

Create a new app that plots the circulation data for one or more libraries over time. Refer to the line graph you created with ggplot in this morning's lesson and use the Shiny documentation to find a widget that allows you to make multiple selections.

> This lesson was derived from RStudio [Lesson 3: Add control widgets](https://shiny.rstudio.com/tutorial/written-tutorial/lesson3/)
