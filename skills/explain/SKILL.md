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

## Simple mode (explain like I'm 13)

Use when the user says "like I'm 13", "ELI13", "dumb it down", "I don't get it", or similar. This replaces the technical register; the format ladder still applies.

- Start with one everyday analogy (a restaurant, a post office, a school). Keep the same analogy to the end.
- No jargon. If a technical word is needed, say it once, then explain it in plain words.
- Short sentences. One idea each.
- Build up: what it is, why it exists, how it works, one small example.
- Never talk down to the user. Simple means clear, not childish.
- End with a one-line recap.

## Examples

### Bad vs good (technical mode)

Question: "What does the API client do?"

- Bad: "The client leverages an interceptor pattern to facilitate the approximately seamless attachment of authentication credentials prior to dispatching requests."
- Good: "The client adds your login token to every request. If the server says 401, it signs you out. It also merges identical GET requests into one."

Why: one idea per sentence, active voice, plain words, no stacked nouns.

### Simple mode

Question: "Explain Redux like I'm 13."

> Think of a school office. Every student (component) needs to know today's schedule. Instead of each student keeping their own copy, the office keeps one board (the store). A student who wants a change fills in a form (an action). The office clerk (the reducer) updates the board. Everyone looks at the same board, so nobody has old info.
>
> Recap: one shared board, changed only through forms.

### Pick the format

| Question | Format | Why |
| -------- | ------ | --- |
| "Why does this hook re-render?" | Text | One cause, one fix |
| "How does a request reach the device?" | Diagram: `Browser → app-studio → optics → device` | It is a path with steps |
| "Explain the whole reports feature" | HTML page | Many parts: list, summary, drill-down |
| "Make a video on how login works" | Explainer video | You asked for one |

### Answer shape

```
Answer: Login sends you to the SSO portal, which returns a token in the URL.
How: ProtectedRoute checks the token (src/containers/ProtectedRoute.tsx:12) → AuthContext stores it → client.js sends it with each request.
Example: open /modules while signed out → redirect to SSO → sign in → back at /modules with ?token=… → URL is cleaned.
Next: read src/utils/ssoHandoff.js for the trust check.
```
