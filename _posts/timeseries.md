---
title: Time Series Analysis in Biomedical Science - What You Really Need to Know
author: roger
comments: true
layout: post
---

For a few years now I have given a guest lecture on time series analysis in our School's *Environmental Epidemiology* course. The basic thrust of this lecture is that you should generally ignore what you read about time series modeling, either in papers or in books.  The reason is because I find much of the time series literature is not particularly helpful when doing analyses in a biomedical or population health context, which is what I do almost all the time. 

## Prediction vs. Inference

First, most of the literature on time series models tends to assume that you are interested in doing prediction---forecasting future values in a time series. I almost am never doing this. In my work looking at air pollution and mortality, the goal is never to find the best model that predicts mortality. In particular, if our goal were to predict mortality, we would probably *never include air pollution as a predictor*. This is because air pollution has an inherently weak association with mortality at the population, whereas things like temperature and other seasonal factors tend to have a much stronger association. 

What I *am* interested in doing is estimating an association between changes in air pollution levels and mortality and making some sort of inference about that association, either to a broader population or to other time periods. The challenges in these types of analyses include estimating weak associations in the presence of many stronger signals and appropriately adjusting for any potential confounding variables that similarly vary over time.

The reason the distinction between prediction and inference is important is that focusing on one vs. the other can lead you to very different model building strategies. Prediction modeling strategies will always want you to include into the model factors that are strongly correlated with the outcome and explain a lot of the outcome's variation. If you're trying to do inference and use a prediction modeling strategy, you may make at least two errors:

1. You may conclude that your key predictor of interest (e.g. air pollution) is not important because the modeling strategy didn't deem to include it
2. You may omit important potential confounders because they have a weak releationship with the outcome (but maybe have a strong relationship with your key predictor). For example, one class of potential confounders in air pollution studies is other pollutants, which tend to be weakly associated with mortality but may be strongly associated with your pollutant of interest.

## Random vs. Fixed






