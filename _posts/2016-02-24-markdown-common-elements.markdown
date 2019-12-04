---
title: "chronic kidney disease"
layout: post
date: 2019-12-05 
image: /assets/images/markdown.jpg
headerImage: false
tag:
- markdown
- elements
star: true
category: blog
author: johndoe
description: Markdown summary with different options
---

## Basic formatting

This note **demonstrates** some of what [Markdown][1] is *capable of doing*.

And that's how to do it.

{% highlight html %}
This note **demonstrates** some of what [Markdown][some/link] is *capable of doing*.
{% endhighlight %}

---

# introduction 
In this project we used different models to predict the chronic kidney disease and compare between these models  .


# preprocessing

### import data 
{% highlight Ruby %}
 dataset <- read.csv('chronic_kidney_disease_full1.csv')
{% endhighlight %} 
### install neccesary packages ,Then import libraries.
 {% highlight Ruby %}
  install.packages(e1071)
  install.packages(dplyr)
  install.packages(lattice)
  install.packages(readxl)
  install.packages(rattle)
  install.packages(rpart)
  install.packages(caret)
  install.packages(rpart.plot)
  install.packages(caTools)

  library(rpart,quietly = TRUE)
  library(caret,quietly = TRUE)
  library(rpart.plot,quietly = TRUE)
  library(rattle)
  library(readxl)
  library(ggplot2)
  library(lattice)
  library(caret)
  library(dplyr)
  library(tidyr)
  library(e1071)
  library(caTools)
  library(class)
  {% endhighlight %}
### freature selection
in our data we found that colmn 21 have alot of missing data so we remove it from our data

### Data imputation 

data has two types of columns data : numeric and factors data

we will replace any missing data with the mean of this column data if it has numeric data and if it has factors we will replace the missing data with the mode of this column

### feature normalization 
Because of the increasing in error when the range of data in each column is different in the width we made feature scalling to decrease this error.

# Methodology
for increasing our accuarcy we used cross validation by using creatfolds function  

## 1. Naive Bayes 

## 2. Deision Tree

## 3. Logistic regression 

## 4. KNN 


## Lists

### Ordered list

1. Item 1
2. A second item
3. Number 3

{% highlight raw %}
1. Item 1
2. A second item
3. Number 3
{% endhighlight %}

### Unordered list

* An item
* Another item
* Yet another item
* And there's more...

{% highlight raw %}
* An item
* Another item
* Yet another item
* And there's more...
{% endhighlight %}

---

## Paragraph modifiers

### Quote

> Here is a quote. What this is should be self explanatory. Quotes are automatically indented when they are used.

{% highlight raw %}
> Here is a quote. What this is should be self explanatory.
{% endhighlight raw %}




{% highlight raw %}
---
{% endhighlight %}

---

## Images

Markdown can also contain images. I'll need to add something here sometime.

{% highlight raw %}
![Markdowm Image][/image/url]
{% endhighlight %}

![Markdowm Image][6]

*Figure Caption*?

{% highlight raw %}
![Markdowm Image][/image/url]
<figcaption class="caption">Photo by John Doe</figcaption>
{% endhighlight %}

![Markdowm Image][6]
<figcaption class="caption">Photo by John Doe</figcaption>

*Bigger Images*?

{% highlight raw %}
![Markdowm Image][/image/url]{: class="bigger-image" }
{% endhighlight %}

![Markdowm Image][6]{: class="bigger-image" }
---
 