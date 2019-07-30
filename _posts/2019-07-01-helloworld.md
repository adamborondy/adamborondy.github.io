---
title: "Test"
date: 2019-07-01
tags: [introduction, webpage]
excerpt: "Machine Learning"
mathjax: true
---
# H1

## H2

Basic text

some *italics*

some **bold**

here's a [link](https://index.hu/)

bullets:
* First
* Second
- Third

number:
1. First
2. Second

```r
library(e1071)
library(rvest)
library(stringr)
library(ggplot2)
```

```r
# site="https://www.macrotrends.net/stocks/charts/AMZN/amazon/revenue"
# pagecode=read_html(site)
# pagecode=html_nodes(pagecode, css = ".col-xs-6") #CSS Field containing the descriptions
# pagecode2=html_text(pagecode)
```

```r
text <- as.character(pagecode2[1])
text <- str_replace_all(text, "[\r\t$,]" , "")
text <- scan(text = text, what="", sep="\n")
text <- matrix(text[-1],nrow = (length(text)-1)/2, ncol = 2, byrow = T)
text <- as.data.frame(text)
colnames(text) <- c("Date","Revenue")
text <- text[nrow(text):1,]
text[,1] <- as.Date(paste0(text[,1], "-12-31"))
text[,2] <- as.numeric(as.character(text[,2]))
```

```r
text[,"Index"] <- seq(1,nrow(text),1)
text[,"Index2"] <- text[,"Index"]^2
```

```r
quadratic_model = lm(formula = Revenue ~ Index + Index2, data = text)

ggplot() +
 geom_point(aes(x = text$Date, y = text$Revenue),
            colour = 'black') +
 geom_line(aes(x = text$Date, y = exp(predict(exponential_model, newdata = text))),
           colour = 'blue') +
 geom_line(aes(x = text$Date, y = predict(quadratic_model, newdata = text)),
           colour = 'red') +
 ggtitle('Exponential and Quadratic Regression of Amazon Revenue 2005-2018') +
 xlab('Year') +
 ylab('Revenue')
 ```

 ```r
 text[nrow(text) + 1,] = list("2019-12-31",25024,(nrow(text)+1),(nrow(text)+1)^2)
 text[nrow(text) + 1,] = list("2020-12-31",30871,(nrow(text)+1),(nrow(text)+1)^2)
 text[nrow(text) + 1,] = list("2021-12-31",38879,(nrow(text)+1),(nrow(text)+1)^2)

 ggplot() +
   geom_point(aes(x = text$Date, y = text$Revenue),
              colour = 'black') +
   geom_line(aes(x = text$Date, y = predict(quadratic_model, newdata = text)),
             colour = 'red') +
   ggtitle('Exponential and Quadratic Regression of Amazon Revenue 2005-2018') +
   xlab('Year') +
   ylab('Revenue')
```


inline code `x+y`.

some math:
$$x=y*z$$
