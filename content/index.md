---
title: "GSoC 2025: Tölvera NLI - Project Completed!"
description: "My completed Google Summer of Code 2025 project - a Natural Language Interface for Tölvera that outperforms frontier models on specialized tasks."
tags:
  - gsoc
  - tolvera
  - nli
  - llm
---

Welcome to my project documentation for the **Google Summer of Code 2025** for Tölvera! This site documents my journey through the Tölvera Natural Language Interface project.

> 🎉 **Project Completed!**
>
> After 12 weeks of development, the Tölvera NLI is now functional and outperforms (thankfully 😅) frontier models like Gemini 2.5 Pro and Claude Opus on Tölvera-specific tasks.
>
> **[[gsoc_final_report|Read the Full Final Report]]** | **[Watch the Demo Video](https://www.youtube.com/watch?v=0puPLa05LeY)** | **[Final Overview Video](https://www.youtube.com/watch?v=jllyR3wAETc)**

## Final GSoC Overview Video

![GSoC Final Overview](https://www.youtube.com/watch?v=jllyR3wAETc)

A summary of the entire 12-week GSoC development journey, showcasing the Natural Language Interface for Tölvera from concept to completion.

## Gallery of Generated Sketches

<style>
.video-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin: 30px 0;
}

.video-item {
  text-align: center;
}

.video-item video {
  width: 100%;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.video-caption {
  margin-top: 10px;
  font-size: 0.9em;
  color: #666;
  font-style: italic;
}

.achievement-box {
  background: #f0f7ff;
  border-left: 4px solid #2196f3;
  padding: 15px;
  margin: 20px 0;
  border-radius: 4px;
}

.achievement-box h3 {
  margin-top: 0;
  color: #1976d2;
}

@media (max-width: 768px) {
  .video-gallery {
    grid-template-columns: 1fr;
  }
}
</style>

<div class="video-gallery">
  <div class="video-item">
    <video controls loop muted autoplay>
      <source src="imgs/particle_motion_repel.mp4" type="video/mp4">
    </video>
    <div class="video-caption">Two species repel each other while moving</div>
  </div>
  
  <div class="video-item">
    <video controls loop muted autoplay>
      <source src="imgs/complex_interactions.mp4" type="video/mp4">
    </video>
    <div class="video-caption">Complex self-organizing behavior</div>
  </div>
  
  <div class="video-item">
    <video controls loop muted autoplay>
      <source src="imgs/boids-osc.mp4" type="video/mp4">
    </video>
    <div class="video-caption">Boids with OSC mapping</div>
  </div>
  
  <div class="video-item">
    <video controls loop muted autoplay>
      <source src="imgs/particle-life.mp4" type="video/mp4">
    </video>
    <div class="video-caption">Particle Life simulation</div>
  </div>
</div>

## The Textual User Interface

![Textual UI Screenshot](imgs/system-screenshot.png)

The completed interface allows users to type natural language descriptions and instantly generate working Tölvera simulations - no coding required!

## Project Overview & Results

My project enhanced creative workflows within the [Tölvera](https://github.com/Tolvera/tolvera) artificial life library. Here is the official abstract from my proposal:

> This project proposes to refine and significantly extend a functional proof-of-concept (POC) Natural Language Interface (NLI) for Tölvera, aiming to enhance creative workflows by improving accessibility for artists and researchers. The NLI translates natural language commands into Tölvera sketch generation and modification, acting as an interactive collaborator for users regardless of their coding expertise. Leveraging local Large Language Models (LLMs) via Ollama prioritizes user privacy and control. The existing tv.llm module, demonstrated for Flock and Slime simulations, uses Pydantic for validation and Jinja2 for reliable code generation. Core GSoC work involves expanding this architecture to more Tölvera modules (including tv.vera, tv.osc, tv.cv, tv.mp, tv.iml), refining prompt strategies, enhancing the user interface concept, and ensuring structured outputs. Evaluation will use functional tests, schema adherence metrics, qualitative user feedback, and LLM-as-a-judge assessments. This project aims to elevate the prototype into a core Tölvera feature, lowering technical barriers for the community of users.

<div class="achievement-box">

### Key Achievements

- **60-85% success rates** for various behavior types (gravity, interactions, species detection)
- **Outperformed frontier models** - Our system succeeded where Gemini 2.5 Pro and Claude Opus failed for initial correct sketch generation
- **Full Textual UI** with syntax highlighting, error recovery, and natural language refinement
- **12 weeks of documented development** with weekly progress reports

</div>

### Comparative Analysis Results

Our system was tested against frontier models (Gemini 2.5 Pro and Claude Opus) with the following results:

**Test Case: Day/Night Cycle Behavior**

- **Our System (Gemini 2.0 Flash):** ✅ Worked on first attempt
- **Gemini 2.5 Pro (Zero-shot):** ❌ Multiple failures with Tölvera API errors
- **Claude Opus (Zero-shot):** ❌ Fundamental misunderstanding of module structure
- **Gemini 2.5 Pro (Full Tölvera Context):** ✅ Generates after several refinements
- **Claude Opus (Full Tölvera Context):** ✅ Generates after several refinements

**Test Case: Food Competition**

- **Our System (Gemini 2.0 Flash):** ✅ Correct implementation with one refinement (for color)
- **Gemini 2.5 Pro:** ⚠️ Works but incorrect mechanics after several refinements
- **Claude Opus:** ❌ Taichi scope violations, never runs

### How It Works

1. **User** provides a natural language command (e.g., "Create a flock with 2 species, one red and one blue").
2. **BehaviorOrchestrator** analyzes and decomposes the request into implementable components
3. **StateManager** dynamically creates required states based on behavior needs
4. **SpeciesManager** create species requirements based on descriptions
5. **CodeGenerator** synthesizes Taichi expert functions with physics-aware prompts
6. **TemplateRenderer** assembles experts and kernels into complete executable sketches
7. The user can **execute the script**, see the visual output, and iteratively refine their creation

### Core Technologies

- **Python**
- **Tölvera**
- **Ollama** (for local LLMs)
- **Gemini 2.0 Flash** (primary synthesis model)
- **Pydantic** (for data validation)
- **Jinja2** (for template rendering)
- **Textual** (for the terminal UI)

---

## Project Resources

### Documentation

- **[[gsoc_final_report|Final Report]]** - Complete technical documentation with architecture diagrams
- **[[journal/week1|Weekly Development Journals]]** - 12 weeks of progress
- **[[journal/midterm|Midterm Report]]** - 6-week implementation plan

### Code & Demos

- **[Demo Video](https://www.youtube.com/watch?v=0puPLa05LeY)** - Full walkthrough of the Natural Language Interface
- **[Final Overview Video](https://www.youtube.com/watch?v=jllyR3wAETc)** - Complete GSoC project summary
- **[Source Code](https://github.com/mclemcrew/tolvera/tree/final-gsoc-report)** - Complete implementation
- **[Try It Yourself](https://github.com/mclemcrew/tolvera/tree/final-gsoc-report/ui_scripts)** - Demo scripts and UI

---

_Special thanks to the Tölvera community and GSoC mentors (Jack, Victor, and Piotr) for their support throughout this project._
