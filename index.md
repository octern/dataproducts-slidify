---
title       : Delay Discounting quiz app
subtitle    : Wait for it...
author      : Michael Cohn
job         : Courserer
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Delay Discounting

Delay discounting is a trait-like measure that describes how much people devalue a reward because they'll have to wait for it. We would like to enable people to learn about their own delay discounting using an online quiz! (also helping to address the dramatic shortage of qiuzzes on the internet). 

For more information, see the "background" tab of the app. (don't have the link to the app yet? You'll just have to wait for it.)

We compute delay discounting using the method of [Wileyto, Audrain-McGovern, Epstein, & Lerman (2004)](http://www.ncbi.nlm.nih.gov/pubmed/15190698). It performs logistic regression, predicting the choice of the immediate reward (coded 0) or the delayed reward (coded 1) based on the length of the delay and the ratio of the delayed to the immediate reward. *k*, the discounting parameter, is the ratio of the two regression parameters. 

--- .class #id 

## Generating Delay Discounting Questions

Participants are shown 10 questions asking them to choose between an immediate reward and a larger, delayed reward. Reward type, delay, and amount of discounting are randomly generated (with a reasonable range applied for each delay period). 

Below are the parameters for generating the questions: 


```r
items<-c("taco", "kitten", "kiss", "flan", "sardine", "penny", "diamond", "hat", "marshmallow")
itemss<-c("tacos", "kittens", "kisses", "flans", "sardines", "pennies", "diamonds", "hats", "marshmallows")
times<-list(
  list(1, "1 day", c(1.1, 1.2, 1.4, 1.7, 2, 4, 6, 10)), 
  list(2, "2 days", c(1.1, 1.2, 1.4, 1.7, 2, 4, 6, 10)), 
  list(7, "1 week", c(1.1, 1.2, 1.4, 1.7, 2, 4, 6, 10)),  
  list(14, "2 weeks", 2:20), 
  list(60, "2 months", 2:20), 
  list(365, "1 year", 2:100), 
  list(730, "2 years", seq(10,1000,10)), 
  list(1825, "5 years", seq(10,1000,10))
)

dollarsign<-"$"
qs<-data.frame(n=numeric(), token=character(), vd=numeric(), vi=numeric(), d=numeric(), dname=character(), r=numeric(), rparam=numeric(), waited=numeric())
tokn<-sample(1:length(items),1)
toks<-itemss[tokn]
tok<-items[tokn]
yyy<-1
```

---

## Randomly Generating Questions

Below we run an iteration of the code and show the types of questions participants might receive:

```r
for(n in 1:10) {
  temp<-data.frame(n=0, token=tok, vd=0, vi=0, d=0, dname="x", r=0, rparam=0, waited=-1)
  temp['n']<-n
  timei<-sample(times, 1)
  temp["d"]<-as.numeric(timei[[1]][[1]])
  temp['dname']<-timei[[1]][[2]]
  temp["vd"]<-sample(timei[[1]][[3]],1)
  temp["vi"]<-1
  temp["r"]<-temp["vi"]/temp["vd"]
  temp["rparam"]<-(1-(temp["vd"]/temp["vi"]))
  qs<-rbind(qs,temp)
}
```

---

## Questions

Below is an example of the questions a user might see, based on the code above. 

Don't forget to check out the app at http://octern.shinyapps.io/shiny!


```
##  1. Would you rather have 1 sardine now or   1.1 of them in 1 week?
##   2. Would you rather have 1 sardine now or  81.0 of them in 1 year?
##   3. Would you rather have 1 sardine now or   1.4 of them in 1 day?
##   4. Would you rather have 1 sardine now or   8.0 of them in 2 months?
##   5. Would you rather have 1 sardine now or   1.2 of them in 1 week?
##   6. Would you rather have 1 sardine now or 420.0 of them in 5 years?
##   7. Would you rather have 1 sardine now or  81.0 of them in 1 year?
##   8. Would you rather have 1 sardine now or   1.7 of them in 1 day?
##   9. Would you rather have 1 sardine now or   3.0 of them in 2 weeks?
##  10. Would you rather have 1 sardine now or 690.0 of them in 5 years?
```

(The questions are randomized each time the page is reloaded)


