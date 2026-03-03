# Assess VC Pitch by Three Amigos

## Goal

Stress-test the VC pitch by assembling a **team** of three specialist agents — a UX Researcher, an Engineer, and a Product Manager — who independently review the pitch, then hold a live discussion round where they challenge and build on each other's thinking. A fourth agent synthesises everything into a final assessment document.

This workflow uses the **Claude Code Teams system** (`TeamCreate`, `SendMessage`) so the specialists genuinely communicate with each other during the discussion round, rather than just reading static files. The team lead orchestrates the phases and records the full discussion as a transcript.

### Outputs

| Output | Location |
|--------|----------|
| Final assessment | `05-outputs/vc-pitch-three-amigos-assessment.md` |
| Discussion transcript | `04-process/three-amigos-reviews/discussion-transcript.md` |

## Context

The VC pitch (`05-outputs/vc-pitch.md`) distils interview research into a one-page investment narrative for a personal AI assistant product. A pitch this condensed inevitably makes trade-offs: it emphasises some things and glosses over others. This workflow catches those gaps before investors do.

The review uses the **DVF framework** (Desirability, Feasibility, Viability) — a standard product assessment lens:

- **Desirability** — Do real users actually want this? Does the pitch reflect genuine needs from the research?
- **Feasibility** — Can it be built? Are the technical claims realistic? What hard problems are glossed over?
- **Viability** — Does the business case hold up? Is the market positioning defensible? Is there a path to revenue?

### Why a "Three Amigos" Panel?

A single reviewer tends to agree with itself. Three independent specialists — who first review blind, then actively discuss and challenge each other — surface genuine tensions. The disagreements between lenses are often more valuable than the agreements.

### How It Works (Teams Approach)

This workflow creates a **formal Claude Code team** using `TeamCreate`. The orchestrator acts as team lead and coordinates five phases:

```
Phase 0 — Prepare
    Python script checks inputs exist, creates working folders.

Phase 1 — Independent Reviews (3 teammates work in parallel)
    Team lead assigns review tasks to all three specialists.
    Each writes a structured assessment from their lens.
    They cannot see each other's work yet.

Phase 2 — Discussion Round (teammates message each other)
    Team lead shares all Phase 1 reviews with all three specialists.
    Specialists use SendMessage to discuss — challenging, agreeing,
    and building on each other's points.
    Team lead records every message into a discussion transcript.

Phase 3 — Synthesis (1 teammate)
    Synthesiser agent reads all review files + the discussion transcript
    and produces the final assessment document.

Phase 4 — Verify & Shutdown
    Python script checks the output meets acceptance criteria.
    Team lead shuts down all teammates and cleans up the team.
```

### What Gets Recorded in the Discussion Transcript

The discussion transcript (`04-process/three-amigos-reviews/discussion-transcript.md`) captures the full Phase 2 conversation — every message between the three specialists, in chronological order. It reads like a meeting transcript:

- Who said what, and when (message order preserved)
- Points of agreement and disagreement
- Follow-up questions and responses
- Cross-cutting insights that emerged from the exchange

This transcript is valuable in its own right — it shows the reasoning behind the final recommendations, not just the conclusions.

## Strategic Success Criteria

- Identify weaknesses in the pitch before investors do
- Surface tensions between what users want (Desirability), what can be built (Feasibility), and what makes business sense (Viability)
- Produce prioritised, actionable recommendations to strengthen the pitch
- Ensure the pitch is grounded in real research evidence, not marketing assumptions
- Preserve the discussion reasoning as a readable transcript for the project team

## Inputs

| Input | Location | Notes |
|-------|----------|-------|
| VC Pitch | `05-outputs/vc-pitch.md` | Must exist. Generate with `analyze-by-vc-pitch` workflow if missing. |
| Strategic Research Brief | `00-brief/strategic-research-brief.md` | Provides the research context and success criteria the pitch should serve. |

## Team Structure

| Role | Agent | Job |
|------|-------|-----|
| **Team Lead** | Orchestrator (you) | Creates team, assigns tasks, records transcript, runs verify, shuts down team |
| **UX Researcher** | `ux-reviewer` | Reviews pitch through Desirability lens |
| **Engineer** | `engineer-reviewer` | Reviews pitch through Feasibility lens |
| **Product Manager** | `pm-reviewer` | Reviews pitch through Viability lens |
| **Synthesiser** | `three-amigos-synthesizer` | Combines all reviews + transcript into final document |

## Acceptance Criteria

The output is complete when **all** of the following are true:

1. Three independent specialist reviews exist (one each for Desirability, Feasibility, Viability)
2. A discussion transcript exists capturing the full Phase 2 exchange between all three specialists
3. The transcript contains genuine back-and-forth — not just three monologues
4. Final synthesis document at `05-outputs/vc-pitch-three-amigos-assessment.md` follows the output template
5. Final document is maximum 5 pages (~2,500 words)
6. Written in bullet points and short sentences throughout — no walls of prose
7. Cross-Cutting Tensions section identifies genuine disagreements between the three lenses
8. Consensus Recommendations section contains no more than 5 prioritised actions that all three lenses support
9. Team is cleanly shut down after completion (no orphaned teammates)

## Workflow

See `02-workflows/assess-vc-pitch-by-three-amigos/` for the detailed orchestration, scripts, and agent definitions.
