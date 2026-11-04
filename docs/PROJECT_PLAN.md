# THE LAST SANCTUARY — Project Plan

## Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| R1 | Egyptian Arabic dialogue and narration | Must |
| R2 | 60–90 minute target runtime | Should |
| R3 | Free/open-source-first toolchain | Must |
| R4 | Human approval at every major milestone | Must |
| R5 | Versioned asset tracking | Should |
| R6 | No paid API keys committed to repo | Must |

## Phases

### Phase 1 — Pre-Production (Weeks 1–4)
- Write and iterate on the script using an AI Writer agent
- Build a world bible and character continuity database
- Generate shot-list and storyboards via the Director/Storyboard agent
- **Acceptance**: Script v1.0 approved; world bible covers all major lore; storyboard for Act 1 complete

### Phase 2 — Prototype Pipeline (Weeks 5–8)
- Implement free/open-source speech-to-text and voice-synthesis modules
- Test visual generation with open-source diffusion models on sample scenes
- Set up automated quality-control checks (audio clarity, frame consistency)
- **Acceptance**: End-to-end pipeline demo for a 2-minute scene using only free tools

### Phase 3 — Production Run (Weeks 9–16)
- Scale to full feature length with batch processing
- Implement retry rules for failed generations
- Human QC gates before final render pass
- **Acceptance**: One complete 60-minute cut delivered; production metrics (success rate, avg. retry count) documented

### Phase 4 — Post-Production & Release (Weeks 17–20)
- Final color grading, sound mixing, and subtitle insertion
- Archive all assets in `assets/` directory structure
- **Acceptance**: Final master delivered; archive integrity verified

## Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Free image-generation models produce inconsistent characters | High | Use reference-guided generation; manual retouching at approval gates |
| Voice synthesis for Egyptian Arabic lacks quality | Medium | Use open-source voices as fallback; allow voice actor dubbing phase |
| GPU compute limits for local generation | Medium | Batch small scenes; use cloud free tiers where available |
| Legal concerns with open-source model training data | Low | Document provenance of every model; prefer models with clear licenses |

## Acceptance Criteria Summary

- [ ] Script reaches v1.0 with Egyptian Arabic dialogue
- [ ] World bible covers main characters, locations, lore
- [ ] Storyboard for all acts at shot level
- [ ] Free-toolchain demo for 2-minute scene works end-to-end
- [ ] Production metrics dashboard tracks success rate per agent
- [ ] Final master delivered at 60+ minutes
- [ ] All secrets excluded from version control
