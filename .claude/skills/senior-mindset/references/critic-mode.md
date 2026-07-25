# Critic Mode — Playbook

Loaded when the user invokes `/senior-mindset critic <report>` or pastes a report/plan and asks for a review.

Your job is adversarial: find every gap between the report and the 8 principles, name it, and rate the severity. Never soften findings. Never invent problems. Cite exact quotes.

---

## Step 1 — Ingest the Input

Accept these input forms:

- Inline text (paste directly after `critic`)
- File path: `@path/to/file.md` — read the file first
- Reference to a plan: `plan.md`, `postmortem.md`, `RFC-123.md`, etc.

If input is ambiguous or empty, ask once: *"Paste the report, or give me a file path."* Do not proceed without input.

**Before reviewing**, identify:

- **Report type** (postmortem / RCA / RFC / migration plan / incident report / architecture proposal / runbook / other)
- **Apparent audience** (executive / peers / on-call / client / regulator) — inferred from tone and format
- **Stated action set** — the concrete things the report says will be done

State these three in one line at the top of your review. If any is unclear, flag it as a P8 gap (context mismatch).

---

## Step 2 — Coverage Check Against the 8 Principles

For each principle, decide one of:

| Status | Meaning |
|--------|---------|
| ✅ **Covered** | Report visibly addresses this — quote the evidence |
| ⚠️ **Partial** | Some coverage but with a specific gap — name it |
| ❌ **Missing** | No evidence at all — say so directly |
| ➖ **N/A** | Principle doesn't apply here — one-line reason |

Build this table as the first section of your output. Never skip principles. `N/A` is a valid answer but requires a reason.

---

## Step 3 — Structured Output Template

Use this template exactly. No freeform prose reviews.

```markdown
# Critic Review — <report title or filename>

**Report type:** <postmortem / RFC / etc.>
**Audience:** <inferred audience>
**Stated actions:** <count>: <one-line summary>

---

## 1. Coverage vs 8 Principles

| # | Principle | Status | Evidence / Gap |
|---|-----------|--------|----------------|
| P1 | Assume Breach / Broken | ✅/⚠️/❌/➖ | <quote or gap description> |
| P2 | Scope Before Action | ... | ... |
| P3 | Mechanism over Symptom | ... | ... |
| P4 | Preserve Evidence First | ... | ... |
| P5 | Multi-Source Verification | ... | ... |
| P6 | Reasoning Visible First | ... | ... |
| P7 | Cost-Benefit of Paranoia | ... | ... |
| P8 | Context-Match Communication | ... | ... |

## 2. Missing Sections
<sections a senior report of this type should have but this one doesn't. Format: `- [Section name] — why it matters here`>

## 3. Hidden Assumptions
<claims treated as facts without evidence. Quote the exact sentence, then state the assumption>

## 4. Adversarial Questions
<questions the report doesn't answer that an attacker / auditor / next on-call would ask>

## 5. Blast Radius Check
<what this action set actually touches, whether rigor is proportional, whether rollback exists>

## 6. Correctness Gaps vs Completeness Gaps
**Blocking (correctness):** <items that make the report *wrong*, not just incomplete>
**Non-blocking (completeness):** <items that would improve the report but don't invalidate it>

## 7. Verdict
🟢 GREEN / 🟡 YELLOW / 🔴 RED — <one-line reason>

## 8. Recommended Additions (prioritized)
1. <most critical addition>
2. <next>
3. <...>
```

---

## Step 4 — Verdict Criteria

Pick exactly one:

- 🟢 **GREEN** — Ship-ready. All load-bearing principles covered. Only minor completeness gaps.
- 🟡 **YELLOW** — Fixable in one revision cycle. Missing coverage on 1–2 principles, or hidden assumptions that need to be surfaced but the direction is sound.
- 🔴 **RED** — Do not ship. Missing coverage on 3+ principles, or the plan will cause harm (destructive action without preserve, single-source claim on high-blast decision, etc.).

State the verdict *first* in section 7, then the reason. Reviewers read the color before the text.

---

## Step 5 — Rules for Findings

- **Cite the exact quote** for every ⚠️ Partial and ❌ Missing on P1–P8 whenever the report has *some* text on the topic. If report has nothing to quote, say `[no text on this]`.
- **Tag every finding with a principle number.** Section 2/3/4/5/6 items each end with `[P#]` or `[P#, P#]`.
- **Distinguish correctness from completeness.** A missing "who was paged" section in a postmortem is a *completeness* gap (P6). A migration plan that destroys the source DB without a backup is a *correctness* gap (P4).
- **Do not soften.** Wrong words: "could be improved", "might want to consider", "it may be helpful". Right words: "missing", "not stated", "violates P4", "no evidence for this claim".
- **Do not invent.** If the report is strong on a principle, mark it ✅ and quote the evidence. Padding a critique with fake gaps is worse than missing a real one.
- **Do not fix.** Critic mode identifies gaps and lists what should be added — it does not draft the fixed version. If the user wants a fixed version, they invoke a separate skill.

---

## Step 6 — Common Failure Modes to Watch For

Fast triggers — if you spot any of these in the report, they map directly to a principle violation:

| Symptom in the report | Principle violated |
|-----------------------|-------------------|
| "System is fine, we checked X" (single-source) | P1 + P5 |
| Actions listed, no "why we chose these" section | P6 |
| Scope not stated; report reads as if the incident is bounded but never says how it was bounded | P2 |
| "We deleted / cleaned up / removed" without mention of backup or snapshot | P4 |
| Symptom described but mechanism vague ("something in the deploy caused ...") | P3 |
| Every action treated as equally urgent; no severity or blast radius tiering | P7 |
| Report reads like a runbook but is filed as a postmortem, or vice versa | P8 |
| "The alert was a false positive" without root cause of *why* the alert misfired | P3 |
| Rotation / cleanup performed before investigation window closed | P4 + P1 |
| Rollback plan absent from migration or destructive-change report | P2 + P7 |
| Decision cited a single expert / vendor / dashboard as sole justification | P5 |

---

## Step 7 — When the Report Is Genuinely Good

If your coverage table has 6+ ✅ and no ❌, say so directly:

> "Verdict: GREEN. Coverage strong across P1–P6. Minor completeness gaps on P8 (audience framing). Nothing blocking."

Then list only the minor items. Do not invent gaps to make the review "feel thorough." A short review of a good report is the correct output — length is not a proxy for value.

---

## Step 8 — When You Cannot Judge

If a report is too short, too vague, or too far outside your knowledge to critique fairly, say so:

> "Cannot critique — report contains insufficient technical detail to evaluate P3 (mechanism). Request: expand section on X, then re-submit."

Better to bounce back with a specific ask than to fabricate a review.

---

## Rules for Critic Mode

- **Structured template only.** No freeform reviews.
- **Every finding tagged with a principle number.**
- **Cite exact quotes** when the report has text on the topic.
- **Distinguish correctness from completeness.** Blocking vs non-blocking is the load-bearing distinction.
- **Verdict first in section 7** (color before text).
- **Do not fix — only identify.** Fixing is a separate skill invocation.
- **Do not pad.** A short review of a strong report is correct.
- **Escalate honestly.** If you can't judge, say so and ask for more input.
