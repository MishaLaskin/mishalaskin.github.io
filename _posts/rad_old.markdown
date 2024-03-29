---
permalink: /rad/
layout: post
title:  "Reinforcement Learning with Augmented Data"
date:   2020-04-24 11:10:11 -0800
image: /images/rad/rad_thumbnail.png
categories: research
affiliation: UC Berkeley, BAIR
authors: "<b>Michael Laskin*</b>, Kimin Lee*, Adam Stooke,<br>Lerrel Pinto, Pieter Abbeel, Aravind Srinivas"
venue: "In Submission"
code: https://github.com/MishaLaskin/rad
arxiv: https://arxiv.org/abs/2004.14990
equal: '*'
press: https://venturebeat.com/2020/05/02/uc-berkeley-researchers-open-source-rad-to-improve-any-reinforcement-learning-algorithm/
twitter: https://twitter.com/MishaLaskin/status/1257001857043529729

---


First extensive study of image augmentation in the RL setting. Showed that simple RL algorithms with augmented data achieve SOTA results on many common RL benchmarks.


Learning from visual observations is a fundamental yet challenging problem in reinforcement learning (RL). Although algorithmic advancements combined with convolutional neural networks have proved to be a recipe for success, current methods are still lacking on two fronts: (a) sample efficiency of learning and (b) generalization to new environments. To this end, we present RAD: Reinforcement Learning with Augmented Data, a simple plug-and-play module that can enhance any RL algorithm. We show that data augmentations such as random crop, color jitter, patch cutout, and random convolutions can enable simple RL algorithms to match and even outperform complex state-of-the-art methods across common benchmarks in terms of data-efficiency, generalization, and wall-clock speed. We find that data diversity alone can make agents focus on meaningful information from high-dimensional observations without any changes to the reinforcement learning method. On the DeepMind Control Suite, we show that RAD is state-of-the-art in terms of data-efficiency and performance across 15 environments. We further demonstrate that RAD can significantly improve the test-time generalization on several OpenAI ProcGen benchmarks. Finally, our customized data augmentation modules enable faster wall-clock speed compared to competing RL techniques.

<center>
<img src="/images/rad/rad_teaser.png" alt="" style="width:80%;"/>
</center>


## Method 

In our paper, we show how data augmentation improves performance and generalization abilities of standard RL algorithms, both on and off-policy. We combine data augmentation with (i) Soft Actor Critic (SAC) for solving tasks on DeepMind control and (ii) PPO for ProcGen environments. Our method does not change the underlying RL pipeline - it only augments the underlying data. 

## Results

(1) <b>RAD is the state-of-the-art algorithm</b> on the majority (<b>5</b> out of <b>6</b>) extensively benchmarked environments on both DMControl100k and DMControl500k benchmarks, matching or outperforming CURL, Dreamer, PlaNet, SLAC, SAC+AE, and Pixel SAC.

(2) RAD quickly <b>matches state based performance</b> on the majority (<b>11</b> out of <b>15</b>) of DeepMind control algorithms. It also performs comparably to or better than the prior state of the art algorithm for data efficiency - [CURL](https://mishalaskin.github.io/rad). 

<center>
<img src="/images/rad/rad_all_dmc.png" alt="" style="width:80%;"/>
</center>-

(3) <b>Random crop</b>, stand-alone, <b>has the highest impact</b> on final performance relative to all other augmentations on DeepMind control. We ablate pair-wise permutations of 6 common augmentations and measure the performance of walker, walk at 500k environments steps. While all data augmentations help, random crop alone results in the highest performance.

<center>
<img src="/images/rad/rad_walker_ablation.png" alt="drawing" style="width:80%;"/>
</center>

(4) <b>RAD achieves state-of-the-art test-time generalization</b> on ProcGen environments like BigFish and StarPilot. Again, RAD with random crop <b>achieves 55.8% relative gain</b> to pixel-based PPO in the BigFish environment. 

(5) RAD trained with 100 training levels outperforms the pixel-based PPO trained with 200 training levels on both BigFish and StarPilot environments. This shows that data augmentation can be more effective in learning generalizable representations compared to simply increasing the number of training environments.

<center>
<img src="/images/rad/rad_big_fish.png" alt="drawing" style="width:80%;"/>
</center>

(5) Random crop fails in environments that require structural generalization (e.g. adapting to new map layout) like Jumper and CoinRun. However, color augmentation like random convolution and color jitter still improve test-time performance on environments like CoinRun. 

<center>
<img src="/images/rad/rad_coin_run.png" alt="drawing" style="width:80%;"/>
</center>

## Why is random crop so effective?

To understand why random crop works so well on DeepMind control, we inspect spatial attention maps across the convolutional encoder for policies learned with all of the various augmentations, including the no augmentation baseline. We notice that random crop help the encoder localize the agent more accurately and reliably than the other augmentations on DeepMind control. In particular, while other augmentations also pay attention to distractors (e.g. stars in the background) or fail to capture the agent state, the policy learned with random crop crisply and reliably extracts the agent from the frame. This suggests that spatial observation jittering helps develop the base agent develop contingency awareness.

<center>
<img src="/images/rad/rad_why_crop.png" alt="drawing" style="width:80%;"/>
</center>


## BibTex
<pre>
@unpublished{laskin_lee2020rad,
  title={Reinforcement Learming with Augmented Data},
  author={Laskin, Michael and Lee, Kimin and Stooke, Adam and Pinto, Lerrel and Abbeel, Pieter and Srinivas, Aravind},
  note={arXiv:2004.14990}
}
</pre>


