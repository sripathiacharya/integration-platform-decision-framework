---
layout: default
title: Reference — Decision Map & Tables
---

[← Back to problem statement & principles](index.html) · **[→ Try the interactive decision tool](decision-tool.html)**

# Reference: full decision map & tables

## Decision map

<div style="overflow-x:auto; background:#f7f8fa; border:1px solid #dfe3e8; border-radius:12px; padding:20px;">
<pre class="mermaid">
flowchart TD
    A["New integration request"] --> Z{"Does a Capability API<br/>already exist for this data/domain,<br/>OR could more than one consumer<br/>ever need it — app, web, partner,<br/>OR another backend system?"}

    Z -- "Yes — reusable / already exists" --> F{"Which layer is<br/>being built or reused?"}
    Z -- "No — genuinely bilateral,<br/>one-off, operational sync only" --> B{"Confirm: no external-facing<br/>consumer today or foreseeable<br/><small>(app, web, partner, AI agent)</small>"}

    B -- "Confirmed — true A2A" --> C{"Is at least one endpoint SAP,<br/>with a native adapter or<br/>accelerator advantage?<br/><small>(IDoc / BAPI / RFC / prebuilt content)</small>"}
    B -- "Consumer surfaces later<br/>→ re-route to Capability API" --> F

    C -- "Yes" --> D["Build in SAP CI<br/><small>A2A — no external consumer,<br/>no API catalog entry needed</small>"]
    C -- "No<br/><small>e.g. Salesforce ↔ Workday</small>" --> E["Build in MuleSoft<br/><small>A2A, platform-agnostic default</small>"]

    F -- "Capability API" --> G{"Source system = SAP,<br/>and SAP CI already has /<br/>can cheaply build native<br/>OData or REST exposure?"}
    G -- "Yes" --> H["Build connectivity in SAP CI<br/>(OData / REST)<br/>↓<br/>Front with MuleSoft<br/>API Manager proxy<br/><small>governance, auth, catalog entry</small>"]
    G -- "No<br/><small>e.g. Salesforce-origin</small>" --> I["Build natively in MuleSoft"]

    F -- "Orchestration API" --> J["Always MuleSoft<br/><small>composes multiple Capability APIs,<br/>platform-agnostic by design</small>"]

    F -- "Experience API" --> K["Always MuleSoft<br/><small>web / mobile / partner /<br/>MCP-agent channel</small>"]

    classDef sap fill:#0a6ed1,stroke:#075aad,color:#ffffff,font-size:13px;
    classDef mule fill:#00a3e0,stroke:#0080b0,color:#ffffff,font-size:13px;
    classDef both fill:#6b46c1,stroke:#553497,color:#ffffff,font-size:13px;
    classDef q fill:#f7f8fa,stroke:#8a94a3,color:#1a1a1a,font-size:13px;
    classDef start fill:#1a1a1a,stroke:#000000,color:#ffffff,font-size:13px;

    class A start
    class Z,B,C,F,G q
    class D sap
    class E,I,J,K mule
    class H both
</pre>
</div>

**Legend:** 🔵 SAP CI builds &nbsp;·&nbsp; 🟦 MuleSoft builds &nbsp;·&nbsp; 🟣 SAP CI + MuleSoft (build + front) &nbsp;·&nbsp; ⬜ Decision point

<script src="https://cdnjs.cloudflare.com/ajax/libs/mermaid/10.9.1/mermaid.min.js"></script>
<script>mermaid.initialize({ startOnLoad: true, theme: 'base', flowchart: { curve: 'basis', htmlLabels: true } });</script>

---

## Reference table

| Scenario | Build in | Notes |
|---|---|---|
| SAP ↔ SAP internal sync | **SAP CI** | Native IDoc/ALE/change-pointer support, no external consumer |
| SAP ↔ Salesforce backend replication (no app/web consumer) | **SAP CI** | SAP-side leverage still applies even though Salesforce is the other endpoint |
| Salesforce ↔ Workday (or any non-SAP pair) | **MuleSoft** | No SAP-native advantage exists for either endpoint |
| Capability API over SAP (billing, etc.) | **SAP CI + MuleSoft** | SAP CI exposes OData/REST; Mule API Manager fronts it for governance/catalog |
| Capability API over Salesforce (CRM, etc.) | **MuleSoft** | Mature native Salesforce connector, no reason to route through SAP CI |
| Orchestration API (cross-capability business process) | **MuleSoft** | Always — stays platform-agnostic regardless of what built the capabilities beneath it |
| Experience API (web, mobile, partner, MCP/agent) | **MuleSoft** | Always — channel-facing layer, never built in SAP CI |

## Capability registry — the enforcement mechanism

> A short, living list of business capabilities and their APIs. Anyone proposing an A2A flow checks this list first. Already listed → mandatory reuse. Not listed and genuinely uncertain whether a second consumer will ever exist → default to registering it, since retrofitting a private pipe into a governed API later is far more expensive.

| Capability | Capability API owner | Known consumers |
|---|---|---|
| Billing | MuleSoft (fronting SAP CI OData) | Mobile app, Web, Salesforce |
| Customer / CRM | MuleSoft (native Salesforce connector) | Mobile app, Web, SAP (if needed) |
| Workforce Management | MuleSoft | Web, field ops app |
| *— add rows as new capabilities are registered —* | | |

---

[← Back to problem statement & principles](index.html) · **[→ Try the interactive decision tool](decision-tool.html)**
