---
title: "Core Level Benchmarking"
teaching: TBD # teaching time in minutes
exercises: TBD # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do you find out if your code is making good use of a single core?
- What separates a "good enough" measurement from a misleading one?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain what core level performance benchmarks are
- Describe how to prepare a good core level benchmark case
- Calculate a core performance ratio and classify it

::::::::::::::::::::::::::::::::::::::::::::::::

When we look at the core level performance the first thing we investigate is measure how well our code utilize a single core. Recently, most of the hardwares designed for using vector instructions efficiently where data moves between memory and compute via fast cachechannels. However, whether our code takes advantage of them is entierly different question.

When you use high level performance analysis tools, it is common you will likely see vectorication ratios, memory utulizations and those kind of metrics which can not be a good starting point too look at. To prepare a good benchmark case, we therefore start with hig level numbers. For example, how close does our code get to the machine's peak performance? Despite the running any heavy profiling tools, these number will tell us whether our code compute bound or memory bound and how it is well utulize the microarcitechture of harware. 

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

This part is for running small examples on COSMA/Azimuth service for instructors.
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Can you do it?

What is the output of this command?

```r
paste("This", "new", "lesson", "looks", "good")
```

:::::::::::::::::::::::: solution 

## Output
 
```output
[1] "This new lesson looks good"
```

:::::::::::::::::::::::::::::::::


## Challenge 2: how do you nest solutions within challenge blocks?

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Figures

You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

::::::::::::::::::::::::::::::::::::::::::::::::


## Math

One of our episodes contains $\LaTeX$ equations when describing how to create
dynamic reports with {knitr}, so we now use mathjax to describe this:

`$\alpha = \dfrac{1}{(1 - \beta)^2}$` becomes: $\alpha = \dfrac{1}{(1 - \beta)^2}$

Cool, right?

::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
