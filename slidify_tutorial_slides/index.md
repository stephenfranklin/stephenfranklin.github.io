---
title       : "Slidify Tutorial Slides"
subtitle    : Data meets presentation
author      : Brian Caffo, Jeffrey Leek, Roger Peng 
job         : Johns Hopkins Bloomberg School of Public Health
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, quiz, bootstrap]
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## What is Slidify?

- Slidify was created by [Ramnath Vaidyanathan](https://github.com/ramnathv) in order to streamline the process of creating and publishing `R` driven presentations.

- Slidify is an almagamation of other technologies including knitr, Markdown, and several javascript libaries for HTML5 presentations.

- Slidify is infinitely extendable and customizable, yet it is easy to use!

- Slidify allows embedded code chunks and mathematical formulas which keeps your presentation reproducable.

- Slidify presentations are just HTML files, so you can view them with any web browser and share them easily on Github, Dropbox, or your own website.

---

## Getting Slidify

- Fire up RStudio! 
- First, make sure you have devtools installed and loaded

```r
install.packages("devtools")
library(devtools)
```

- Second, install Slidify

```r
install_github('slidify', 'ramnathv')
install_github('slidifyLibraries', 'ramnathv')
```

- Third, load Slidify

```r
library(slidify)
```

---

## Getting started with Slidify

- Set the working directory to where you want to create your Slidify project


```r
setwd("~/coursera/ds3_data_products/dp_week2/slidify_tutorial/")
```

- Create your project and give your project a name (My project is named "first_deck")

```r
author("first_deck")
```

---

## Getting started with Slidify

- `author("first_deck")` causes the following to happen:

1. A directory with the name of your project is created inside of your current directory.
2. Inside of this directory an assets directory and a file called "index.Rmd" is created.
3. The assets directory is populated with the following empty folders: css, img, js, and layouts.
4. The newly created `index.Rmd` R Markdown file will open up in RStudio.

- Any custom css, images, or javascript you want to use should respecively be put into the newly created css, img, and js folders.

---

## Getting to know `index.Rmd` : `YAML`

- `index.Rmd` is the R Markdown document which you will use to compose the conent of your presentation.
- The first part of an `index.Rmd` file is a bit of `YAML` (Yaml Ain't Markup Language) code which will look like this:

```YAML
---
title       : 
subtitle    : 
author      : 
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---
```

---

## Getting to know `index.Rmd` : `YAML`

- You can edit your `YAML` to include the title, subtitle, author, and job of the author, including what slide framework you wish to use, which code highlighter you wish to use, and any widgets you want to include.

- Other fields you can include in your `YAML`: a logo to appear in your title slide under `logo`, the path to your assets folder and the paths to any other folders you may be using under `url`, and the specific theme for your code highlighter of choice under `hitheme`.

```YAML
logo    : my_logo.png
url     :
    assets: ../assets
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : zenburn       # 
```

- Remember that `../` signifies the parent directory.

- The pound sign # denotes a comment.

---

## Getting to know `index.Rmd` : `YAML`

- The `YAML` for the presentation you're currently viewing looks like this:

```YAML
---
title       : Slidify
subtitle    : Data meets presentation
author      : Jeffrey Leek, Assistant Professor of Biostatistics 
job         : Johns Hopkins Bloomberg School of Public Health
logo        : bloomberg_shield.png
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
url:
  lib: ../../libraries
  assets: ../../assets
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---
```

---

## Getting to know `index.Rmd` : `YAML`

- framework : Chooses the framework to format the slides.
- highlighter : Highlights code depending on language.
- hitheme : There are various themes.
- widgets : 
    - mathjax : mathematical equation rendering;` $\LaTeX$.
    - quiz : makes automated quizzes
    - bootstrap : the twitter bootstrap style (which is a css style)
- mode : The selfcontained or standalone option packages all the libraries for presenting independent of the internet.

---

## Getting to know `index.Rmd` : Making Slides

Your first two slides are made for you under the `YAML`:
```Rmd
## Read-And-Delete

1. Edit YAML front matter
2. Write using R Markdown
3. Use an empty line followed by three dashes to separate slides!

- - - .class #id 

## Slide 2
```

---

## Getting to know `index.Rmd` : Making Slides
- Whatever you put after `##` will be the title of the slide.  
   - `##` is equivalent to html H1.
- `---` marks the end of the slide.
- `.class #id` are `CSS` attributes you can use to customize the slide.
- Whatever you put between `##` and `---` is up to you! As long as it is valid R Markdown or `HTML`.

---

## Getting to know `index.Rmd` : Making Slides

- To compile your presentation make sure the working directory contains your `index.Rmd` file and enter the following command:

```r
slidify("index.Rmd")
```

- An `HTML` flie should appear in your current directory, open it with your favorite web browser and enjoy your Slidify deck!

Or if you load library(knitr), you can view it with `browseURL()`:

```r
library(knitr)
browseURL("index.html")
```

---

## Publishing to Github

- First, log in to GitHub and [create](https://help.github.com/articles/creating-a-new-repository) a new empty repository.
- Use the following command, but replace `user` with your username and `repo` with the name of your new repository (both arguments are strings).

```r
publish_github(user, repo)
```


---

## `HTML5` Deck Frameworks

The following frameworks are compatible with Slidify for making your presentations:

- [io2012](https://code.google.com/p/io-2012-slides/)
- [html5slides](https://code.google.com/p/html5slides/)
- [deck.js](http://imakewebthings.com/deck.js/)
- [dzslides](http://paulrouget.com/dzslides/)
- [landslide](https://github.com/adamzap/landslide)
- [Slidy](http://www.w3.org/Talks/Tools/Slidy2/Overview.html#)

---

## Mathjax
- You can include $\LaTeX$ math formatting as follows
- Edit your YAML
```YAML
widgets     : [mathjax]
```
- Enter inline math code with  `$x^2$` $x^2$
- Enter centered code with  `$$\frac{-b \pm \sqrt{b^2 - 4 a c}}{2a}$$`
$$\frac{-b \pm \sqrt{b^2 - 4 a c}}{2a}$$


---

## HTML
- Just include html in the Rmd file and it will get kept as html when it's slidified
- Especially useful for stuff like images or tables where you need finer control of the html options
- Also, remember you can edit the final html slide
  - This isn't the best solution (since why do mostly slidify, a reproducible format if you're going to break that reproducibility at the last step?)
  - But, sometimes useful in a pinch (like if you're frantically preparing course slides at the last minute)
- Similarly, you can incorporate JS, or anything else you can do in a web page

---

## Adding interactive elements to slidify
- You can add interactive elements to slidify
  - Quiz questions
  - interactive Rcharts plots
  - Shiny apps
- Of course, you could do this directly with html/js
- More easily, the dev version of slidify has this built in
- See [http://slidify.github.io/dcmeetup/demos/interactive/](http://slidify.github.io/dcmeetup/demos/interactive/)
  - The following example was taken from there

---



## Rmd syntax 
First, make sure your YAML contains:  
widgets     : [mathjax, quiz]  # bootstrap <-- optionally.

\-\-\- &radio  
\#\# Question 1

What is 1 + 1?

1. 1
2. \_2\_
3. 3
4. 4

\*\*\* .hint
This is a hint

\*\*\* .explanation
This is an explanation

---

## Rmd syntax
That code is already in the first_deck example.
Again, you can then render it with:

```r
slidify("index.Rmd")
```
or
```r
browseURL("index.html")
```

---

## R Commands in Slidify using knitr
We can use knitr to make a slidify document and even use the knit HTML button to preview it.

- You need to have your YAML set correctly, 
    - knit        : slidify::knit2slides 
- and the directory structure in place. 
- So this tutorial should be index.Rmd and an author() used. 
    - See the slidify_tutorial_slides directory.

In that case, using slidify is exactly the same as using knitr.


```r
setwd("~/coursera/ds3_data_products/dp_week2/")
author("slidify_tutorial_slides")
```

---
## R Commands in Slidify using knitr

Then open that index.Rmd and paste in this Rmd into index.Rmd and hit 'knit HTML' from with index.Rmd.


```r
x <- rnorm(5)
x
```

```
## [1] 1.5793 0.3245 0.4121 0.4760 0.3091
```

```r
pnorm(x)
```

```
## [1] 0.9429 0.6272 0.6599 0.6830 0.6214
```

```r
mean(x)
```

```
## [1] 0.6202
```

