---
layout: default
title: Right Tech, Right Reason
---

# Right tech, right reason: an integration platform framework

A proposal for how we decide where to build integrations — SAP CI vs. MuleSoft — without turning it into bureaucracy.

**[→ Try the interactive decision tool](decision-tool.html)** · **[→ Full decision map & reference tables](reference.html)**

---

## 1. The problem

Today, the choice between SAP CI and MuleSoft is made ad hoc — by whoever's available, or by habit, not by what the integration actually needs. That's creating real cost:

- **Duplicate logic** — Two teams independently build access to the same backend data (e.g. SAP billing), each with its own rules — and they quietly drift apart.
- **Inconsistent answers** — Different consumers (Salesforce, a mobile app) can end up seeing different versions of "the same" data because each was integrated separately.
- **Tech debt by accretion** — Every ad hoc integration is a permanent maintenance liability — and nobody's asking "does this already exist?" before building new.
- **Platform turf conflict** — Without a shared decision framework, "which tool do we use" becomes a recurring argument instead of a five-minute decision.

None of this is anyone's fault — it's what happens by default when two capable platforms coexist without a shared reasoning framework. This proposal isn't about restricting either platform. It's about using each one for what it's genuinely good at, and making sure we build a thing once and reuse it — not enforcing process for its own sake.

## 2. Principles

These are the reasoning behind every decision in the framework. The tool applies them mechanically to common cases — but the principles are what should guide judgment on anything the tool doesn't cover.

### 1. Fit for purpose over familiarity
Choose the platform whose native strengths match the job — not the one a team is more comfortable with or has spare capacity in.
> SAP CI and MuleSoft each have real, different strengths. Defaulting by convenience is how turf fights and inconsistent architecture happen.

### 2. One capability, one source of truth
A business capability is exposed through exactly one governed API, reused by every consumer — whether that consumer is a customer-facing app or another backend system.
> Duplicate access paths to the same data inevitably drift apart — different logic, different validation, inconsistent answers to the same question.

### 3. Integration is a liability, not just a feature
Every integration carries ongoing maintenance, security, and complexity cost — "do we need this at all" matters as much as "how do we build it."
> Most integration sprawl isn't malicious — nobody just asked whether reuse was possible before building new.

### 4. Governance scales with exposure, not effort
Oversight should match how widely something is consumed and how much risk it carries — not how hard it was to build.
> This is why a private internal sync skips the API catalog while anything with an external or cross-team consumer doesn't.

### 5. Decisions are transparent and revisitable
Every architecture decision should be traceable to a reason, and open to revisiting if the reason changes.
> This is what keeps the framework a living tool instead of law handed down forever — review it periodically as platforms and systems evolve.

---

**Next:** [Try the interactive decision tool →](decision-tool.html)
