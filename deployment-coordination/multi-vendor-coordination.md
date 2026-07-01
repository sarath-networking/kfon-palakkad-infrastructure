# Multi-Vendor Coordination — KFON Palakkad District Deployment

## Based on: Kerala Fibre Optic Network (KFON) — Palakkad District Deployment

This document covers the multi-vendor coordination approach used during the KFON
Palakkad district deployment. It reflects direct operational experience managing
simultaneous workstreams across civil works contractors, fibre laying teams, splicing
specialists, equipment suppliers, and technology vendors across a district-scale
government infrastructure project.

In a deployment of this scale, vendor coordination is not an administrative function —
it is a critical path dependency. Delays, quality issues, or communication failures
with any single vendor have direct knock-on effects across the entire deployment
sequence.

---

## Vendor Landscape — KFON Palakkad

The Palakkad deployment involved multiple vendor categories operating simultaneously
across different geographic areas of the district:

| Vendor category | Role | Key dependencies |
|---|---|---|
| Civil works contractors | Trenching, ducting, pole installation | Must complete before fibre laying |
| Fibre laying teams | Cable pulling, aerial stringing, underground laying | Must complete before splicing |
| Splicing specialists | Fibre joint preparation and testing | Must complete before commissioning |
| Equipment suppliers | Cisco, Juniper, Fortinet, Arista delivery | Must arrive before installation |
| Installation teams | Rack mounting, cabling, device commissioning | Must follow civil and fibre completion |
| Testing and acceptance | Optical power testing, splice loss measurement | Must pass before integration |
| Government/KSEB coordination | Permission, pole access, power supply | Parallel track, gates all above |

The interdependency between these workstreams meant that delays in any one category
created cascading effects across others. A civil works delay at one PoP site prevented
fibre laying, which prevented splicing, which prevented commissioning — regardless of
how ready all other vendors were.

---

## Coordination Structure

### Single Point of Contact Per Vendor

All coordination with each vendor was routed through a single named contact on both
sides — one point of contact from the project team, one from the vendor. This
prevented conflicting instructions from reaching vendor teams and ensured that all
commitments were trackable to a specific person.

Where vendors had multiple teams working in different parts of the district
simultaneously, the vendor's named contact was responsible for cascading instructions
to their own teams. The project team did not communicate directly with individual
vendor field operatives — all coordination went through the agreed contact structure.

### Weekly Vendor Coordination Meetings

All active vendors participated in a weekly coordination meeting covering:

- Progress against the previous week's commitments
- Planned activities for the coming week
- Pending issues and blockers — what each vendor needed from the project team or
  from other vendors to proceed
- Delivery schedule alignment — confirming that equipment and materials would arrive
  at sites in line with the commissioning sequence

Issues that could be resolved at working level were addressed in the meeting.
Issues requiring escalation — permissions, design changes, contractual matters —
were flagged and tracked with a named owner and target resolution date.

### Dependency Tracking

The interdependency between vendor workstreams was tracked explicitly — not assumed.
For each PoP in the deployment sequence, the status of every prerequisite workstream
was recorded:

- Civil works complete — yes/no
- Fibre laid and tested — yes/no
- Splice points completed and tested — yes/no
- Equipment delivered — yes/no
- Power supply confirmed — yes/no
- Permissions in place — yes/no

A PoP did not move to the installation phase until all prerequisites were confirmed.
This prevented field teams from arriving at sites that were not ready, and prevented
equipment from being delivered to sites where installation could not yet proceed.

---

## Equipment and Material Logistics

### Delivery Sequencing

Equipment and material delivery was coordinated against the commissioning sequence —
ensuring that what was needed at each site arrived at the right time.

**Early delivery created problems:**
Equipment arriving at a site before civil works were complete had nowhere suitable
to be stored securely. Public sector locations did not always have secure storage
available, and leaving equipment on-site before installation increased the risk of
damage or loss.

**Late delivery created delays:**
Installation teams arriving at a site to find that equipment had not been delivered
meant a wasted mobilisation — field teams travelling to a site they could not work
at. In a district-scale deployment with teams moving between multiple sites, wasted
mobilisations compounded quickly into significant schedule impact.

The target was equipment arriving within the specific window between civil and fibre
completion and the planned installation date — close enough to minimise storage
risk, with enough buffer that minor delivery delays did not cause immediate schedule
impact.

### Acceptance Testing at Delivery

Equipment was not accepted as ready for installation on delivery alone. A physical
inspection was conducted on arrival — checking for transit damage, verifying model
numbers and specifications against the approved LLD, and confirming that all
required accessories and documentation were included.

Discrepancies identified at acceptance were significantly faster to resolve than
discrepancies discovered during installation, when field teams were on-site and
waiting.

---

## Quality Management Across Vendors

### Civil Works Quality

The quality of civil works — particularly duct installation and pole preparation —
directly affected the ease of subsequent fibre laying. Ducts installed with
inadequate conduit radius or at incorrect burial depth created problems during
cable pulling that were expensive to rectify after the fact.

Quality checkpoints were established at key civil works stages:
- Duct installation inspected before backfilling — checking depth, conduit radius,
  and draw-wire installation
- Pole installation inspected before aerial cable stringing — checking height,
  stay-wire installation, and structural condition

### Fibre Acceptance Testing

Before any fibre segment was handed over for splicing, optical acceptance testing
was conducted on the installed cable:

- Optical Time Domain Reflectometer (OTDR) trace taken for each fibre
- Insertion loss measured against the acceptable threshold for the segment length
- Any anomalies — splice points, bends, or physical damage — identified and
  resolved before splicing commenced

Segments that did not pass acceptance testing were not progressed to splicing.
Identifying fibre issues before splicing was significantly less disruptive than
discovering them after splice closures had been sealed.

### Splice Loss Measurement

After splicing, each splice point was measured for insertion loss. Splice loss
exceeding the acceptable threshold required the splice to be redone — a process
that was manageable when caught immediately but significantly more disruptive if
discovered after the PoP had been commissioned and integrated into the live network.

---

## Lessons Learned

**Vendor coordination structure must be established before deployment begins.**
Trying to establish coordination protocols after problems arise is significantly
harder than establishing them at the start. Named contacts, meeting cadence, and
escalation paths should be agreed with all vendors before any field work begins.

**Dependency tracking cannot be informal.**
In a deployment with 30+ PoPs and multiple simultaneous vendor workstreams, informal
tracking of prerequisites introduces risk. A structured, explicit record of what
is complete and what is pending for each site is what prevents teams from
mobilising to sites that are not ready.

**Quality checkpoints are an investment, not an overhead.**
The time spent on civil works inspection, fibre acceptance testing, and splice loss
measurement before each phase was consistently recovered many times over by
preventing rework and site revisits. The cost of catching a quality issue early
was always lower than the cost of discovering it later.

**Delivery timing is as important as delivery completion.**
Getting equipment to a site on time means within a specific window — not just
before the deadline. Early delivery and late delivery both create operational
problems, in different ways. Coordinating delivery against the installation
sequence required active management throughout the deployment, not a one-time
logistics arrangement at the start.

---

*This document reflects direct operational experience from the KFON Palakkad
district deployment as Network Engineer and Project Coordinator. Multi-vendor
coordination approaches are documented as actually applied during the deployment,
not as theoretical project management frameworks.*
