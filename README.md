# MATH-READING-SKILL v1.0

[English](#english) | [中文](#中文)

---

## English

### What this is
Engineering-style mathematical literature reading for AI research. Turn math papers into reusable assets: traceable theorems/assumptions, proof-pattern extraction, proposition drafts, and curve-based evaluation protocols — with anti-hallucination guardrails.

### Core guarantees (anti-hallucination)
- Every key claim must include a location pointer (Theorem/Lemma/Section/Eq.)
- evidence_quote ≤ 25 words per key claim
- INFERRED vs EXTRACTED vs UNLOCATED must be explicit
- Incomplete text → partial output + failure_report (never stall)

### Deliverables (3 + 2 + 1)
**Required (3)**
- One-Pager
- Symbol Mapping (≥10 rows)
- Transferable Component

**Recommended (2)**
- Proposition Draft
- Protocol Draft (curve-based)

**Archive (1)**
- Toolbox Entry

### Quickstart
1) Paste the **System Prompt** from `MATH-READING-SKILL_v1.0.md` into your agent/system instructions  
2) Use the **User Prompt Template** to send `paper_meta`, `target_context`, and `paper_text`  
3) Get outputs in **JSON + Markdown**

### Files
- `MATH-READING-SKILL_v1.0.md` — Full skill definition, prompt, template, schema

---

## 中文

### 这是什么
一个“数学文献研读工程化”的 Agent Skill：把数学论文转成 AI 研究可复用资产，输出可追溯的定理/假设、证明套路抽象、命题草案与曲线型评测协议，并内置反幻觉约束。

### 严格性保证（反幻觉）
- 每条关键断言必须附 `location`（定理/引理/章节/公式）
- 每条关键断言附 ≤25 词 `evidence_quote`
- 必须区分 `EXTRACTED / INFERRED / UNLOCATED`
- 文本不完整也不停摆：输出部分结果 + `failure_report`

### 交付物（3 + 2 + 1）
**必交付（3）**
- One-Pager（结构化摘要）
- 符号映射表（≥10行）
- 可迁移组件（结论/思路至少一个）

**建议交付（2）**
- 命题草案（可写进论文）
- 实验协议草案（必须是曲线型）

**归档（1）**
- Toolbox Entry（入库条目）

### 快速使用
1) 将 `MATH-READING-SKILL_v1.0.md` 中的 **System Prompt** 放进你的 Agent 系统提示词  
2) 用 **User Prompt Template** 发送 `paper_meta`、`target_context`、`paper_text`  
3) 输出得到 **JSON + Markdown**

### 文件说明
- `MATH-READING-SKILL_v1.0.md` — 完整 skill 定义、提示词、模板、JSON schema


