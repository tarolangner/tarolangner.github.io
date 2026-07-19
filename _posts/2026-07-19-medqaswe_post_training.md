---
layout: post
title: Passing the Swedish Medical Licensing Exam by Post-Training Open-Weight LLMs
author: Taro Langner
---

<p class="message">
    In this post: SFT and RLVR on Swedish MedQA<br>
    <I>(10 min read)</I><br>
    
</p>


To practice medicine in Sweden, foreign medical doctors who want to validate their license are first required to pass a multiple-choice test. Given around 140 questions with 5 answer options each, they must reach at least 60% accuracy to pass.

This theory test is challenging, with a pass rate of just about [one in four](https://lakartidningen.se/vetenskap/vagar-till-svensk-legitimation-for-lakare-utbildade-i-tredje-land/) and only 54% of participants ultimately succeeding after one or more attempts.

I was curious how well newer open-weight LLMs could do on this task by now. This post documents what turned into a little summer project, pushing the accuracy of smaller open-weight LLMs on Swedish MedQA with post-training techniques like supervised fine-tuning (SFT) and reinforcement learning with verifiable rewards (RLVR).


## Related Work

For English language, similar benchmark datasets with medical multiple-choice questions like MedQA have already been mostly saturated, with [frontier models scoring above 95%](https://pricepertoken.com/leaderboards/benchmark/medqa).

Swedish, however, accounts for less than 1% of pre-training data for LLMs, making it a [‘medium resource language’](https://arxiv.org/pdf/2410.08928). Its medical vocabulary, local treatment standards and medication also do not cleanly translate from English MedQA. 

Fortunately for me, [MedQA-SWE released by Hertzberg & Lokrantz in 2024](https://aclanthology.org/2024.lrec-main.975/) is composed of exactly the medical doctors' licensing exam data I was interested in. LLMs were evaluated on this data both in the original paper and also by [Moëll et al. in the 2025 Swedish Medical LLM Benchmark (SMLB)](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2025.1557920/full).

When published a year ago, it already reported several open-weight models as capable of passing the test on data of MedQA-SWE, with Gemma2-9B as the smallest (with 61.3%) and DeepSeek R1 Distill Llama-70B as the most accurate (with 77.8%).

## Data, Prompt and Evaluation

The relevant dataset used in the SMLB paper overlaps with MedQA-SWE. To avoid contamination through shared samples, I therefore isolated the MedQA-SWE samples with the most recent exam date as a validation set (158 samples) and kept the rest of it in reserve for training (3022 samples). All results reported here refer to greedy decoding on that validation set, which has no overlap with the training set. The prompt and evaluation harness are based on those used by Moëll et al., expecting the correct answer to be stated verbatim. 

## MedGemma-1.5-4B

Just six months ago, researchers at Google Health released MedGemma-1.5-4B for medical tasks. It has multimodal capabilities for both medical image analysis and clinical reasoning, so it seemed like a perfect candidate for this task.

When deployed out-of-the-box for inference, it only reached a somewhat disappointing 14.6% accuracy, however. Many of its outputs actually give the correct answer eventually, but fail the formatting requirement of stating the correct answer option verbatim. Instead, the model tends to digress with lengthy explanations that the evaluation harness scores with zero.

This failure in instruction-following appears to be a known failure mode of MedGemma-1.5-4B, even for English. In fact, the authors provide their own [post-training example](https://github.com/Google-Health/medgemma/blob/main/notebooks/reinforcement_learning_with_hugging_face.ipynb) for resolving this, as well as [one for SFT](https://github.com/google-health/medgemma/blob/main/notebooks/fine_tune_with_hugging_face.ipynb).


While working on this, I also found another paper, [PeruMedQA by Carrillo-Larco et al.](https://link.springer.com/article/10.1007/s40670-026-02692-w), that successfully used the SFT strategy to adapt an older variant of MedGemma to Peruvian medical licensing exam questions in Spanish language.

So I decided to set up a similar approach here, using the MedQA-SWE samples from prior years as training data for SFT with LoRA adapters on MedGemma-1.5-4B, to try and get the model to respond with the correct answer option verbatim. To reduce the risk of memorization, all answer options were randomly shuffled with re-assigned letters during training.

This post-training strategy raised the model accuracy on the validation set from 14.6% to 60.8% on the first attempt, sufficient for passing the exam. Find the [implementation on GitHub](https://github.com/tarolangner/medqaswe_medgemma_sft).

Rather than outright instilling new medical knowledge or improving Swedish language comprehension of the model, the predominant impact of SFT from such a small training set is improved format compliance. By learning to state the correct answer verbatim and nothing else, the model learns to generate outputs that never get truncated and are correctly scored by the evaluation harness. The underlying medical knowledge was likely already baked in the model weights from the start.


Overall, this is a rather interesting result for a 4B parameter model, considering that a minimum of 9B was reported for this just a year ago. But turns out that we can do even better.


## Gemma4-E4B

After Google Health released MedGemma-1.5-4B in January, which built on the Gemma3 series, Google DeepMind more recently released the newer Gemma4 series in April. 

When applying its Gemma4-E4B variant to the chosen validation set, it reached 77.2% accuracy out-of-the-box. With no post-training, it reaches almost perfect format compliance, robustly handles the prompt, questions and answers in Swedish language and exceeds the 60.8% accuracy of the fine-tuned MedGemma-1.5-4B reported above. It would appear as if, within a span of three months, Google has been left behind by Google.

Even its smaller variant Gemma4-E2B reached 52.5%. However, neither seemed to respond well to SFT. The recipe from above failed to improve their accuracy, perhaps due to their already excellent format compliance. Out of curiosity, I decided to venture outside of the Google ecosystem from here.


## Qwen3.5-4B

Released by Chinese Alibaba in March this year, Qwen3.5-4B (with 77.2% accuracy here) and Qwen3.5-2B (with 46.8%) turned out to perform virtually on par with their similarly sized counterparts from Google. Again, the SFT recipe did not yield any improvement for these.

However, I was curious to see how far the performance could be pushed by enabling reasoning for the 4B model. In the original SMLB paper, o3 in particular was noted for its good performance due to its reasoning capability. In the given project here, Qwen3.5-4B could also generate more or less extensive reasoning traces enclosed in `<think>` blocks that could be stripped before scoring the verbatim answer.

With reasoning enabled, Qwen3.5-4B improved from 77.2% (with ‘no thinking’) to 88.0% accuracy. These gains, however, come at a cost of substantially longer inference times. From the verbatim responses with up to just ~50 tokens, these reasoning traces can grow to 7,000 tokens and beyond. Three of them never concluded despite the reasoning traces showing a strong preference for the correct option, exhausting the entire context window limit of 32,768 tokens with repetitive reasoning loops about formatting formalities. Interestingly, all reasoning by this model is exclusively in English, in spite of the Swedish prompt, question, answer options and final response.

This uncapped reasoning can take up to five minutes for a single answer even on an A100 GPU. So from here, I looked into several approaches for getting the best of both worlds: Condensing as much of the accuracy gains from reasoning as possible into shorter and thus faster reasoning traces.

### Reasoning Compression

**Truncation with max_tokens**  
A simple way to cut down on inference time is a hard limit, stopping all outputs at a maximum count of 1024 tokens per sequence. Doing this here yields an answer within about 10s, but often truncates the model responses mid-reasoning, so that only 29.1% are completed with the correct answer.

**Thinking Intervention**  
A more sophisticated type of thinking intervention is proposed in [a 2025 paper](https://arxiv.org/pdf/2505.07686) on early-exit techniques for prevention of overthinking in LLMs.

It halts the decoding at a pre-determined token count and appends the phrase `Time is limited, stop thinking and start answering. \n</think>\n\n` to conclude the reasoning block with a soft transition. Decoding then proceeds, making the model provide its actual response immediately.

For my experiments on MedQA-SWE here, I applied this technique at a token limit of 896, leaving enough room for any verbatim response to conclude within 1024 tokens. On the validation set, this raised the accuracy of Qwen3.5-4B to 85.4%.

About one in seven questions were easy enough for the model to answer with shorter reasoning that did not even hit this token count limit while still providing perfect answers.

**Reinforcement Learning with Verifiable Rewards (RLVR)**  
The same paper also proposes the reinforcement learning technique *Serial-Group Decaying-Reward Policy Optimization* (S-GRPO). It generates a given sequence up to the specified limit and then creates early-exit variants of multiple lengths from it as rollouts that are each scored against a reward function. The shortest correct sequence yields the highest reward, training the model to produce shorter responses overall. 

Here, I set up this technique to run on a single A100 with 80GB, using vLLM in a colocate setup for speed, syncing the updated LoRA weights into the inference engine at every step. This approach raised the accuracy of Qwen3.5-4B on the validation set from 85.4% to 86.7%. 

This result is somewhat mixed, however. It ultimately represents just two additional questions flipped from false to correct, well within the range of statistical noise. Furthermore, the reasoning traces still required the early-exit intervention and actually ended up longer by six tokens on average instead of getting compressed. 

While improving upon the simple reasoning intervention, this result falls short of capturing all accuracy gains of the uncapped reasoning run in shorter outputs. Chances are that far more compute and experimentation would be required than budgeted for here (much of this project was done from a hammock in a nature reserve).

Up to 90% accuracy could perhaps be condensed out of the model in this way, judging by the uncapped reasoning run. There, it correctly answered another two questions and expressed a preference for the correct answer in the three degenerate reasoning traces that spiralled until exhausting the entire context window. Whether a more elaborate S-GRPO setup could elicit these or even more from the model will remain an open question for now.

### Memorization
Since MedQA-SWE predates both Qwen3.5-4B and Gemma4-E4B, their high performance could be trivially explained by them having memorized the questions and answers as part of their training data. Their remarkably similar accuracy (when reasoning is deactivated) is striking in this regard.

However, rather than reproducing identical answers, they actually exhibit quite distinct failure modes. Just about three quarters of their correct responses overlap, whereas half of the errors of one model are answered correctly by the other. 

While memorization is hard to conclusively disprove here, this pattern provides at least some evidence to the contrary, with both models having different strengths and weaknesses.

## Result Overview

<img src="/assets/medqa_swe_post_training.png" alt="MedQA-SWE result comparison">
*Accuracy for Medical Question Answering in Swedish (MedQA-SWE) by LLMs of varying sizes. Note that the two papers and this project all used different subsets of MedQA-SWE for evaluation. Nonetheless, striking performance gains have made small, open-weight LLMs competitive in this task with proprietary frontier models within just two years.*


<style>
table.compact { width: 100%; }
table.compact td:nth-child(1), table.compact th:nth-child(1),
table.compact td:nth-child(2), table.compact th:nth-child(2) { white-space: nowrap; width: 1%; padding-right: 2em; }
table.compact td:nth-child(3), table.compact th:nth-child(3) { width: 100%; text-align: left; }
</style>

| Model | Accuracy | Note |
|---|---|---|
| MedGemma-1.5-4B | 14.6% | format failures |
| MedGemma-1.5-4B (post-trained) | **60.8%** | SFT (LoRA) |
| | | |
| Gemma4-E2B | 52.5% | |
| Gemma4-E4B | 77.2% | |
| Qwen3.5-2B | 46.8% | |
| Qwen3.5-4B | 77.2% | |
| | | |
| Qwen3.5-4B, uncapped reasoning | 88.0% | 5 min latency |
| Qwen3.5-4B, truncation (max 1024) | 29.1% | |
| Qwen3.5-4B, early-exit intervention | 85.4% | |
| Qwen3.5-4B (post-trained) | **86.7%** | RLVR (S-GRPO) |
{: .compact}


In summary, MedGemma-1.5-4B narrowly pushed past the goal line after SFT resolved its formatting failures. Nonetheless, the newer models Gemma4-E4B and Qwen3.5-4B significantly outperform it outright, even without any post-training and no reasoning. 

With reasoning enabled, the latter rivals the highest accuracy yet reported for any LLM on MedQA-SWE. The gain in accuracy from reasoning comes at the cost of longer inference times, with uncapped reasoning spiralling up to five minutes for a single question until exhausting the context with no response.

Thinking interventions like the early-exit strategy cut this down to just 10s while capturing most of the accuracy gain, reaching arguably the best tradeoff in speed, accuracy and engineering effort here. Reinforcement learning takes this idea further with S-GRPO and yielded additional modest accuracy gains while under the early-exit scheme that maintains its speed.

## Conclusion

In 2025, the top accuracy on MedQA-SWE required the frontier model o3, estimated at hundreds of billions of parameters. One year later, this project virtually matched its performance with a mere 4B parameter open-weight model and reinforcement learning techniques (albeit on a subset of the data). 

Swedish language does not seem to pose a major obstacle even for these smaller models, despite its sparse representation among LLM training data. Both Gemma4 and Qwen3.5-4B are multilingual and faithfully handled the Swedish instructions, prompt, questions and verbatim responses in Swedish, even if reasoning traces for the latter here were generated entirely in English. 

Even in the span of mere months, these models are rapidly outpacing one another. The domain specialist MedGemma-1.5-4B was notably outperformed by generalist models of similar size released just 2-3 months after.

What does this mean for European and Swedish domestic efforts to train language-specific, sovereign LLMs? Now that discussion is safely beyond the scope of this post. It seems safe to assume either way that LLM capabilities for Swedish will keep improving.

So is AI finally ready to automate medicine? For radiologists, [we are five years overdue](https://tensorlabbet.com/2025/01/29/radiology-image-segmentation/) by now. But while the medical imaging community figures out the last remaining details there, this project witnessed a new milestone of human-like performance being passed by LLMs: Medical question answering that takes forever due to excessive focus on data entry. And with that, let me leave you with one of the uncapped reasoning traces [you can view on GitHub](https://github.com/tarolangner/tarolangner.github.io/tree/main/assets/medqa_swe_qwen35_4b_reasoning_spiral.txt).