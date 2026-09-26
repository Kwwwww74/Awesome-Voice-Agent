# 🎙️ Awesome Voice Agents

<p align="center">
  <a href="https://github.com/sindresorhus/awesome"><img src="https://awesome.re/badge.svg" alt="Awesome"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/stargazers"><img src="https://img.shields.io/github/stars/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub stars"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/network/members"><img src="https://img.shields.io/github/forks/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub forks"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/issues"><img src="https://img.shields.io/github/issues/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub issues"></a>
  <a href="https://github.com/Kwwwww74/Awesome-Voice-Agent/commits/main"><img src="https://img.shields.io/github/last-commit/Kwwwww74/Awesome-Voice-Agent?style=flat-square&logo=github" alt="GitHub last commit"></a>
</p>

<p align="center">
  <em>A curated and continuously updated collection of voice-agent research, organized by demonstrated agentic capability.</em>
</p>

Voice interfaces are evolving from pre-LLM spoken-dialogue systems into agents that can reason, use external tools, and complete long-horizon tasks. This repository tracks that progression through a five-level taxonomy:

> **L0 Pre-LLM Systems → L1 Direct-Response Models → L2 Reasoning Models → L3 Tool-Using Agents → L4 Long-Horizon Agents**

The collection currently contains **137 papers, systems, and documented configurations**.

> [!NOTE]
> Levels describe the **highest capability demonstrated by a concrete system or evaluated configuration**. Natural speech, low latency, full-duplex interaction, multimodality, or a long conversation does not by itself establish a higher level.

**Last updated:** September 26, 2026

---

## 📌 Table of Contents

- [Introduction](#-introduction)
- [What Is a Voice Agent?](#-what-is-a-voice-agent)
- [Capability Taxonomy](#-capability-taxonomy)
- [Research Collections](#-research-collections)
- [Classification Rules](#-classification-rules)
- [How to Contribute](#-how-to-contribute)
- [Citation](#-citation)
- [Star History](#-star-history)
- [Acknowledgement](#-acknowledgement)

---

## 🌍 Introduction

Voice agents combine speech interaction with the ability to make decisions and advance a user goal. Earlier systems relied on rules, task trees, statistical dialogue policies, and specialized neural components. Recent systems increasingly use large language models to reason over spoken input, invoke tools, maintain task state, and act in external environments.

This repository provides:

- a capability-oriented taxonomy spanning the pre-LLM and LLM eras;
- curated collections for direct response, reasoning, tool use, and long-horizon execution;
- operational criteria for distinguishing adjacent levels;
- links to papers, technical reports, official documentation, and project pages.

The taxonomy is intentionally **architecture-agnostic**. A voice agent may use a cascaded ASR–LLM–TTS pipeline, an end-to-end speech language model, or a hybrid design.

---

## 🗣️ What Is a Voice Agent?

We use the following working definition:

> A **voice agent** is an interactive system that receives spoken input, maintains relevant conversational or task state, selects a communicative or external action, and uses the resulting observation to advance a user request or delegated goal.

This definition separates voice agents from systems that only transcribe, synthesize, or classify audio. Standalone ASR, TTS, voice activity detection, datasets, and benchmarks may enable voice agents, but they are not themselves assigned an agent level.

### Capability versus interaction quality

The L0–L4 scale measures **agentic capability**, not overall system quality. The following properties are important but orthogonal to the level:

- latency and streaming efficiency;
- turn-taking, interruption, and full-duplex interaction;
- naturalness, emotion, persona, and voice quality;
- multilingual and multimodal support;
- safety, privacy, robustness, and accessibility.

---

## 🧭 Capability Taxonomy

| Level | Category | Operational criterion | Insufficient evidence |
|---|---|---|---|
| **L0** | **Pre-LLM Voice Systems** | Uses rules, task trees, statistical dialogue policies, or specialized pre-LLM models as the central dialogue and task controller. | Real-world actions or database access do not move a pre-LLM architecture into an LLM-era level. |
| **L1** | **Direct-Response Voice Models** | Produces context-sensitive spoken responses without a demonstrated intermediate reasoning process, autonomous tool loop, or long-horizon controller. | Fluent conversation, full duplex, interruption handling, emotion, persona, or long context alone. |
| **L2** | **Reasoning Voice Models** | Demonstrates explicit, implicit, latent, incremental, or speech-time reasoning that affects the response or decision. | A component named “Thinker,” a prompt to think, or stronger final answers without evidence of a reasoning mechanism. |
| **L3** | **Tool-Using Voice Agents** | Selects and invokes an external tool, retrieval system, API, skill, or environment action, then uses the observation to continue the interaction. | A fixed pipeline, externally triggered retrieval, or merely producing a function-call string without consuming its result. |
| **L4** | **Long-Horizon Voice Agents** | Maintains a persistent goal and task state across a complex multi-step task, coordinating tools and checking, repairing, or replanning execution. | Long audio, many dialogue turns, multiple scripted tool calls, or a single fixed workflow without adaptation. |

### Level progression

```text
L0  Pre-LLM control
 │
 ▼
L1  Direct spoken response
 │   + demonstrated reasoning
 ▼
L2  Reasoning over spoken interaction
 │   + closed-loop external tool use
 ▼
L3  Tool-using voice agent
 │   + persistent goals, multi-step execution, and repair
 ▼
L4  Long-horizon voice agent
```

L0 is a historical architecture category. L1–L4 describe the highest demonstrated capability of LLM-era systems and configurations.

---

## 📚 Research Collections

| Level | Collection | Scope | Entries |
|---|---|---|---:|
| **L0** | [☎️ Pre-LLM Voice Systems](./papers/L0.md) | Rule-based, statistical, and specialized pre-LLM spoken systems | **27** |
| **L1** | [🎙️ Direct-Response Voice Models](./papers/L1.md) | LLM-era spoken interaction without demonstrated reasoning or tool use | **47** |
| **L2** | [🧠 Reasoning Voice Models](./papers/L2.md) | Explicit, latent, incremental, and duplex speech reasoning | **17** |
| **L3** | [🛠️ Tool-Using Voice Agents](./papers/L3.md) | Closed-loop retrieval, function calling, APIs, and environment actions | **43** |
| **L4** | [🧭 Long-Horizon Voice Agents](./papers/L4.md) | Persistent goals, multi-step execution, checking, repair, and replanning | **3** |
|  | **Total** |  | **137** |

Each collection is grouped by publication year and links directly to the corresponding paper, official documentation, or project page.

---

## ✅ Classification Rules

1. **Classify the concrete configuration.** A model family or platform may appear at different levels when different configurations expose different capabilities.
2. **Assign the highest demonstrated level.** Marketing claims or architectural potential are not treated as demonstrated capability.
3. **Keep L0 historical.** Pre-LLM systems remain L0 even when they can query databases, control devices, or complete constrained real-world tasks.
4. **Require evidence for reasoning.** L2 needs an identifiable reasoning mechanism, reasoning-oriented training objective, or reasoning evaluation.
5. **Require a closed tool loop.** L3 requires the agent to select or initiate an external operation, observe its result, and use that result in subsequent behavior.
6. **Require persistent execution for L4.** L4 needs goal and task-state maintenance together with multi-step execution and completion checking, correction, recovery, or replanning.
7. **Separate capability from quality.** Naturalness, latency, duplex communication, emotion, and multimodality are descriptive dimensions rather than level-defining criteria.

### Quick decision procedure

```text
Is the central controller a pre-LLM architecture?
├── Yes → L0
└── No
    ├── Persistent goal + multi-step execution + repair/replanning? → L4
    ├── Closed-loop external tool or environment interaction?      → L3
    ├── Demonstrated intermediate reasoning process?               → L2
    └── Interactive spoken response?                               → L1
```

---

## 🤝 How to Contribute

Contributions from researchers and practitioners are welcome. Please open an [issue](https://github.com/Kwwwww74/Awesome-Voice-Agent/issues) or submit a pull request.

For a new entry, please provide:

```text
Title or system name:
Year:
Paper, documentation, or project URL:
Suggested level:
Evidence supporting the suggested level:
```

Before submitting, please check that:

- speech is part of the interactive decision loop;
- the entry is a system or concrete configuration rather than only a component or benchmark;
- the suggested level follows the operational criteria above;
- the linked source provides evidence for the claimed capability;
- the entry is not already included under another name.

You may also contact the maintainer at **kaiwenluo74@gmail.com**.

---

## 📝 Citation

If this repository is useful for your research, please cite it as:

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

- Maintainer: [Kaiwen Luo](https://kwwwww74.github.io), [Yang Xiao](https://swagshaw.github.io)
- The repository structure is inspired by [Awesome Trustworthy Audio-LLMs](https://github.com/Kwwwww74/Awesome-Trustworthy-AudioLLMs).
- Thanks to all researchers, engineers, and contributors advancing voice-agent research.

If you find this repository useful, please consider giving it a ⭐ and sharing it with the community.
