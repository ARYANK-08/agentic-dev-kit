---
name: explain
description: Use whenever the user asks to explain, walk through, or help them understand anything (code, a flow, a bug, a concept, an architecture, a model output). Picks the clearest output format and writes in simplified technical English.
---

# Explain

Goal: the user understands fast. Pick the lightest format that works, then escalate only when it helps.

## Format ladder

1. **Text** — default. Write in ~80% ASD-STE100 (see rules below).
2. **Diagram** — when the answer is a flow, structure, sequence, or relationship. Use ASCII/Mermaid in the terminal; for a richer one, publish via the Artifact tool (`artifact-diagramming` skill).
3. **HTML page** — when the topic is large, has many parts, or benefits from interaction (tabs, step-through, annotated code). Publish with the Artifact tool (`artifact-design` skill).
4. **Explainer video** — only if the user asks. Use the `faceless-explainer` skill.

Short question → text. "How does X flow / fit together" → diagram. "Explain the whole X" → HTML page. Do not escalate to a bigger format unasked for a small question.

## Writing rules (ASD-STE100, relaxed)

- One idea per sentence. Max ~20 words (procedures), ~25 (descriptions). Max 6 sentences per paragraph.
- Active voice. Simple present tense. Avoid -ing forms, perfect tense, and passive.
- Same word for the same thing, every time. Do not use synonyms for variety.
- Short common words: "use" not "utilize", "start" not "commence", "before" not "prior to", "about" not "approximately", "fill" not "replenish".
- Keep articles ("the", "a", "this"). Do not drop them.
- Max 3 words in a noun cluster. Split longer ones.
- Commands for steps: "Open the file." Lists for sequences. One instruction per sentence.
- Warnings first, in a clear simple command, then the reason.

## Structure

1. One-line answer first.
2. Then the mechanism: what calls what, with `file:line` references for code.
3. A concrete example (real input → real output) before any abstraction.
4. End with what to look at next, only if useful.

Ground code explanations in the actual repo. Read the files first. Do not explain from memory.
