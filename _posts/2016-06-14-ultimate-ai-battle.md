---
author: roger
comments: true
layout: post
title: Ultimate AI battle - Apple vs. Google
---

Yesterday, Apple launched its Worldwide Developer's Conference (WWDC) and had its public keynote address. While many new things were announced, the one thing that caught my eye was the [dramatic expansion](http://go.theinformation.com/HnOAdA6DQ7g) of Apple's use of artificial intelligence (AI) tools. I talked a bit about AI with Hilary Parker on the latest [*Not So Standard Deviations*](http://simplystatistics.org/2016/06/09/nssd-episode-17/), particularly in the context of Amazon's Echo/Alexa, and I think it's definitely going to be an area of intense competition between the major tech companies.

Pretty much every major tech player is involved in AI--Google, Facebook, Amazon, Apple, Microsoft--the list goes on. Recently, a [some commentators](https://marco.org/2016/05/21/avoiding-blackberrys-fate) have suggested that Apple in particular will never catch up with the likes of Google with respect to AI because of Apple's strict stance on privacy and unwillingness to gather/aggregate data from all its users. However, yesterday at WWDC, Apple revealed a few clues about what it was up to in the AI world. 

First, Apple mentioned deep learning more than a few times, including specifically calling out its use of [LSTM](https://en.wikipedia.org/wiki/Long_short-term_memory) in its Messages app and facial recognition in its Photos app. Previously, Apple had been rumored to be applying deep learning to its [Siri assistant and its fingerprint sensor](http://go.theinformation.com/4Z2WhEs9_Nc). At WWDC, Craig Federighi stressed Apple's continued focus on privacy and how Apple does not need to develop "user profiles" server-side, but rather does most computation on-device (in this case, on the iPhone). 

However, it can't be that Apple does all its deep learning computation on the iPhone. These models tend to be enormous and take advantage of reams of data that can only be reasonablly processed server-side. Unfortunately, because most companies (Apple in particular) release few details about what they do, we may never how this works. But we can definitely speculate!

## Apple vs. Google

I think the Apple/Google dichotomy provides an interesting opportunity to talk about how models can be learned using data in different ways. There are two approaches being represented here by Apple and Google:

* **Google way** - Collect lots of data from users and store them on a server in the Googleplex somewhere. Then use that data to fit an enormous model that can predict when you've taken a picture of a cat. As users generate more data, bring that data back to the Googleplex and update/refine the model.
* **Apple way** - Build a "starter model" in the Apple [Mothership](http://9to5mac.com/2015/10/05/spaceship-campus-2-drone-video-october/). As users generate data on their phones, bring the model to the phone and update the model using just their data. Bring the updated model back to the Apple Mothership and leave the user's data on the phone.

Perhaps the easiest way to understand this difference is with the arithmetic mean, which is perhaps the simplest "model". There are two ways you can think about computing the arithmetic mean of a bunch of numbers $X_1, X_2, X_2,\dots,X_n$.

![Google way](https://raw.githubusercontent.com/simplystats/simplystats.github.io/master/_images/googleway.png)


![Apple way](https://raw.githubusercontent.com/simplystats/simplystats.github.io/master/_images/appleway.png)



I do not do any work anywhere close to the AI field (beyond the fact that AI is related to statistics) but it 



* Description at a high level because I am not an expert in AI, Deep Learning, etc.
* Fusion science: Big Data = Prior, Small Data = Likelihood
* Thin client, Big Server vs. Fat Client, Big Server
* Examples:
	* Updating the mean one observation at a time (prior/posterior)
	* Updating a linear model one observation at a time.
* 

