# Worker-Informed Participation Protocol (WIPP): Construction & Field Services Version

**Version 1.0**  
**Date:** October 2026  
**Base document:** [WIPP Clause v1.0](../WIPP-CLAUSE.md)  
**Repository:** [WorkerInformedAI](https://github.com/nphoenix/WorkerInformedAI)

## Purpose and Scope

This version adapts WIPP to construction, maintenance, installation, utility, and other field-service work. These sectors have features the base clause does not fully address:

- **Multi-employer worksites**: general contractors, subcontractors, staffing agencies, and owners may each deploy or control technology on the same site.
- **Short-duration and mobile work**: crews change often, work spans many sites, and workers may be dispatched through hiring halls or apps.
- **Wearables and site sensing**: proximity sensors, fatigue and heat-stress monitors, smart PPE, site cameras with computer vision, and drones.
- **Algorithmic scheduling and dispatch**: route optimization, job-time estimates, and automated assignment for field technicians.
- **Exposure monitoring**: digital monitoring of silica, noise, heat, vibration, and other hazards.
- **Vehicle and device telematics**: GPS, driver-behavior scoring, and mobile-device tracking.

All six mandatory requirements of the base WIPP clause apply. This document adds sector-specific requirements, labeled **C-1** and onward, under each one.

---

## Mandatory Requirements (Sector Adaptations)

### a. Early-Stage Involvement
- **C-1. Representation across employers.** On multi-employer sites, worker representatives from each trade or employer materially affected by a System shall be invited to participate, not only employees of the deploying employer.
- **C-2. Accessible participation.** Participation activities shall be scheduled during paid working time, held at or near the site or by mobile-friendly means, and offered in the languages spoken by the crews.
- **C-3. Field validation.** Requirements shall be tested against real site conditions, such as weather, PPE, gloves, noise, connectivity, and lighting, with workers who perform the tasks.

### b. Collaborative Impact Assessment
In addition to the base assessment criteria, the joint team shall assess:
- **C-4. Safety-critical reliance.** Whether workers or supervisors may rely on the System for hazard warnings (e.g. proximity alerts, gas or heat alerts), and what happens when it fails, gives false alarms, or loses connectivity. Alarm fatigue shall be considered explicitly.
- **C-5. Displacement of existing controls.** Confirmation that the System supplements, and does not replace, required engineering controls, competent-person duties, or existing safety programs.
- **C-6. Pace and fatigue.** Effects of dispatch, routing, and job-time estimates on rest breaks, travel time, heat exposure, and pressure to skip safety steps.
- **C-7. Off-site and off-shift data.** Whether wearables, vehicles, or apps collect location or biometric data during travel, breaks, or off-duty time.

### c. Iterative Co-Design and Testing
- **C-8. Pilot on representative crews.** Pilots shall include a range of trades, shifts, experience levels, and body sizes for wearables and smart PPE. Fit, comfort, and heat burden shall be evaluated.
- **C-9. Failure drills.** Testing shall include simulated sensor failure and loss of connectivity, with documented fallback procedures.

### d. Pre-Deployment Approval Gate
- **C-10. Site-level approval.** Approval applies to each deployment context. Moving a System to a new site type or hazard profile requires review.
- **C-11. Controlling-employer coordination.** On multi-employer sites, the employer controlling the System shall share the Impact Assessment, data practices, and worker notice with other employers' worker representatives before workers are covered by the System.
- **C-12. Vendor data inventory.** Procurement shall include the [Vendor Telemetry Addendum](vendor-telemetry-addendum.md) or equivalent terms, in particular for wearables and telematics.

### e. Ongoing Governance
- **C-13. Committee continuity.** Because crews and sites change, the Joint Worker Participation Committee may operate at the project, regional, or employer level, as agreed. It shall have a defined way to take input from workers who are only on site for a short time.
- **C-14. Exposure data access.** Workers shall have timely access to their own exposure monitoring results, in addition to any notification required by applicable occupational safety and health regulations. Aggregate results shall be shared with the Committee.
- **C-15. Use restrictions.** Data from safety wearables, exposure monitors, and site cameras shall be used for health and safety purposes. It shall not be used for productivity scoring or discipline, except as specifically agreed through the WIPP process with a named human reviewer and disclosure of the data to the worker.
- **C-16. Telematics limits.** Vehicle and device location tracking shall be limited to working time and work vehicles or devices, unless otherwise agreed. Driver-behavior scores shall not be the sole basis for discipline.
- **C-17. Right to raise stop-work concerns.** Workers may report System malfunctions or unsafe System-driven instructions without retaliation. A credible report of a safety-critical malfunction triggers review and, where warranted, suspension of the affected function.

### f. Training and Capacity Building
- **C-18. Practical, site-based training.** Training shall be hands-on and delivered in crew languages during paid time. It shall cover what the System monitors, its limits, fallback procedures, and how to raise concerns.
- **C-19. Training for supervisors and competent persons.** Supervisors shall be trained on appropriate and prohibited uses of System outputs.

## Documentation and Compliance

- The WIPP Record shall identify, for each site or deployment context, the System version, approved configuration, applicable worker notice, and the employer responsible.
- Where AI services are used, such as computer-vision safety analytics or dispatch optimization, the [reference architecture](../docs/architecture.md) can be used to enforce agreed use restrictions and to provide the Committee with an audit log.
- Violations or unresolved safety concerns trigger grievance procedures, independent audits, or deployment halts, as in the base clause.

## Adaptability and Review

This sector version may be adapted by mutual agreement while preserving the core participation rights of the base WIPP clause. It shall be reviewed annually, or when a significant technology change occurs or a safety incident involves a covered System, with worker input required.

---

**License**: This work is released under [CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/).  
You are free to adapt and use it with attribution to:  
**inXsol LLC** — [WorkerInformedAI](https://github.com/nphoenix/WorkerInformedAI)

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
