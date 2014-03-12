---
title: Determinants of Bird Richness and Tombs at TIL
tags: [Thousand Island Lake, AIC, Zhejiang]
categories: [Statistics,Fun]
layout: post
comments: yes
---


#### Based on the Model Selection and Multimodel Inference

[**Xingfeng Si**](http://sixf.org/en)

Institute of Imagination Sciences, College of Life Sciences of Zhejiang University, Hangzhou Zhejiang 310035, China

## Abstract

Because of the biases and shortcomings of the stepwise multiple regression, the Information Theoretic (IT) are becoming a reliable method to inference the data well, even there have a larger number of competing models. Here, based on the Akaike Information Criterion, we analysed the determinants of the bird richness at the Thousand Island Lake using the method multimodel inference. Additionally, we discussed the distribution pattern of tombs on the islands. Bird communities on the island were determined by island area and habitat richness, while the occupancy of tombs was determined by habitat richness only. Our results firstly showed bird richness significantly related with tomb occupancy, which may be a potential indicator to find the tombs in the region of Thousand Island Lake.

## Keywords

AIC, model selection, birds, multimodel inference,  stepwise regression,Thousand Island Lake, tomb distribution

## Introduction

How to select the model as you are facing a larger number of competing models in your analyses? Using stepwise multiple regression, or the Information Theoretic Analysis? Whittingham et al. (2006) found 57% of 65 papers published in three leading ecological journals used a stepwise approach. Although the stepwise regression include several principal drawbacks, such as bias in parameter estimation, inconsistencies among model selection algorithms, an inherent problems of multiple hypothesis testing, and an inappropriate focus or reliance on a single best model, it is still widely used. For the detail mechanisms underlying these shortages of stepwise regression is not the scope of this blog. In this blog, I will introduce how to use the AIC to make the model selection.

The [Thousand Island Lake](http://sixf.org/en/pages/thousand-island-lake/)(hereafter, the Lake for simplify) locates at the western Zhejiang Province, eastern China. It was created in 1959 by the damming construction. Flooding more than 500 km^2, in formed 1078 islands with area > 0.25 ha at 108 m water-level, which is a natural experiment for the studying of island biogeography, and conservation biology. [Our group](http://mypage.zju.edu.cn/personnelCard/pingding) began to survey the bird communities since 2002, and now expanded to many biological categories, e.g. spider, reptiles, amphibians, snake, monkey, insects, small mammals, butterflies and vegetation monitoring. It is a rapidly growing project as welcome all the ecologists who have an interest. Just several months ago, I talked with the spider Dr. Wu in our group who forces on the spider researches, and discuss the possibility of analyzing the relationship between bird richness and fengshui. Yes, I know it is not easy to explain the word fengshui in English which is a special culture existing in Chinese history. Fengshui may be simply similar as good luck. For example, when someone was diseased, his/her family will try to find some place have a good fengshui to build the tomb as hope he/she will have another good destination after died. 

Here, I employed the method of model selection and multimodel inference to analysis the determinants of the bird richness and tomb occurrence on the islands. This blog addressed these questions: 1) What is the AIC? Does it mean the American International College? 2) the key processes to run the multimodel inference. 3) the determinants of the bird and tomb distribution on the islands.


## Materials and Methods 

### Study area and island attributes

We stratified randomly sampled 40 islands across the area and isolation gradients at the Lake.Since 2002, many islands attributes were measured which relate to bird richness, such as island area, isolation, plant richness, habitat types, perimeter, perimeter to area ratio (PAR), shape index (SI), and elevation. I also imagined several island attributed that may relate to discover the tombs on the islands, such as convex, slope, aspect, Al, Si, sand, and pH.

The elements of Al and Si are the main substances of earth which has a good material for waterproof. The index of sand means the possibility of building a tomb on the island, because it is impossible to find a tomb on sand. pH might be related to the organic materiel on the tomb. Other factors, e.g. SI, convex, slope and aspect are the key indicators for fengshui. For example, a mountain with a perfect round shape, thick earth and high plant richness is the priority place to set a tomb.

### AIC

AIC(Akaika Information Criterion) is a measure of the relative quality of a statistical model, for a given set of data. AIC is founded on information entropy, so it does not provide a test of a model in the sense of testing a null hypothesis, i.e. AIC can tell nothing about the quality of the model in an absolute sense. If all the candidate models fit poorly, AIC will not give any warning of that.

Basically, AIC is

![](http://sixf.org/files/images/2014/03/eq1.png)

where *k* is the number of parameters in the statistical model, and *L* is the maximized value of the likelihood function for the estimated model. We need not the know the detail calculation method, as there are already having existing functions in R packages, such as `AIC` function in `stat` package, and `extractAIC` in `stats` package. If you would like to calculate AIC by yourself, it is also easy to make it. If the variance of the model distributes normally, and n is the number of sampling, RSS is the residual-sum-squares, so

![](http://sixf.org/files/images/2014/03/eq2.png)

Given a set of candidate models for the data, the preferred model is the one with the minimum AIC value. Hence AIC not only rewards goodness of fit, but also includes a penalty that is an increasing function of the number of estimated parameters. This penalty discourages overfitting.

For the sample sizes, the AIC is corrected by AICc (corrected AIC)

![](http://sixf.org/files/images/2014/03/eq3.png)

where *n* denotes the sample size. Burnham & Anderson(2002) strongly recommend using AICc, rather than AIC, if *n* is small or *k* is larger. Since AICc converges to AIC as *n* gets large, AICc generally should be employed regardless (Most of the contents in the section was borrowed from [Wikipeadia](http://en.wikipedia.org/wiki/Akaike_information_criterion), whereas there is a mistake in the Chinese version of this page as it cited the Burnham & Anderson's book in 2004)

If the overdispersion exists in the data, the QAIC would be a better choice, which is

![](http://sixf.org/files/images/2014/03/eq4.png)

$\hat{c}$ is the variance inflation factors, or the overdispersion coefficient. If $\hat{c}$ > 1, the QAIC should be used. 

### Calculating the model weights

Once get all the AIC values for each model, then sorting these model in the decreasing order of AIC. ∆AIC means the AIC of each model minus the small one. The model weight, also called Akaika weight(*w<sub>i</sub>*), is calculated as

![](http://sixf.org/files/images/2014/03/eq5.png)

where *w<sub>i</sub>* the weight of the *i*th model。*w<sub>i</sub>* ranges between 0 and 1, and the sum of them equals 1. The larger the model weight, the more possibility to be the best "true" model. For example, if we get a model with the model weight *w<sub>2</sub>* is 0.31, indicating the probability of this model to be the best possible model is 31%.

The importance of each parameters can be calculated by the model weights, which add the weights of the model containing the parameter. After ranking the importance in decreasing order, it is clear which parameter is the most important one.

### Model selection uncertainity and multimodel inference

In practice, the result will be not so perfect as assumed. All the previous results were based on the assumption of ∆AIC > 2, meaning the AIC of second best model is larger than 2 points the smallest AIC. If ∆AIC > 2, it is safe to use the first model as the best model. If not, it means the first several competing models have substantially supports. So, how to deal with under this circumstance? The terminal weapon: model averaging.

Once ∆AIC > 2 is a golden rule (Burnham & Anderson, 2002), whereas Anderson (2008) suggested it is better to conclude all the possible models, UNLESS some model should be removed with confidence evidence. As the model with very small AIC, which also have small model weight, so the result will not be influenced a lot by the such models. Suppose *Y<sup>^</sup>* is the observed dependent value, such as the bird richness or the occupancy of the tomb in my case, whose averaging observed value is

![](http://sixf.org/files/images/2014/03/eq6.png)

It means if you have nine candidate models, so there are nine model weights, and could calculate nine observes. The averaging observe dependence value is calculated for each observe multiply its model weight, i.e.

![](http://sixf.org/files/images/2014/03/eq7.png)

As similar as the averaging observed dependent estimates, we can also get the model-averaged estimates of parameter. Suppose the estimate of the *i*th  parameter is *θ<sub>i</sub>*, it can be calculated directly from the model with smallest AIC value if the ∆AIC > 2. Once ∆AIC < 2, the averaged estimate of parameter is given by

![](http://sixf.org/files/images/2014/03/eq8.png)

Then using the model weight, we obtained the unconditional variance estimate (Burnham & Anderson, 2002, p162)

![](http://sixf.org/files/images/2014/03/eq9.png)

Anderson suggested we should use the alternative one (Anderson, 2008 p111), which is

![](http://sixf.org/files/images/2014/03/eq10.png)

where $\hat{\bar{θ}}$ is the model-averaged estimate, *w<sub>i</sub>* is model weight, and *g<sub>i</sub>* is the *i*th model. As described by Anderson (2008), an estimator of the variance of parameter estimator estimates that incorporates both sampling variance, given a model, and a variance component for model selection uncertainty. So the confidence intervals is 

![](http://sixf.org/files/images/2014/03/eq11.png)

### Case study

Before running the code below, to be sure these package were installed: `glmulti`, `MuMIn`, `bbmle`. If not, simply put the below code to the R console, and the installation will start automatically.

{% highlight r %}
install.packages("glmulti")
{% endhighlight %}

Or else, download these packages from any CRAN of R project, and install them locally.


#### Case One: the determinant of bird richness at the Lake

Load `glmulti` package


{% highlight r %}
library(glmulti)
{% endhighlight %}

```
## Loading required package: rJava
```


Load the bird and island data (this is the real data, but I shuffled the data randomly)


{% highlight r %}
tilbird <- read.table("tilbird.txt", h = T)  #find 'tilbird.txt' and open it
str(tilbird)  # check the data structure of `til.bird`
{% endhighlight %}

```
## 'data.frame':  40 obs. of  9 variables:
##  $ birdspp  : int  43 34 35 32 31 27 30 33 24 24 ...
##  $ area     : num  1289.2 143.2 109 55.1 46.4 ...
##  $ isolation: num  897 1415 965 954 730 ...
##  $ plants   : int  198 99 86 59 51 49 57 69 74 85 ...
##  $ habitats : int  7 6 6 5 5 5 5 3 4 3 ...
##  $ Pe       : num  105965 17465 12022 7570 10444 ...
##  $ PAR      : num  82.2 122 110.3 137.4 225.2 ...
##  $ SI       : num  832 412 325 288 433 ...
##  $ elev     : num  298 251 227 198 174 ...
```


The first column of the data is the bird species on each island, and thereby eight island attributes, which are area, isolation, plant richness, habitat types, perimeter, PAR, SI and elevation. Larger PAR indicates more edges comparing the interior area on an island, and SI will be 1 if the island is a perfect circle.

Before running the model, we should check the independence of each variables. There are several available methods, such as correlation test, VIF and PCA analyses. Here, we use the common method of correlation test.

The R function for correlation test is `cor.test`, which is a test for two factors. Function `cor` can run the correlation with more than two factors, but no p-values in the result. So, I wrote a function to run the test with p-value in the result, named `cor.sig`.

{% highlight r %}
cor.sig = function(test) {
    res.cor = cor(test)
    res.sig = res.cor
    res.sig[abs(res.sig) > 0] = NA
    nx = dim(test)[2]
    for (i in 1:nx) {
        for (j in 1:nx) {
            res.cor1 = as.numeric(cor.test(test[, i], test[, j])$est)
            res.sig1 = as.numeric(cor.test(test[, i], test[, j])$p.value)
            if (res.sig1 <= 0.001) {
                sig.mark = "***"
            }
            if (res.sig1 <= 0.01 & res.sig1 > 0.001) {
                sig.mark = "** "
            }
            if (res.sig1 <= 0.05 & res.sig1 > 0.01) {
                sig.mark = "*  "
            }
            if (res.sig1 > 0.05) {
                sig.mark = "   "
            }
            if (res.cor1 > 0) {
                res.sig[i, j] = paste(" ", as.character(round(res.cor1, 3)), 
                  sig.mark, sep = "")
            } else {
                res.sig[i, j] = paste(as.character(round(res.cor1, 3)), sig.mark, 
                  sep = "")
            }
        }
    }
    as.data.frame(res.sig)
}
{% endhighlight %}

Put all the attributes into correlation test,


{% highlight r %}
cor.sig(tilbird[, 2:9])  # exclude the first column which is the bird richness, the Y values.
{% endhighlight %}

```
##                area isolation    plants  habitats        Pe       PAR
## area           1*** -0.115     0.798***  0.623***  0.996*** -0.429** 
## isolation -0.115         1*** -0.132    -0.191    -0.117     0.299   
## plants     0.798*** -0.132         1***  0.542***  0.798*** -0.521***
## habitats   0.623*** -0.191     0.542***      1***  0.676*** -0.805***
## Pe         0.996*** -0.117     0.798***  0.676***      1*** -0.481** 
## PAR       -0.429**   0.299    -0.521*** -0.805*** -0.481**       1***
## SI         0.857*** -0.045     0.697***  0.827***  0.898*** -0.619***
## elev       0.726*** -0.127     0.666***  0.924***  0.775*** -0.803***
##                  SI      elev
## area       0.857***  0.726***
## isolation -0.045    -0.127   
## plants     0.697***  0.666***
## habitats   0.827***  0.924***
## Pe         0.898***  0.775***
## PAR       -0.619*** -0.803***
## SI             1***  0.888***
## elev       0.888***      1***
```


The results indicated a significant correlation existed among area, perimeter, PAR, SI and elevation. We know area is a very important parameter in the theory of island biogeography. Other parameters may be resulted by area, so I excluded the perimeter, PAR, SI and elevation, and only four parameter entering the analyses: area, isolation, plant richness and habitat types.

I simply used the linear model. The global model is 


{% highlight r %}
global.model <- lm(birdspp ~ area + isolation + plants + habitats, data = tilbird)
{% endhighlight %}


Then use the function `glmulti` in the `glmulti` package to choose the 'best ' model whose AIC is the smallest. Because I have four parameters, so totally have 2^4=16 candidate model (**excluding the interaction effect between island attributs**).


{% highlight r %}
bird.model <- glmulti(global.model, level = 1, crit = "aicc")  # use the AICc to choose the model because it works better in small samples
{% endhighlight %}

```
## Initialization...
## TASK: Exhaustive screening of candidate set.
## Fitting...
## Completed.
```

{% highlight r %}
summary(bird.model)
{% endhighlight %}

```
## $name
## [1] "glmulti.analysis"
## 
## $method
## [1] "h"
## 
## $fitting
## [1] "lm"
## 
## $crit
## [1] "aicc"
## 
## $level
## [1] 1
## 
## $marginality
## [1] FALSE
## 
## $confsetsize
## [1] 100
## 
## $bestic
## [1] 204.9
## 
## $icvalues
##  [1] 204.9 205.3 206.9 207.5 214.3 214.9 216.6 217.1 217.8 218.4 220.6
## [12] 221.3 226.2 226.7 243.6 244.5
## 
## $bestmodel
## [1] "birdspp ~ 1 + plants + habitats"
## 
## $modelweights
##  [1] 4.005e-01 3.296e-01 1.499e-01 1.103e-01 3.555e-03 2.653e-03 1.141e-03
##  [8] 9.180e-04 6.250e-04 4.660e-04 1.578e-04 1.095e-04 9.564e-06 7.474e-06
## [15] 1.568e-09 1.005e-09
## 
## $includeobjects
## [1] TRUE
```

The result came out. The best model included the area and habitat types. This will check all the possible model one by one and find the best one.


{% highlight r %}
lm9 <- lm(birdspp ~ area + habitats, data = tilbird)
summary(lm9)
{% endhighlight %}

```
## 
## Call:
## lm(formula = birdspp ~ area + habitats, data = tilbird)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -6.665 -2.266  0.128  1.844  8.594 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 17.47172    2.33167    7.49  6.3e-09 ***
## area         0.00779    0.00343    2.27   0.0289 *  
## habitats     2.29668    0.65987    3.48   0.0013 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.42 on 37 degrees of freedom
## Multiple R-squared:  0.545,	Adjusted R-squared:  0.52 
## F-statistic: 22.2 on 2 and 37 DF,  p-value: 4.71e-07
```


Check the AICc values:


{% highlight r %}
summary(bird.model)$icvalue
{% endhighlight %}

```
##  [1] 204.9 205.3 206.9 207.5 214.3 214.9 216.6 217.1 217.8 218.4 220.6
## [12] 221.3 226.2 226.7 243.6 244.5
```


The ∆AICc of the second model is 225.6429-225.4588=0.1841, which is < 2. If it is > 2, the process of model selection was finished, as the best model is the first model. Now, we should run the model averaging, and list all the possible model (16 models):


{% highlight r %}
lm1 <- lm(birdspp ~ area + isolation + plants + habitats, data = tilbird)
lm2 <- lm(birdspp ~ isolation + plants + habitats, data = tilbird)
lm3 <- lm(birdspp ~ area + plants + habitats, data = tilbird)
lm4 <- lm(birdspp ~ area + isolation + habitats, data = tilbird)
lm5 <- lm(birdspp ~ area + isolation + plants, data = tilbird)
lm6 <- lm(birdspp ~ plants + habitats, data = tilbird)
lm7 <- lm(birdspp ~ isolation + habitats, data = tilbird)
lm8 <- lm(birdspp ~ isolation + plants, data = tilbird)
lm9 <- lm(birdspp ~ area + habitats, data = tilbird)
lm10 <- lm(birdspp ~ area + plants, data = tilbird)
lm11 <- lm(birdspp ~ area + isolation, data = tilbird)
lm12 <- lm(birdspp ~ area, data = tilbird)
lm13 <- lm(birdspp ~ isolation, data = tilbird)
lm14 <- lm(birdspp ~ plants, data = tilbird)
lm15 <- lm(birdspp ~ habitats, data = tilbird)
lm16 <- lm(birdspp ~ 1, data = tilbird)
{% endhighlight %}


Looks nice? It will be tricky if you have 10 parameter as there are 2^10=1024 candidate models! Take easy, we can create a loop function to let the computer run the calculation (not shown here)

Average the model together,


{% highlight r %}
library(MuMIn)
lm.ave <- model.avg(lm1, lm2, lm3, lm4, lm5, lm6, lm7, lm8, lm9, lm10, lm11, 
    lm12, lm13, lm14, lm15, lm16)
summary(lm.ave)
{% endhighlight %}

```
## 
## Call:
## model.avg.default(object = lm1, lm2, lm3, lm4, lm5, lm6, lm7, 
##     lm8, lm9, lm10, lm11, lm12, lm13, lm14, lm15, lm16)
## 
## Component models:
##        df  logLik  AICc Delta Weight
## 24      4  -97.88 204.9  0.00   0.40
## 234     5  -96.76 205.3  0.39   0.33
## 124     5  -97.55 206.9  1.96   0.15
## 1234    6  -96.46 207.5  2.58   0.11
## 34      4 -102.60 214.3  9.45   0.00
## 4       3 -104.13 214.9 10.03   0.00
## 134     5 -102.43 216.6 11.72   0.00
## 14      4 -103.95 217.1 12.16   0.00
## 12      4 -104.34 217.8 12.93   0.00
## 123     5 -103.32 218.4 13.51   0.00
## 2       3 -106.95 220.6 15.68   0.00
## 23      4 -106.08 221.3 16.41   0.00
## 13      4 -108.52 226.2 21.29   0.00
## 1       3 -110.00 226.7 21.78   0.00
## 3       3 -118.47 243.6 38.72   0.00
## (Null)  2 -120.09 244.5 39.61   0.00
## 
## Term codes:
##      area  habitats isolation    plants 
##         1         2         3         4 
## 
## Model-averaged coefficients: 
##              Estimate Std. Error Adjusted SE z value Pr(>|z|)    
## (Intercept) 14.016589   2.311063    2.372339    5.91   <2e-16 ***
## plants       0.092700   0.022636    0.023348    3.97   0.0001 ***
## habitats     1.921310   0.542074    0.560239    3.43   0.0006 ***
## isolation   -0.000818   0.000573    0.000593    1.38   0.1677    
## area        -0.002977   0.004172    0.004313    0.69   0.4901    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Full model-averaged coefficients (with shrinkage): 
##  (Intercept)    plants  habitats isolation      area
##    14.016589  0.092572  1.905393 -0.000364 -0.000784
## 
## Relative variable importance:
##    plants  habitats isolation      area 
##      1.00      0.99      0.45      0.26
```


The first part of the result 'Component models', have listed the degree of freedom for all models(df), the log likelihood (logLik), the AICc values, ∆AICc and model weights. Here, the weight of the best model is **0.22**, it means the possibility to-be the "true" model is 22%, which is pretty low. It will be nice if the weight reaches to 0.6-0.7. It should be to know the data here was shuffled by me, so the result have no meanings.

The fourth part of the result is 'Full model-averaged coefficients'.

The fifth is 'Relative variable importance'. The largest one equals 1. In this case, area is the most important attributes as it equals 1. The next is the habitat types, and the isolation and plants looks no importance in the models.

Now we can predict the bird species on island 1using the averaged predictions,


{% highlight r %}
pred.mat <- matrix(NA, ncol = 16, nrow = 40, dimnames = list(paste("isl", 1:40, 
    sep = ""), paste("lm", 1:16, sep = "")))  # created a blank matrix to store the predicted valude on 40 islands for 16 models
pred.mat[, 1] <- predict(lm1)
pred.mat[, 2] <- predict(lm2)
pred.mat[, 3] <- predict(lm3)
pred.mat[, 4] <- predict(lm4)
pred.mat[, 5] <- predict(lm5)
pred.mat[, 6] <- predict(lm6)
pred.mat[, 7] <- predict(lm7)
pred.mat[, 8] <- predict(lm8)
pred.mat[, 9] <- predict(lm9)
pred.mat[, 10] <- predict(lm10)
pred.mat[, 11] <- predict(lm11)
pred.mat[, 12] <- predict(lm12)
pred.mat[, 13] <- predict(lm13)
pred.mat[, 14] <- predict(lm14)
pred.mat[, 15] <- predict(lm15)
pred.mat[, 16] <- predict(lm16)
# show the 40 averaged predicted values which are the hat-bar(Y)
bird.pred <- pred.mat %*% summary(lm.ave)$summary$Weight
t(bird.pred)  #transfer the matrix to save the space of the page. Nothing related to analyses
{% endhighlight %}

```
##       isl1  isl2  isl3  isl4  isl5 isl6  isl7 isl8 isl9 isl10 isl11 isl12
## [1,] 43.83 33.87 33.09 28.86 28.33 27.2 28.02 26.5 28.5 26.65 29.07 27.45
##      isl13 isl14 isl15 isl16 isl17 isl18 isl19 isl20 isl21 isl22 isl23
## [1,] 22.86 23.73 26.22 27.59 27.66 23.43 23.15 23.57 26.14 24.94 24.95
##      isl24 isl25 isl26 isl27 isl28 isl29 isl30 isl31 isl32 isl33 isl34
## [1,] 24.81 22.83 22.66 21.37 22.21 25.95  22.7  25.9 23.78 23.28 25.64
##      isl35 isl36 isl37 isl38 isl39 isl40
## [1,] 26.37 24.06 22.33 23.14 23.75 24.61
```


The final point is the unconditional variance estimator, which is a bitter complex. The calculation method is similar as $\hat{\bar{Y}}$ , and will run this estimation in the near future.

#### Case Two: determinants of the occurancy of tombs at the Lake

The procedure is exactly the same as before, so make it in the same way,


{% highlight r %}
tiltomb <- read.table("tiltomb.txt", h = T)  #read the database 'tiltomb.txt'
cor.sig(tiltomb[, -1])
{% endhighlight %}

```
##               area    plants  habitats        SI      elev    convex
## area          1***  0.798***  0.623***  0.857***  0.726***  0.041   
## plants    0.798***      1***  0.542***  0.697***  0.666*** -0.019   
## habitats  0.623***  0.542***      1***  0.827***  0.924***  0.394*  
## SI        0.857***  0.697***  0.827***      1***  0.888***  0.237   
## elev      0.726***  0.666***  0.924***  0.888***      1***  0.307   
## convex    0.041    -0.019     0.394*    0.237     0.307         1***
## slope     0.248     0.394*    0.311     0.247     0.322*    0.264   
## aspect   -0.114    -0.031     0.226     0.069     0.278     0.075   
## Al        0.088     0.204     0.308     0.223     0.326*     0.06   
## Si        0.055     0.184     0.173      0.14     0.243     0.081   
## sand     -0.207     0.021    -0.118     -0.22    -0.191    -0.311   
## pH       -0.194    -0.326*   -0.247     -0.17    -0.228     0.018   
##              slope    aspect        Al        Si      sand        pH
## area      0.248    -0.114     0.088     0.055    -0.207    -0.194   
## plants    0.394*   -0.031     0.204     0.184     0.021    -0.326*  
## habitats  0.311     0.226     0.308     0.173    -0.118    -0.247   
## SI        0.247     0.069     0.223      0.14     -0.22     -0.17   
## elev      0.322*    0.278     0.326*    0.243    -0.191    -0.228   
## convex    0.264     0.075      0.06     0.081    -0.311     0.018   
## slope         1*** -0.093     0.412**   0.334*    0.111     -0.53***
## aspect   -0.093         1***  0.075     0.101    -0.086     0.198   
## Al        0.412**   0.075         1***  0.887***  0.615*** -0.756***
## Si        0.334*    0.101     0.887***      1***  0.504*** -0.646***
## sand      0.111    -0.086     0.615***  0.504***      1*** -0.598***
## pH        -0.53***  0.198    -0.756*** -0.646*** -0.598***      1***
```


The result showed area, SI and elevation have significant correlation. Considering the reality, area will not be an important parameter when choosing the site of a tomb which is not related to fengshui. Whereas the SI is an essential factor because the round island, or round mountaintop before inundation, means a good luck in the world of fengshui, so I keep the SI and excluded others. Sand index correlated to SI, as sand index also an importance factor related to fengshui, so I kept both of them. The elements of Al and Si, and slope have strong correlation, which is easy to explain as the earth both have these two elements. Because the proportion of Al is more than Si, I dropped Si and slope.Sand index had correlation with pH. I am sure sand index should be reserved, so excluded the pH.

Then look again the matrix after excluding the strong correlated attributes. The results looks nice.


{% highlight r %}
cor.sig(tiltomb[, c("plants", "habitats", "SI", "convex", "aspect", "Al", "sand")])
{% endhighlight %}

```
##             plants  habitats        SI    convex    aspect        Al
## plants        1***  0.542***  0.697*** -0.019    -0.031     0.204   
## habitats  0.542***      1***  0.827***  0.394*    0.226     0.308   
## SI        0.697***  0.827***      1***  0.237     0.069     0.223   
## convex   -0.019     0.394*    0.237         1***  0.075      0.06   
## aspect   -0.031     0.226     0.069     0.075         1***  0.075   
## Al        0.204     0.308     0.223      0.06     0.075         1***
## sand      0.021    -0.118     -0.22    -0.311    -0.086     0.615***
##               sand
## plants    0.021   
## habitats -0.118   
## SI        -0.22   
## convex   -0.311   
## aspect   -0.086   
## Al        0.615***
## sand          1***
```

The similar way as I did for the bird data. The difference here is that the dependent values is binary, which is the presence-absence data, so I should use the logistic regression with the function `glm`. Running the code below,

{% highlight r %}
global.model.tomb <- glm(tomb ~ plants + habitats + SI + convex + aspect + Al + 
    sand, family = binomial("logit"), data = tiltomb)
tomb.model <- glmulti(global.model.tomb, level = 1, crit = "aicc")
{% endhighlight %}

```
## Initialization...
## TASK: Exhaustive screening of candidate set.
## Fitting...
## 
## After 50 models:
## Best model: tomb~1+habitats
## Crit= 55.4946426318003
## Mean crit= 61.2928677656059
```

![](http://sixf.org/files/images/2014/03/unnamed-chunk-141.png) 

```
## 
## After 100 models:
## Best model: tomb~1+habitats
## Crit= 55.4946426318003
## Mean crit= 62.1673748202582
```

![](http://sixf.org/files/images/2014/03/unnamed-chunk-142.png) 

```
## 
## After 150 models:
## Best model: tomb~1+habitats
## Crit= 55.4946426318003
## Mean crit= 61.961797879279
```

![](http://sixf.org/files/images/2014/03/unnamed-chunk-143.png) 

```
## Completed.
```

{% highlight r %}
summary(tomb.model)
{% endhighlight %}

```
## $name
## [1] "glmulti.analysis"
## 
## $method
## [1] "h"
## 
## $fitting
## [1] "glm"
## 
## $crit
## [1] "aicc"
## 
## $level
## [1] 1
## 
## $marginality
## [1] FALSE
## 
## $confsetsize
## [1] 100
## 
## $bestic
## [1] 55.49
## 
## $icvalues
##   [1] 55.49 57.02 57.37 57.54 57.86 57.88 57.92 57.98 58.33 59.11 59.19
##  [12] 59.39 59.43 59.51 59.61 59.84 59.96 59.97 59.98 60.05 60.07 60.12
##  [23] 60.17 60.22 60.31 60.39 60.39 60.45 60.50 60.75 60.82 60.89 61.22
##  [34] 61.43 61.57 61.59 61.68 61.74 61.79 61.80 61.83 61.87 61.87 61.89
##  [45] 62.01 62.12 62.13 62.15 62.17 62.39 62.44 62.57 62.59 62.60 62.66
##  [56] 62.67 62.70 62.72 62.73 62.75 62.75 62.77 62.78 62.79 62.82 62.83
##  [67] 62.87 62.95 63.01 63.08 63.09 63.41 63.53 63.54 63.66 63.73 63.81
##  [78] 63.91 64.05 64.14 64.20 64.39 64.41 64.45 64.47 64.52 64.57 64.59
##  [89] 64.60 64.61 64.62 64.68 64.70 64.75 64.77 64.78 64.78 64.83 64.87
## [100] 64.92
## 
## $bestmodel
## [1] "tomb ~ 1 + habitats"
## 
## $modelweights
##   [1] 0.128895 0.060215 0.050588 0.046452 0.039523 0.039070 0.038387
##   [8] 0.037162 0.031300 0.021153 0.020362 0.018351 0.018034 0.017282
##  [15] 0.016432 0.014668 0.013839 0.013729 0.013665 0.013229 0.013062
##  [22] 0.012760 0.012424 0.012150 0.011631 0.011135 0.011126 0.010795
##  [29] 0.010573 0.009297 0.008987 0.008661 0.007364 0.006612 0.006189
##  [36] 0.006106 0.005841 0.005679 0.005542 0.005503 0.005417 0.005326
##  [43] 0.005319 0.005273 0.004959 0.004704 0.004660 0.004631 0.004590
##  [50] 0.004106 0.004004 0.003754 0.003715 0.003699 0.003581 0.003571
##  [57] 0.003510 0.003485 0.003459 0.003434 0.003418 0.003393 0.003378
##  [64] 0.003356 0.003311 0.003295 0.003230 0.003100 0.003011 0.002909
##  [71] 0.002890 0.002458 0.002319 0.002313 0.002168 0.002098 0.002018
##  [78] 0.001918 0.001790 0.001706 0.001663 0.001510 0.001494 0.001468
##  [85] 0.001450 0.001413 0.001381 0.001368 0.001358 0.001354 0.001343
##  [92] 0.001308 0.001292 0.001261 0.001246 0.001244 0.001240 0.001211
##  [99] 0.001190 0.001156
## 
## $includeobjects
## [1] TRUE
```

The results shows the best model only had habitat parameter, which is also looks good. although the troublesome ∆AICc is still < 2. I will not run the model averaging here, so there are 2^7=128 candidate models.


## Results

The determinants of bird richness at the Lake is the area and habitat types, and habitat types is the only determinant for tomb occupancy.


## Disccussion

I have heard there is a more powerful method, called [Random forest model](http://blog.sciencenet.cn/blog-661364-615921.html), which do not the independence test in the beginning of the analyses. I do not use this model, and will try it in future.

PS: the results below is just for fun.

The priority rule to find a tomb on the islands of the Lake is the habitat types. So, once you have a tourist at the Lake, please do not visit the so-called monkey islands or snake islands, you should land on some islands with high habitat types. Oops, how to identify the habitat type, you may suggestion you learning some basic knowledge of [community ecology](http://en.wikipedia.org/wiki/Community_(ecology))。

Finally, I ran the correlation test between bird richness and tomb occupancy.


{% highlight r %}
cor.test(tilbird[, 1], tiltomb[, 1])
{% endhighlight %}

```
## 
## 	Pearson's product-moment correlation
## 
## data:  tilbird[, 1] and tiltomb[, 1]
## t = 3.256, df = 38, p-value = 0.002378
## alternative hypothesis: true correlation is not equal to 0
## 95 percent confidence interval:
##  0.1821 0.6797
## sample estimates:
##    cor 
## 0.4671
```

The result showed they have significant correlation (t = 3.2562, df = 38, p-value = 0.002378). The islands with tombs are the islands having good fengshui. My result verified our prediction talked with Dr. Spider that bird richness related to fengshui significantly. For the detail underlying mechanisms, I should use the pathway analyses to explore the patterns. It may be a follow-up paper to answer this question.

## Acknowlegements

Thanks for your reading this long boring blog. Thanks for the supports for our group as I have a little time to imagine something having no connection with my academic stuffs. I also thanks the Lake data from our group and the data of island attributes which comes from the [Gutianshan plot](http://blog.sciencenet.cn/blog-267448-463699.html). I just run the anaysis anyway as they have no relations. I thanks for <a href="https://gist.github.com/sixf/9488518">this tutorial</a> providing the original code of this analyses. The code of this blog could be downloaded from [here](https://github.com/sixf/TIL-model-selection/archive/master.zip). Feel free to leave any reviews below as you are exactly the referee. Thanks!

## References

1.	Anderson, David R. (2008) *Model based inference in the life sciences: a primer on evidence*. New York: Springer.
Burnham, Kenneth P., and David R. Anderson. (2002) *Model selection and multimodel inference: a practical information-theoretic approach*. Springer.
2.	Symonds, Matthew RE, and Adnan Mouθalli. (2011) A brief guide to model selection, multimodel inference and model averaging in behavioural ecology using Akaike’s information criterion. *Behavioral Ecology and Sociobiology*, **65**: 13-21.
APA  
3.	Whittingham, Mark J., et al. (2006) Why do we still use stepwise modelling in ecology and behaviour?. *Journal of animal ecology*, **75**: 1182-1189.

