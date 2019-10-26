present
========================================================
author: Mukesh kumar
date:   24/10/19
autosize: true

First Slide
========================================================

Introduction

The Mtcars Plotter is an plotting tool for an exploratory data analysis of the mtcars data set in R. It allows you display diffrent dimensions of the dataset and plot it agains an axis of choice. Furthermore you can display a smoother and facet the rows and columns.

The Mtcars Dataset

The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973 -74 models).

A data frame with 32 observations on 11 (numeric) variables.

    mpg Miles/(US) gallon
    cyl Number of cylinders
    disp Displacement (cu.in.)

UI Slide With Code
========================================================


```r
library(shiny)
library(ggplot2)
dataset <- mtcars
shinyUI(pageWithSidebar(
    headerPanel("Mtcars Plotter"),
    sidebarPanel(
        sliderInput('sampleSize', 'Sample Size', min=10, max=nrow(dataset), value=min(10, nrow(dataset)), step=5, round=0),
        selectInput('x', 'X', names(dataset)), selectInput('y', 'Y', names(dataset), names(dataset)[[2]]),
        selectInput('color', 'Color', c('None', names(dataset))),
        checkboxInput('jitter', 'Jitter'),
        checkboxInput('smooth', 'Smooth'),
        selectInput('facet_row', 'Facet Row', c(None='.', names(dataset))),
        selectInput('facet_col', 'Facet Column', c(None='.', names(dataset))) ),
    mainPanel(
        plotOutput('plot')
        )
    )
)
```

<!--html_preserve--><div class="container-fluid">
<div class="row">
<div class="col-sm-12">
<h1>Mtcars Plotter</h1>
</div>
</div>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label class="control-label" for="sampleSize">Sample Size</label>
<input class="js-range-slider" id="sampleSize" data-min="10" data-max="32" data-from="10" data-step="5" data-grid="true" data-grid-num="4.4" data-grid-snap="false" data-prettify-separator="," data-prettify-enabled="true" data-keyboard="true" data-data-type="number"/>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="x">X</label>
<div>
<select id="x"><option value="mpg" selected>mpg</option>
<option value="cyl">cyl</option>
<option value="disp">disp</option>
<option value="hp">hp</option>
<option value="drat">drat</option>
<option value="wt">wt</option>
<option value="qsec">qsec</option>
<option value="vs">vs</option>
<option value="am">am</option>
<option value="gear">gear</option>
<option value="carb">carb</option></select>
<script type="application/json" data-for="x" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="y">Y</label>
<div>
<select id="y"><option value="mpg">mpg</option>
<option value="cyl" selected>cyl</option>
<option value="disp">disp</option>
<option value="hp">hp</option>
<option value="drat">drat</option>
<option value="wt">wt</option>
<option value="qsec">qsec</option>
<option value="vs">vs</option>
<option value="am">am</option>
<option value="gear">gear</option>
<option value="carb">carb</option></select>
<script type="application/json" data-for="y" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="color">Color</label>
<div>
<select id="color"><option value="None" selected>None</option>
<option value="mpg">mpg</option>
<option value="cyl">cyl</option>
<option value="disp">disp</option>
<option value="hp">hp</option>
<option value="drat">drat</option>
<option value="wt">wt</option>
<option value="qsec">qsec</option>
<option value="vs">vs</option>
<option value="am">am</option>
<option value="gear">gear</option>
<option value="carb">carb</option></select>
<script type="application/json" data-for="color" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="jitter" type="checkbox"/>
<span>Jitter</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<div class="checkbox">
<label>
<input id="smooth" type="checkbox"/>
<span>Smooth</span>
</label>
</div>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="facet_row">Facet Row</label>
<div>
<select id="facet_row"><option value="." selected>None</option>
<option value="mpg">mpg</option>
<option value="cyl">cyl</option>
<option value="disp">disp</option>
<option value="hp">hp</option>
<option value="drat">drat</option>
<option value="wt">wt</option>
<option value="qsec">qsec</option>
<option value="vs">vs</option>
<option value="am">am</option>
<option value="gear">gear</option>
<option value="carb">carb</option></select>
<script type="application/json" data-for="facet_row" data-nonempty="">{}</script>
</div>
</div>
<div class="form-group shiny-input-container">
<label class="control-label" for="facet_col">Facet Column</label>
<div>
<select id="facet_col"><option value="." selected>None</option>
<option value="mpg">mpg</option>
<option value="cyl">cyl</option>
<option value="disp">disp</option>
<option value="hp">hp</option>
<option value="drat">drat</option>
<option value="wt">wt</option>
<option value="qsec">qsec</option>
<option value="vs">vs</option>
<option value="am">am</option>
<option value="gear">gear</option>
<option value="carb">carb</option></select>
<script type="application/json" data-for="facet_col" data-nonempty="">{}</script>
</div>
</div>
</form>
</div>
<div class="col-sm-8">
<div id="plot" class="shiny-plot-output" style="width: 100% ; height: 400px"></div>
</div>
</div>
</div><!--/html_preserve-->

Server Slide With Code
========================================================




```
Error in parse(text = x, srcfile = src) : 
  <text>:23:0: unexpected end of input
21:     }
22: 
   ^
```
