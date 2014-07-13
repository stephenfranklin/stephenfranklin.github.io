---
title       : rCharts Tutorial
subtitle    : 
author      : Stephen Franklin
job         : Modified notes from Brian Caffo, Jeffrey Leek  at the Johns Hopkins Bloomberg School of Public Health
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides

---



## Installing
You can install rCharts from github using the devtools package

```r
install.packages("devtools")
require(devtools)
install_github('rCharts', 'ramnathv')
```


### Also you'll need slidify as well as knitr:

```r
require(devtools)
install_github("slidify", "ramnathv")
install_github("slidifyLibraries", "ramnathv")
library(slidify)
```

`knitr` should already be installed in RStudio.

---

## Installing
- Create your slidify project and give your project a name:

```r
author("rCharts_tutorial")
```
- That will create the slidify directory structure within your working directory, and will create 'index.Rmd' which is the primary slidify document.

- Update the YAML heading in index.Rmd.
    - (See slidify_tutorial.Rmd.)

- Create a directory 'fig' in the working directory for the rCharts figures.

- Use `---` sandwiched between two newlines to separate the slides.

---

## Example 1
In this first example we make a plot:

- which is an rCharts function called `nplot`. 

- We assign it to `n1`, then save it as an html document.

- Finally, we `cat` it for embedding in `slidify`.

- To simply view the plot in Rstudio, run `nplot` without assigning it.

---

## Example 1

The knitr chunk header is:  
`{r ex1, echo = FALSE, eval=TRUE, results='asis', message=FALSE}`


```r
require(rCharts)
haireye = as.data.frame(HairEyeColor)
n1 <- nPlot(Freq ~ Hair, group = 'Eye', 
            type = 'multiBarChart',
            data = subset(haireye, Sex == 'Male')
            )
n1$save('fig/n1.html', cdn = TRUE)
cat('<iframe src="fig/n1.html" width=100%, height=600></iframe>')
```

---

## Example 1
- Notice that it's interactive!

<iframe src="fig/n1.html" width=100%, height=600></iframe>

---

## Viewing the plot
- The object `n1` contains the plot.
  - In RStudio, typing `n1` brings up the plot in the RStudio viewer (or you can just not assign it to an object)
- Do `n1$` then hit TAB to see the various functions contained in the object
  - `n1$html()` prints out the html for the plot
- Do `n1$save(filename)` then bring the code back into slidify document with `cat()`.
- Then you can open the html file in a browser!
  - This is recommended for slidify, but if you're just looking at the plot in RStudio, it's unnecessary.

- That first example uses the nvd3 javascript library.
- You may need to include something like this line in the YAML:  
`yaml ext_widgets : {rcharts: ["libraries/nvd3", "libraries /highcharts", "libraries/morris"]}`

---

## Example 2 - Faceted Scatterplot


```r
names(iris) = gsub("\\.", "", names(iris))
r1 <- rPlot(SepalLength ~ SepalWidth | Species, data = iris,
            color = 'Species', type = 'point')
r1$save('fig/r1.html', cdn = TRUE)
cat('<iframe src="fig/r1.html" width=100%, height=600></iframe>')
```

- The options for rCharts aren't well documented,
    - but there are many examples online.

---

## Example 2 - Faceted Scatterplot

<iframe src="fig/r1.html" width=100%, height=600></iframe>

---

## Example 3 - Faceted Barplot


```r
hair_eye = as.data.frame(HairEyeColor)
r2 <- rPlot(Freq ~ Hair | Eye, color = 'Eye', data = hair_eye, type = 'bar')
r2$save('fig/r2.html', cdn = TRUE)
cat('<iframe src="fig/r2.html" width=100%, height=600></iframe>')
```

---

## Example 3 - Faceted Barplot

<iframe src="fig/r2.html" width=100%, height=600></iframe>

---

## How to get the js/html or publish an rChart
Now you can add whatever you'd like

```r
install.packages("jsonlite")
r1 <- rPlot(mpg ~ wt | am + vs, data = mtcars, type = "point", color = "gear")
r1$print("chart1") # print out the js 
r1$save('myPlot.html') #save as html file
r1$publish('myPlot', host = 'gist') # save to gist, package `rjson` required
r1$publish('myPlot', host = 'rpubs') # save to rpubs
```

---
## rCharts has links to several libraries

Ramnath mentions that slidify style `io2012` and the `polychart` interface have conflicting js if you're embedding `rCharts` into `slidify`.

---

## morris
Another plotting package is called "morris"

```r
data(economics, package = "ggplot2")
econ <- transform(economics, date = as.character(date))
m1 <- mPlot(x = "date", y = c("psavert", "uempmed"), type = "Line", data = econ)
m1$set(pointSize = 0, lineWidth = 1)
m1$save('fig/m1.html', cdn = TRUE)
cat('<iframe src="fig/m1.html" width=100%, height=600></iframe>')
```

- With `morris` we can plot a time-series with multiple  variables.
    - Notice the two y variables.
- And the mouse-over shows the data for all variables at the given point.
- This chart uses package `ggplot2`.

---

## morris
Another plotting package is called "morris"
<iframe src="fig/m1.html" width=100%, height=600></iframe>

---

## xCharts

```r
require(reshape2)
uspexp <- melt(USPersonalExpenditure)
names(uspexp)[1:2] = c("category", "year")
x1 <- xPlot(value ~ year, group = "category", data = uspexp, type = "line-dotted")
x1$save('fig/x1.html', cdn = TRUE)
cat('<iframe src="fig/x1.html" width=100%, height=600></iframe>')
```

- This chart uses package `reshape2`.

---

## xCharts
<iframe src="fig/x1.html" width=100%, height=600></iframe>

---

## Leaflet
Leaflet is a mapping library

```r
map3 <- Leaflet$new()
map3$setView(c(51.505, -0.09), zoom = 13)
map3$marker(c(51.5, -0.09), bindPopup = "<p> Hi. I am a popup </p>")
map3$marker(c(51.495, -0.083), bindPopup = "<p> Hi. I am another popup </p>")
map3$save('fig/map3.html', cdn = TRUE)
cat('<iframe src="fig/map3.html" width=100%, height=600></iframe>')
map3
```

- You can zoom and move the map.
- You can provide popup markers.

---

## Leaflet
Leaflet is a mapping library.

<iframe src="fig/map3.html" width=100%, height=600></iframe>

```
## Error: object 'opts_current' not found
```

---

## Rickshaw
Rickshaw provides some interactivity to charts.

```r
usp = reshape2::melt(USPersonalExpenditure)
# get the decades into a date Rickshaw likes
usp$Var2 <- as.numeric(as.POSIXct(paste0(usp$Var2, "-01-01")))
p4 <- Rickshaw$new()
p4$layer(value ~ Var2, group = "Var1", data = usp, type = "area", width = 560)
# add a helpful slider this easily; other features TRUE as a default
p4$set(slider = TRUE)
p4$save('fig/p4.html', cdn = TRUE)
cat('<iframe src="fig/p4.html" width=100%, height=600></iframe>')
```

- You can select the variables shown.
- You can add a slider to adjust the timespan.

---

## Rickshaw

<iframe src="fig/p4.html" width=100%, height=600></iframe>

---

## highchart

```r
h1 <- hPlot(x = "Wr.Hnd", y = "NW.Hnd", data = MASS::survey, type = c("line", 
    "bubble", "scatter"), group = "Clap", size = "Age")
h1$save('fig/h1.html', cdn = TRUE)
cat('<iframe src="fig/h1.html" width=100%, height=600></iframe>')
```

- The size of the bubble can represent a variable (age).
- This plot uses the `survey` data from the `MASS` package.
    - `Wr.Hnd` is the size (span) of the writing hand.
    - `NW.Hnd` is the size of the non-writing hand.
    - Left, right, or neither refers to the hand that is on top after clapping.
- This particular example is ugly because it's displaying several aspects of the chart rather than displaying the data in a useful way.
- It has transparent overlays.

---

## highchart
<iframe src="fig/h1.html" width=100%, height=600></iframe>

---

## dTable
I don't know why this is here. It must mean *something*. I'll leave it for now.


```r
data(airquality)
dTable(airquality, sPaginationType = "full_numbers")
```

---

## rCharts summarized
- rCharts makes creating interactive javascript visualizations in R ridiculously easy
- However, non-trivial customization is going to require knowledge of javascript
- If what you want is not too big of a deviation from the rCharts examples, then it's awesome
  - Otherwise, it's challenging to extend without fairly deep knowledge of the JS
    libraries that it's calling.
- rCharts is under fairly rapid development
- Many stackexchange posts.
