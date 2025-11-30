---
layout: post
title: It's Hard to Feel the AGI
author: Taro Langner
---

<p class="message">
    In this post: A reality check from leading researchers <br>
    <I>(6 min read)</I><br>
    
</p>

In the heat of the ongoing AI summer, a chilling effect is starting to spread from the growing cracks between marketing claims and the underlying technology. To a backdrop of comparisons with the dot com bubble, some of the most accomplished minds of the field are beginning to revise their projections for what can realistically be expected for the near future.

**[Ilya Sutskever](https://en.wikipedia.org/wiki/Ilya_Sutskever)** shared his view on [a recent podcast](https://www.dwarkesh.com/p/ilya-sutskever-2) that the current approach around transformer-based LLMs is likely to stall out in the coming years as the scaling paradigm hits a ceiling. He notes a remarkable discrepancy in their excellent performance in evaluations despite inadequate generalization and low economic impact in practice. He argues that fundamentally new research insights are needed to break through this plateau.

Moreover, he expresses doubts about the future profitability of the current business models around LLMs, despite massive potential revenues, due to lacking differentiation between competitors.
Ultimately, he revises his estimate for the emergence of systems with human-like learning abilities back by 5-20 years. His startup, *Safe Superintelligence Inc.*, is currently exploring research ideas that may identify viable new approaches towards this goal.

As former chief scientist of OpenAI, his doubts about the future direction and profitability of their business model should raise concerns. OpenAI plays a central role in what has been described as circular investment dealings related to enormous investments into hardware and data centers. The latter have been claimed to [account for over 90% of growth in US GDP](https://fortune.com/2025/10/07/data-centers-gdp-growth-zero-first-half-2025-jason-furman-harvard-economist/) over the first half of 2025.

They are now seeking unprecedented funding for future spending commitments, with controversy around their CFO publicly commenting on their financial innovations and seemingly floating the idea that [the US government could act as a financial backstop](https://fortune.com/2025/11/10/scott-galloway-nowhere-to-hide-ai-bubble-sam-altman/).


**[Andrej Karpathy](https://en.wikipedia.org/wiki/Andrej_Karpathy)** previously featured [on the same podcast](https://www.dwarkesh.com/p/andrej-karpathy)
and voiced a noteworthy critique of the current industry hype around LLM-based AI Agents. He argues that, while impressive, the technology still needs a decade of work and improvements. Only then could they hope to reach the promised level of performing like an automated employee or coworker, whereas currently *“they’re cognitively lacking and it’s just not working”*. 

He expects these systems to contribute to gradual economic growth within the ongoing, long-term compounding pattern seen ever since the onset of the industrial revolution rather than a sudden jump in GDP.

He compares this comparatively slow development to earlier ambitions around automating radiology and self-driving cars. Despite witnessing impressive demos for the latter already in 2014 and contributing as director of AI at Tesla, he argues that neither field reached this goal yet. He points out that current self-driving technology still requires human supervision and frequent manual intervention by remote operators. 

Development efforts over this decade instead faced diminishing returns, with ‘the march of nines’ in reliability requiring a constant amount of effort for the same relative reduction in errors. Ultimately, he revised ‘the year of agents’ to be ‘the decade of agents’ instead.

In the software industry, widespread reporting posits [AI and automation as the main cause for large-scale layoffs](https://fortune.com/2025/07/27/artificial-intelligence-skills-18000-salaries-28-percent/), but the degree of autonomy vs supervision that tools for agentic code generation require remains controversial. As an example, a recent study deployed frontier AI agent frameworks on projects sourced from online freelancing platforms with [a success rate of just 2.5%](https://arxiv.org/abs/2510.26787v1).



**[Rich Sutton](https://de.wikipedia.org/wiki/Richard_S._Sutton)** appeared [on the same podcast](https://www.dwarkesh.com/p/richard-sutton) in a rather contentious earlier episode to share his view that LLMs are a dead end in AI research.
He argues that, while surprisingly effective, LLMs have no internal ‘world model’ based on which they could explore potential actions and predict their outcomes, but instead merely mimic human use of language through imitation learning. He points out their lack of any actual goal towards which to take action as opposed to just mechanistically processing tokens. 

He notes that, whereas LLMs gain the ability for next-token prediction in a supervised learning phase, no such thing occurs in nature. Instead, he emphasizes their critical lack of continual learning abilities. According to his [‘Big World Hypothesis’](https://openreview.net/pdf?id=Sv7DazuCn8) the world is too complex for any agent to successfully navigate without this ability to adapt and learn from experience.

He mentions [Moravec’s Paradox](https://en.wikipedia.org/wiki/Moravec%27s_paradox), which contrasts the ease with which machines can imitate more highly evolved, specific cognitive tasks as opposed to their inability to perform lower-order, largely unconscious biological functions such as sensory, motorical and social skills.

He raises conceptual limitations of deep learning and gradient descent for generalization. While he considers machine superintelligence as ultimately inevitable, he also highlights that even the intelligence exhibited by a squirrel remains fundamentally beyond our current understanding.



**[Yann LeCun](https://en.wikipedia.org/wiki/Yann_LeCun)** has been a [long](https://openreview.net/pdf?id=BZ5a1r-kVsf)-[standing](https://lexfridman.com/yann-lecun-3-transcript/) [critic](https://www.youtube.com/watch?v=4__gg83s_Do) of the idea that LLMs could scale to human-level intelligence. Over recent years he shared many insights and concerns in this regard that overlap with those listed above. 

He argues that language is not intelligence. He considers it a low-bandwidth modality, with a discrete and restricted vocabulary that language models can predict probability distributions over to determine which word or symbols are likely to follow each other. The physical world is instead experienced by human vision with high bandwidth in high-dimensional and continuous representations. These cannot be enumerated in the same way to form a probability distribution over. Similar to Rich Sutton, he therefore argues that LLMs fundamentally lack an adequate mental model of the physical world in which they could plan a sequence of actions to arrive at an intended goal. This limits their cognitive abilities to a level below the intelligence of young children or even cats or dogs with no language abilities.

He expects that a truly intelligent system could acquire common sense and an understanding of the physical world from multimodal inputs like video, operate with persistent memory and perform reasoning and planning. He considers LLMs incapable of inventing solutions to new problems rather than merely performing knowledge retrieval from vast training data. 

To him, the current exuberance around LLMs is not a new phenomenon, with parallels to the hype around [expert systems](https://en.wikipedia.org/wiki/Expert_system) of the 80s that set high expectations followed by failures and disillusionment. Although he does not consider it likely that any isolated group could suddenly discover the secret to AGI, he expects the required capabilities to be gradually developed through innovations from industry and academia. Along with his own work on a Joint Embedding Predictive Architecture (JEPA), these may become more viable within the coming 3-5 years.

## Conclusion

These findings may not be entirely unexpected for many who have been following the field for a while. What is more surprising is the consensus that is taking hold even among those who previously presented much more optimistic timelines, sometimes in a context of financial incentives.

In sober review, there are undoubtedly many tangible achievements that have been reached by LLMs and other generative models. For tasks like generating text, images, video and audio, brainstorming, planning, summarization and agentic tasks with varying degrees for human supervision for software engineering and more, the technology can already provide genuine value for years to come.

Pinpointing the limits of their autonomy will remain a challenging task with a moving target.
This nuance will hopefully not be lost if the industry climate drops to a new ‘AI Winter’ among disillusioned investors who may have massively bought into pre-orders for science fiction that conflated machine learning with human-like robots.

But is it conceivable that the collective wisdom of investors overprovisioned billions of dollars in tech funding in vain? If so, we could take consolation in a thought few have had the courage to consider, round up these hundreds of thousands of GPUs, take a daring bet, and use them instead to finally fire up the Metaverse.