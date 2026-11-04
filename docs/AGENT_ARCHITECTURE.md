# THE LAST SANCTUARY — Agent Architecture

This document defines the AI agents, their responsibilities, and the handoff protocol.

> **Note:** These agents represent the planned architecture. Free/open-source models and
> prompt-based orchestration are used as building blocks; no single agent guarantees
> fully autonomous creative output at production scale today.

## Agent Roster

### 1. Writer Agent
- **Role**: Draft and revise the screenplay in Egyptian Arabic
- **Inputs**: Project brief, character notes, world bible
- **Outputs**: Scene-by-scene script, dialogue drafts, narration text
- **Tools**: Open-source LLM (e.g., Llama, Mistral via local API or free tier)
- **Handoff**: Sends approved scenes to Director/Storyboard and Voice/Sound

### 2. Continuity / Worldbuilding Agent
- **Role**: Maintain a living world bible and track character consistency
- **Inputs**: Script drafts, previous asset decisions
- **Outputs**: Character sheets, location descriptions, timeline, lore notes
- **Tools**: Embedding-based retrieval, vector database (Chroma / FAISS)
- **Handoff**: Provides reference descriptions to Visual Generation for scene composition

### 3. Director / Storyboard Agent
- **Role**: Convert script into shot lists and visual storyboards
- **Inputs**: Approved scenes from Writer Agent
- **Outputs**: Shot list with camera angles, lighting notes, composition sketches
- **Tools**: LLM for shot description; free image models for thumbnail storyboards
- **Handoff**: Sends scene prompts and composition references to Visual Generation

### 4. Visual Generation Agent
- **Role**: Produce visual frames and short clips per storyboard
- **Inputs**: Shot prompts, character reference images from Continuity Agent
- **Outputs**: Sequence of frames/clips, style guide adherence report
- **Tools**: Open-source diffusion models (Stable Diffusion variants), local GPU or free cloud tier
- **Handoff**: Sends raw visual clips to Editor/QC for assembly and quality check

### 5. Voice / Sound Agent
- **Role**: Generate dialogue audio, narration, and basic soundscapes
- **Inputs**: Dialogue from Writer Agent, scene mood notes from Director Agent
- **Outputs**: Spoken dialogue WAVs, ambient sound layers, music cues
- **Tools**: Free/open-source TTS (e.g., Coqui, Piper), open-source audio libraries (Librosa, FFmpeg)
- **Handoff**: Sends audio tracks to Editor/QC for sync and mixing

### 6. Editor / QC Agent
- **Role**: Assemble clips, verify continuity, enforce quality thresholds
- **Inputs**: Visual clips from Visual Generation, audio from Voice/Sound
- **Outputs**: Rendered scenes, QC pass/fail report, retry suggestions
- **Tools**: FFmpeg for assembly, custom scripts for QC metrics (audio loudness, frame consistency)
- **Handoff**: Returns scenes to human approver; if fail, routes back to the responsible agent with retry instructions

## Handoff Protocol

```
Writer ──→ Director ──→ Visual Generation ──┐
Writer ──→ Voice/Sound ─────────────────────┤
                                            ├──→ Editor/QC ──→ Human Approval
Continuity ──────────────────────────────────┘
```

- Every handoff includes a structured JSON manifest: agent, version, inputs, outputs, timestamps
- Failed generations trigger an automatic retry (max 3 attempts) with adjusted prompts
- Human approval gates are required before any asset enters the final render pipeline
