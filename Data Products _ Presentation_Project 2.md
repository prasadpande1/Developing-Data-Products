Data Products - Unit Converter
========================================================
author: Prasad Pande
date: 23rd Nov 2018
autosize: true

Shiny Application Details
========================================================

- Shiny app is created to convert Weight, length and temperature between Imperial and Metric system
- User needs to enter weight, length and temperature
- User then needs to select the appropriate unit to which above values needs to be converted

Shiny application widgets used
========================================================

- numericInput to capture the details of weight, length and temperature
- selectInput function is used to ask user about the unit to be converted
- Based on the User input the units are converted

Slide With UI Code
========================================================


```r
library(shiny)

# Define UI for application that converts
shinyUI(fluidPage(
  
  # Application title
  titlePanel("Metrics to Imperial converter"),
  
  # Sidebar with a slider input for number of bins 
  sidebarLayout(
    sidebarPanel(
       numericInput("Weight", "Weight:", 10),
       numericInput("Length", "Length:", 10),
       numericInput("Temperature", "Temperature:", 10),
       selectInput("Convert", "Convert to:", choices = c("Metric", "Imperial"))
       
           ),
    
    # Show a plot of the generated distribution
    mainPanel(
       #plotOutput("distPlot")
       h3(textOutput("Converted Weight")),
       h3(textOutput("Converted Length")),
       h3(textOutput("Converted Temperature"))    )
  )
))
```

<!--html_preserve--><div class="container-fluid">
<h2>Metrics to Imperial converter</h2>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label for="Weight">Weight:</label>
<input id="Weight" type="number" class="form-control" value="10"/>
</div>
<div class="form-group shiny-input-container">
<label for="Length">Length:</label>
<input id="Length" type="number" class="form-control" value="10"/>
</div>
<div class="form-group shiny-input-container">
<label for="Temperature">Temperature:</label>
<input id="Temperature" type="number" class="form-control" value="10"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="Convert">Convert to:</label>
<div>
<select id="Convert"><option value="Metric" selected>Metric</option>
<option value="Imperial">Imperial</option></select>
<script type="application/json" data-for="Convert" data-nonempty="">{}</script>
</div>
</div>
</form>
</div>
<div class="col-sm-8">
<h3>
<div id="Converted Weight" class="shiny-text-output"></div>
</h3>
<h3>
<div id="Converted Length" class="shiny-text-output"></div>
</h3>
<h3>
<div id="Converted Temperature" class="shiny-text-output"></div>
</h3>
</div>
</div>
</div><!--/html_preserve-->

Slide With Server Code
========================================================


```r
library(shiny)
# Define server logic required to convert units
shinyServer(function(input, output) {
   
  output$`Converted Weight` <- renderText({
    
    # Convert weight based on the selection
    if(input$Convert == "Metric")
        paste("Converted weight in kilograms::",input$Weight*0.453)
    else 
      paste("Converted weight in pounds::",input$Weight/0.453)
    
  })
  output$`Converted Length` <- renderText({
    
    # Convert length based on the selection
    if(input$Convert == "Metric")
      paste("Converted length in meters::",input$Length*0.0254)
    else 
      paste("Converted length in inches::",input$Length/0.0254)
    
  })
  output$`Converted Temperature` <- renderText({
    
    # Convert temperature based on the selection
    if(input$Convert == "Metric")
      paste("Converted temperature in celcius::", 5/9*(input$Temperature-32))
    else 
     paste("Converted temperature in farenhiet::",9/5*(input$Temperature+32))
           
  })

})
```
