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

# introduction 
In this project we used different models to predict the chronic kidney disease and compare between these models  .


# preprocessing

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

### import data
[download](https://archive.ics.uci.edu/ml/machine-learning-databases/00336/) data
Then import it
{% highlight Ruby %}
 dataset <- read.csv('chronic_kidney_disease_full1.csv')
{% endhighlight %} 
### Encoding Categorial Data

{% highlight Ruby %}
  dataset$sg = factor(dataset$sg, levels= c(1.005,1.01,1.015,1.02,1.025))
  dataset$al = factor(dataset$al,levels = c(0,1,2,3,4,5))
  dataset$su = factor(dataset$su,levels = c(0,1,2,3,4,5))
  dataset$pc = factor(dataset$pc,levels = c('normal','abnormal'),
                      labels= c(1,0))
  dataset$pcc = factor(dataset$pcc,levels = c('present','notpresent'),
                       labels= c(1,0))
  dataset$ba = factor(dataset$ba,levels = c('present','notpresent'),
                      labels= c(1,0))
  dataset$class = factor(dataset$class, levels = c('ckd','notckd'),
                         labels = c(1,0))
  dataset$rbc = factor(dataset$rbc, levels = c('normal','abnormal'),
                       labels = c(1,0))
  dataset$htn = factor(dataset$htn, levels = c('yes', 'no'),
                       labels = c(1,0))
  dataset$dm = factor(dataset$dm, levels = c('yes', 'no'),
                      labels = c(1,0))
  dataset$cad = factor(dataset$cad, levels = c('yes', 'no'),
                       labels = c(1,0))
  dataset$pe = factor(dataset$pe, levels = c('yes', 'no'),
                      labels = c(1,0))
  dataset$ane = factor(dataset$ane, levels = c('yes', 'no'),
                       labels = c(1,0))
  dataset$appet = factor(dataset$appet, levels = c('good', 'poor'),
                         labels = c(1,0))
  
{% endhighlight %} 


### freature selection
In our data we found that colmn 21 have alot of missing data so we remove it from our data
 
 {% highlight Ruby %}
 dataset <- dataset[,-21]
 {% endhighlight %}

### Data imputation 
In chronic_kidney_disease_full1.csv file the missing data is replaced with a '?' so to deal with these data we must convert it to 'NAN'
 
 {% highlight Ruby %}
  dataset <- na_if(dataset,'?')
 {% endhighlight %}
 
Data has two types of columns data : numeric and catergorical data

We will replace any missing data with the mean of this column data if it has numeric data ,But when it has catergorical we will replace the missing data with the mode of this column

{% highlight Ruby %}

dataset <- lapply(dataset, function(x)
  {
    if(is.factor(x)) replace(x, is.na(x), Mode(na.omit(x)))
    else if (is.numeric(x)) replace(x, is.na(x) , mean(x, na.rm = TRUE))
    else x
  })
#### we must convert the dataset into datafram to be able to deal with it.
  dataset = data.frame(dataset)
 {% endhighlight %}
 

### feature normalization 
Because of the increasing in error when the range of the numeric data in each column is different in the width we made feature scalling to decrease this error.
 
 {% highlight Ruby %}
 dataset [, 1:11] = scale(dataset[,1:11])
 {% endhighlight %}
 
# Methodology
for increasing our accuarcy we used [cross validation](https://magoosh.com/data-science/k-fold-cross-validation/).  
{% highlight Ruby %}
folds = createFolds(dataset$class , k = 5)
{% endhighlight %} 

## 1. Naive Bayes 

## 2. Deision Tree

## 3. Logistic regression 

First of all to understand logistic regression you must pass by linear regression , Take a look at [Linear regression](https://machinelearningmastery.com/linear-regression-for-machine-learning/)
As you have seen in linear regression , we used hypothesis relation to predict the output but this time we need that our predictions be the binary outcome of either 0 or 1.
So, we use the same hypothesis but with a little modification by using  the sigmoid function.

g(theta.x)=1/1+e^(-theta.x)
g(z)=1/(1+e^(-z) 

{% highlight Ruby %}
cv_LR = lapply(folds, function(x){
    training_fold = dataset[-x,]
    test_fold = dataset [x,]
    classifier = glm (formula =class ~.,
                      family = binomial,
                      data = training_fold)

    prob_pred = predict.glm(classifier , type = 'response', newdata = test_fold[-24])
    
    y_pred = ifelse(prob_pred > 0.5 , 1 ,0 )
    
    CM_V = table(dataset[x,24], y_pred)
    
    accuracy_V = (CM_V[1,1] + CM_V[2,2]) / (CM_V[1,1] + CM_V[2,2] + CM_V[1,2] + CM_V[2,1])
    
    sens_v = (CM_V[1,1])/(CM_V[1,1]+CM_V[2,1])
    
    spec_v = (CM_V[2,2])/(CM_V[2,2]+CM_V[1,2])
    
    statisitcs = c(accuracy_V,sens_v,spec_v)
    return(statisitcs)
  })
  
 {% endhighlight %}



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
 