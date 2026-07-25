# The 8 Principles — Detailed Reference

Load this file when a coach or critic session needs deeper reasoning for a specific principle, or when the user asks *why* a principle exists.

Each principle follows the same schema so you can quote it consistently:

- **Junior default** — what people do wrong
- **Senior behavior** — what to do instead
- **Why** — the root cause (bias, incident class, cost model)
- **Self-check questions** — questions to trigger the principle in coach mode
- **Example** — a concrete case from real DevOps/engineering practice

---

## P1 — Assume Breach / Assume Broken

**Junior default:** Search for evidence the system is fine. First green dashboard = "we're good."

**Senior behavior:** Invert the burden of proof. Search for evidence the system *is* compromised / broken / miscounted / racing. Only when that search comes back empty do you tentatively call it clean.

**Why:** Confirmation bias is the single most reliable cause of missed incidents. If your default hypothesis is "fine," you will unconsciously stop looking. Zero Trust (NIST SP 800-207) and Google BeyondCorp both institutionalize this inversion.

**Self-check questions:**
- If the system *were* compromised right now, where would I see the first sign?
- What am I *not* looking at that could contradict my current conclusion?
- Whose word am I taking as evidence — mine, a tool's, or another human's?

**Example:** Task-role permissions are tight, so "AWS is safe." But if the dev's laptop credentials leaked, the task role is irrelevant — attacker uses another door. Assume the door was opened; then prove it wasn't.

---

## P2 — Scope Before Action

**Junior default:** See a problem → act immediately. "Rotate the keys," "restart the service," "drop the index."

**Senior behavior:** Map the blast radius before touching anything. What does this action affect? Who depends on it? What breaks if it fails halfway? Only after the map is drawn does action begin.

**Why:** Under-scoped fixes miss real damage (only rotating CI secrets when a dev laptop was also compromised). Over-scoped fixes cause outages (rotating a shared DB password without updating all consumers). Both fail modes come from skipping the scoping step.

**Self-check questions:**
- What is the smallest set of things that must change, and what is the largest set that *might* need to change?
- If this action succeeds, what is the observable difference? If it fails partway, what state is the system in?
- Am I acting on the reported symptom or on the actual scope of the incident?

**Example:** Supply-chain attack via npm. Junior scopes to the CI runner. Senior draws: dev laptop → CI runner → build image → ECR → running containers. Every arrow is a possible compromise point. Only after the full map do you decide what to rotate and what to preserve.

---

## P3 — Mechanism over Symptom

**Junior default:** Fix what the ticket says. Symptom disappears → close.

**Senior behavior:** Understand the mechanism that produced the symptom. Only mechanism-level understanding tells you where else the same cause may be hiding.

**Why:** Symptoms are downstream. The same mechanism can produce many symptoms; fixing one symptom leaves the others live. In security, mechanism-vs-symptom is the difference between "malware activates on `npm install`" (mechanism → anyone who ran install is affected) vs "we upgraded axios" (symptom → false sense of closure).

**Self-check questions:**
- What is the exact causal chain from root event to the symptom I'm seeing?
- If this mechanism is real, what *other* symptoms should I expect to also see?
- Am I fixing the mechanism or removing one instance of its output?

**Example:** API returning 5xx. Symptom-fix: bounce the pods. Mechanism-fix: pods OOM because a downstream service is slow, retries pile up, memory blows. Bouncing pods resets the counter; it does nothing to the mechanism, which fires again in 20 minutes.

---

## P4 — Preserve Evidence First (Contain > Eradicate)

**Junior default:** See something bad → delete it. Clean state = success.

**Senior behavior:** Contain first (block access, isolate, tag). Eradicate only after the investigation window has closed. Preserve evidence for audit and forensic use — even if you're 90% sure you don't need it.

**Why:** Deletion is one-way. Six months later, when a security team wants to trace an attacker's lateral movement, the deleted artifact was the pivot point they needed. SANS PICERL (Prep → Identify → **Contain** → Eradicate → Recover → Learn) puts containment before eradication for exactly this reason. NIST SP 800-86 (forensic integration) codifies chain-of-custody.

**Self-check questions:**
- Is this action reversible? If not, what evidence am I about to destroy?
- Who might need to look at this artifact in the next 12 months?
- Can I *block use* of this artifact without removing it?

**Example:** ECR image with malicious axios. Junior deletes the image. Senior tags it, then attaches an ECR Repository Policy blocking `BatchGetImage` on tagged images. Image still visible for forensics, but no one can pull it.

---

## P5 — Multi-Source Verification

**Junior default:** One dashboard is green → everything is fine. One log says clean → clean.

**Senior behavior:** Correlate across independent telemetry sources. A single signal is a claim, not a fact. Facts emerge from convergence.

**Why:** Any single telemetry has blind spots — sampling gaps, collection failures, deliberate attacker evasion. An attacker who compromises one signal is playing on easy mode. Defense-in-depth of *observability* mirrors defense-in-depth of *security*.

**Self-check questions:**
- What are the independent sources for this claim? (independent = different collection path, different vendor if possible)
- If the primary source were lying (broken or compromised), what would corroborate or contradict it?
- Am I combining sources that share a common failure mode? (e.g., two dashboards both fed by the same broken exporter)

**Example:** "No malicious activity in AWS." Check: CloudTrail (API actions) + VPC Flow Logs (network) + GuardDuty (behavioral) + Config (drift) + Resource Explorer (unexpected resources). One clean signal = one claim. Four independent clean signals = evidence.

---

## P6 — Reasoning Visible First

**Junior default:** Report is a list of actions. "1. Did X. 2. Did Y. 3. Done."

**Senior behavior:** Report leads with strategy: what did we think, what did we assume, what did we choose to scope in/out, why. Actions come after and are traceable back to the strategy.

**Why:** A reviewer can only validate what they can see. Actions without reasoning force the reviewer to either trust blindly or reverse-engineer the logic. Both are expensive. In enterprise contexts (Japanese enterprise culture especially), missing reasoning kills trust even when actions are correct.

**Self-check questions:**
- If someone reads only the first paragraph of this report, do they know *why* we did what we did?
- What assumptions am I treating as facts? Are they stated anywhere?
- Could a reviewer disagree with my conclusion after reading only the actions section? If not, the reasoning is invisible.

**Example:** Postmortem sections in order: **Context → Hypothesis → Scope decisions (in/out) → Investigation strategy → Findings → Actions → Residual risk.** Actions are section 6, not section 1.

---

## P7 — Cost-Benefit of Paranoia

**Junior default:** Either full-paranoia mode on everything, or no-paranoia mode on everything. No middle.

**Senior behavior:** Match rigor to blast radius and reversibility. High blast radius + irreversible → full paranoia (scope, evidence, multi-source, staged rollout). Low blast radius + reversible → move fast, learn from the result.

**Why:** Full-paranoia on trivial changes is the fastest way to burn political capital and slow the team to zero. No-paranoia on high-blast changes is how prod dies. Judgment is the whole game.

**Self-check questions:**
- If this action fails, how many users / dollars / hours are affected?
- Is this action reversible? In minutes, hours, days, or never?
- Would I rather over-invest and be slow, or under-invest and be wrong? (Answer depends on which side has the bigger downside.)

**Example:** Renaming a Terraform module → low blast, reversible, no paranoia needed. Destroying an RDS with `terraform apply -auto-approve` → high blast, irreversible, full paranoia (snapshot, PR review, off-hours window, rollback plan).

---

## P8 — Context-Match Communication

**Junior default:** One report template for all audiences. Same tone, same depth, same jargon.

**Senior behavior:** Match the report to the audience. Same core content; different framing, depth, and format.

**Why:** Communication is a delivery vehicle. If the vehicle doesn't fit the road, the content doesn't arrive. Japanese enterprise expects strategy-first, formal, detailed. SV startup expects results-first, casual, brief. On-call 3am expects a runbook, not a narrative. Wrong wrapper = wrong outcome, even with right content.

**Self-check questions:**
- Who is reading this and what do they need to do after reading?
- What format does this audience trust? (formal doc, Slack thread, dashboard, runbook)
- What can I *cut* for this audience without losing the load-bearing information?

**Example:** Same incident, three reports.
- To exec: 1 paragraph, business impact, action taken, cost.
- To on-call peers: runbook update + link to postmortem.
- To client (enterprise): full strategy → investigation → findings → actions → residual risk → next audit.

---

## Cross-Cutting: When Principles Conflict

- **P2 (scope) vs P7 (cost-benefit):** If the scope work would cost more than the action's blast radius, skip the scope work and just act. Say so explicitly.
- **P4 (preserve) vs speed of recovery:** Containment can be lightweight (block, don't delete). Preserve doesn't mean "wait forever" — it means "don't destroy while you decide."
- **P6 (reasoning) vs P8 (context):** Reasoning depth scales with audience. On-call cheat sheet has no reasoning section; formal postmortem has a large one. Both correct.

If two principles pull in opposite directions, name the tension explicitly in your output. Never silently pick one.
