---
name: "scene-engine"
description: "Use when writing or auditing a film scene, sequence, outline or script for structural strength: goal, obstacle, tactic, reversal and value shift."
---

# Scene engine

Adapted from Higgsfield's "prompt engine" skill (Oct 2026), which is a screenplay-structure tool, not a prompt formatter. Write and audit scenes against a five-element engine. These definitions are specific; apply them as written, not textbook versions.

## The five elements

### 1. Goal
The single, unchanging thing the hero fights for: to fix what has already been established and reach the result that resolves it, fast. "Already established" can be backstory or the previous minute.
- The story goal never changes, and the hero is never wrong about it. They can be wrong about tactics.
- Every scene goal must be a causal link toward the story goal. Removal test: if the scene can be cut and the chain still holds, it fails.
- The right move is dictated by obstacle plus stakes. A tactic the stakes wouldn't justify is a flaggable inconsistency (bad writing or deliberate self-sabotage; name which).

### 2. Obstacle
A strong circumstance that jeopardizes one stage of the path or the whole goal. It threatens, not merely costs.
- Either a branching search space or a single hard wall (which spawns a new sub-goal).
- Scale: local (threatens the current stage) or global (threatens the whole goal). Always name which.
- Audit: name exactly what is at risk and at what scale. Nothing at risk means the scene goes slack.

### 3. Tactic
The move the threat forces: a reasonable guess on the hero's current, incomplete knowledge. Search under uncertainty, not stupidity.
- The engine is the gap between what the hero believes and what is true.
- Each failed tactic must return information that narrows the search and reshapes the next move.
- Weak: a tactic with no reason to try it, or a failure that teaches nothing.

### 4. Reversal
A turn against expectation:
1. My own action flips on me (what I did for something starts working against it).
2. Hidden agency revealed (the person I thought I was acting on was acting on me all along). Often fires when the truth gap closes.
3. General: the situation turns opposite to what the tactic intended.
- At least one reversal per sequence. A sequence runs from when a specific jeopardy opens to when it resolves. Sequences nest; each resolving unit needs its own reversal.

### 5. Value shift
The change in the AUDIENCE's verdict on a character, triggered by a reversal. It happens in the viewer's mind, not on the page.
- A reversal with no value shift is inert. If you can't name a before-verdict and an after-verdict, the reversal is dead weight.
- Across a sequence, the verdicts should build a designed, deepening arc (nice, then cunning, then desperate, then devoted...), not random flip-flops.

## The chain
Goal (fixed; every scene a causal link) → Obstacle (what's at risk, what scale) → Tactic (forced, reasonable, returns information) → Reversal (≥1 per sequence) → Value shift (audience re-judges the character; none means the reversal is useless).

## Modes
- **Audit:** an existing scene, sequence, outline or script. For a full script, first segment it into sequences (jeopardy opens to jeopardy resolves), then audit each.
- **Write:** a new scene or options. Before writing, name all five elements. Options should differ in tactic or reversal, so the value shifts differ, not just tone.
- **Co-write:** back and forth, auditing continuously.

If the story goal is unknown, ask for it; a scene can't be audited for Goal without it.

## Audit output (in chat)

```
SCENE/SEQUENCE: <one line>

CHAIN CHECK
• Goal — <verdict + one line>
• Obstacle — <what's jeopardized + scale + verdict>
• Tactic — <forced? reasonable? returns information? verdict>
• Reversal — <form + present? ≥1 in sequence? verdict>
• Value shift — <before → after per reversal, or INERT; trajectory note>

WEAKEST POINT: <the single element that recovers the most if fixed>

WHAT IF…
1. Minimal fix: change only the weakest point; keep the rest of the user's version.
2. Clean fix: a version that fully works, even if it departs more.
3. Optional: only if it genuinely adds something.
```

Rewritten lines or beats go in screenplay format: sluglines in caps (INT./EXT. LOCATION - TIME), present-tense action, character cue in caps, dialogue below, parentheticals in lower case.

## For AI film work
- Run this before writing video prompts for a new story; the prompt skills handle how a shot looks, this handles whether the scene works.
- The most common real failure: a reversal that turns the plot but doesn't move the audience's verdict. Surface it first.