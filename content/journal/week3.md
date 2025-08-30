
---
title: "Week 3: Research and Planning"
description: Exploring MoE and PoE architectures
tags:
  - journal-entry
  - research
  - gsoc
---

### Week 3: Research and Planning for Expert Architectures

This week was primarily focused on researching and planning the implementation of specialized agent architectures for the `tv.llm` module. After exploring various approaches to improve the reliability of natural language to code translation, I settled on implementing a Mixture of Experts (MoE) and Program of Experts (PoE) architecture.

The core idea was to move away from a monolithic LLM approach to a more modular system where specialized agents would handle specific aspects of the Tölvera code generation. This week involved:

- Researching existing MoE/PoE implementations and their applicability to creative coding
- Designing the agent orchestration system
- Planning the specialized agents needed for different aspects of particle system generation

For the detailed implementation of these concepts and the actual code developed, please see [[week4|Week 4: MoE and PoE Implementation]], where the full architecture was built out with the `CodeGenerationOrchestrator` and its suite of specialized agents.

### Resources
- [Programmatic Video Prediction Using Large Language Models](https://arxiv.org/abs/2505.14948)
- [PoE World Paper](https://arxiv.org/abs/2505.10819)
- [Guidance LLM Steering](https://github.com/guidance-ai/guidance)