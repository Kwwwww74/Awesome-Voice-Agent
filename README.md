# 🎙️ Awesome Voice Agents

<p align="center">
  <a href="https://github.com/sindresorhus/awesome"><img src="https://awesome.re/badge.svg" alt="Awesome"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/stargazers"><img src="https://img.shields.io/github/stars/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub stars"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/network/members"><img src="https://img.shields.io/github/forks/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub forks"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/issues"><img src="https://img.shields.io/github/issues/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub issues"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/commits/main"><img src="https://img.shields.io/github/last-commit/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub last commit"></a>
</p>

<p align="center">
  <em>A curated and continuously updated collection of papers, models, benchmarks, datasets, and engineering resources for voice agents.</em>
</p>

Voice agents are rapidly evolving from conventional spoken-dialogue systems into reasoning models that can use tools and complete long-horizon tasks. This repository organizes the field with a five-level capability taxonomy:

> **L0 Pre-LLM Systems → L1 Direct-Response Models → L2 Reasoning Models → L3 Tool-Using Agents → L4 Long-Horizon Agents**

The collection covers speech-to-speech models, full-duplex interaction, audio reasoning, retrieval and tool use, task execution, evaluation, turn management, data, safety, and production systems.

> [!NOTE]
> The taxonomy records the **highest capability demonstrated by a concrete system or evaluated configuration**. A model description, API feature list, or product claim alone is not sufficient evidence for a level.

**Last updated:** September 20, 2026

---

## 📌 Table of Contents

- [Introduction](#-introduction)
- [What Is a Voice Agent?](#-what-is-a-voice-agent)
- [Capability Taxonomy](#-capability-taxonomy)
- [Research Collections](#-research-collections)
  - [L0: Pre-LLM Voice Systems](#l0-pre-llm-voice-systems)
  - [L1: Direct-Response Voice Models](#l1-direct-response-voice-models)
  - [L2: Reasoning Voice Models](#l2-reasoning-voice-models)
  - [L3: Tool-Using Voice Agents](#l3-tool-using-voice-agents)
  - [L4: Long-Horizon Voice Agents](#l4-long-horizon-voice-agents)
- [Commercial Platforms](#-commercial-platforms)
- [Surveys and Position Papers](#-surveys-and-position-papers)
- [Benchmarks and Evaluation](#-benchmarks-and-evaluation)
- [Enabling Research](#-enabling-research)
- [Safety and Trustworthiness](#-safety-and-trustworthiness)
- [Engineering Resources](#-engineering-resources)
- [Recommended Starting Points](#-recommended-starting-points)
- [Recent News](#-recent-news)
- [How to Contribute](#-how-to-contribute)
- [Citation](#-citation)
- [Star History](#-star-history)
- [Acknowledgement](#-acknowledgement)

---

## 🌍 Introduction

Large language models are changing the role of speech interfaces. Earlier systems primarily converted speech into text, applied a predefined dialogue policy, and synthesized a response. Modern voice agents can reason over spoken input, coordinate external tools, interact in real time, and act on behalf of users.

This repository tracks that transition and provides:

- a capability-based taxonomy for comparing voice agents across generations;
- representative end-to-end systems and speech-language models;
- work on reasoning, retrieval, tool use, planning, and task execution;
- benchmarks for dialogue quality, turn-taking, proactivity, and tool use;
- datasets, training methods, reward models, and interaction components;
- safety, security, fairness, and deployment resources.

The repository focuses on **interactive systems in which speech is part of the decision loop**. General audio understanding models are included only when they directly support voice-agent capabilities.

---

## 🗣️ What Is a Voice Agent?

We use the following working definition:

> A **voice agent** is an interactive system that receives spoken input, maintains relevant conversational or task state, selects a communicative or external action, and uses the resulting observation to advance a user request or delegated goal.

A voice agent may be implemented as a cascaded pipeline, an end-to-end speech language model, or a hybrid architecture. Speech naturalness, low latency, full-duplex communication, emotion, and persona are important properties, but they do not by themselves determine the agent level.

### Scope

| Included | Usually listed as supporting research |
|---|---|
| End-to-end spoken dialogue systems | Standalone ASR, TTS, VAD, or endpointing components |
| Speech-language models evaluated in interaction | Datasets and data-processing pipelines |
| Reasoning and tool-using voice systems | Benchmarks and evaluation methods |
| Voice agents deployed for concrete tasks | Surveys, safety audits, and engineering tutorials |

---

## 🧭 Capability Taxonomy

### Overview

| Level | Name | Operational definition | Minimum evidence | What is not sufficient |
|---|---|---|---|---|
| **L0** | **Pre-LLM Voice System** | A historical spoken-dialogue or task system built before LLM-based language reasoning became the central controller. | A complete pre-LLM speech or dialogue pipeline, neural spoken-dialogue model, or deployed voice system. | L0 is a historical baseline, not a claim that every L0 system is less task-capable than every L1 model. |
| **L1** | **Direct-Response Voice Model** | An LLM-era model maps spoken context to a response without a demonstrated deliberative or chain-of-thought stage. | Context-sensitive spoken responses in an end-to-end or cascaded interactive system. | Natural speech, full duplex, interruption handling, emotion, persona, or long context alone. |
| **L2** | **Reasoning Voice Model** | The model performs explicit or latent deliberation before or during response generation, and reasoning affects its answer or decision. | A reasoning mechanism plus experiments on multi-step inference, incremental reasoning, planning, or comparable reasoning tasks. | A prompt that asks the model to “think,” a hidden state with no reasoning evaluation, or better dialogue quality alone. |
| **L3** | **Tool-Using Voice Agent** | The system selects and invokes an external tool, retrieval system, API, or environment action, observes the result, and uses it in the ongoing interaction. | A closed tool loop: **select → execute → observe → continue or report**. | Merely emitting a function-call string, using fixed offline knowledge, or listing tool support in documentation. |
| **L4** | **Long-Horizon Voice Agent** | The system maintains a goal over an extended multi-step task, manages dependencies and persistent state, and replans or recovers when conditions change. | Multi-step planning, state tracking, tool orchestration, and recovery or replanning evaluated in a long-horizon task. | Several scripted tool calls, a long conversation, or a single successful workflow without adaptation. |

### Important interpretation of L0

L0 is intentionally a **historical category**. The remaining levels describe capabilities of LLM-era systems. A pre-LLM system such as Google Duplex may execute a real task, but it remains L0 in this taxonomy because its primary value is as a predecessor to LLM-based voice agents.

### Assignment rules

1. **Historical precedence:** systems whose core architecture predates the LLM era are assigned to L0.
2. **Highest demonstrated capability:** LLM-era systems receive the highest level supported by experiments or a documented deployment.
3. **No level skipping by feature accumulation:** low latency, full duplex, empathy, and multimodality do not compensate for missing reasoning, tool use, or long-horizon planning.
4. **Reasoning does not require public raw chain-of-thought:** hidden or latent reasoning can qualify for L2 when the mechanism and its contribution are evaluated.
5. **Runtime retrieval can be a tool:** RAG qualifies for L3 only when the agent actively invokes retrieval, observes the result, and adapts its subsequent behavior.
6. **Platforms are not single systems:** commercial APIs that can support several configurations are shown as capability ranges rather than assigned one fixed level.
7. **Components are not agents:** datasets, benchmarks, VAD modules, turn predictors, reward models, and surveys are listed separately and are not assigned L0-L4.

### Decision procedure

```text
Was the core system designed before the LLM era?
├── Yes → L0
└── No
    ├── Does it demonstrate long-horizon planning, persistent state,
    │   and replanning or recovery? → L4
    ├── Does it execute external tools/actions and use their results? → L3
    ├── Does it demonstrate a reasoning or deliberation process? → L2
    └── Does it directly generate an interactive spoken response? → L1
```

### Evidence markers used below

- ✅ **Demonstrated:** supported by an experiment, system evaluation, or documented deployment.
- 🧪 **Candidate:** the architecture or available report suggests the level, but stronger task-level evidence should be checked.
- 🏢 **Platform:** supports several possible levels depending on the agent configuration.
- 🧩 **Supporting work:** enables or evaluates agents but is not itself assigned a level.

---

## 🧭 Research Collections

### L0: Pre-LLM Voice Systems

Historical systems and resources that established task-oriented dialogue, turn-taking, spoken-language understanding, and real-world voice interaction before LLM-based voice agents.

| Year | Work | Main contribution | Evidence |
|---|---|---|---|
| 2018 | [Google Duplex: An AI System for Accomplishing Real-World Tasks over the Phone](https://research.google/blog/google-duplex-an-ai-system-for-accomplishing-real-world-tasks-over-the-phone/) | Real-world telephone task completion with a specialized dialogue system | ✅ Deployment report |
| 2021 | [Duplex Conversation in Outbound Agent System](https://dblp.org/search?q=Duplex%20Conversation%20in%20Outbound%20Agent%20System) | Production-oriented duplex outbound calling | 🧪 System report |
| 2022 | [Generative Spoken Dialogue Language Modeling](https://arxiv.org/search/?query=Generative+Spoken+Dialogue+Language+Modeling&searchtype=title) | Generative modeling of spoken dialogue and acoustic behavior | ✅ Model evaluation |
| 2022 | [Duplex Conversation: Towards Human-like Interaction in Spoken Dialogue Systems](https://arxiv.org/search/?query=Duplex+Conversation+Towards+Human-like+Interaction&searchtype=title) | User-state detection, backchannels, and interruption in duplex dialogue | ✅ System evaluation |

### L1: Direct-Response Voice Models

L1 systems generate interactive spoken responses but do not provide sufficient evidence of a distinct reasoning process, runtime tool loop, or long-horizon planning.

| Year | Model or system | Main capabilities | Evidence |
|---|---|---|---|
| 2024 | [Moshi](https://arxiv.org/abs/2410.00037) | Native full-duplex speech, inner monologue stream, interruption, and backchannels | ✅ |
| 2024 | [SyncLLM](https://arxiv.org/abs/2409.15594) | Synchronized listening and speaking for real-time dialogue | ✅ |
| 2024 | [OmniFlatten](https://arxiv.org/abs/2410.17799) | Flattened interleaved speech-text streams for full-duplex modeling | ✅ |
| 2024 | [Freeze-Omni](https://arxiv.org/abs/2411.00774) | Low-latency speech-to-speech interaction around a frozen LLM | ✅ |
| 2024 | [Language Model Can Listen While Speaking](https://arxiv.org/search/?query=Language+Model+Can+Listen+While+Speaking&searchtype=title) | Concurrent listening and speaking | ✅ |
| 2024 | [Beyond the Turn-Based Game: Enabling Real-Time Conversations with Duplex Models](https://arxiv.org/search/?query=Beyond+the+Turn-Based+Game&searchtype=title) | Real-time overlapping spoken interaction | ✅ |
| 2024 | [BLSP-Emo](https://arxiv.org/search/?query=BLSP-Emo&searchtype=title) | Emotion-aware spoken language modeling | 🧪 |
| 2024 | [PerceptiveAgent](https://arxiv.org/search/?query=PerceptiveAgent+Empathetic+Dialogue&searchtype=title) | Acoustic perception and empathetic spoken responses | 🧪 |
| 2025 | [MinMo](https://arxiv.org/abs/2501.06282) | Full-duplex interaction, emotion, dialect, and singing | ✅ |
| 2025 | [SALM-Duplex](https://arxiv.org/abs/2505.15670) | Joint listener and speaker modeling | ✅ |
| 2025 | [SALMONN-omni](https://arxiv.org/abs/2505.17060) | Dynamic turn management and interruption handling | ✅ |
| 2025 | [DuplexMamba](https://arxiv.org/search/?query=DuplexMamba&searchtype=title) | Streaming duplex speech with Mamba-based modeling | ✅ |
| 2025 | [CleanS2S](https://arxiv.org/search/?query=CleanS2S&searchtype=title) | Lightweight framework for proactive speech-to-speech interaction | ✅ |
| 2025 | [Sesame: Crossing the Uncanny Valley of Conversational Voice](https://www.sesame.com/research/crossing_the_uncanny_valley_of_voice) | Natural conversational speech, prosody, and expression | 🧪 |
| 2025 | [Hume EVI 3](https://dev.hume.ai/docs/speech-to-speech-evi/overview) | Empathy, persona, expression, and controllable voice | 🧪 |
| 2026 | [PersonaPlex](https://arxiv.org/abs/2602.06053) | Controllable persona and voice behavior in full-duplex dialogue | ✅ |
| 2026 | [MiniCPM-o 4.5](https://arxiv.org/abs/2604.27393) | Full-duplex audio-visual-text interaction | ✅ |
| 2026 | [BayLing-Duplex](https://arxiv.org/abs/2606.14528) | Learned turn control, listening, speaking, and interruption | ✅ |
| 2026 | [SteerDuplex](https://arxiv.org/abs/2609.12623) | Controllable full-duplex behavior, persona, style, and timing | ✅ |
| 2026 | [Lychee-FD](https://arxiv.org/search/?query=Lychee-FD&searchtype=title) | Hierarchical acoustic-semantic full-duplex modeling | 🧪 |
| 2026 | [Human-1](https://arxiv.org/search/?query=Human-1+Full-Duplex+Conversational+Modeling&searchtype=title) | Full-duplex conversational modeling for Hindi | 🧪 |
| 2026 | [KAME](https://arxiv.org/search/?query=KAME+Speech-to-Speech+Conversational+AI&searchtype=title) | Tandem knowledge enhancement for real-time speech-to-speech dialogue | ✅ |

### L2: Reasoning Voice Models

L2 requires evidence that deliberation changes the model's response or decision. Raw chain-of-thought does not have to be exposed; evaluated latent or incremental reasoning is sufficient.

| Year | Model or system | Reasoning capability | Evidence |
|---|---|---|---|
| 2025 | [SHANKS: Simultaneous Hearing and Thinking for Spoken Language Models](https://arxiv.org/search/?query=SHANKS+Simultaneous+Hearing+and+Thinking&searchtype=title) | Incremental reasoning while receiving streaming speech | ✅ |
| 2026 | [LTS-VoiceAgent: A Listen-Think-Speak Framework via Semantic Triggering and Incremental Reasoning](https://arxiv.org/search/?query=LTS-VoiceAgent&searchtype=title) | Semantic triggering and incremental listen-think-speak reasoning | 🧪 |
| 2026 | [PRISM: Prosody-Integrated Multi-Agent Reasoning for Empathetic Spoken Dialogue](https://arxiv.org/search/?query=PRISM+Prosody-Integrated+Multi-Agent+Reasoning&searchtype=title) | Multi-agent reasoning over prosodic and semantic signals | 🧪 |

### L3: Tool-Using Voice Agents

L3 systems close the loop between spoken requests and external information or actions. Models that also reason are placed here when tool use is the highest demonstrated capability.

| Year | Model or system | Tools or external actions | Evidence |
|---|---|---|---|
| 2025 | [LUCY](https://arxiv.org/abs/2501.16327) | Function calling in an emotionally expressive voice agent | ✅ |
| 2025 | [AURA: Agent for Understanding, Reasoning, and Automated Tool Use in Voice-Driven Tasks](https://arxiv.org/search/?query=AURA+Automated+Tool+Use+Voice-Driven+Tasks&searchtype=title) | Reasoning and automated tool use from spoken instructions | ✅ |
| 2025 | [Step-Audio 2](https://arxiv.org/abs/2507.16632) | External search, tool use, voice switching, and style control | ✅ |
| 2025 | [FireRedChat](https://arxiv.org/abs/2509.06502) | Full-duplex interaction with task and psychological tools | ✅ |
| 2025 | [Fun-Audio-Chat / Duplex](https://arxiv.org/abs/2512.20156) | Streaming function calling in duplex dialogue | ✅ |
| 2025 | [Stream RAG](https://arxiv.org/search/?query=Stream+RAG+Spoken+Dialogue&searchtype=title) | Runtime streaming retrieval during spoken interaction | ✅ |
| 2026 | [MoshiRAG](https://arxiv.org/abs/2604.12928) | Asynchronous retrieval during continuous speech | ✅ |
| 2026 | [VoxMind](https://arxiv.org/abs/2604.15710) | Think-before-speaking and dynamic tool management | 🧪 |
| 2026 | [DuplexOmni](https://arxiv.org/abs/2606.09186) | Asynchronous reasoning and tool use in full-duplex interaction | 🧪 |
| 2026 | [JoyAI-Talker](https://arxiv.org/abs/2608.01119) | Thinker-Talker architecture with tool calling | 🧪 |
| 2026 | [NVIDIA NemotronLabs VoiceChat 11B](https://huggingface.co/models?search=NemotronLabs%20VoiceChat%2011B) | Independent tool-script channel for real-time voice tools | 🧪 |

### L4: Long-Horizon Voice Agents

L4 is intentionally strict. A system should retain goals and task state across many steps, coordinate tools, and demonstrate replanning or recovery rather than merely execute a fixed workflow.

| Year | Model or system | Long-horizon capability | Evidence |
|---|---|---|---|
| 2026 | [DuplexSLA](https://arxiv.org/abs/2605.20755) | Speech-language-action planning, structured tool calls, and full-duplex interaction | 🧪 Candidate L4 |
| 2026 | [Gander / Omni Interaction Agent](https://arxiv.org/abs/2609.08977) | Complex multimodal tasks, dynamic planning, and tool orchestration | 🧪 Candidate L4 |

> [!IMPORTANT]
> L4 assignments should be audited against the original experiments. If a paper does not evaluate persistent task state, plan adaptation, or failure recovery, it should be classified as L3 even if the architecture contains a planner.

---

## 🏢 Commercial Platforms

Commercial APIs are configurable platforms rather than single evaluated agents. Their ranges indicate what developers may build, not a fixed demonstrated level for every deployment.

| Platform | Indicative range | Relevant capabilities | Resource |
|---|---|---|---|
| OpenAI Realtime models | L1-L3 | Real-time speech, reasoning-capable backends, and function calling | [Documentation](https://developers.openai.com/api/docs/guides/realtime) |
| OpenAI Voice Agents | L1-L3 | Realtime sessions, prompting, tools, and workflow integration | [Documentation](https://developers.openai.com/api/docs/guides/voice-agents) |
| Google Gemini Live | L1-L3 | Real-time audio, multimodal input, and tool calling | [Documentation](https://ai.google.dev/gemini-api/docs/live) |
| Amazon Nova Sonic | L1-L3 | Bidirectional speech streaming and tool integration | [Documentation](https://docs.aws.amazon.com/nova/latest/userguide/speech.html) |
| Hume EVI | L1-L2 | Empathetic dialogue, expression, persona, and voice control | [Documentation](https://dev.hume.ai/docs/speech-to-speech-evi/overview) |
| Ultravox | L1-L3 | Real-time speech agent platform and tool integration | [Documentation](https://docs.ultravox.ai/) |
| xAI Voice | L1-L3 | Real-time voice interaction and application integration | [Documentation](https://docs.x.ai/) |
| ByteDance Seed Speech / SeedDuplex | L1-L2 | Full-duplex speech, interruption, and adaptive endpointing | [Seed](https://seed.bytedance.com/) |

---

## 📚 Surveys and Position Papers

- [Recent Advances in Speech Language Models: A Survey](https://arxiv.org/search/?query=Recent+Advances+in+Speech+Language+Models&searchtype=title)
- [From Turn-Taking to Synchronous Dialogue: A Survey of Full-Duplex Spoken Language Models](https://arxiv.org/search/?query=From+Turn-Taking+to+Synchronous+Dialogue&searchtype=title)
- [A Survey of Full-Duplex Spoken Dialogue Systems: Architectural Hierarchy, Interaction Ontology, and Decision State Machine](https://arxiv.org/search/?query=Survey+Full-Duplex+Spoken+Dialogue+Systems+Architectural+Hierarchy&searchtype=title)
- [A Survey of Audio Reasoning in Multimodal Foundation Models](https://arxiv.org/search/?query=Survey+Audio+Reasoning+Multimodal+Foundation+Models&searchtype=title)
- [A Survey of Large Audio Language Models: Generalization, Trustworthiness, and Outlook](https://arxiv.org/search/?query=Survey+Large+Audio+Language+Models+Generalization+Trustworthiness&searchtype=title)
- [Toward Fair Speech Technologies: A Comprehensive Survey of Bias and Fairness in Speech AI](https://arxiv.org/search/?query=Toward+Fair+Speech+Technologies&searchtype=title)

---

## 📊 Benchmarks and Evaluation

### General voice-agent evaluation

- [EVA-Bench: A New End-to-End Framework for Evaluating Voice Agents](https://arxiv.org/search/?query=EVA-Bench+Voice+Agents&searchtype=title)
- [VAmoS Bench: Voice Agent Simulation and Benchmark](https://arxiv.org/search/?query=VAmoS+Bench+Voice+Agent&searchtype=title)
- [WildSpeech-Bench: Benchmarking End-to-End SpeechLLMs in the Wild](https://arxiv.org/search/?query=WildSpeech-Bench&searchtype=title)
- [SD-Eval: A Benchmark Dataset for Spoken Dialogue Understanding Beyond Words](https://arxiv.org/search/?query=SD-Eval+Spoken+Dialogue&searchtype=title)

### Agentic capabilities

- [From Reactive to Proactive: Assessing the Proactivity of Voice Agents via ProVoice-Bench](https://arxiv.org/search/?query=ProVoice-Bench&searchtype=title)
- [From Text to Voice: A Reproducible and Verifiable Framework for Evaluating Tool-Calling LLM Agents](https://arxiv.org/search/?query=Evaluating+Tool+Calling+LLM+Agents+Voice&searchtype=title)
- [TurnBench: A Multi-Domain Benchmark for Turn-Taking Dynamics in Spoken Dialogue](https://arxiv.org/search/?query=TurnBench+Spoken+Dialogue&searchtype=title)
- [Game-Time: Evaluating Temporal Dynamics in Spoken Language Models](https://arxiv.org/search/?query=Game-Time+Temporal+Dynamics+Spoken+Language+Models&searchtype=title)
- [ParaS2S: Benchmarking and Aligning Spoken Language Models for Paralinguistic-Aware Speech-to-Speech Interaction](https://arxiv.org/search/?query=ParaS2S&searchtype=title)

### Evaluator reliability

- [Testing the Testers: Human-Driven Quality Assessment of Voice AI Testing Platforms](https://arxiv.org/search/?query=Testing+the+Testers+Voice+AI&searchtype=title)
- [Benchmarking LLM Judges for Voice-Agent Evaluation](https://arxiv.org/search/?query=Benchmarking+LLM+Judges+Voice-Agent&searchtype=title)

---

## 🧩 Enabling Research

### Turn-taking, endpointing, and interaction control

- [TurnGPT: A Transformer-Based Language Model for Predicting Turn-Taking in Spoken Dialogue](https://arxiv.org/search/?query=TurnGPT&searchtype=title)
- [Voice Activity Projection: Self-Supervised Learning of Turn-Taking Events](https://arxiv.org/search/?query=Voice+Activity+Projection&searchtype=title)
- [Multilingual Turn-Taking Prediction Using Voice Activity Projection](https://arxiv.org/search/?query=Multilingual+Turn-taking+Prediction+Voice+Activity+Projection&searchtype=title)
- [Triadic Multi-Party Voice Activity Projection for Turn-Taking in Spoken Dialogue Systems](https://dblp.org/search?q=Triadic%20Multi-party%20Voice%20Activity%20Projection)
- [Phoenix-VAD: Streaming Semantic Endpoint Detection for Full-Duplex Speech Interaction](https://arxiv.org/search/?query=Phoenix-VAD&searchtype=title)
- [FastTurn: Unifying Acoustic and Streaming Semantic Cues for Low-Latency and Robust Turn Detection](https://arxiv.org/search/?query=FastTurn+Turn+Detection&searchtype=title)
- [JAL-Turn: Joint Acoustic-Linguistic Modeling for Real-Time Turn Detection](https://arxiv.org/search/?query=JAL-Turn&searchtype=title)
- [X2-Turn: Frame-Synchronous Dual-Head Modeling for Joint Streaming ASR and Turn State Prediction](https://arxiv.org/search/?query=X2-Turn&searchtype=title)
- [SoulX-Duplug: Plug-and-Play Streaming State Prediction Module](https://arxiv.org/search/?query=SoulX-Duplug&searchtype=title)
- [FlexDuo: A Pluggable System for Enabling Full-Duplex Capabilities in Speech Dialogue Systems](https://arxiv.org/search/?query=FlexDuo&searchtype=title)

### Emotion, persona, and expressive interaction

- [Chain-Talker: Chain Understanding and Rendering for Empathetic Conversational Speech Synthesis](https://aclanthology.org/search/?q=Chain-Talker)
- [ChatGPT-EDSS: Empathetic Dialogue Speech Synthesis Trained from ChatGPT-Derived Context Word Embeddings](https://dblp.org/search?q=ChatGPT-EDSS)

### Data, training, and reward modeling

- [SLURP: A Spoken Language Understanding Resource Package](https://aclanthology.org/2020.emnlp-main.588/)
- [SpokenWOZ: A Large-Scale Speech-Text Benchmark for Spoken Task-Oriented Dialogue Agents](https://arxiv.org/search/?query=SpokenWOZ&searchtype=title)
- [DuplexGen: Adaptive Synthesis of Human-AI Turn-Taking Dialogues](https://arxiv.org/search/?query=DuplexGen&searchtype=title)
- [Sommelier: Scalable Open Multi-Turn Audio Pre-Processing for Full-Duplex Speech Language Models](https://arxiv.org/search/?query=Sommelier+Full-duplex+Speech+Language+Models&searchtype=title)
- [Spirit LM: Interleaved Spoken and Written Language Model](https://arxiv.org/search/?query=Spirit+LM&searchtype=title)
- [OpusLM: A Family of Open Unified Speech Language Models](https://arxiv.org/search/?query=OpusLM&searchtype=title)
- [VoXtream / VoXtream2](https://arxiv.org/search/?query=VoXtream&searchtype=title)
- [Dual-Axis Generative Reward Model toward Semantic and Turn-Taking Robustness in Interactive Spoken Dialogue](https://arxiv.org/search/?query=Dual-Axis+Generative+Reward+Model+Spoken+Dialogue&searchtype=title)

---

## 🛡️ Safety and Trustworthiness

- [Voice Jailbreak Attacks against GPT-4o](https://arxiv.org/search/?query=Voice+Jailbreak+Attacks+Against+GPT-4o&searchtype=title)
- [Piggybacking on Perception: Stealthy Concurrent Audio Prompt Injections against Multimodal LLM Agents](https://arxiv.org/search/?query=Piggybacking+on+Perception+Audio+Prompt+Injections&searchtype=title)
- [Auditing Bias and Safety in Voice AI Customer Care](https://arxiv.org/search/?query=Auditing+Bias+and+Safety+Voice+AI+Customer+Care&searchtype=title)
- [VOICE: A Voice AI Agent System for Prehospital Stroke Assessment](https://arxiv.org/search/?query=Voice+AI+Agent+Prehospital+Stroke+Assessment&searchtype=title)
- [Cloning a Conversational Voice AI Agent from Call Recording Datasets for Telesales](https://arxiv.org/search/?query=Cloning+Conversational+Voice+AI+Agent+Telesales&searchtype=title)
- [NVIDIA: How to Build a Voice Agent with RAG and Safety Guardrails](https://developer.nvidia.com/blog/?s=voice+agent+RAG+safety+guardrails)

---

## 🛠️ Engineering Resources

- [OpenAI: Voice Agents](https://developers.openai.com/api/docs/guides/voice-agents)
- [OpenAI: Realtime API](https://developers.openai.com/api/docs/guides/realtime)
- [OpenAI: Realtime Conversations](https://developers.openai.com/api/docs/guides/realtime-conversations)
- [LiveKit: Solving End-of-Turn Detection](https://blog.livekit.io/using-a-transformer-to-improve-end-of-turn-detection/)
- [Daily / Pipecat: Smart Turn](https://www.daily.co/blog/tag/pipecat/)
- [AWS: Building Real-Time Voice Assistants Compared to Cascading Architectures](https://aws.amazon.com/blogs/machine-learning/?s=real-time+voice+assistant+cascading)
- [AWS: Scalable Voice-Agent Design with Multi-Agent Systems, Tools, and Session Segmentation](https://aws.amazon.com/blogs/machine-learning/?s=voice+agent+multi-agent+session)
- [AWS: Migrating a Text Agent to a Voice Assistant with Amazon Nova Sonic](https://aws.amazon.com/blogs/machine-learning/?s=Nova+Sonic+voice+assistant)
- [AWS: Evaluating Amazon Nova Sonic Voice Agents at Scale](https://aws.amazon.com/blogs/machine-learning/?s=evaluate+Nova+Sonic+voice+agent)
- [a16z: AI Voice Agents](https://a16z.com/ai-voice-agents/)

---

## 🎒 Recommended Starting Points

- **Full-duplex foundation:** [Moshi](https://arxiv.org/abs/2410.00037)
- **Reasoning while listening:** [SHANKS](https://arxiv.org/search/?query=SHANKS+Simultaneous+Hearing+and+Thinking&searchtype=title)
- **Voice-driven tool use:** [AURA](https://arxiv.org/search/?query=AURA+Automated+Tool+Use+Voice-Driven+Tasks&searchtype=title)
- **Tool-enabled speech model:** [Step-Audio 2](https://arxiv.org/abs/2507.16632)
- **Long-horizon candidate:** [DuplexSLA](https://arxiv.org/abs/2605.20755)
- **Voice-agent evaluation:** [EVA-Bench](https://arxiv.org/search/?query=EVA-Bench+Voice+Agents&searchtype=title)
- **Proactivity evaluation:** [ProVoice-Bench](https://arxiv.org/search/?query=ProVoice-Bench&searchtype=title)
- **Safety:** [Voice Jailbreak Attacks against GPT-4o](https://arxiv.org/search/?query=Voice+Jailbreak+Attacks+Against+GPT-4o&searchtype=title)

---

## 🗞️ Recent News

- **[2026.09.19]** 🎙️ Awesome Voice Agents was created.
- **[2026.09.20]** 🧭 The L0-L4 capability taxonomy and the first research collection were released.

---

## 🤝 How to Contribute

Contributions from researchers and practitioners are welcome. Please open an [issue](https://github.com/Kwwwww74/Awesome-Voice-Agent/issues) or submit a pull request.

For a new paper, model, benchmark, dataset, or engineering resource, please provide:

```text
Title:
Authors or organization:
Year:
Paper/project URL:
Code/model URL (if available):
Suggested category or level:
One-sentence justification:
Evidence for reasoning, tool use, or long-horizon behavior (if applicable):
```

### Classification checklist

- Is this a complete interactive system, or a supporting component/resource?
- Is it a pre-LLM system and therefore L0?
- For L2, where is reasoning evaluated?
- For L3, does the system execute a tool and consume its result?
- For L4, does the evaluation include persistent state, replanning, or failure recovery?
- Is the proposed level demonstrated, or only claimed by the architecture or product page?

You can also contact the maintainer at **kaiwenluo74@gmail.com**.

---

## 📝 Citation

If this repository is helpful to your research, please cite it as:

```bibtex
@misc{luo2026awesomevoiceagents,
  title        = {Awesome Voice Agents},
  author       = {Luo, Kaiwen and Contributors},
  year         = {2026},
  howpublished = {\url{https://github.com/Kwwwww74/Awesome-Voice-Agent}},
  note         = {A curated collection and capability taxonomy for voice agents}
}
```

---

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=Kwwwww74/Awesome-Voice-Agent&type=Date)](https://star-history.com/#Kwwwww74/Awesome-Voice-Agent&Date)

---

## 🙏 Acknowledgement

- Maintainer: [Kevin Luo](https://kwwwww74.github.io)
- The organization of this repository is inspired by [Awesome Trustworthy Audio-LLMs](https://github.com/Kwwwww74/Awesome-Trustworthy-AudioLLMs).
- Thanks to all researchers, engineers, and contributors advancing voice-agent research.

---

<p align="center">
  If you find this repository useful, please consider giving it a ⭐ and contributing new work.
</p>
