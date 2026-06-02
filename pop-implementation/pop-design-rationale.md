# PoP Design Rationale — KFON Palakkad District

## Based on: Kerala Fibre Optic Network (KFON) — Palakkad District Deployment

This document covers the design rationale for Points of Presence (PoPs) across the
Palakkad district KFON deployment. It explains the decisions behind PoP placement,
tier selection, device configuration approach, and the operational considerations
that shaped the final design.

---

## What is a PoP in the KFON Context

A Point of Presence in the KFON architecture is a physical network node — a location
where active network equipment is housed to aggregate, switch, and route traffic
across the fibre ring. In the Palakkad district deployment, PoPs ranged from large
core facilities housing enterprise-grade switching and routing equipment to smaller
spur locations serving a handful of end offices.

The KFON architecture defines four PoP tiers:

| Tier | Role | Typical equipment |
|---|---|---|
| Core PoP | District-level aggregation, state backbone connection | Cisco Nexus, Juniper MX |
| Pre-Aggregation PoP | Aggregates multiple aggregation rings upstream | Juniper EX, Arista |
| Aggregation PoP | Serves a geographic cluster of end offices | Cisco, Juniper EX |
| Spur PoP | Access tier — connects individual end offices | Cisco, edge switches |

---

## PoP Placement Decisions

PoP placement is not purely a technical decision. In a government infrastructure
project like KFON, placement involves technical requirements, physical availability,
permissions, power supply, and stakeholder approvals — all of which interact and
sometimes conflict.

### Technical Criteria for PoP Placement

**Geographic coverage.**
Each Aggregation PoP must be positioned to serve a defined cluster of end offices
within a reasonable fibre distance. Excessive fibre runs between a PoP and its end
offices increase latency, introduce more splice points, and raise the risk of
signal degradation. In the Palakkad deployment, Aggregation PoPs were positioned
to keep end office fibre runs within practical limits for the required bandwidth.

**Ring topology integrity.**
PoP locations must allow the fibre ring to be physically completed — the chosen
location must be reachable by fibre from both directions of the ring without
excessive deviation from the planned route. A PoP location that works for coverage
but breaks the ring geometry forces a compromise in redundancy.

**Upstream connectivity.**
Each PoP tier must have a viable path to the tier above it. Pre-Aggregation PoPs
must be reachable from Core. Aggregation PoPs must be reachable from
Pre-Aggregation. This upstream path requirement influenced placement decisions
significantly in areas where terrain or permissions limited fibre routing options.

### Non-Technical Constraints on PoP Placement

**Physical space availability.**
A PoP requires a dedicated room or cabinet space with controlled access, adequate
ventilation, and power supply. In government buildings and public institutions
across Palakkad, suitable physical space was not always available at the technically
preferred location. In several cases, the PoP location was adjusted to the nearest
government building with suitable space — which then required reassessing the
fibre route and ring geometry.

**Power supply.**
Enterprise networking equipment requires stable, conditioned power supply with
UPS backup. Several initially preferred PoP locations were rejected or required
significant additional work because the available power supply did not meet
requirements. In rural areas of Palakkad district, power supply quality was a
recurring constraint that affected both PoP placement and the specification of
power conditioning equipment.

**Government approvals.**
Every PoP location required formal approval from the relevant government authority
responsible for the building or land. Approval timelines varied significantly —
from days to weeks — depending on the authority involved. PoP placement planning
had to account for this approval uncertainty, with contingency locations identified
for situations where primary approvals were delayed or refused.

> *In one case during the Palakkad deployment, a preferred Aggregation PoP location
> was approved at design stage but the physical space allocation changed before
> installation could begin. The alternative location required adjusting the fibre
> route for two ring segments and revising the LLD for three adjacent PoPs.*

---

## Device Selection and Configuration Approach

### Equipment Used Across PoP Tiers

The KFON Palakkad deployment used enterprise-grade equipment from multiple vendors
across different PoP tiers:

- **Cisco Nexus 7K** — Core and high-capacity aggregation nodes
- **Juniper EX and MX series** — Aggregation and Pre-Aggregation PoPs
- **Fortinet FortiGate** — Security and firewall at PoP locations
- **Arista** — Selected aggregation nodes
- **Cisco Catalyst series** — Spur and access-tier PoPs

### Configuration Consistency Across 30+ PoPs

Maintaining configuration consistency across 30+ PoPs deployed over an extended
period — with multiple field teams working across different areas simultaneously —
required a structured approach to configuration management.

Key principles applied in the Palakkad deployment:

**Template-based configuration.**
Base configurations were developed for each PoP tier and used as the starting
point for every PoP of that tier. Device-specific parameters — management IPs,
interface assignments, VLAN IDs — were applied on top of the base template.
This reduced configuration errors and made peer review faster.

**HLD and LLD validation before installation.**
Every PoP went through HLD and LLD review before physical installation began.
The LLD for each PoP specified interface assignments, VLAN configuration, routing
parameters, and uplink details. Field teams worked from the approved LLD — not
from verbal instructions.

**As-built verification.**
After installation, each PoP configuration was verified against the approved LLD
and any deviations documented. This as-built verification step caught configuration
errors before the PoP was integrated into the live ring.

---

## Monitoring and Management Setup

Each PoP was added to SolarWinds for centralised monitoring, asset management,
and SLA tracking across the district. Key monitoring parameters configured per PoP:

- Interface status and utilisation
- CPU and memory thresholds
- Link state alerts for uplinks and ring connections
- Power supply status where supported by equipment
- Out-of-band management access for remote troubleshooting

ArcGIS was used to maintain the geographic record of each PoP location — physical
coordinates, building details, and the fibre route connecting it to the ring.
This GIS record became the operational reference for field teams during fault
response and for planning future modifications to the network.

---

## Lessons Learned from PoP Design and Deployment

**Design for the building you will get, not the building you want.**
The technically ideal PoP location and the practically available location are
often different. Build contingency into the design process — identify alternative
locations before approval processes begin so that a rejection does not stall
deployment.

**Power is as important as connectivity.**
A PoP location with excellent fibre connectivity but inadequate power supply
creates ongoing operational problems. Power supply assessment should be part of
the site survey, not an afterthought after equipment is specified.

**LLD accuracy determines installation quality.**
Field teams install what the LLD says. An LLD error does not get caught until
the PoP is being commissioned — at which point fixing it requires either
re-cabling or configuration rework on-site. Investment in LLD accuracy before
installation saves significant time during commissioning.

**Document every deviation immediately.**
When a PoP location, configuration, or fibre route changes from the approved
design, document it immediately. Deviations accumulated across 30+ PoPs over
a multi-month deployment become very difficult to reconcile retrospectively.

---

*This document reflects direct operational experience from the KFON Palakkad
district deployment as Network Engineer and Project Coordinator. PoP design,
placement decisions, and configuration approach are documented as actually
implemented, not as theoretical best practice.*
