---
layout: post
title: Reviewing “AI Engineering” by Chip Huyen
author: Taro Langner
---

<p class="message">
    In this post: A book review <br>
    <I>(5 min read)</I><br>
    
</p>

In January this year, [Chip Huyen](https://huyenchip.com/) published her newest book [*‘AI Engineering’*](https://www.amazon.com/dp/1098166302?&linkCode=sl1&tag=chiphuyen-20&linkId=0a4e5ad4b14080d44c42640550a9291e&language=en_US&ref_=as_li_ss_tl), which quickly [made waves](https://www.youtube.com/watch?v=98o_L3jlixw&pp=ygUscHJhZ21hdGljIGVuZ2luZWVyIGFpIGVuZ2luZWVyaW5nIGNoaXAgaHV5ZW4%3D) online. 

Having read her previous book [*‘Designing Machine Learning Systems’* (2022)](https://www.amazon.com/Designing-Machine-Learning-Systems-Production-Ready/dp/1098107969?&_encoding=UTF8&tag=chiphuyen-20&linkCode=ur2&linkId=0a1dbab0e76f5996e29e1a97d45f14a5&camp=1789&creative=9325), which I warmly recommend, I wondered what could possible remain to be covered in 500+ additional pages. It really turned out to be something entirely different, and this blog post will attempt a short review for anyone still curious about the book.

## Machine Learning vs AI Engineering
Her previous book, *‘Designing Machine Learning Systems’*, was a gentle but comprehensive overview of machine learning terms, techniques and applications that went easy on mathematical notation. While it briefly mentioned Large Language Models (LLMs) and remains highly relevant, it was published about half a year before the release of ChatGPT in November 2022, pre-dating its impact on the field.

The new book *‘AI Engineering’* is now entirely dedicated to working with LLMs. Subtitled *'Building Applications with Foundation Models'*, it addresses a much wider audience than just ML Engineers or Researchers with a technical or scientific interest. Indeed, it clearly sets apart ML from the scope of the book and expects little prior knowledge of the field. The contents have therefore hardly any overlap with the previous book and are mostly complementary.

## Format and Style
The field is now moving faster than anyone could hope to read about, with sensational new announcements almost every week. Technical specifics are quickly outdated and the book accordingly sticks to more timeless high-level concepts, insights and approaches. These are nonetheless often supported by hard evidence from statistics or relevant papers and first-hand accounts from industry experts. However, this also tends to make it a quite verbose, lighter read of often more ‘qualitative’ nature, with plenty of examples and a minimum of mathematical notation and formulas.


## Content
The author has an hopeful but grounded take on the capabilities of LLMs, with the credentials to back it up. The book provides many use cases and guides, but also known failure modes backed by the scientific literature, along with techniques to mitigate them. 

The contents include concepts such as pre- and post-training, retrieval-augmented generation (RAG), agents, tool-use, evaluation techniques, emergent properties and quirks of the models. It offers strategies for application development, an in-depth chapter on fine-tuning with techniques such as Low-Rank Adaptation (LoRA) as well as optimization strategies for inference and more.

The facts laid out in the book are well-researched and appear solid overall. Only one assertion struck me as wrong, which is the often repeated claim that the 2012 [AlexNet paper](https://dl.acm.org/doi/abs/10.1145/3065386) was the first to utilize GPUs for training of neural networks. As mentioned in my previous [summary on AlexNet](https://tensorlabbet.com/#AlexNet) the truth seems [somewhat more nuanced](https://www.deeplearningbook.org/contents/applications.html). Chances are that the author already has a rebuttal waiting in their inbox by 
[Jürgen Schmidhuber](https://arxiv.org/abs/2212.11279).




## Conclusion

The book provides a comprehensive overview and also offers many insights that were new to me, from the [mapped-out political leanings of LLMs](https://arxiv.org/html/2403.18932v1) over the availability of [training material in different languages](https://commoncrawl.github.io/cc-crawl-statistics/plots/languages.html) to prompt injection attacks that could leak sensitive training data when tasked to merely [repeat the word ‘poem’ an infinite number of times](https://arxiv.org/abs/2311.17035).

The distinction between ML and AI Engineering itself is thought-provoking. It illustrates how ML-based capabilities which used to be academic research topics are rapidly becoming applicable, abstracted and commoditized via APIs.

As with any other API, these capabilities thereby become accessible even without any deeper understanding of the field. The latter nonetheless helps, as simple LLM wrappers still encounter many limitations which are laid out in the book (hallucinations, costs, prompt injection attacks etc) and are still rarely competitive for hard engineering challenges (as seen e.g. in Kaggle challenges). 

The book provides a solid foundation in this regard. Even with a more technical background, its balance between breadth and depth covered many gaps in my knowledge and makes it likely to remain relevant for years to come, so that it was well worth reading for me.


*Disclaimer: I have no affiliation with the author and this review is not monetized, sponsored or funded in any other way. Originally, this post was meant to also review the book [‘Alice’s Adventures in a Differentiable Wonderland’](https://www.sscardapane.it/alice-book/) by Simone Scardapane that I read earlier, but that will remain for a future post.*