---
layout: post
title: When Machines that Simulate Intelligence Seemed Like a Summer Project
author: Taro Langner
---

<p class="message">
    In this post: A look back at pioneering thoughts on AI research <br>
    <I>(7 min read)</I><br>
    
</p>

I recently stumbled upon a research proposal that must have raised a lot of eyebrows and received widespread attention in machine learning circles:

> _['We propose that a 2 month, 10 man study of artificial intelligence be carried out [...]. The study is to proceed on the basis of the conjecture that every aspect of learning or any other feature of intelligence can in principle be so precisely described that a machine can be made to simulate it. An attempt will be made to find how to make machines use language, form abstractions and concepts, solve kinds of problems now reserved for humans, and improve themselves. We think that a significant advance can be made in one or more of these problems if a carefully selected group of scientists work on it together for a summer.'](http://jmc.stanford.edu/articles/dartmouth/dartmouth.pdf)_

The summer in question was 1956, now almost seventy years ago.
The resulting [meeting at Dartmouth College](https://en.wikipedia.org/wiki/Dartmouth_workshop) in Hanover, New Hampshire, has often been called the time and place that established research on ‘artificial intelligence’ as a scientific field of its own.


Even today, [the research proposal](http://jmc.stanford.edu/articles/dartmouth/dartmouth.pdf) itself still makes for a fascinating read.
Many of its core themes remain remarkably relevant, whereas others played out in unexpected directions. This blog post is dedicated to some observations on how these pioneering thoughts from over two generations ago are reflected in the technological reality of today.

## The Conjecture

Just like in the hype of today, it would only take two years for the media to ascribe human-like intent, abilities and emotions to [early implementations](https://en.wikipedia.org/wiki/Perceptron#Mark_I_Perceptron_machine
) of these research concepts. 

The proposal itself, however, is remarkably sober. It largely avoids the notion of human-like machines that _are_ intelligent and instead explicitly aims for machines able to _simulate_ intelligence.

As one of the originators of the proposal, [Marvin Minsky](https://en.wikipedia.org/wiki/Marvin_Minsky)
proposes how the actions of a machine _“[...] would seem rather clever, and the behaviour would have to be regarded as rather ‘imaginative’.”_ if it was designed to build an internal, abstract model of its environment in which to first explore solutions to a given task before taking action.

Nowadays, there is an ongoing debate about whether multi-modal LLMs form an internal ‘world model’ that mirrors this idea. And it is not the only concept that rings surprisingly familiar from the discourse of today. The proposal specifically lists seven major themes to be examined towards its goal.


## Aspects of the Artificial Intelligence Problem

**1. Automatic Computers**
are proposed as able to simulate the behaviour of any machine, and ultimately even higher functions of the human brain, limited mainly by lack of efficient algorithms rather than computing resources.

Looking back today, the jury is still out on the first half of this point and it seems unclear as to whether it will ever be attained. But especially the second part of this assertion turned out exactly opposite to what was proposed here, with the [‘Bitter Lesson’](http://www.incompleteideas.net/IncIdeas/BitterLesson.html) by Rich Sutton concluding that, in general, increasing computing power has proven far more impactful than clever design of algorithms.


**2. How can a computer be programmed to use a language**
and perform reasoning based on words, forming sentences that imply one another and resemble human thought?

Here, the field of natural language processing made substantial progress. Examples include techniques that allow for words to be encoded as embeddings, like [word2vec](https://arxiv.org/abs/1301.3781) and language models like [BERT](https://arxiv.org/pdf/1810.04805)
that can furthermore relate embedded words to one another. Today, LLMs can iterate on intermediate processing steps in natural language with techniques like [Chain-of-Thought](https://en.wikipedia.org/wiki/Prompt_engineering#Chain-of-thought), marketed outright as ‘reasoning’ with ‘thinking’ models.

**3. Neuron nets**
were proposed as a promising approach, to be arranged so as to form concepts.

This research direction, among all competing paradigms of the time, proved to be spot on and foreshadowed what would later become known as deep learning. The [McCulloch-Pitts neuron model](
https://en.wikipedia.org/wiki/Artificial_neuron#McCulloch%E2%80%93Pitts_(MCP)_neuron)
Had already been invented over a decade earlier. Arranging variants of this neuron model into network architectures with ever more layers would ultimately give rise to deep neural networks that enabled many of the most decisive capabilities within the field of AI research today.


**4. Theory of the size of a calculation**
was to be developed, to quantify the efficiency of calculations and the complexity of functions,

Later work on algorithmic time complexity and space complexity would explore these questions more deeply, from the sixties onwards. Concepts of information theory such as the [Minimum Description Length principle and Kolmogorov complexity](https://tensorlabbet.com/#MDL)
would furthermore be developed providing some theoretical backing to the power of machine learning with neural networks.

**5. Self-improvement**
was expected to be a defining theme of intelligence.

Here, the reality of today is somewhat mixed. Machine learning emerged as a sub-discipline of AI research, with algorithms designed to adapt to given data. Many methods feature some aspects of self-improvement. 

Generative adversarial networks (GANs) feature two competing networks, with one facilitating the training process of the other. In reinforcement learning, improvements occur dynamically from interaction with an (often simulated) environment. Online learning and related methods also see ongoing improvement, often used in recommender systems. Self-criticism in LLMs enables them to refine their outputs during inference time.

Nonetheless, as of today, it is still common for many methods to feature a distinct training phase, after which trainable parameters are locked or frozen before deployment. Capabilities for an exponentially compounding self-improvement across varied skill sets still appear out of reach for now.


**6. Abstractions**
formed by machines from sensory and other data were to be explored.

This point has seen substantial progress, like the ability to encode language and image data into relatable embeddings with models like [CLIP](https://arxiv.org/abs/2410.02746), which can also be used to control image generation with natural language via CLIP-guided denoising diffusion for image generation as with [Stable Diffusion](https://arxiv.org/abs/2112.10752).
Likewise, manipulation of the latent space learned by models powers other abstract capabilities, such as image inpainting with generative fill.

**7. Randomness and creativity**
were conjectured to be related, with injections of controlled randomness enabling orderly thinking to reach imaginative solutions.

This direction took a surprising turn, as the success of generative models caught even many experts off guard. Randomness indeed turned out to be an important factor, from the randomized noise that serves as input to image generators like GANs and Stable Diffusion to the temperature setting in LLMs that controls how often less probable outputs are produced.

Creativity was long considered a defining trait that separated humans from machines. Until recently, a prevailing line of thinking was therefore that machines could eventually automate all menial and administrative tasks and give humans the leisure to socialize and pursue poetry, music, arts and crafts.

Chances are that the originators of the Dartmouth proposal would have been stunned by haikus generated with LLMs, images from Stable Diffusion, videos from Leo or music from Suno. When looking at the results of [all that put together](https://www.youtube.com/watch?v=EICWYazyqu4), they may have in fact wanted to row things back.



## Conclusion

For many of these ideas, it might be still too early to make a final call, as the ultimate goals of the proposal have arguably still not been fully attained. With time, some approaches that are hyped today may well seem like dead ends in hindsight, whereas others will seem obvious.

There is much more to the document yet than can be unpacked here, and this does not even include the individual proposals by its originators, 
[John McCarthy](https://en.wikipedia.org/wiki/John_McCarthy_(computer_scientist)),
[Marvin Minsky](https://en.wikipedia.org/wiki/Marvin_Minsky),
[Nathaniel Rochester](https://en.wikipedia.org/wiki/Nathaniel_Rochester_(computer_scientist)) and
[Claude Shannon](https://en.wikipedia.org/wiki/Claude_Shannon). Many more big names were ultimately involved in this summer project, but all that may well warrant another blog post in the future.