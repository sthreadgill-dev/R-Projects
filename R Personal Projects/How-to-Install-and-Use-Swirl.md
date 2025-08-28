How to Install and Use Swirl
================

## What is Swirl?

Swirl is an interactive learning package available for R. As with R
itself, it is an open source package where others may create their own
courses to be made available to download via the package. You can learn
more about the history of R refer to his blog post by Jon Calder: [Why
swirl? \| R-bloggers](https://www.r-bloggers.com/2017/01/why-swirl/)

It is one of the only formats to learn more that take place in your IDE.
So not only do you get to learn different skills in R, you get to do it
in your local environment. It is a self paced learning package offering
beginner, intermediate, and advanced lessons. If you’d like to learn
more about the Swirl package and what lessons are available visit
[swirl: Learn R, in R.](https://swirlstats.com/)

## Getting started

First install the Swirl package

``` r
install.packages("swirl")
```

## Adding courses

After the package has been installed you can now download different
available courses:

``` r
#Install  Beginner Courses 
swirl::install_course("The R Programming Environment") 
swirl::install_course("R Programming") 

#Install Intermediate Courses 
swirl::install_course("Regression Models") 
swirl::install_course("Getting and Cleaning Data") 

#Install Advanced Courses 
swirl::install_course("Statistical Inference") 
swirl::install_course("Advanced R Programming")
```

## Additional Courses

Again because Swirl is open source new courses are often being added.
You can view a complete list with download instructions in the [Swirl
Course Network](https://swirlstats.com/scn/title.html),

## Taking a course

Once you have the course or courses you wish to take installed, jumping
into one is easy! Just load the package and run it. The instructions
that generate will guide you along the rest.

``` r
library(swirl)
swirl()
```
