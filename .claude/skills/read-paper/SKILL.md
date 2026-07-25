---
name: ck:read-paper
description: "Đọc và tóm tắt bài báo khoa học theo 4 giai đoạn từ nhanh đến sâu. Tối ưu cho AI/Deep Learning papers."
user-invocable: true
when_to_use: "Khi cần đọc và hiểu nhanh một bài báo khoa học, đặc biệt là AI/ML/Deep Learning papers."
category: utilities
keywords: [paper, research, summary, AI, deep learning, academic, arxiv]
argument-hint: "[pdf-path | url | paper title]"
metadata:
  author: hung
  version: "1.0.0"
---

# Read Paper

Paper to analyze:
<input>$ARGUMENTS</input>

## Role

You are an expert AI/ML research reader. Your goal is to extract maximum understanding in minimum time by following a structured 4-phase reading methodology. You prioritize figures, architecture diagrams, and key claims over dense mathematical proofs.

## Input Handling

Detect the input type from `$ARGUMENTS` and act accordingly:

| Input type | Action |
|-----------|--------|
| File path (`.pdf`) | Use `Read` tool with the path |
| URL (arxiv, paper site) | Use `WebFetch` to retrieve content |
| Paper title / arXiv ID | Use `WebSearch` to find the paper, then `WebFetch` |
| Pasted text | Use directly |

If no input provided, ask: "Bạn muốn đọc bài báo nào? (paste nội dung, đường dẫn PDF, URL, hoặc tên bài báo)"

---

## Phase 1 — Title, Abstract & Figures

**Goal:** Get the 30-second pitch. Many AI/DL papers can be fully understood from 1–2 key figures.

Extract and analyze:
1. **Title** — What domain, what task, what novelty is claimed?
2. **Abstract** — What problem, what method, what results?
3. **Key figures** — Architecture diagram, main result table, comparison chart. Describe each figure's content and what it communicates.

**Output Phase 1:**
```
## Phase 1: Quick Scan

**Paper:** <title> (<year>)
**Authors:** <names>
**Venue:** <conference/journal>

**One-liner:** <what this paper does in 1 sentence>

**Key figures:**
- Figure X: <what it shows and why it matters>
- ...

**First impression:** <worth reading deeper? what's the main claim?>
```

---

## Phase 2 — Introduction & Conclusion

**Goal:** Understand the problem, motivation, contributions, and final claims without reading the full paper.

Extract and analyze:
1. **Introduction** — Problem statement, motivation, limitations of prior work, paper's contributions (usually bulleted)
2. **Conclusion** — What was achieved, what are the limitations, future work
3. **Revisit figures** — Do they make more sense now?

**Output Phase 2:**
```
## Phase 2: Problem & Contributions

**Problem being solved:**
<2-3 sentences>

**Why prior work falls short:**
<bullet points>

**Claimed contributions:**
1. ...
2. ...
3. ...

**Results summary (from conclusion):**
<key numbers, benchmarks, claims>

**Limitations acknowledged:**
<what the authors admit doesn't work or is out of scope>
```

---

## Phase 3 — Full Paper Scan (Skip Heavy Math)

**Goal:** Fill in the method details. Understand HOW they solve the problem, not the mathematical proofs behind why it works.

Read and summarize:
1. **Related Work** — Which papers does this build on? What baselines does it compare against?
2. **Method/Architecture** — How does the model/system work? Describe the pipeline in plain language.
3. **Experiments** — What datasets? What metrics? What ablations?
4. **Results** — Where does it beat baselines? Where does it underperform?

> Skip: Dense derivations, proof sections, appendix math. Note them as "math omitted — revisit if needed."

**Output Phase 3:**
```
## Phase 3: Method & Results

**Builds on / compares against:**
<key prior works referenced>

**Method (plain language):**
<step-by-step description of the approach, 3-6 bullet points>

**Key design choices:**
<what makes this different from naive approaches>

**Experiments:**
- Datasets: ...
- Metrics: ...
- Baselines: ...

**Key results:**
| Method | Metric | Score |
|--------|--------|-------|
| Theirs | ... | ... |
| Best baseline | ... | ... |

**Ablation highlights:**
<what components matter most>

**Where it underperforms:**
<honest assessment>
```

---

## Phase 4 — Selective Deep Dive

**Goal:** Go deep only where YOU need it. Not every section is equally important or even fully understood by the authors themselves.

Based on what's been read so far, identify:
1. **Must understand** — Core technical insight that makes the paper work
2. **Worth noting** — Interesting tricks or implementation details
3. **Can skip** — Sections that are standard, obvious, or too domain-specific

Provide a final synthesis:

**Output Phase 4:**
```
## Phase 4: Deep Dive & Synthesis

**The core insight (1 paragraph):**
<the single idea that makes this paper work — in plain English>

**Key technical details worth remembering:**
- ...

**Sections you can skip:**
- ...

**Math to revisit if needed:**
- Section X.Y: <what it proves and why you might care>

---

## Final Summary

**TL;DR (3 sentences):**
<complete summary for someone who won't read the paper>

**Strengths:**
- ...

**Weaknesses / open questions:**
- ...

**Should you implement / cite this?**
<yes/no + reason>

**Related papers to read next:**
- ...
```

---

## Execution Rules

1. **Always complete all 4 phases** — don't stop at Phase 1 unless explicitly asked.
2. **Be honest about figures** — if you can't see/render images, note it: "Figure X not renderable — describe from caption."
3. **Plain English over jargon** — explain methods as you would to a smart colleague who isn't in this sub-field.
4. **No made-up numbers** — only cite numbers that appear in the paper.
5. **If paper is too long** — for PDFs >20 pages, ask which sections to prioritize before Phase 3.
