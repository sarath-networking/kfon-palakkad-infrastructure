# Fibre Ring Architecture — KFON Palakkad District Deployment

## Based on: Kerala Fibre Optic Network (KFON) — Palakkad District

This document covers the fibre ring architecture designed and deployed across Palakkad
district as part of the Kerala Fibre Optic Network (KFON) — a Government of Kerala
initiative to deliver high-speed broadband connectivity across the state. It reflects
direct operational experience from the district-level deployment, covering design
decisions, implementation challenges, and lessons learned.

---

## Project Context

The KFON Palakkad district deployment involved:

- 500+ km of fibre network infrastructure across the district
- 30+ Points of Presence (PoPs) — Core, Pre-Aggregation, Aggregation, and Spur
- 450+ end offices — government institutions, public service delivery points
- Multiple vendor coordination across a geographically diverse district
- Strict government delivery timelines and approval processes

The fibre ring architecture was the foundation of the entire deployment. Every
design decision made at this stage had direct consequences on redundancy, scalability,
and operational reliability months and years after go-live.

---

## Why Ring Topology

A linear or star topology was not viable for a district-level deployment of this
scale. The key requirements that drove the ring architecture decision:

**Redundancy without duplication of equipment.**
A ring allows traffic to route in either direction around the loop. If a fibre break
occurs at any single point, traffic automatically reroutes in the opposite direction
with no manual intervention. For a network serving government offices and public
institutions, this level of resilience was a baseline requirement.

**Scalability across a large geographic area.**
Palakkad district covers diverse terrain — urban areas, rural stretches, and
geographically challenging sections. A ring topology allows new PoPs to be added
to the ring without redesigning the upstream architecture, making it well-suited
for phased deployment.

**Alignment with KFON's multi-tier PoP structure.**
The KFON architecture defines four PoP tiers — Core, Pre-Aggregation, Aggregation,
and Spur. A ring topology at each tier level allows traffic aggregation to flow
upward through the hierarchy while maintaining local redundancy at each ring.

---

## PoP Hierarchy and Ring Structure

The Palakkad district deployment followed a four-tier PoP hierarchy:

### Core PoP
The highest tier in the district hierarchy. Connects to the state-level KFON
backbone. All district traffic aggregates here before being handed off upstream.
Core PoPs are fully redundant — dual uplinks, redundant power, and out-of-band
management.

### Pre-Aggregation PoP
Sits between Core and Aggregation tiers. Aggregates traffic from multiple
Aggregation rings before passing upstream to Core. Pre-Aggregation PoPs form their
own ring connecting back to the Core PoP, ensuring no single point of failure
between tiers.

### Aggregation PoP
The primary distribution tier across the district. Multiple Aggregation PoPs form
a ring, each serving a geographic cluster of end offices. Aggregation rings were
sized based on the number of end offices in each cluster and the projected traffic
demand per area.

### Spur PoP
The access tier — connects individual end offices to the Aggregation ring. Spur
PoPs are typically single-homed to the Aggregation ring rather than forming their
own ring, as end offices represent the termination point of the network rather than
a transit node.

---

## Design Decisions and Ground-Level Challenges

### Fibre Route Planning vs Physical Reality

The most significant gap in ring architecture deployment is between the planned
route on a GIS map and what can actually be built on the ground.

In the Palakkad deployment, planned fibre routes were designed using GIS mapping
tools — identifying the shortest viable path between PoP locations that completed
the ring. However, physical deployment consistently revealed constraints that
required route modifications:

- **Permission delays** — certain road stretches required approvals from local
  authorities, highways departments, or private landowners. A permission refusal
  on a planned segment could stall that section of the ring for weeks
- **Existing underground infrastructure** — undocumented utilities, drainage
  systems, and previously laid cables created obstacles that were not visible
  in GIS data
- **Terrain constraints** — particularly in rural and hilly sections of Palakkad,
  planned aerial routes sometimes required additional pole installations or
  underground ducting that was not accounted for in the original design

Every route modification at one point in the ring had downstream implications —
for the fibre count, splice point locations, and the LLD documentation for adjacent
PoPs. Managing this deviation process systematically was critical to maintaining
design integrity across the deployment.

> *In one case in Palakkad, a planned fibre route segment had to be redesigned
> entirely because the approved path ran through an area where underground
> permissions could not be obtained in the required timeframe. The rerouting
> added approximately 8km of additional fibre and required revising the LLD
> for two adjacent PoPs.*

### Ring Closure — The Critical Milestone

Deploying a ring is not complete until the ring is physically closed — the fibre
path returns to its starting point and the optical signal can travel in both
directions. In a large district deployment with 30+ PoPs, ring closure involves
coordinating fibre laying, splicing, and testing across potentially dozens of
kilometres simultaneously.

Until the ring is closed, the network operates in a linear, non-redundant state.
Any fibre break during this period causes a complete loss of connectivity for
everything downstream of the break point. Managing this exposure window — keeping
it as short as possible — was a key operational priority during deployment.

### Fibre Count Planning

Each ring segment requires sufficient fibre count to support:
- Current traffic capacity at the designed bandwidth
- Protection paths (typically 1+1 protection for critical segments)
- Future capacity headroom — additional fibres for planned expansion
- Management connectivity — out-of-band management fibres for PoP devices

Under-provisioning fibre count at the design stage is one of the most costly
mistakes in a ring deployment. Adding fibre to an existing duct requires either
pulling new fibre through the existing duct (if space allows) or laying entirely
new duct — both significantly more expensive than getting the count right at
the initial installation.

### Splice Point Documentation

Every splice point in the ring — where fibre lengths are joined — must be
precisely documented. Splice points are the most common location for future
fault events, and without accurate documentation of their physical location,
fault diagnosis and repair becomes significantly slower.

In the Palakkad deployment, splice point documentation was maintained as part
of the as-built records for each ring segment, updated in real time as deployment
progressed rather than retrospectively after completion.

---

## Lessons Learned

**Design for deviation, not just for the ideal path.**
In a district-scale deployment, assuming the planned route will be built exactly
as designed is unrealistic. Build a deviation management process into the project
from the start — a standard way to assess, document, and update design when the
ground demands a change.

**Ring closure planning is as important as ring design.**
The sequence in which ring segments are built determines how long the network
operates in a non-redundant linear state. Plan the deployment sequence to minimise
this exposure window — prioritise completing the ring over optimising individual
segment efficiency.

**As-built documentation starts on day one.**
Documentation created retrospectively after deployment relies on memory and is
significantly less accurate than documentation created in real time. For a ring
with 30+ PoPs, the accumulation of small undocumented deviations creates a gap
between the design and the actual network that takes significant effort to reconcile.

**Fibre count decisions cannot be reversed cheaply.**
Get the fibre count right at design stage. The additional cost of provisioning
slightly more fibre than current demand requires is negligible compared to the
cost of adding fibre to an installed route later.

---

## Technology Stack — Palakkad Deployment

- **Core and Aggregation switching** — Cisco Nexus, Juniper, Arista
- **Security and access control** — Fortinet FortiGate
- **Network monitoring** — SolarWinds (asset management, SLA tracking, monitoring)
- **GIS mapping** — ArcGIS (route planning, network mapping, analytical data modelling)
- **Design documentation** — HLD, LLD, and SLD prepared for each PoP tier

---

*This document reflects direct operational experience from the KFON Palakkad district
deployment as Network Engineer and Project Coordinator. It is written to document
real design decisions and ground-level challenges, not as a theoretical overview
of ring topology principles.*
