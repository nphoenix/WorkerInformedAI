# WorkerInformedAI Roadmap

**Project Goal**: Advance meaningful, structured worker participation in the design and deployment of AI and software systems that affect health, safety, and working conditions through open protocols, tools, and practical resources.

**Current Version**: 1.1 (October 2026)

---

## 📍 Completed

### v1.0 (June 2026)
- Initial release of the **Worker-Informed Participation Protocol (WIPP)** boilerplate clause
- Joint Worker-Employer Impact Assessment Template
- Core repository structure, README, and contributing guidelines
- Licensing and attribution framework (CC-BY-4.0 via inXsol LLC)
- Alignment with NIST AI RMF, UC Berkeley Labor Center, and NIEHS themes

### v1.1 (October 2026)
- [Reference architecture](docs/architecture.md) for policy authoring, enforcement, and audit
- [CBA-to-policy walkthrough](examples/cba-to-policy-walkthrough.md), an illustrative worked example
- [Vendor Telemetry & Data Disclosure Addendum](clauses/vendor-telemetry-addendum.md)
- [Construction & Field Services sector version](clauses/WIPP-CLAUSE-construction-field-services.md)

---

## 🔧 Now: Active Development (Q4 2026)

The reference architecture moved forward from the earlier 2027–2028 plan. It is now in active development as three workstreams:

- **Authoring**: Collaborative policy authoring in which worker representatives and employers co-author policy informed by collective bargaining agreements. One source produces contract terms, plain-language worker notices, and policy-as-code.
- **Enforcement**: Open Policy Agent (Rego) policy bundles with tests, plus integration examples for existing open-source AI gateways (e.g. LiteLLM, Envoy AI Gateway, Kong AI Gateway). Each request gets a WIPP policy check. No traffic interception or decryption.
- **Audit**: OpenTelemetry event schema (GenAI semantic conventions plus `wipp.*` attributes), an append-only hash-chained log format, and a chain verifier the Joint Worker Participation Committee can run. Optional xAPI worker-facing records.

The vendor telemetry approach (contractual disclosure, log export, egress/DNS metadata checks against the procurement data inventory) is being developed alongside these workstreams.

---

## 🗓️ Q4 2026 – Q1 2027 (Short-term)

- Remaining sector versions:
  - Manufacturing / Industrial
  - Healthcare / Clinical
- Additional templates:
  - Joint Worker Participation Committee Charter
  - Co-Design Workshop Facilitation Guide
  - Sample RFP / Procurement Language
- **WIPP Implementation Guide** (how-to for unions and employers)
- First tagged release of reference policy bundles and audit schema
- Outreach and feedback from unions, worker organizations, and EHS professionals

---

## 2027 (Medium-term)

- Harden the reference components based on pilot feedback
- Committee-facing audit views and summary reports built on the audit log
- GitHub / Jira ticket integration for WIPP Record tracking
- Versioning support for libraries and AI knowledge sources (prompts, retrieval data)
- Training materials (slide decks, videos) for worker representatives
- Case studies and a pilot documentation framework
- Internationalization: Spanish translation of core documents
- Collaboration with labor centers and training organizations

---

## 2028+ (Long-term)

- Compliance reporting and Joint Committee dashboard, built on the audit stream
- Mappings to related standards (ISO/IEC 42001, EU AI Act worker provisions)
- Community-driven extensions and sector-specific toolkits
- Long-term sustainability: open core, with optional commercial verification services via inXsol LLC
- Potential nonprofit collaboration for broad adoption

---

## How You Can Help

- ⭐ Star and share the repository
- Open issues with your use cases or suggested improvements
- Submit Pull Requests with adaptations or new templates
- Test the WIPP clause in real negotiations or pilots (share anonymized learnings)
- Provide feedback from unions, workers, EHS professionals, or AI developers

**Success Metric**: Widespread adoption of WIPP language in union contracts, corporate policies, and responsible AI frameworks — leading to safer, more equitable workplace technology.

---

**License**: This roadmap is released under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) with attribution to **inXsol LLC** — [WorkerInformedAI](https://github.com/nphoenix/WorkerInformedAI)
