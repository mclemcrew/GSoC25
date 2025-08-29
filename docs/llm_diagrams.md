# Tölvera LLM Engine: Visual Architecture Guide

This document provides architectural diagrams for the Tölvera LLM code generation engine. These diagrams illustrate how the system transforms natural language descriptions into executable particle simulations through a multi-stage pipeline. The engine leverages language models with intelligent context selection to generate optimized Taichi GPU kernels for complex particle behaviors.

## Main Workflow: Natural Language to Code Pipeline

This diagram illustrates the complete synthesis pipeline from natural language input to executable code output. The flow demonstrates how each component processes and transforms data through the system.

```mermaid
flowchart TB
    %% Styling
    classDef userNode fill:#e1f5e1,stroke:#4caf50,stroke-width:3px,color:#1b5e20
    classDef orchestratorNode fill:#fff3e0,stroke:#ff9800,stroke-width:2px,color:#e65100
    classDef analysisNode fill:#e3f2fd,stroke:#2196f3,stroke-width:2px,color:#0d47a1
    classDef synthNode fill:#fce4ec,stroke:#e91e63,stroke-width:2px,color:#880e4f
    classDef outputNode fill:#f3e5f5,stroke:#9c27b0,stroke-width:3px,color:#4a148c
    classDef contextNode fill:#fffde7,stroke:#fbc02d,stroke-width:2px,color:#f57f17

    %% Entry Point
    User["User Description<br/>'particles swarm and glow'"]
    UI[Textual UI<br/>tolvera_llm_demo.py]
    BO[BehaviorOrchestrator<br/>Main Controller]

    User --> UI
    UI --> BO

    %% Analysis & Decomposition Stage
    subgraph Analysis ["<br/>Analysis & Decomposition Stage"]
        BA[BehaviorAnalyzer<br/>Decomposes Complex Behaviors]
        DC{Decomposed<br/>Components?}
        Components[Component List<br/>- Force behaviors<br/>- Visual effects<br/>- State updates]
        SimplePath[Single Behavior]

        BA --> DC
        DC -->|Yes| Components
        DC -->|No| SimplePath
    end

    %% Connect to Analysis
    BO --> BA

    %% Detection & Configuration
    subgraph Detection ["<br/>Detection & Configuration"]
        SM[StateManager<br/>Detects Required States]
        SPM[SpeciesManager<br/>Detects Species]
        CR[ColorResolver<br/>Maps Colors to RGBA]
        States[Custom States<br/>- Global<br/>- Particle<br/>- Species]
        Species[Species Config<br/>- IDs & Names<br/>- Colors<br/>- Interactions]

        SM --> States
        SPM --> Species
        SPM --> CR
    end

    %% Connect Analysis to Detection
    Components --> SM
    Components --> SPM
    SimplePath --> SM
    SimplePath --> SPM

    %% Context Selection
    subgraph Context ["<br/>Intelligent Context Selection"]
        CS[ContextSelector<br/>LLM-Powered Selection]
        BaseCtx[Base Context<br/>Core APIs Always Loaded]
        SuppCtx[Supplementary Context<br/>Dynamically Selected Patterns]
        MergedCtx[Merged Context]

        CS --> BaseCtx
        CS --> SuppCtx
        BaseCtx --> MergedCtx
        SuppCtx --> MergedCtx
    end

    %% Connect to Context
    Components --> CS
    SimplePath --> CS

    %% Synthesis Loop
    subgraph Synthesis ["<br/>Expert Synthesis Loop"]
        CG[CodeGenerator<br/>Synthesizes Experts]
        ExpertCode[Expert Functions<br/>@ti.func decorated]
        BR[BehaviorRegistry<br/>Stores & Manages Experts]
        CheckMore{More<br/>Components?}
        KernelGen[Generate Kernels]

        CG --> ExpertCode
        ExpertCode --> BR
        BR --> CheckMore
        CheckMore -->|Yes| CG
        CheckMore -->|No| KernelGen
    end

    %% Connect to Synthesis
    MergedCtx --> CG
    States --> CG
    Species --> CG

    %% Template Rendering - Simplified
    subgraph Rendering ["<br/>Template Rendering"]
        TR[TemplateRenderer<br/>Jinja2 Templates]

        subgraph Kernels ["Kernel Generation"]
            IntKernel[Integration Kernel]
            DrawKernel[Drawing Kernel]
            UtilKernel[Utility Kernel]
        end

        subgraph DataModels ["Data Model Rendering"]
            ExpertRender[Expert Functions]
            ForceComp[Force Computation]
            DrawComp[Drawing Computation]
        end

        SketchRender[render_sketch<br/>Final Assembly]

        TR --> Kernels
        TR --> DataModels
        Kernels --> SketchRender
        DataModels --> SketchRender
    end

    %% Connect to Rendering
    KernelGen --> TR
    BR -.-> TR
    States -.-> TR
    Species -.-> TR

    %% Final Output - Place at bottom
    SketchRender ==> FinalSketch

    FinalSketch[["<br/>Generated Sketch<br/>Complete Python/Taichi Code<br/>Ready to Run"]]

    %% Apply styles
    class User userNode
    class BO orchestratorNode
    class BA,SM,SPM,CR analysisNode
    class CS,BaseCtx,SuppCtx,MergedCtx contextNode
    class CG,BR,ExpertCode,CheckMore,KernelGen synthNode
    class TR,IntKernel,DrawKernel,UtilKernel,ExpertRender,ForceComp,DrawComp,SketchRender synthNode
    class FinalSketch outputNode
    class States,Species outputNode
```

## Context Selection Architecture

This diagram details the intelligent context selection mechanism. The system employs a two-tier approach where base contexts are always loaded while supplementary contexts are dynamically selected based on behavior requirements, optimizing token usage and generation quality.

```mermaid
flowchart TB
    %% Styling
    classDef userNode fill:#e1f5e1,stroke:#4caf50,stroke-width:3px,color:#1b5e20
    classDef orchestratorNode fill:#fff3e0,stroke:#ff9800,stroke-width:2px,color:#e65100
    classDef analysisNode fill:#e3f2fd,stroke:#2196f3,stroke-width:2px,color:#0d47a1
    classDef synthNode fill:#fce4ec,stroke:#e91e63,stroke-width:2px,color:#880e4f
    classDef outputNode fill:#f3e5f5,stroke:#9c27b0,stroke-width:3px,color:#4a148c
    classDef contextNode fill:#fffde7,stroke:#fbc02d,stroke-width:2px,color:#f57f17

    %% Entry Point
    User["User Description<br/>'particles swarm and glow'"]
    UI[Textual UI<br/>tolvera_llm_demo.py]
    BO[BehaviorOrchestrator<br/>Main Controller]

    User --> UI
    UI --> BO

    %% Analysis & Decomposition Stage
    subgraph Analysis ["Analysis & Decomposition Stage"]
        BA[BehaviorAnalyzer<br/>Decomposes Complex Behaviors]
        DC{Decomposed<br/>Components?}
        Components[Component List<br/>- Force behaviors<br/>- Visual effects<br/>- State updates]
        SimplePath[Single Behavior]

        BA --> DC
        DC -->|Yes| Components
        DC -->|No| SimplePath
    end

    %% Connect to Analysis
    BO --> BA

    %% Detection & Configuration
    subgraph Detection ["Detection & Configuration"]
        SM[StateManager<br/>Detects Required States]
        SPM[SpeciesManager<br/>Detects Species]
        CR[ColorResolver<br/>Maps Colors to RGBA]
        States[Custom States<br/>- Global<br/>- Particle<br/>- Species]
        Species[Species Config<br/>- IDs & Names<br/>- Colors<br/>- Interactions]

        SM --> States
        SPM --> Species
        SPM --> CR
    end

    %% Connect Analysis to Detection
    Components --> SM
    Components --> SPM
    SimplePath --> SM
    SimplePath --> SPM

    %% Context Selection
    subgraph Context ["Intelligent Context Selection"]
        CS[ContextSelector<br/>LLM-Powered Selection]
        BaseCtx[Base Context<br/>Core APIs Always Loaded]
        SuppCtx[Supplementary Context<br/>Dynamically Selected Patterns]
        MergedCtx[Merged Context]

        CS --> BaseCtx
        CS --> SuppCtx
        BaseCtx --> MergedCtx
        SuppCtx --> MergedCtx
    end

    %% Connect to Context
    Components --> CS
    SimplePath --> CS

    %% Synthesis Loop
    subgraph Synthesis ["Expert Synthesis Loop"]
        CG[CodeGenerator<br/>Synthesizes Experts]
        ExpertCode[Expert Functions<br/>@ti.func decorated]
        BR[BehaviorRegistry<br/>Stores & Manages Experts]
        CheckMore{More<br/>Components?}
        KernelGen[Generate Kernels]

        CG --> ExpertCode
        ExpertCode --> BR
        BR --> CheckMore
        CheckMore -->|Yes| CG
        CheckMore -->|No| KernelGen
    end

    %% Connect to Synthesis
    MergedCtx --> CG
    States --> CG
    Species --> CG

    %% Template Rendering - Simplified
    subgraph Rendering ["Template Rendering"]
        TR[TemplateRenderer<br/>Jinja2 Templates]

        subgraph Kernels ["Kernel Generation<br/><br/>"]
            IntKernel[Integration Kernel]
            DrawKernel[Drawing Kernel]
            UtilKernel[Utility Kernel]
        end

        subgraph DataModels ["Data Model Rendering<br/><br/>"]
            ExpertRender[Expert Functions]
            ForceComp[Force Computation]
            DrawComp[Drawing Computation]
        end

        SketchRender[render_sketch<br/>Final Assembly]

        TR --> Kernels
        TR --> DataModels
        Kernels --> SketchRender
        DataModels --> SketchRender
    end

    %% Connect to Rendering
    KernelGen --> TR
    BR -.-> TR
    States -.-> TR
    Species -.-> TR

    %% Final Output - Place at bottom
    SketchRender ==> FinalSketch

    FinalSketch[["<br/>Generated Sketch<br/>Complete Python/Taichi Code<br/>Ready to Run"]]

    %% Apply styles
    class User userNode
    class BO orchestratorNode
    class BA,SM,SPM,CR analysisNode
    class CS,BaseCtx,SuppCtx,MergedCtx contextNode
    class CG,BR,ExpertCode,CheckMore,KernelGen synthNode
    class TR,IntKernel,DrawKernel,UtilKernel,ExpertRender,ForceComp,DrawComp,SketchRender synthNode
    class FinalSketch outputNode
    class States,Species outputNode
```

## Architecture Components

### Analysis Phase

The BehaviorOrchestrator receives natural language descriptions through the Textual UI and coordinates the synthesis pipeline. Complex behaviors are decomposed by the BehaviorAnalyzer into implementable components including force behaviors, visual effects, and state updates.

### Detection and Configuration

The StateManager analyzes requirements to detect and create necessary custom states (global, particle, or species-level). Concurrently, the SpeciesManager identifies species mentions, extracts relationships, and configures multi-agent interactions. The ColorResolver maps semantic color descriptions to RGBA values for visual consistency.

### Context Selection

The ContextSelector employs a two-tier approach to documentation loading. Base contexts containing core APIs are always included, while supplementary contexts are dynamically selected using LLM analysis based on the specific behavior requirements. This optimization reduces token usage while maintaining generation quality.

### Code Generation

The CodeGenerator synthesizes Taichi expert functions using the merged context and detected configurations. Each generated expert is registered in the BehaviorRegistry, which tracks types, weights, and species associations. The synthesis loop continues until all decomposed components are processed.

### Template Rendering

The TemplateRenderer provides comprehensive code generation through multiple specialized methods:

- **Kernel Generation**: `render_integration_kernel`, `render_utility_kernel`, and `render_drawing_kernel` generate the main execution kernels from registered experts
- **Data Model Conversion**: `render_expert_function` transforms structured data models into Taichi code, delegating to `render_force_computation` for physics and `render_drawing_computation` for visual effects
- **Sketch Assembly**: `render_sketch` combines all generated components (kernels, experts, initialization, states) into a complete executable Python file with proper update call ordering and particle rendering logic

The renderer includes code cleaning utilities to ensure syntactically valid output and uses Jinja2 templates located in the `templates/` directory for consistent code structure.

## Development Notes

These diagrams represent the architecture as implemented for the Google Summer of Code 2025 final submission. The modular design facilitates extension through:

- Adding new behavior patterns to the context library
- Implementing additional LLM providers in the factory pattern
- Extending the template system with new kernel types
- Creating custom decomposition strategies for novel behavior categories

The system maintains clear separation of concerns with each component responsible for a specific aspect of the synthesis pipeline. Refer to the README.md files in each subdirectory for detailed implementation notes and extension guidelines.
