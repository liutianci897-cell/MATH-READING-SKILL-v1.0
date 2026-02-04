# MATH-READING-SKILL v1.0

[English](#english) | [中文](#中文)

---

## English

**Engineering-style mathematical literature reading for AI research.**  
Turn math papers into reusable research assets: traceable theorems/assumptions, proof-pattern extraction, proposition drafts, and curve-based evaluation protocols—**with anti-hallucination guardrails**.

> If you want “一区风格”的严谨度：clear problem setup + explicit assumptions + testable properties/guarantees + standardized evaluation protocols (curves, not single points).  
> This repo provides an Agent Skill you can directly feed to an AI to execute.

---

## ✨ What this is
This repository contains **MATH-READING-SKILL v1.0**, an Agent Skill (prompt + output contract + JSON schema) that converts a mathematical paper (PDF-to-text / LaTeX / pasted text) into structured deliverables for AI research:

- **Theorem-driven assets**: formal results, bounds, guarantees, assumptions (with strict source pointers)
- **Method-driven assets**: proof skeletons, reusable proof patterns, lemma toolchains
- **AI instantiation assets**: proposition drafts + curve-based evaluation protocols
- **Knowledge-base assets**: toolbox entries ready for Notion/Obsidian/DB

---

## ✅ Core guarantees (anti-hallucination)
The Skill enforces:

1. **No hallucination**: every key claim must include a `location` pointer (Theorem/Lemma/Section/Eq.).  
2. **Evidence quote cap**: each key claim includes an `evidence_quote` ≤ 25 words (or paraphrase + exact numbering).  
3. **Explicit inference**: inferred content is tagged `INFERRED` with justification.  
4. **Unlocated content is downgraded**: `UNLOCATED` + `low confidence` and must not be treated as fact.  
5. **Never stalls**: if text is incomplete, output partial results + `failure_report` instead of stopping.

---

## 📦 Deliverables (3 + 2 + 1)
For each paper, the agent must output:

### Required (3)
- **One-Pager**: problem class, objects, assumptions, main results, proof skeleton, toolchain tags, limitations, next actions
- **Symbol Mapping** (≥ 10 rows): paper symbols → meaning → your target correspondence
- **Transferable Component**: at least one reusable theorem/bound OR proof pattern/framework

### Recommended (2)
- **Proposition Draft**: a paper-ready proposition/theorem (can be a weak version)
- **Protocol Draft**: **curve-based** evaluation protocol (budget/noise/load/alpha sweeps)

### Archive (1)
- **Toolbox Entry**: database-ready entry for your personal math-method library

---

## 🗂 Repository contents
- `MATH-READING-SKILL_v1.0.md`  
  The full skill file: constraints, pipeline, output schema, system prompt, user prompt template.

> If you only need one file: start with `MATH-READING-SKILL_v1.0.md`.

---

## 🚀 Quickstart (copy/paste)
There are two common ways to use this skill.

### Option A — Use in ChatGPT / Custom GPT / any agent that supports a “System Prompt”
1. Copy the **System Prompt** section from `MATH-READING-SKILL_v1.0.md`.
2. Set it as your agent/system instruction.
3. Send a user message with the **User Prompt Template** (also included in the skill file).
4. Paste the paper text (PDF-to-text / LaTeX / plain text).
5. The agent returns:
   - **(A) JSON** (machine-friendly)
   - **(B) Markdown** (human-friendly)

### Option B — Use in your own pipeline (RAG/agent framework)
- Store the system prompt as `math_reading_system_prompt.txt`
- Your ingestion step converts PDF → text
- Then call your model with:
  - `system`: the prompt
  - `user`: the template + paper text
- Parse the returned JSON for automation (DB insert, tagging, search, etc.)

---

## 🧾 Input contract (recommended template)
```text
paper_meta:
- title:
- authors:
- year:
- venue/arxiv:
- url (optional):

target_context:
- My AI research direction:
- Constraints (compute/data/time):
- Need formal guarantees? (yes/no):
- desired_depth (lite/standard/deep):

paper_text:
<<< paste the paper text here >>>
