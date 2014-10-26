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

## Justification

I was looking at the internet the other day, and I said to myself, "what we really need is another online quiz." And at the same time I was computing delay discounting values for a study of meth-using MSM, so I decided to implement a delay discounting quiz for another audience (who are hopefully not using meth, unless the coursera deadline was just too much for them). 


--- .class #id 

## Delay Discounting

Delay discounting is a trait-like measure that describes how much people devalue a reward because they'll have to wait for it. For more information, see the "background" tab of the app. (don't have the link to the app yet? You'll just have to wait for it.)

--- .class #id 

## The computation

We compute delay discounting using the method of [Wileyto, Audrain-McGovern, Epstein, & Lerman (2004)](http://www.ncbi.nlm.nih.gov/pubmed/15190698). It performs logistic regression, predicting the choice of the immediate reward (coded 0) or the delayed reward (coded 1) based on the length of the delay and the ratio of the delayed to the immediate reward. *k*, the discounting parameter, is the ratio of the two regression parameters. 


--- .class #id 

## Features to implement in the future

The current version of the application uses 10 questions, with randomly-generated delay periods and degrees of discounting and a randomly selected type of reward. We would like to implement an option to run the test with money instead of other material rewards (a simple matter of doing some reformatting and adding a UI option). It might also be interesting to provide a plot of the user's discounting across different time periods (usually modeled with a hyperbolic function).






