---
title: "GSoC 2025: Tölvera NLI"
description: "My project journal for Google Summer of Code 2025, focused on enhancing Tölvera with a Natural Language Interface."
tags:
  - gsoc
  - tolvera
  - nli
  - llm
---

Welcome to my project log for **Google Summer of Code 2025**! This site will serve as a public journal for my work on the Tölvera project.

## Project Overview

My project focuses on enhancing creative workflows within the [Tölvera](https://github.com/Tolvera/tolvera) creative coding library. Here is the official abstract from my proposal:

> This project proposes to refine and significantly extend a functional proof-of-concept (POC) Natural Language Interface (NLI) for Tölvera, aiming to enhance creative workflows by improving accessibility for artists and researchers. The NLI translates natural language commands into Tölvera sketch generation and modification, acting as an interactive collaborator for users regardless of their coding expertise. Leveraging local Large Language Models (LLMs) via Ollama prioritizes user privacy and control. The existing tv.llm module, demonstrated for Flock and Slime simulations, uses Pydantic for validation and Jinja2 for reliable code generation. Core GSoC work involves expanding this architecture to more Tölvera modules (including tv.vera, tv.osc, tv.cv, tv.mp, tv.iml), refining prompt strategies, enhancing the user interface concept, and ensuring structured outputs. Evaluation will use functional tests, schema adherence metrics, qualitative user feedback, and LLM-as-a-judge assessments. This project aims to elevate the prototype into a core Tölvera feature, lowering technical barriers for the community of users.

### The Goal

The primary motivation for this project is to make the powerful tools in Tölvera more accessible. Tölvera is a fantastic Python environment for generative art, but its reliance on programming can be a hurdle for artists and researchers who aren't primarily coders. The goal is to build an NLI that acts as a bridge, translating a user's creative intent from natural language into functional Tölvera code.

### How It Works

The core of the project is the `tv.llm` module, which follows a clear, robust workflow:

1.  A **user** provides a natural language command (e.g., "Create a flock with 2 species, one red and one blue").
2.  The command is sent to the **Prompt Formulation** component, where it's enhanced with examples, schema definitions, and other context to create an effective prompt for the LLM. 
3.  The enhanced prompt is sent to a local **Large Language Model** (LLM) running via Ollama. 
4.  The LLM returns a structured **JSON configuration** based on the prompt. 
5.  This JSON is **validated** against a Pydantic model to ensure all parameters are correct. If not, error handling is triggered.
6.  Once validated, the configuration is passed to a **Jinja2 template**, which generates the final, executable Python code for the Tölvera sketch.
7.  The user can then **execute the script**, see the visual output, and continue the conversation to iteratively refine their creation.

### Core Technologies
* **Python**
* **Tölvera**
* **Ollama** (for local LLMs)
* **Pydantic** (for data validation)
* **Jinja2**

---

You can follow my progress by exploring the notes on this site. I'll be documenting my weekly progress, technical challenges, and key learnings as I work to bring this interface to life.