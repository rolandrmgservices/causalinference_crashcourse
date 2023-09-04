# Various Notebooks
Here I have listed various notebooks, each making a specific point about causal inference. They are currently not organized, but I hope to organize them into the following themes:
* Causal ML DML and Otherwise;
* Experimental Analysis and Deep Diving Treatment Effects;
* General Points about Estimating Treatment Effect Models; and
* How Data Cleaning and Manipulation Affect Results



<hr style="border:5px solid red">
**Note that the below information is not updated regularly, and I cannot guarantee that links still work.**
# ML Info and Causality Review

## Causality Review
Causal problems can be reframed around the problem of not observing the potential outcomes of a given unit under treatment and control status. That is, we only see their outcome under treatment or control status, but not both. Learn more about potential outcomes [here](https://youtu.be/q8x9aetyok0) and the fundamental problem of causal inference [here](https://youtu.be/RGvI0uVMgtw).

For a review of the conditional independence assumption AKA unconfoundedness, you can watch [these for an intuitive](https://www.youtube.com/watch?v=XJrTIsy_2Mk&list=PLwJRxp3blEvaxmHgI2iOzNP6KGLSyd4dz&index=61) explanation. Here is a [paper](https://www.kellogg.northwestern.edu/faculty/research/researchdetail?guid=aabd515d-67f4-11eb-a9b5-0242ac160003) that also finds limitations of propensity-based models, and that running experiments should continue to be the gold standard for inference.

2017 AEA Continuing Education Webcast on [“Mastering Mostly Harmless”](https://www.aeaweb.org/conference/cont-ed/2017-webcasts), with a summary of each video:
1. Causality, Potential Outcomes, and the Estimation of Treatment Effects in Randomized Studies (Abadie), including Fisher’s Exact Test
2. Regression (Angrist)
3. IV Regression, Part 1 (Angrist)
4. IV Regression, Part 2 (Angrist)
5. Matching and Propensity Scores (Abadie)
6. Difference-in-Difference and Synthetic Control (Abadie)
7. Regression Discontinuity (Walters)
8. Structural Selection Models (Walters)
9. Bayesian and ML (Walters) - Note this is “ML-lite” for econometrics, mostly just Lasso 



## Causal ML / Heterogeneous Treatment Effects

Esther Duflo has a [high-level overview](https://conference.nber.org/conf_papers/f114791.slides.pdf) of how ML and econometrics can mix.  The linked slides touch on material covered below. Please note that “real” ML is not just running a lasso regression.

### Multiple Hypothesis Testing

Heterogeneous treatment effects broadly run a multiple hypothesis testing problem. For example, suppose there are 100 individual level treatment effects estimated. Then 5\% of them should be statistically significant at the 95\% level due to random chance. You can think of this as the False Discovery Rate (FDR). It is not clear how to address this problem, but here are some things to think about:
1. [Alpha-investing](http://www-stat.wharton.upenn.edu/~stine/research/mfdr.pdf) by Foster and Stine )
2. FRD by Efron and Hastie’s [Computer Age and Statistical Inference](https://web.stanford.edu/~hastie/CASI_files/PDF/casi.pdf) Chapter 15.

Here is also a good chapter on understanding statistical power from [Andrew Gelman's book](http://www.stat.columbia.edu/~gelman/stuff_for_blog/chap20.pdf). 


### Feature Selection and High Dimensionality

One of the ways ML informs causal work is feature selection. The risk of having too many features is overfitting. Related to this is that often datasets are “high dimensional.” There is no set definition of “high dimensional” but scientists often refer to the sample size (*N)* and how many features/covariates there are (*P*). The challenge is that ML models can do feature selection, but they cannot be directly. used for inference.
[Belloni, Chernozhukov, and Hansen (2014)](https://www.aeaweb.org/articles?id=10.1257/jep.28.2.29) and [Belloni and Chernozhukov (2013)](https://projecteuclid.org/journals/bernoulli/volume-19/issue-2/Least-squares-after-model-selection-in-high-dimensional-sparse-models/10.3150/11-BEJ410.full) propose using LASSO regressions to do feature selection, after which another OLS is run for inference. The advantage of LASSO is that there is only one hyperparameter to tune. Other ML models like random forests, neural nets, etc. can be used, but they have many more hyperparameters. This of course comes as the cost of LASSO’s accuracy relative to other models.


## Double Machine Learning 

The [double machine learning paper](https://arxiv.org/abs/1608.00060) which I recommend you read in its entirety. I have encountered many scientists who do not know about the interactive regression model. Note that DML is not a novel technique, it is essentially the [Frisch-Waugh-Lovell theorem](https://en.wikipedia.org/wiki/Frisch%E2%80%93Waugh%E2%80%93Lovell_theorem). Whenever I review it, I also find myself needing to review the difference between ATE and ATET, which Newey has a good [memo](https://ocw.mit.edu/courses/economics/14-386-new-econometric-methods-spring-2007/readings/treatment_effect.pdf) about. 
Here is a [good set of slides](https://scholar.princeton.edu/sites/default/files/bstewart/files/felton.chern_.slides.20190318.pdf) for describing DML. 
There are several extensions of the DML framework for estimating HTE. I would check out these: [SGCT](https://arxiv.org/abs/1712.09988), and [Kennedy](https://arxiv.org/abs/2004.14497). There is a ML-model “free” model, [Generic ML Inference](https://arxiv.org/abs/1712.04802), which like Double Machine Learning, is agnostic to what sort of ML model you use. It also provides some metrics to assess whether the heterogeneity is valid.

## Causal Forest / Generalized Random Forest

There are two papers, which you should read sequentially. First is the [Causal Forest](https://arxiv.org/abs/1510.04342) which gives a high-level understanding, and second is the [Generalized Random Forest](https://arxiv.org/abs/1610.01271), which is more up to date. An optional third paper is [Local Linear Forests](https://arxiv.org/abs/1807.11408), which extends generalized random forests with local linear regressions. 

## Deep Neural Nets

[Farrell et al](https://arxiv.org/abs/1809.09953). have a paper on this, where the main contribution is the inference result.

### Elements of Statistical Learning Book

You should start with either the _Element of Statistical Learning Book_ or _Introduction to Statistical Learning_ before diving into the other ML topics listed below. These will give you a strong foundation to build upon the specialized topics. If you jump right into the deep topics, you will be lost in terms of notation and the big picture.

Available at [here](https://web.stanford.edu/~hastie/Papers/ESLII.pdf). 
I would start with Chapters 3 and 4 to see how ML views OLS and linear regressions, and jump to Chapter 7 to understand cross-validation. You’ll see a lot of people using random forests (Chapter 15 and 16) and boosted regressions (Chapter 10). 

### Introduction to Statistical Learning
Available at: [here](https://static1.squarespace.com/static/5ff2adbe3fe4fe33db902812/t/6062a083acbfe82c7195b27d/1617076404560/ISLR%2BSeventh%2BPrinting.pdf).
Sections 2.2 and 3.3.2 have brief sections on prediction intervals, and why we should care about them instead of confidence intervals.

### Deep Learning

[Goodfellow, Bengio, and Courville](https://www.deeplearningbook.org/) is a good resource for learning more about neural networks as a specialized ML topic.

### Reinforcement Learning

[Sutton and Barto’s Book](http://incompleteideas.net/book/the-book.html) and Stanford’s undergrad CS234 available on [YouTube](https://www.youtube.com/watch?v=FgzM3zpZ55o). RL is where you will also hear about ‘bandit models,’ and can be thought of an extension of the dynamic programming problems taught in Econ graduate courses, where the Bellman equation needs to be optimized with a policy functions.





