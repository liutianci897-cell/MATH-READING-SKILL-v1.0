# MATH-READING-SKILL v1.0

## English
**Engineering-style mathematical literature reading Skill (Agent-ready).**  
Feed a math paper (PDF-to-text/LaTeX/pasted text) to an AI agent and get structured research assets (results + methods + toolchain + AI transfer + proposition drafts + evaluation protocols), enforcing **traceability + confidence + anti-hallucination**.

---

## 0. Version
- **Skill ID**: MATH-READING-SKILL
- **Version**: 1.0
- **Status**: Stable (fixed Prompt + fixed JSON output contract)
- **Primary Use**: AI research topic selection/proposal, theory + evaluation protocol for top-tier papers, personal math toolbox building

---

## 1. Goal
Given a math paper text, produce reusable research assets:
1. **Result assets**: theorems/bounds/guarantees/optimality/coverage/regret/approximation (with conditions + source pointers)
2. **Method assets**: proof patterns, constructions, decompositions, toolchain (lemma toolbox)
3. **AI instantiation assets**: install math models into AI themes (RAG/PEFT/Serving/MM/TS/Graph)
4. **Paper-ready assets**: proposition drafts + curve-based evaluation protocols
5. **Archival assets**: toolbox entry (Notion/Obsidian/DB friendly)

---

## 2. Hard Constraints
### 2.1 No Hallucination
Any **key claim** (assumption/result/lemma/definition/algorithm step) must include:
- `location`: e.g. `Theorem 2.1` / `Lemma 4.3` / `Section 3.2` / `Eq.(7)`
- `evidence_quote`: <= 25 words quote (or paraphrase + exact numbering)

If cannot locate:
- set `status = UNLOCATED`
- set `confidence = low`
- must NOT be treated as fact

### 2.2 Explicit Inference Tagging
Any inferred content must be:
- `status = INFERRED`
- with justification (e.g., “inferred from proof sketch step 2”)

### 2.3 Never Stall
Even if paper text is incomplete:
- output partial extraction
- include `failure_report`
- do not stop or ask for more info

### 2.4 Mandatory 3+2+1 Deliverables
Unless text is severely missing, always output:
- Required 3: One-Pager + Symbol Mapping (>=10) + Transferable Component
- Recommended 2: Proposition Draft + Protocol Draft (at least one)
- Archive 1: Toolbox Entry

---

## 3. Input Contract
### 3.1 Minimal Input (required)
- `paper_text`: paper body text (may be partial; ideally includes intro, defs, main theorem, proof outline)

### 3.2 Recommended Inputs
- `paper_meta`: `title`, `authors`, `year`, `venue_or_arxiv`, `url` (optional)
- `target_context` (optional but strongly recommended): your AI research direction/topic
- `constraints` (optional): `compute`, `data`, `time_horizon`, `need_formal_guarantee`
- `desired_depth`: `lite | standard | deep` (default `standard`)

---

## 4. Output Contract
Return two sections:
- (A) **JSON**: stable interface for automation
- (B) **Markdown**: human-readable report

---

## 5. Deliverables (3 + 2 + 1)
### 5.1 One-Pager
Must include:
- Problem class
- Objects
- Assumptions (explicit + implicit)
- Main results
- Proof skeleton (3–7 steps)
- Toolchain tags (proof patterns)
- Transfer points
- Limitations
- Next actions

### 5.2 Symbol Mapping (>=10 rows)
- Paper symbol → meaning → target correspondence → notes

### 5.3 Transferable Component
At least one:
- result-type (bound/guarantee/metric construction), or
- method-type (reusable proof pattern/decomposition framework)

### 5.4 Proposition Draft
At least one proposition (weak version allowed):
- condition → conclusion
- variable explanations
- mapping to extracted toolchain
- validation plan (experimental support)

### 5.5 Protocol Draft
Must be curve-based, at least one curve:
- performance vs budget (token/latency/params/labels)
- robustness vs noise strength
- regret vs time
- coverage vs alpha
- tail latency vs load (P99/P999)

### 5.6 Toolbox Entry
Unified archival format:
- Citation
- Problem class
- Proof patterns (tags)
- Core lemma/tools (3–7)
- Reusable assets
- Instantiation notes
- Risks/assumptions

---

## 6. Internal Pipeline
### Phase 0: Paper Triage
- completeness check (defs/main theorem/proof outline present?)
- classify: `theorem-driven` or `method-driven`
- output `risk_flags`: symbol overloading, implicit assumptions, external dependencies, appendix-only results

### Phase 1: Formalization Extraction
- Objects
- Assumptions
- Main results
- produce: assumption table, API-style theorem rewriting

### Phase 2: Proof Blueprint
- 3–7 step proof skeleton
- key turning points
- toolchain tags
- 3–7 toolbox lemmas/tools

### Phase 3: Instantiation to AI
- if `target_context` provided: prioritize mapping to it
- else: map to common AI themes (RAG/PEFT/Serving/MM/TS/Graph)
- must generate: proposition draft + protocol draft

### Phase 4: Quality Gates
- every key claim has location/status/confidence
- inference explicit
- missing parts go to `failure_report`

---

## 7. Evidence & Confidence Fields
For all key items (assumptions/results/lemmas), include:
- `location`
- `evidence_quote` (<=25 words)
- `confidence`: `high | medium | low`
- `status`: `EXTRACTED | INFERRED | UNLOCATED`

---

## 8. JSON Output Schema
```json
{
  "paper_meta": {
    "title": "",
    "authors": [],
    "year": "",
    "venue_or_arxiv": "",
    "url": ""
  },
  "triage": {
    "paper_type": "theorem-driven | method-driven",
    "completeness_score": 0.0,
    "risk_flags": []
  },
  "one_pager": {
    "problem_class": "",
    "objects": [],
    "assumptions_summary": [],
    "main_results_summary": [],
    "proof_skeleton": [],
    "toolchain_tags": [],
    "transfer_points": [],
    "limitations": [],
    "next_actions": []
  },
  "assumptions": [
    {
      "id": "A1",
      "statement": "",
      "location": "",
      "evidence_quote": "",
      "status": "EXTRACTED | INFERRED | UNLOCATED",
      "confidence": "high | medium | low",
      "notes": ""
    }
  ],
  "main_results": [
    {
      "id": "T1",
      "statement": "",
      "result_type": "upper_bound | lower_bound | optimality | consistency | regret | coverage | approximation | stability | other",
      "location": "",
      "evidence_quote": "",
      "status": "EXTRACTED | INFERRED | UNLOCATED",
      "confidence": "high | medium | low",
      "notes": ""
    }
  ],
  "symbol_mapping": [
    {
      "paper_symbol": "",
      "paper_meaning": "",
      "target_correspondence": "",
      "notes": ""
    }
  ],
  "proof_blueprint": {
    "steps": [],
    "key_turning_points": [],
    "toolchain_tags": []
  },
  "toolbox_lemmas": [
    {
      "name": "",
      "role": "",
      "assumptions_needed": [],
      "statement": "",
      "location": "",
      "evidence_quote": "",
      "status": "EXTRACTED | INFERRED | UNLOCATED",
      "confidence": "high | medium | low",
      "reuse_ideas": []
    }
  ],
  "transfer_map": {
    "to_target_context": {
      "summary": "",
      "candidate_research_claims": [],
      "candidate_metrics": [],
      "candidate_algorithmic_moves": []
    },
    "to_general_ai": [
      {
        "theme": "RAG_reliability | PEFT_continual | LLM_serving | multimodal_grounding | time_series | graph",
        "how_it_maps": "",
        "what_to_build": "",
        "what_to_measure": ""
      }
    ]
  },
  "proposition_drafts": [
    {
      "title": "",
      "formal_statement": "",
      "assumptions": [],
      "proof_sketch": "",
      "what_is_new": "",
      "how_to_validate": ""
    }
  ],
  "protocol_drafts": [
    {
      "title": "",
      "goal": "",
      "budget_control": "",
      "perturbation_or_load_sweep": "",
      "metrics": [],
      "baselines": [],
      "statistics": "",
      "expected_curves": ""
    }
  ],
  "toolbox_entry": {
    "citation": "",
    "problem_class": "",
    "proof_patterns": [],
    "core_tools": [],
    "reusable_assets": [],
    "instantiation_notes": "",
    "risks": []
  },
  "next_actions": [],
  "failure_report": {
    "is_partial": false,
    "missing_sections": [],
    "notes": ""
  }
}
