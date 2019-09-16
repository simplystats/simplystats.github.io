---
title: Example post
author: jeff
layout: post
comments: true
---

Editor's note this is a guest post by ... 

# Practical tips for RL engineering
Learning from experiences and the associated rewards or punishments is the core idea behind **reinforcement learning** (**RL**). In RL, the model trains from experience rather than labeled data. Instead of providing the model with the correct actions, we provide it with rewards and punishments. The model receives information about the current state of the environment, for example, the computer game screen. It then outputs an action, such as a joystick movement. The environment reacts to this action and provides the next state, along with any rewards.

_This is an excerpt from the book [Machine Learning for Finance](https://www.packtpub.com/big-data-and-business-intelligence/machine-learning-finance?utm_source=simplystatistics&utm_medium=referral&utm_campaign=Outreach_PEN) written by Jannes Klaas. This book introduces the study of machine learning and deep learning algorithms for financial practitioners._

RL allows us to learn sophisticated decision-making rules while having no data at all. RL is the go-to techniques if no supervised learning is possible, but a reward signal is available. In this article section, we will be introducing some practical tips for building RL systems. We will also highlight some current research frontiers that are highly relevant to financial practitioners. 

## Designing good reward functions

Reinforcement learning is the field of designing algorithms that maximize a reward function. But creating good reward functions is surprisingly hard, as everyone who has ever managed people knows. People game the system and machines do, too. The literature on RL is full of examples of researchers finding bugs in Atari games that had been hidden for years by an agent exploiting it. In the game "Fishing" for example, OpenAI has reported a reinforcement learning agent achieving a higher score than is possible according to the game makers—without catching a single fish.

While it is fun for games, such behavior can be dangerous when happening in financial markets. An agent trained on maximizing returns from trading, for example, could resort to illegal trading activities such as spoofing trades, without its owners knowing about it. There are three methods to create better reward functions:

### Careful, manual reward shaping

By manually creating rewards, practitioners can help the system to learn. This works especially well if the natural rewards of the environment are sparse. If, say, a reward is usually only given if a trade is successful, and this is a rare event, it helps to manually add a function that gives a reward if the trade was nearly successful. Equally, if an agent is engaging in illegal trading, a hard-coded "robot policy" can be set up that gives a huge negative reward to the agent if it breaks the law. Reward shaping works if the rewards and the environment are relatively simple. In complex environments, it can defeat the purpose of using machine learning in the first place. Creating a complex reward function in a very complex environment can be just as big a task as writing a rule-based system acting in the environment.

Yet, especially in finance, and especially in trading, hand-crafted reward shaping is useful. Risk-averse trading is an example of creating a clever objective function. Instead of maximizing the expected reward, risk-averse reinforcement learning maximizes an evaluation function, u, which is an extension of the utility-based shortfall to a multistage setting:

<p align="center"><img src="https://github.com/packtpartner/simplystats.github.io/blob/master/public/image1.png"; alt="Equation 1" /></p>

Here _u_ is a concave, continuous, and strictly increasing function that can be freely chosen according to how much risk the trader is willing to take. The RL algorithm now maximizes as follows:

<p align="center"><img src="https://github.com/packtpartner/simplystats.github.io/blob/master/public/image2.png"; alt="Equation 2" /></p>

### Inverse reinforcement learning

In **inverse reinforcement learning** (**IRL**), a model is trained to predict the reward function of a human expert. A human expert is performing a task, and the model observes states and actions. It then tries to find a value function that explains the human expert's behavior. More specifically, by observing the expert, a policy trace of states and actions is created. One example is the maximum likelihood IRL algorithm which works as follows:

1.	Guess a reward function, _R_.
2.	Compute the policy, 𝜋, that follows from _R_, by training an RL agent.
3.	Compute the probability that the actions observed, _D_, were a result of 𝜋, _p_(_D_|𝜋).
4.	Compute the gradient with respect to _R_ and update it.
5.	Repeat this process until _p_(_D_|𝜋) is very high.

### Learning from human preferences

Similar to IRL, which produces a reward function from human examples, there are also algorithms that learn from human preferences. A reward predictor produces a reward function under which policy is trained. The goal of the reward predictor is to produce a reward function that results in a policy that has a large human preference. Human preference is measured by showing the human the results of two policies and letting the human indicate which one is more preferable:

<p style="text-align:center"><p align="center"><img src="https://github.com/packtpartner/simplystats.github.io/blob/master/public/image3.png"; alt="Figure 1" /></p>

<p align="center">Figure 1: Learning from preferences.</p>

## Robust RL

Much like for GANs, RL can be fragile and can be hard to train for good results. RL algorithms are quite sensitive to hyperparameter choices. But there are a few ways to make RL more robust:

- **Using a larger experience replay buffer**: The goal of using experience replay buffers is to collect uncorrelated experiences. This can be achieved by just creating a larger buffer or a whole buffer database that can store millions of examples, possibly from different agents.
- **Target networks**: RL is unstable in part because the neural network relies on its own output for training. By using a frozen target network for generating training data, we can mitigate problems. The frozen target network should be updated only slowly by, for example, moving the weights of the target network only a few percent every few epochs in the direction of the trained network.
- **Noisy inputs**: Adding noise to the state representation helps the model generalize to other situations and avoids overfitting. It has proven especially useful if the agent is trained in a simulation but needs to generalize to the real, more complex world.
- **Adversarial examples**: In a GAN-like the setup, an adversarial network can be trained to fool the model by changing the state representations. The model can, in turn, learn to ignore the adversarial attacks. This makes learning more robust.
- **Separating policy learning from feature extraction**: The most well-known results in reinforcement learning have learned a game from raw inputs. However, this requires the neural network to interpret, for example, an image by learning how that image leads to rewards. It is easier to separate the steps by, for example, first training an autoencoder that compresses state representations, then training a dynamics model that can predict the next compressed state, and then training a relatively small policy network from the two inputs.

Similar to the GAN tips, there is little theoretical reason for why these tricks work, but they will make your RL work better in practice.

# Frontiers of RL
You have now seen some practical tips using RL techniques. Yet, RL is a moving field. This article cannot cover all current trends that might be interesting to practitioners, but it can highlight some that are particularly useful for practitioners in the financial industry.

## Multi agent RL
Markets, by definition, include many agents. Lowe and others, 2017, _Multi-Agent Actor-Critic for Mixed Cooperative-Competitive Environments_ (see [https://arxiv.org/abs/1706.02275](https://arxiv.org/abs/1706.02275)), shows that reinforcement learning can be used to train agents that cooperate, compete, and communicate depending on the situation.

<p align="center"><img src = "https://github.com/packtpartner/simplystats.github.io/blob/master/public/image4.png"; alt="Figure 2" /></p>
<p align="center">Figure 2: Multiple agents (in red) working together to chase the green dots. From the OpenAI blog</p>

In an experiment, Lowe and others let agents communicate, by including a communication vector into the action space. The communication vector one agent outputted was then made available to other agents. They showed that the agents learned to communicate to solve a task. Similar research showed that agents adopted collaborative or competitive strategies based on the environment. 

In a task where the agent had to collect reward tokens, agents collaborated as long as plenty of tokens were available and showed competitive behavior as tokens got sparse. 

## Learning how to learn

A shortcoming of deep learning is that skilled humans have to develop neural networks. Because of that, a longstanding dream of researchers and companies having to pay PhDs is to automate the process of designing neural networks. 
One example of this so-called Auto-ML is the **neural evolution of augmenting topologies**, **NEAT**, algorithm. NEAT uses an evolutionary strategy to design a neural network that is then trained by standard backpropagation:

<p align="center"><img src = "https://github.com/packtpartner/simplystats.github.io/blob/master/public/image5.png"; alt="Figure 3" /></p>
<p align="center">Figure 3: A network developed by the NEAT algorithm.</p>

As you can see in the preceding diagram, the networks developed by NEAT are often smaller than traditional, layer-based neural nets. They are hard to come up with. This is the strength of AutoML, it can find effective strategies that humans would not have discovered. 

An alternative to using evolutionary algorithms for network design is to use reinforcement learning, which yields similar results. There are a couple "off-the-shelf" AutoML solutions:

- **tpot** ([https://github.com/EpistasisLab/tpot](https://github.com/EpistasisLab/tpot)): This is a data science assistant that optimizes machine learning pipelines using genetic algorithms. It is built on top of scikit-learn, so it does not create deep learning models but models useful for structured data, such as random forests.
- **auto-sklearn** ([https://github.com/automl/auto-sklearn](https://github.com/automl/auto-sklearn)): This is also based on scikit-learn but focuses more on creating models rather than feature extraction.
- **AutoWEKA** ([https://github.com/automl/autoweka](https://github.com/automl/autoweka)): This is similar to auto-sklearn, except that it is built on the WEKA package, which runs on Java.
- **H2O AutoML** ([http://docs.h2o.ai/h2o/latest-stable/h2o-docs/automl.html](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/automl.html)): This is an AutoML tool that is part of the H2O software package, which provides model selection and ensembling.
- **Google cloud AutoML** ([https://cloud.google.com/automl/](https://cloud.google.com/automl/)): This is currently focused on pipelines for computer vision.

For the subfield of hyperparameter search, there are a few packages available as well:

- **Hyperopt** ([https://github.com/hyperopt/hyperopt](https://github.com/hyperopt/hyperopt)): This package allows for distributed, asynchronous hyperparameter search in Python.
- **Spearmint** ([https://github.com/HIPS/Spearmint](https://github.com/HIPS/Spearmint)): This package is similar to Hyperopt, optimizing hyperparameters but using a more advanced Bayesian optimization process.
AutoML is still an active field of research, but it holds great promise. Many firms struggle to use machine learning due to a lack of skilled employees. If machine learning could optimize itself, more firms could start using machine learning.

## Understanding the brain through RL

The other emerging field in finance and economics is behavioral economics. But recently, reinforcement learning has been used to understand how the human brain works. Wang and others, 2018, _Prefrontal cortex as a meta-reinforcement learning system_ (see [http://dx.doi.org/10.1038/s41593-018-0147-8](http://dx.doi.org/10.1038/s41593-018-0147-8)), for example, derive new insights into the frontal cortex and the function of dopamine.

Similarly, Banino and others, 2018, _Vector-based navigation using grid-like representations in artificial agents_ (see [https://doi.org/10.1038/s41586-018-0102-6](https://doi.org/10.1038/s41586-018-0102-6)), replicate so-called "grid cells" that allow mammals to navigate using reinforcement learning.

The method is similar: Both papers train RL algorithms on tasks related to the area of research, for example, navigation. They then examine the learned weights of the model for emergent properties. Such insight can be used to create more capable RL agents but also to further the field of neuroscience. 

As the world of economics gets to grips with the idea that humans are not rational, but irrational in predictable ways, understanding the brain becomes more important to understand economics. The results of neuroeconomics are particularly relevant to finance as they deal with how humans act under uncertainty, deal with risk why humans are loss averse. Using RL is a promising avenue to yield further insight into human behavior.

# Summary

In this article, we learned some practical tips for RL engineering. We looked into how we can make RL robust. You also looked into the direction of current research and how you can benefit from this research today. To know more about the practicalities of developing, debugging, and deploying machine learning systems, pick a copy of book [_Machine Learning for Finance_](https://www.packtpub.com/big-data-and-business-intelligence/machine-learning-finance?utm_source=simplystatistics&utm_medium=referral&utm_campaign=Outreach_PEN), by _Jannes Klaas_. 

# About the Author

Jannes Klaas is a quantitative researcher with a background in economics and finance. He taught machine learning for finance as lead developer for machine learning at the Turing Society, Rotterdam. He has led machine learning bootcamps and worked with financial companies on data-driven applications and trading strategies.
Jannes is currently a graduate student at Oxford University with active research interests including systemic risk and large-scale automated knowledge discovery.


