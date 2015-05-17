---
title       : BMI Calculator
subtitle    : Shiny Application
author      : azhubryd
job         : Coursera student
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction


 - Body Mass Index (BMI) is a value derived from the mass (weight) and height of an individual.
 
 - The index was devised by Adolphe Quetelet from 1830 to 1850 during which time he developed what he called "social physics".
 
$$latex 
\mathrm{BMI = \frac{mass_{kg}}{height_{m}^{2}} = \frac{mass_{lbs}}{height_{in}^{2}}\times 703} 
$$

## Input

Application requires the next inputs from the user:

 - Measurement system: Imperial or metric
 
 - Mass of a person: `kg` in metric, `lbs` in imperial
 
 - Height of a person: `m` in metric, `'` and/or `"` in imperial

---

## Transformation of inputs

In case of imperial units of height, application accepts different kinds of inputs and tries to transform it, remove errors

Examples of inputs: 5'6", 5' 6", 5' 6 '', 6', 30'', 30 ".



Special funtion <code>meters()</code> gets a height in imperial units as a string and outputs the height in meters.


```r
examples <- c('5\'6"', "5' 6\"", "5' 6''", "6'", "30''", '30 "')
round(sapply(X = examples, FUN = meters, simplify = TRUE),digits = 2)
```

```
##   5'6"  5' 6" 5' 6''     6'   30''   30 " 
##   1.68   1.68   1.68   1.83   0.76   0.76
```

---

## Outputs

 - Calculated BMI:

```r
height <- examples[1]
weight <- 80

BMI <- weight / (meters(height))^2
round(BMI, digits = 2)
```

```
## [1] 28.47
```

---

## Outputs

 - Calculate to which category individual belongs:


```r
categoryBMI(BMI)
```

```
## [1] "overweight"
```

 - Calculate a range of recommended weight for given height:


```r
paste0('Recommended weight for your height is in the range of [',
        paste(round(c(18.5, 25) * meters(height)^2, digits = 1)
              ,collapse = ', '), 
       '] kg.')
```

```
## [1] "Recommended weight for your height is in the range of [52, 70.3] kg."
```
