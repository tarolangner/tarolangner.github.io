---
layout: post
title: The Rise of Open-Weight LLMs
author: Taro Langner
category: LLM Engineering
summary: "A survey of the open LLM ecosystem"
---

<p class="message">
    In this post: A survey of the open LLM ecosystem <br>
    <I>(7 min read)</I><br>
    
</p>


Leading model providers like Anthropic, OpenAI and xAI have been pushing the envelope by developing ever more capable Large Language Models (LLMs). These _closed-weight_ frontier models are proprietary and served through APIs or subscription plans. 

The big bet of the AI race, on which over [$1 trillion have been invested](https://www.visualcapitalist.com/visualized-big-tech-ai-spending/), is that substantial returns on investment are possible, especially for a single provider that ‘wins’ and comes to dominate the field. 


## Locking In

Whereas OpenAI recently started [introducing ads](https://www.adweek.com/media/exclusive-leaked-deck-reveals-stackadapts-playbook-for-chatgpt-ads/) for some of their usage plans,
Anthropic has started to adjust the generosity of their offering by limiting third-party access, tightening usage limits and [barring certain users](https://news.ycombinator.com/item?id=47854477) from signing up for Claude Code on Pro subscription plans.
The models of xAI, in turn, tend to act in [ways many find surprising](https://preview.redd.it/grok-lobotomised-succesfully-v0-iafrkqmw5l2g1.jpg?width=640&crop=smart&auto=webp&s=86960a3112fd4a17f18a89c1838424d38b10c4cd) and have [gone through a lot in general](https://www.theguardian.com/technology/2025/jul/09/grok-ai-praised-hitler-antisemitism-x-ntwnfb).

SpaceX became the parent company of [xAI earlier this year](https://x.ai/news/xai-joins-spacex) and recently secured an [option to acquire Anysphere](https://www.forbes.com/sites/sandycarter/2026/04/23/spacex-bets-60-billion-on-cursor-ai-the-real-winner-is-a-surprise/), the startup behind AI-assisted code editor Cursor, in a further step towards consolidation.

With OpenAI, Anthropic and SpaceX all three moving towards [IPOs in 2026 while currently unprofitable](https://www.reuters.com/business/biggest-ipo-wave-history-promises-3-trillion-value-with-no-profits-2026-04-23/), it might indeed seem like the late game may consist of consolidating and raising margins on a captive audience. But how captive is this audience, really?

## Open-weight Models

Whereas these frontier models remain proprietary, new generations of open-weight models are rapidly catching up in capabilities. Some now rival the benchmark results that proprietary frontier models reached only recently, with some putting the gap at [just 3 months](https://epoch.ai/data-insights/open-weights-vs-closed-weights-models).

These open-weight models are available for free under permissive software licenses. This was common practice in academic research for reproducibility. But for LLMs in particular, this changed in 2019 when the non-profit OpenAI withheld the release of GPT-2, citing safety concerns and later calling for regulation. Parallels have since [been drawn](https://the-decoder.com/from-gpt-2-to-claude-mythos-the-return-of-ai-models-deemed-too-dangerous-to-release/) to the recent announcements around Claude Mythos.

Open-weight models have already undergone pre-training, the most capital-intensive phase of model creation, in which they are trained for next-token prediction on vast corpora of digitized books, encyclopedias, websites, social media content, scientific publications and code. 
The resulting base models are furthermore often also offered as instruct models, which have completed additional phases of model creation consisting of supervised fine-tuning (SFT) on curated question-answer pairs. Often, they have also undergone alignment phases in which they adapt the style, tone and formats to human preferences.

Even without massive compute resources as would be required for pre-training, these models can be adapted for specific applications with techniques for Parameter-Efficient Fine Tuning (PEFT) and alignment phase techniques like Proximal Policy Optimization (PPO) used in Reinforcement Learning from Human Feedback (RLHF), Direct Preference Optimization (DPO) or Group-relative Policy Optimization (GRPO) used in reinforcement learning from verifiable rewards (RLVR).

In addition to outright LLMs above 70B parameters (beyond one trillion for some) that typically require multi-GPU or entire clusters for serving, newer generations of smaller models are increasingly competitive. Small Language Models (SLMs) up to about 7B parameters can often run on consumer-grade GPUs with 12 to 24GB VRAM and Apple Silicon Macs. Tiny Language Models (TLMs) up to 1B parameters can run on even smartphones and edge devices. 

Dozens of open-weight LLM model families have been released by now, such as:
* [Qwen-3.6-35B-A3B](https://www.alibabacloud.com/blog/qwen3-6-35b-a3b-agentic-coding-power-now-open-to-all_603043) from Alibaba (China) for agentic coding 
* [Gemma 4](https://blog.google/innovation-and-ai/technology/developers-tools/gemma-4/) from Google (US) with ability to process vision and audio inputs
* [Ministral 3](https://mistral.ai/news/mistral-3) from Mistral (France) for edge devices

Overall, the lineup is diverse in geopolitical terms and widely disseminated to a degree where they are likely to stay around. 
Community-driven derivatives and variants on platforms like HuggingFace already cover over 2.5m distinct models (including models other than language models). 


## Hardware and Compression

The landscape of viable hardware accelerators is diversifying too. Beyond the ability to run on Mac, many models challenge the dominance of CUDA-powered Nvidia GPUs through wider compatibility. Chinese labs targeted by US export restrictions are training on chips by Huawei. Furthermore, GPUs by AMD with ROCm (or even Vulkan) are increasingly viable. 

Some models combine the expressive power of larger, ‘dense’ models with drastically reduced compute budgets through a Mixture of Experts (MoE) architecture. By dynamically routing requests to separate, specialized subsets of the underlying neural network, they achieve a low number of active parameters during inference. 

Quantization offers another avenue for compression, by representing model weights, activations, gradients and optimizer states with lower precision data types. From the original float32, this line of optimization has pushed from mixed-precision, with data types like bfloat16, down to 4-bit and beyond.

Another target of quantization and various other optimization techniques is the KV cache. It stores the key and value tensors computed for the attention mechanism of LLMs, which can be efficiently reused when predicting new tokens during inference.

## Tool Use and Serving

Many useful capabilities like web search and code execution require a harness around the LLM for tool use and agentic loops. For this, too, a growing ecosystem of open-source solutions is emerging.

[Open WebUI](https://github.com/open-webui/open-webui) provides a frontend with chat interface resembling ChatGPT and support for pipelines like web search, document ingestion with RAG and workflow orchestration.
[LangGraph](https://github.com/langchain-ai/langgraph) can alternatively handle agentic loops and tool use without needing any frontend.
[OpenCode](https://github.com/anomalyco/opencode) enables agentic coding with tool use for searching files, code execution and sub-agents.

All of the above depend on a backend that can run the actual LLM inference. Here, [Ollama](https://github.com/ollama/ollama) offers convenience and local serving, whereas [vLLM](https://github.com/vllm-project/vllm) and [SGLang](https://github.com/sgl-project/sglang) offer heavily optimized inference serving that is also viable for larger models and even multi-node inference.

All of these are open-source, with many using OpenAI-compatible APIs as standard. Adding to this is a growing number of [experimental custom setups](https://news.ycombinator.com/item?id=47863217) and use cases from individual users.


Many of these can be self-hosted locally, potentially even on air-gapped systems that are entirely self-contained. Alternatively, there is a growing range of flexible cloud hosting services for GPU rentals from commercial providers.


## Conclusion

The field is opening up remarkably and the capabilities of open-weight models seem to increasingly converge with the state of the art at frontier labs. At the same time, access to the pre-trained models, hardware and options for serving are diversifying too. 
 
With this, it seems increasingly unlikely for any one state actor or commercial entity to ‘win’ the race and establish a monopoly. Instead, competition is thriving and the future may hold widespread open-source development for self-hosted use as everyday utility.
