---
toc: true
layout: post
description: Small primer on Bayesian Hierarchical Models
categories: [markdown]
title: Hierarchical Models
---

# Hierarchical Models

## Books

### Forecasting: Principles and Practice - Hierarchical or Grouped Time Series
> [Forecasting: Principles and Practice - Chapter 10 Forecasting hierarchical or grouped time series](https://otexts.com/fpp2/hierarchical.html)

## Blog Posts

### Bayesian Methods for Multilevel Modelling
> [A Primer on Bayesian Methods for Multilevel Modeling](https://docs.pymc.io/notebooks/multilevel_modeling.html)

### Hierarchical Linear Regression in PyMC3
> [The best of both worlds: Hierarchical Linear Regression in PyMC3](https://twiecki.io/blog/2014/03/17/bayesian-glms-3/)

#### Introduction

Hierarchical modeling is especially advantageous when in the presence of multi-level data, making the most of all available information by it's "shrinkage-effect".
Software like [HDDM](https://github.com/hddm-devs/hddm) allows hierarchical Bayesian estimation of a widely used decision making model, but here we will use a classical example of hierarchical linear regression to predict [radon levels in houses](#Bayesian-Methods-for-Multilevel-Modelling).

Gelman et al.'s (2007) radon dataset is the canonical example for Bayesian Hierarchical Modelling. In the dataset  the amount of radiation has been measured amongst different households in all counties of several US States. Radon gas is known as the highest cause of lung cancer in non-smokers. It is believed to enter the house through the basement. Additionally its concentration differs regionally due to differences in soil type. 

The exercise is to attempt to predict radon levels in different counties and where in the house it was measured. 

Data Source: radon.csv  
Columns: _**county**_, _**log_radon**_, _**floor**_  
where floor = 0 is the basement, floor = 1 is the 1st floor, and so forth.

#### Single regression (pooled model)

A common way of solving this would be to pool all the data and estimate one regression to assess the influence of measurement across counties. The model would follow the following specification:

$$
radon_{i,c} = \alpha + \beta * floor_{i,c} + \epsilon
$$

where $i$ corresponds to the measurement, $c$ corresponds to the county and floor corresponds to which floor the measurement was made.
We then estimate a _single_ intercept and a _single_ slope for all measurements over all counties. We are assuming that all the counties are exactly the same.

#### Separate regressions (unpooled model)

Imagine however we were interested, for instance, in seeing the differences in relationship (slope) or base-rates of radon (intercept) across counties.
We could generate $n$ regressions, where $n$ is the number of counties. Such model would follow the following specification:

$$
radon_{i,c} = \alpha_c + \beta_c * floor_{i,c} + \epsilon_c
$$

Now, for every county $c$, we are estimating $\alpha_c$ and $\beta_c$, up to $n$ total counties.
In this version, the upooled version, we assume the extreme opposite of the former model. Instead of assuming all counties are exactly the same, we are assuming they share no similarities between them.

#### Hierarchical Regression

There is a middle ground between a fully pooled model and an unpooled model. It's a Hierarchical Model.  
Specifically, while we may assume that while $\alpha$s and $\beta$s are different for each county, they all come from a common group distribution:

$$
\alpha_c \sim \mathcal{N}(\mu_\alpha, \sigma^2_\alpha)
\\
\beta_c \sim \mathcal{N}(\mu_\beta, \sigma^2_\beta)
$$

Here the assumption is that the intercepts $\alpha$ and slopes $\beta$ all come from a normal distribution centered around their respective group mean $\mu$ with a certain standard deviation $\sigma^2$, values (posteriors) which we also estimate. 
It is for this reason that such a model is named Multilevel or Hierarchical.

Using Probabilistic Programming, with a framework like pyMC3, 


### Advanced Hierarchical Linear Regression in PyMC3
> [Why hierarchical models are awesome, tricky, and Bayesian](https://twiecki.io/blog/2017/02/08/bayesian-hierchical-non-centered/)

### HDDM Demo
> [HDDM Demo](http://ski.clps.brown.edu/hddm_docs/tutorial_python.html)

## Tools
> [htsprophet](https://github.com/CollinRooney12/htsprophet)
> [HDDM](https://github.com/hddm-devs/hddm)


## Extra Notes

[The Inference Button: Bayesian GLMs made easy with PyMC3](https://twiecki.github.io/blog/2013/08/12/bayesian-glms-1/)  
[This world is far from Normal(ly distributed): Bayesian Robust Regression in PyMC3](https://twiecki.github.io/blog/2013/08/27/bayesian-glms-2/)
