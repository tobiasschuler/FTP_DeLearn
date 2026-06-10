# CLAUDE.md — LaTeX Generation Guide for `prism`

Project-specific instructions for this repo. This builds **exam-summary documents**
in LaTeX (see `FTP_DeLearn_Summary.tex`). When I paste lecture notes, convert them
into clean, exam-focused LaTeX that fits the existing template and its custom boxes —
don't transcribe everything.

---

## 1. Golden rule: exam relevance only

When I paste raw lecture text, **keep only what could plausibly appear in an exam
question, or what is needed to answer one.** Aggressively cut the rest.

**Keep**
- Definitions, named concepts, theorems
- Formulas + the meaning of every variable
- Comparisons (X vs Y), trade-offs, pros/cons
- Conditions, assumptions, edge cases, units
- The *method* of a worked example (steps, not narration)

**Drop**
- Motivational intros, anecdotes, course logistics, dates
- Filler transitions ("as we saw last week", "moving on…")
- Repetition and anything the lecturer flagged as non-examinable

If unsure whether something is examinable, keep it as a **short bullet**, not a paragraph.

---

## 2. Format: structure over prose

- **Never write long prose paragraphs.** Default to bullet points, one idea per bullet.
- Use the template's custom boxes for emphasis:
  - `definitionbox` → definitions and key concepts
  - `formulabox` → formulas (always in proper math mode `\[ ... \]`)
  - `importantbox` → critical facts, "don't forget", common pitfalls
  - `examtipbox` → likely exam questions, shortcuts, typical mistakes
- **After every formula**, list its variables as a short bullet list: `$\eta$: learning rate`.
- For **"compare A and B"** content, use a `booktabs` table — not sentences.
- Use `multicols` for short flat lists (activation functions, optimizer variants, …).

---

## 3. Keep it simple

- Prefer the **smallest correct representation**: a 3-row table beats three paragraphs.
- One concept per bullet; aim for single-line bullets.
- No nested bullets deeper than two levels.
- Don't pad. If a topic is small, a single box is enough.

---

## 4. Convert to graphics when it helps

Turn text into a visual when **structure, flow, or relationships** are the point:
- Network architectures, computation graphs, forward/backprop flow
- Pipelines, taxonomies, decision trees, state transitions

Guidance:
- Use **TikZ**. If `\usepackage{tikz}` isn't in the preamble yet, add it and say so.
- Keep diagrams minimal and **labeled**; no decorative clutter.
- A process or comparison is often clearer as a small diagram or table than as bullets.
- Don't force a graphic where a one-line formula or a 2-column table is already clearer.

---

## 5. Add exam hints for every topic

- End each topic with an `examtipbox` predicting **1–3 likely questions**.
- Mark formulas as **derive vs. apply** (examiners often ask you to derive backprop,
  but only to apply gradient descent).
- Call out **common mistakes** (sign error in the gradient, forgetting the bias term,
  confusing softmax with sigmoid).
- Flag examiner favorites: *"explain in your own words"*, *"why do we use X?"*,
  *compare/contrast*, *"what happens if …?"*.

---

## 6. Consistency & correctness

- **Match existing notation**: `\theta` params, `\eta` learning rate, `J(\theta)` loss,
  `w` weight, `b` bias, `\nabla` gradient. Add any new symbol to the **Cheat Sheet** table.
- Only use packages already in the preamble. If a new one is genuinely needed,
  state it at the top of your output and add the `\usepackage` line.
- Replace the `Week XX – Topic Name` placeholder with the real topic; keep the
  `\section` / `\subsection` hierarchy consistent with the template.
- **Output must compile**: balanced braces, closed environments, valid math.
- **Don't invent facts.** If pasted notes are ambiguous or incomplete, insert a
  `% TODO: ...` comment instead of guessing.
- Deduplicate overlapping points when I paste a wall of text.

---

## 7. Default response shape per pasted topic

1. `\subsection{Topic}`
2. `definitionbox` with the core concept
3. `formulabox` (if any) + variable list
4. Key points as bullets / `multicols` / `booktabs` table
5. Diagram (TikZ) if structure matters
6. `examtipbox` with predicted questions and common mistakes

---

## 8. Working in this repo (Claude Code)

- Edit `FTP_DeLearn_Summary.tex` directly when adding a topic; don't create new
  scratch `.tex` files unless I ask.
- After edits, verify it compiles if a TeX toolchain is available
  (e.g. `pdflatex -interaction=nonstopmode FTP_DeLearn_Summary.tex`); fix errors
  before reporting done. Run it twice when the table of contents needs updating.
- Don't commit build artifacts (`.aux`, `.log`, `.out`, `.toc`, `.pdf`) unless asked.
- Keep diffs small and focused on the topic I pasted — leave unrelated sections untouched.
