# Walkthrough: From a CBA Clause to an Enforceable, Auditable Policy

> **Illustrative example only.** The bargaining agreement, employer, system name, and all values below are fictional. They show the shape of the process, not a recommended contract or a real deployment.

This walkthrough follows one provision through the five stages of the [WIPP reference architecture](../docs/architecture.md):

1. CBA clause → 2. WIPP term → 3. Plain-language worker notice → 4. Policy-as-code rule → 5. Audit event

---

## 1. Sample CBA clause (fictional)

> **Article 14: Technology and Electronic Monitoring**
>
> 14.1 The Employer shall give the Union at least thirty (30) days' written notice before introducing or materially changing any electronic monitoring or algorithmic management system, and shall bargain over its effects on request.
>
> 14.2 Location data shall not be collected or used outside an employee's scheduled working time.
>
> 14.3 Data from electronic monitoring or algorithmic systems shall not be the sole basis for discipline. Any disciplinary use requires review by a named supervisor, and the employee shall be given the underlying data.

## 2. WIPP term

The joint authoring group maps the clause onto [WIPP](../WIPP-CLAUSE.md) requirements and makes it specific to one system, here a fictional AI scheduling assistant, `shift-assist-v2`.

| WIPP term | Source | WIPP requirement |
|---|---|---|
| **MON-1.** Only systems approved by the Joint Worker Participation Committee may call AI services through the gateway. Approval follows the 30-day notice and the Impact Assessment. | Art. 14.1 | (b) Impact Assessment, (d) Approval Gate |
| **MON-2.** Requests that include location data are refused when the worker is not on shift. | Art. 14.2 | (b) Privacy |
| **MON-3.** Any request with purpose `discipline` must name a human reviewer. The output and the inputs it relied on are logged for disclosure to the employee. | Art. 14.3 | (e) Ongoing Governance, override |
| **MON-4.** All decisions are written to the committee's audit log. Prompt and response content is not logged. | Art. 14.1, 14.3 | Documentation & WIPP Record |

## 3. Plain-language worker notice

> **About Shift Assist (AI scheduling tool)**
>
> **What it does:** Suggests shift schedules and swaps based on your availability, skills, and staffing needs. A scheduler makes the final decision.
>
> **What it uses:** Your availability, certifications, past shifts, and, *during your shift only*, which work zone you are assigned to.
>
> **What it will not do:**
> - It will not use your location when you are off shift.
> - It cannot be the only reason for discipline. A named supervisor must review, and you have the right to see the data used.
>
> **Who checks:** The Joint Worker Participation Committee, which includes worker representatives, reviews a log of how the tool is used.
>
> **Questions or concerns:** Talk to your steward or committee member. Raising a concern is protected; there is no retaliation.

## 4. Policy-as-code (Open Policy Agent / Rego)

The same terms, written as a short Rego policy that the AI gateway checks on each request. The tests encode the negotiated protections, so a later change that weakens them fails review.

```rego
package wipp.monitoring

import rego.v1

default allow := false

# Systems approved by the Joint Worker Participation Committee (WIPP d)
approved_systems := {"shift-assist-v2"}

deny contains msg if {
	not input.system.id in approved_systems
	msg := "WIPP-MON-1: system not approved by Joint Committee"
}

deny contains msg if {
	"location" in input.request.data_categories
	not input.worker.on_shift
	msg := "WIPP-MON-2: location data outside working time"
}

deny contains msg if {
	input.request.purpose == "discipline"
	not input.request.human_reviewer
	msg := "WIPP-MON-3: monitoring output used for discipline without human review"
}

allow if count(deny) == 0
```

```rego
package wipp.monitoring_test

import rego.v1

import data.wipp.monitoring

test_discipline_requires_reviewer if {
	not monitoring.allow with input as {
		"system": {"id": "shift-assist-v2"},
		"request": {"purpose": "discipline", "data_categories": ["productivity"]},
		"worker": {"on_shift": true},
	}
}

test_scheduling_allowed if {
	monitoring.allow with input as {
		"system": {"id": "shift-assist-v2"},
		"request": {"purpose": "scheduling", "data_categories": ["availability"]},
		"worker": {"on_shift": true},
	}
}
```

Run with `opa test . -v`. In practice the approved-systems list would be loaded as data from the WIPP Record, not hard-coded.

## 5. Audit event (OpenTelemetry)

Each decision is emitted as an OpenTelemetry log event. It uses the [GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/) for the model call and `wipp.*` attributes for the policy decision, and it is appended to the hash-chained audit log. This example shows a denied disciplinary request with no named reviewer:

```json
{
  "timestamp": "2026-10-12T15:42:07Z",
  "event_name": "wipp.policy.decision",
  "attributes": {
    "gen_ai.operation.name": "chat",
    "gen_ai.provider.name": "example-provider",
    "gen_ai.request.model": "example-model",
    "wipp.system.id": "shift-assist-v2",
    "wipp.policy.bundle": "wipp.monitoring",
    "wipp.policy.version": "2026.10.1",
    "wipp.record.ref": "WIPP-REC-0042",
    "wipp.request.purpose": "discipline",
    "wipp.request.data_categories": ["productivity"],
    "wipp.decision": "deny",
    "wipp.decision.reasons": ["WIPP-MON-3: monitoring output used for discipline without human review"],
    "wipp.subject.ref": "pseudonymous:7f3a…",
    "wipp.content_logged": false
  },
  "wipp.audit.prev_hash": "sha256:9b1e…",
  "wipp.audit.hash": "sha256:c47d…"
}
```

Notes:
- Workers are identified by a pseudonymous reference. Re-identification is limited to cases set out in the agreement, such as when a worker requests their own records.
- Hashes are truncated for readability. Each `hash` covers the record contents plus `prev_hash`, so removing or editing any record breaks the chain.
- `wipp.*` attribute names are a proposed convention in this repository, not part of the OpenTelemetry specification.

---

**Next steps for adapters:** replace the fictional clause with your own agreement language, keep the four-way mapping (term → notice → rule → event), and record each version in your WIPP Record.

---

**License**: This work is released under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/).  
You are free to adapt and use it with attribution to:  
**inXsol LLC** — [WorkerInformedAI](https://github.com/nphoenix/WorkerInformedAI)

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
