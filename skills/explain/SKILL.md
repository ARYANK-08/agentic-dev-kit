---
name: explain
description: Use whenever the user asks to explain, walk through, or help them understand anything (code, a flow, a bug, a concept, an architecture, a model output). Picks the clearest output format and writes in simplified technical English.
---

# Explain

Goal: the user understands fast. Pick the lightest format that works, then escalate only when it helps.

## Format ladder

1. **Text** — default. Write in ~80% ASD-STE100 (see rules below).
2. **Diagram** — when the answer is a flow, structure, sequence, or relationship. Follow the Diagram style below. In the terminal use plain ASCII boxes and arrows; for a richer one, publish via the Artifact tool (`artifact-diagramming` skill).
3. **HTML page** — a one-page reference sheet (see below) when the topic is large, has many parts, or benefits from interaction (tabs, step-through, annotated code). Publish with the Artifact tool (`artifact-design` skill).
4. **Explainer video** — only if the user asks. Use the `faceless-explainer` skill.

Short question → text. "How does X flow / fit together" → diagram. "Explain the whole X" → HTML page. Do not escalate to a bigger format unasked for a small question.

## Reference sheet (HTML explainer style)

For "explain the whole X" or any spec, overview, or system with many parts. One page, lettered panels, like an engineering drawing sheet.

- **Frame:** thin outer border with grid references (columns 1-8, rows A-D) on the edges. White page, dark text.
- **Panels:** bordered cards in a grid. Each has a dark letter chip (A, B, C), a bold title, and a small mono caption on the right (e.g. "annotated examples").
- **Panel types, pick what fits:**
  - Structure: a tree of the parts.
  - Anatomy: one real example with brackets and short labels under each part.
  - Table: rows with a status column, check (blue) for right, cross (red) for wrong.
  - Limits: horizontal bars with a max marker.
  - History: a timeline with 3-4 dots.
- **Color:** one meaning each. Red = wrong or not allowed. Blue = approved, or an annotation. Grey = secondary text. Nothing else.
- **Type:** mono for examples, code, captions, and numbers. Clean sans for titles and body.
- **Title block** (bottom-right): title, source, owner, sheet "1 of 1".
- **Content:** every panel shows a real example, never only a definition. Wrong next to right, side by side.
- Build with the Artifact tool and the `artifact-design` skill. Works in light and dark mode. Must fit a phone width by stacking panels.

Use the Excalidraw style below for flows and paths. Use the sheet style for specs and overviews. Do not mix them on one page.

## Diagram style (Excalidraw look)

Minimal, hand-drawn, calm. Looks like a whiteboard sketch, not a corporate slide.

- **Shapes:** rounded rectangles, plain arrows, a few ellipses. No shadows, gradients, icons, or 3D.
- **Lines:** hand-drawn feel. Slight wobble, 2px stroke, round caps. In SVG use an `feTurbulence` + `feDisplacementMap` filter (scale ~1.5); in HTML use `roughjs` from cdnjs.
- **Colors:** black strokes on white (dark mode: light strokes on near-black). One accent color at most, plus soft pastel fills for grouping.
- **Text:** hand-style font (`Caveat` or `Kalam` from Google Fonts), 2-4 words per label. Never a sentence in a box.
- **Layout:** left to right or top to bottom, generous spacing, one arrow per relationship, no crossing lines. Max ~8 boxes; split the diagram if you need more.
- **Arrows:** label only when the verb is not obvious ("sends token", "401").
- **Output:** inline SVG in an Artifact for rich diagrams. For editable output, write an `.excalidraw` JSON file the user can open at excalidraw.com.

Terminal fallback:

```
 [Browser] --token--> [app-studio] --> [optics] --> [Device]
```

## Writing rules (ASD-STE100, relaxed)

Limits:

| Item | Max |
| ---- | --- |
| Procedural sentence | 20 words |
| Descriptive sentence | 25 words |
| Paragraph | 6 sentences, one topic |
| Noun cluster | 3 words |
| Instructions per sentence | 1 (except simultaneous actions) |

Verbs:

| Form | Example | OK |
| ---- | ------- | -- |
| Command | Close the valve. | yes |
| Simple present / past / future | The valve closes. | yes |
| Infinitive | Turn the knob to close it. | yes |
| Past participle as adjective | The closed valve | yes |
| Progressive (-ing) | The valve is closing. | no |
| Perfect | The valve has closed. | no |
| Passive in procedures | The valve must be closed. | no |

Words:

- Same word for the same thing, every time. No synonyms for variety.
- Keep "the", "a", "this". Do not drop articles.
- Short common words: use not utilize, start not commence, before not prior to, about not approximately, fill not replenish, make sure not ensure, to not in order to.
- Active voice. Simple present tense. Use vertical lists for complex text.

Safety: put the command first, then the reason. `WARNING` = risk of injury. `CAUTION` = risk of damage.
Example: "WARNING: Do not touch the brake unit until it is cool. Hot parts can cause injury."

Rewrite check (same meaning, 12 words instead of 16):
- Before: "It is imperative that the operator ensures the hydraulic reservoir is replenished prior to commencing operation."
- After: "Make sure the hydraulic reservoir is full before you start the operation."

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
| "Explain the whole reports feature" | HTML reference sheet | Many parts: list, summary, drill-down |
| "Make a video on how login works" | Explainer video | You asked for one |

### Answer shape

```
Answer: Login sends you to the SSO portal, which returns a token in the URL.
How: ProtectedRoute checks the token (src/containers/ProtectedRoute.tsx:12) → AuthContext stores it → client.js sends it with each request.
Example: open /modules while signed out → redirect to SSO → sign in → back at /modules with ?token=… → URL is cleaned.
Next: read src/utils/ssoHandoff.js for the trust check.
```
