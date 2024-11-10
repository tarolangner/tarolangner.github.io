---
layout: post
title: The Lost Reading Items
author: Taro Langner
---

<p class="message">
    In this post: An attempt to reconstruct Ilya Sutskever's 2020 AI reading list <br>
    <I>(8 min read)</I><br>
    
</p>

I recently [shared a summary](https://tensorlabbet.com/2024/09/24/ai-reading-list/) of a [viral AI reading list](https://arc.net/folder/D0472A20-9C20-4D3F-B145-D2865C0A9FEE) attributed to Ilya Sutskever, which laid claim to covering ‘*90% of what matters*’ back in 2020. It boils down the reading items to barely one percent of the original word count to form the TL;DR I would have wished for before reading. 

The viral version of the list as shared online is known to be incomplete, however, and includes [only 27](https://x.com/andrew_n_carr/status/1752526711311507526) of [about 40](https://dallasinnovates.com/exclusive-qa-john-carmacks-different-path-to-artificial-general-intelligence/?utm_source=www.turingpost.com&utm_medium=referral&utm_campaign=the-mysterious-ai-reading-list-ilya-sutskever-s-recommendations) original reading items.
The rest [allegedly](https://news.ycombinator.com/item?id=34641359) fell victim to the E-Mail deletion policy at OpenAI. These missing reading items have inspired some good discussions in the past, with many different ideas as to which papers would have been important enough to include.

This post is an attempt to identify these lost reading items. It builds on clues gathered from the viral list, contemporary presentations given by Ilya Sutskever, resources shared by OpenAI and more. 

# Filling the Gaps

The main piece of evidence is [a claim shared along with the list](https://x.com/andrew_n_carr/status/1752526711311507526) according to which an entire selection of *meta-learning* papers was lost. 

Meta-learning is often said to pursue *‘learning to learn’*, with neural networks being trained for a general ability to adapt more easily to new tasks for which only few training samples are available. A network should thus be able benefit from its existing weights without requiring an entirely new training from scratch on the new data. *One-shot learning* provides just a single training sample to a model from which it is expected to learn a new downstream task, whereas *zero-shot* settings provide no annotated training samples at all.

For some of the candidate papers listed below, the case can be strengthened further by evidence in the form of an endorsement straight from OpenAI itself. Ilya Sutskever was chief scientist at a time when OpenAI published the educational resource ['Spinning Up in Deep RL'](https://spinningup.openai.com/en/latest/index.html) which includes several of these candidates in an entirely separate reading list of 105 [‘Key Papers in Deep RL’](https://spinningup.openai.com/en/latest/spinningup/keypapers.html#meta-rl). Below, the papers which also appear in that list are marked with a symbol (⚛). 




## Clues from the Preserved Reading Items

Some meta-learning concepts can be found even in the known parts of the list.
The preserved reading items can be arranged into a narrative arc around a related branch of research on [Memory-Augmented Neural Networks (MANNs)](https://arxiv.org/abs/1410.3916). Following the [‘Neural Turing Machine’ (NTM)](https://tensorlabbet.com/2024/09/24/ai-reading-list/#NTM) paper, ['Set2Set'](https://tensorlabbet.com/2024/09/24/ai-reading-list/#Set2Set) and ['Relational RNNs'](https://tensorlabbet.com/2024/09/24/ai-reading-list/#RelationalRNN) experimented with external memory banks that an RNN could read and write information on. They directly cite or closely relate to several papers which may well have been part of the original list: 

**Potential Reading Items (Part 1):**

- ['Meta-learning with memory-augmented neural networks'](http://proceedings.mlr.press/v48/santoro16.pdf) <br>
*from 2016* 
<!-- <span style="color:gray">Adapts NTM for one-shot classification of [Omniglot](https://www.cs.cmu.edu/~rsalakhu/papers/LakeEtAl2015Science.pdf) characters</span> -->
- ['Prototypical networks for few-shot learning'](https://proceedings.neurips.cc/paper_files/paper/2017/file/cb8da6767461f2812ae4290eac7cbc42-Paper.pdf) <br> 
*from 2017* 
<!-- Learn embedding spaces for few- and zero-shot classification  -->
- ['Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks'](http://proceedings.mlr.press/v70/finn17a/finn17a.pdf)⚛ <br>
*from 2017*


## Clues from Contemporary Presentations

Certain papers about meta-learning and *competitive self-play* also feature repeatedly in a series of presentations held by Ilya Sutskever around this time and may well have eventually been included in the reading list too.

<p class="message">

<b>Recorded Presentations:</b> <br>

<a href="https://www.youtube.com/watch?v=BCzFs9Xb9_o">- Meta Learning and Self Play - Ilya Sutskever, OpenAI (YouTube)</a>, 2017 <br>
<a href="https://www.youtube.com/watch?v=AopSlxNYqX8">- OpenAI - Meta Learning & Self Play - Ilya Sutskever (YouTube)</a>, 2018 <br>
<a href="https://www.youtube.com/watch?v=9EN_HoEk3KY">- Ilya Sutskever: OpenAI Meta-Learning and Self-Play (YouTube)</a>, 2018 <br>
</p>


These presentations largely overlap and repeatedly reference known contents of the reading list. They open with a fundamental motivation of why deep learning works, framing backpropagation with neural networks as a search for *small circuits* that relate to the [Minimum Description Length principle](https://tensorlabbet.com/2024/09/24/ai-reading-list/#MDL), according to which the shortest program that can explain given data will reach the best generalization possible. 

Next, all three presentations reference the following meta-learning papers:

**Potential Reading Items (Part 2):**
- ['Human-level concept learning through probabilistic program induction'](https://amygdala.psychdept.arizona.edu/labspace/JclubLabMeetings/Lijuan-Science-2015-Lake-1332-8.pdf) <br> 
as *Lake et al., 2016*
- ['Neural Architecture Search with Reinforcement Learning'](https://arxiv.org/pdf/1611.01578) <br> 
as *Zoph and Le, 2017*
- ['A Simple Neural Attentive Meta-Learner'](https://arxiv.org/pdf/1707.03141)⚛ <br> 
as *Mishra et al., 2017*

Reinforcement Learning (RL) also features heavily in all three presentations, with close links to meta-learning. One key concept is *competitive self-play* in which agents interact in a simulated environment to reach specific, typically adversarial objectives. As a way to *‘turn compute into data’*, this approach enabled simulated agents to outperform human champions and invent new moves in rule-based games. Ilya Sutskever presents an evolutionary biology perspective that relates competitive self-play to the impact of social interaction on brain size [(pay-walled link)](https://www.science.org/doi/10.1126/science.1098410).
He goes on to suggest that rapid competence gain in a simulated *‘agent society’* may ultimately, according to his judgement, provide [a plausible path towards a form of AGI](https://www.youtube.com/watch?v=9EN_HoEk3KY&t=2325s). 

Given the significance he ascribes to these concepts, it seems plausible that some of the cited papers on self-play may have later also been included in the reading list. They may form a sizeable chunk of the missing items, especially as RL is otherwise mentioned by [only one](https://tensorlabbet.com/2024/09/24/ai-reading-list/#MachineSuperIntelligence) of the preserved reading items.

**Potential Reading Items (Part 3):**

- ['Hindsight Experience Replay'](https://proceedings.neurips.cc/paper_files/paper/2017/file/453fadbd8a1a3af50a9df4df899537b5-Paper.pdf)⚛ <br> 
as *Andrychowicz et al., 2017*
- ['Continuous control with deep reinforcement learning'](https://arxiv.org/abs/1509.02971)⚛ <br>
as *DDPG: Deep Deterministic Policy Gradients, 2015*
- ['Sim-to-Real Transfer of Robotic Control with Dynamics Randomization'](https://arxiv.org/abs/1710.06537) <br>
as *Peng et al., 2017* 
- ['Meta Learning Shared Hierarchies'](https://arxiv.org/abs/1710.09767) <br>
as *Frans et al., 2017*
- ['Temporal Difference Learning and TD-Gammon [1995]'](https://www.csd.uwo.ca/~xling/cs346a/extra/tdgammon.pdf) <br>
as *Tesauro et al., 1992*
- ['Karl Sims - Evolved Virtual Creatures, Evolution Simulation, 1994'](https://www.youtube.com/watch?v=JBgG_VSP7f8&t=2s) <br>
as *Carl Sims, 1994 (YouTube video [4:09])*
- ['Emergent Complexity via Multi-Agent Competition'](https://arxiv.org/abs/1710.03748) <br> 
as *Bansal et al., 2017*
- ['Deep reinforcement learning from human preferences'](https://arxiv.org/abs/1706.03741)⚛ <br> 
as *Christiano et al., 2017* (Note: Introduces RLHF)



Even today, these presentations from around 2018 are still worth watching. Next to fascinating bits of knowledge, they also include gems such as the statement:
> [‘Just like in the human world: The reason humans find life difficult is because of other humans’](https://www.youtube.com/watch?v=BCzFs9Xb9_o&t=2532s)
> <div style="text-align: right">-Ilya Sutskever </div>


While some concepts in computer science accordingly appear timeless, other points may seem surprising today, like the casual remark of an audience member in the Q&A session:
> ['It seems like an important sub-problem on the path to AGI will be understanding language, and the state of generative language modelling right now is pretty abysmal.’](https://www.youtube.com/watch?v=9EN_HoEk3KY&t=3082s) 
> <div style="text-align: right">-Audience member </div>

To which Ilya Sutskever responds:
> [‘Even without any particular innovations beyond models that exist today, simply scaling up models that exist today on larger datasets is going to go surprisingly far.’](https://www.youtube.com/watch?v=9EN_HoEk3KY&t=3106s)
> <div style="text-align: right">-Ilya Sutskever (in 2018)</div>

This response was later confirmed by experimental results in the reading item ['Scaling Laws for Neural Language Models'](https://tensorlabbet.com/2024/09/24/ai-reading-list/#ScalingLaws) (which echoes the ['Bitter Lesson'](http://www.incompleteideas.net/IncIdeas/BitterLesson.html) by Rich Sutton). It was ultimately proven true, as he would oversee Transformer architectures scaled up to [an estimated 1.8 trillion parameters and costing over $60 million to train on 128 GPUs](https://the-decoder.com/gpt-4-architecture-datasets-costs-and-more-leaked/) forming Large Language Models (LLMs) which are today capable of generating text that is increasingly difficult to distinguish from human writing.


# Honorable Mentions

Many other works and authors may have featured on the original list, but the evidence wears increasingly thin from here on. 

Overall, the preserved reading items manage to strike an impressive balance between covering different model classes, applications and theory while also including many famous authors of the field. Perhaps the exceptions to this rule are worth noting, even if they may have slipped among the *'10% of what matters'* that didn't make the original list.

As such, it would have seemed plausible to include:
- [Yann LeCun](https://en.wikipedia.org/wiki/Yann_LeCun) with [pioneering work on CNNs](https://hal.science/hal-03926082/document) for real-world use
- [Ian Goodfellow](https://en.wikipedia.org/wiki/Ian_Goodfellow) with [Generative Adversarial Networks (GANs)](https://proceedings.neurips.cc/paper_files/paper/2014/hash/5ca3e9b122f61f8f06494c97b1afccf3-Abstract.html) that dominated image generation at the time and
- [Demis Hassabis](https://en.wikipedia.org/wiki/Demis_Hassabis) for [RL research](https://daiwk.github.io/assets/dqn.pdf) towards [AlphaFold](https://ccsp.hms.harvard.edu/wp-content/uploads/2020/11/AlphaFold-at-CASP13-AlQuraishi.pdf) that earned a Nobel prize

# Conclusion

This post will remain largely speculative until more becomes known. After all, even the viral list itself was never officially confirmed to be authentic. Nonetheless, the potential candidates for the lost reading items listed above seemed worth sharing. Taken together, they may well fill a gap in the viral version of the list that would, in the words of the author, corresponded roughly to a missing _'30% of what matters'_ at its time.

