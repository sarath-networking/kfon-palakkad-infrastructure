# PoP Commissioning Checklist — KFON Palakkad District

## Based on: Kerala Fibre Optic Network (KFON) — Palakkad District Deployment

This checklist covers the commissioning process for Points of Presence (PoPs) across
the Palakkad district KFON deployment. It reflects the actual steps followed during
site preparation, equipment installation, configuration validation, and handover for
each PoP tier — Core, Pre-Aggregation, Aggregation, and Spur.

Commissioning a PoP in a government infrastructure project involves more than
technical configuration. It requires physical site readiness, stakeholder sign-off,
documentation accuracy, and integration into the wider network — all of which must
be completed in sequence before the PoP can carry live traffic.

---

## Pre-Commissioning — Site Readiness

Before any equipment is installed, the physical site must meet the following
requirements. Commissioning a PoP in a site that is not ready creates delays that
are significantly more disruptive than addressing site issues before equipment arrives.

### Physical Space
- [ ] Dedicated room or cabinet space confirmed and accessible
- [ ] Space is clean, dust-controlled, and free from water ingress risk
- [ ] Cable management routes identified — fibre entry points, patch panel locations
- [ ] Equipment rack installed and secured — rack dimensions match equipment specs
- [ ] Physical access control confirmed — site is secured against unauthorised access

### Power Supply
- [ ] Mains power supply confirmed at the required voltage and current capacity
- [ ] UPS installed and tested — confirmed operational before equipment installation
- [ ] UPS battery runtime verified — meets minimum backup duration requirement
- [ ] Earth bonding confirmed — equipment chassis earthed to building earth point
- [ ] Power distribution within rack confirmed — PDUs installed and tested

### Environmental
- [ ] Ambient temperature within acceptable range for equipment specifications
- [ ] Ventilation or air conditioning confirmed operational
- [ ] Temperature and humidity monitoring in place for Core and Pre-Aggregation PoPs

> *In the Palakkad deployment, power supply readiness was the most common cause
> of commissioning delays. Several sites required additional electrical work before
> equipment could be safely installed. Power supply assessment during the site survey
> stage — before equipment is ordered — prevents these delays.*

---

## Equipment Installation

- [ ] Equipment delivered to site — quantities and models verified against LLD
- [ ] Physical inspection completed — no transit damage to equipment
- [ ] Equipment mounted in rack per the approved rack elevation diagram
- [ ] Cable management installed — fibre and copper runs dressed and labelled
- [ ] Fibre patch cables connected — LC/SC connectors confirmed, fibre type verified
- [ ] Optical power levels tested — Tx and Rx within acceptable range for each link
- [ ] Copper patch cables connected — verified against LLD port assignment
- [ ] All equipment powered on — no fault indicators on hardware

---

## Configuration

### Base Configuration
- [ ] Management IP address assigned per IP address plan
- [ ] Hostname configured per naming convention
- [ ] Out-of-band management access confirmed — SSH accessible from NOC
- [ ] NTP configured and synchronised — time confirmed accurate
- [ ] SNMP configured — device visible in SolarWinds NMS
- [ ] Syslog configured — logs forwarding to central log server
- [ ] User accounts configured — local admin account and NOC read-only account

### Layer 2 Configuration
- [ ] VLANs configured per LLD — VLAN IDs, names, and descriptions verified
- [ ] Trunk ports configured — VLAN membership verified on each trunk
- [ ] Access ports configured — VLAN assignment verified per end office mapping
- [ ] STP configured — root bridge assignment verified, no topology changes observed
- [ ] Port security configured where required — MAC address limits set

### Layer 3 Configuration
- [ ] IP addressing configured per LLD — no conflicts verified
- [ ] OSPF configured — area assignment, network statements, passive interfaces
- [ ] OSPF adjacency established with upstream PoP — neighbour state confirmed Full
- [ ] Routing table verified — all expected prefixes present, no unexpected routes
- [ ] BGP configured where applicable — peer sessions established, prefixes verified
- [ ] Static routes configured where required — verified reachable

### Security Configuration
- [ ] ACLs configured per security policy — inbound and outbound rules verified
- [ ] Management plane protection — SSH only, Telnet disabled, console timeout set
- [ ] SNMP community strings set — default strings removed
- [ ] Unused interfaces shut down — no active ports without documented purpose
- [ ] Fortinet firewall configured where applicable — policies verified against LLD

> *Configuration accuracy at commissioning stage is critical. In the KFON Palakkad
> deployment, configuration errors discovered post-commissioning required field team
> revisits that added significant time to the overall deployment schedule. Peer review
> of LLD against running configuration before sign-off caught the majority of errors.*

---

## Integration Testing

After individual PoP configuration is complete, integration into the wider network
must be verified before the PoP is handed over for operational use.

### Connectivity Testing
- [ ] End-to-end connectivity verified from this PoP to Core PoP
- [ ] End-to-end connectivity verified to all end offices served by this PoP
- [ ] OSPF adjacency stable — observed for minimum 30 minutes with no flapping
- [ ] Traffic path verified — traceroute confirms expected routing through the ring
- [ ] Redundancy tested — primary link failed, traffic confirmed switching to secondary
- [ ] Recovery time verified — traffic restored within acceptable period after failover

### End Office Connectivity
- [ ] Each end office connected to this PoP tested individually
- [ ] VLAN assignment verified per end office — correct VLAN reachable from each port
- [ ] End office device management access confirmed — reachable from NOC
- [ ] End office connectivity confirmed operational — services verified end-to-end

### Monitoring Verification
- [ ] PoP visible in SolarWinds — all interfaces monitored
- [ ] Interface utilisation baselines recorded — normal traffic levels documented
- [ ] Alerts configured and tested — interface down alert confirmed triggering
- [ ] OSPF adjacency monitoring confirmed — alert on neighbour state change verified
- [ ] ArcGIS record updated — PoP location, equipment, and connected end offices recorded

---

## Documentation

- [ ] As-built configuration exported and stored — dated, labelled with PoP name
- [ ] Any deviations from LLD documented — what changed, why, and downstream impact
- [ ] Rack elevation diagram updated — reflects actual installed equipment
- [ ] Cable schedule updated — all physical connections documented
- [ ] IP address plan updated — all assigned addresses recorded
- [ ] End office mapping confirmed accurate — each end office correctly assigned to PoP

---

## Sign-Off

- [ ] Technical sign-off completed — commissioning engineer confirms all tests passed
- [ ] Government stakeholder notified — relevant authority informed PoP is live
- [ ] NOC handover completed — NOC team briefed on PoP, added to monitoring coverage
- [ ] Commissioning report filed — completed checklist retained as project record

---

## Lessons Learned from KFON PoP Commissioning

**Site readiness must be confirmed before equipment is dispatched.**
Arriving at a site with equipment and finding it is not ready creates immediate
pressure to proceed anyway. Resist this. A structured site survey with a readiness
checklist — power, space, access, environmental — before equipment is ordered
prevents the majority of commissioning delays.

**Peer review of configuration before testing saves field time.**
A second engineer reviewing the running configuration against the LLD before
integration testing begins consistently catches errors that the commissioning
engineer misses. The cost of a review is minutes. The cost of a field revisit
to fix a configuration error is hours.

**Document deviations at the time they happen.**
Every change from the approved LLD must be documented immediately — not after
commissioning is complete. In a deployment with 30+ PoPs, deviations accumulate
quickly and become very difficult to reconstruct after the fact.

**Redundancy testing is not optional.**
Testing that the primary path works is not the same as testing that failover works.
Every PoP commissioning must include a deliberate failover test — primary link
pulled, traffic confirmed switching to secondary, recovery time measured.

---

*This checklist reflects direct operational experience from the KFON Palakkad
district deployment. It is written as an operational document — not as a theoretical
framework — and reflects the actual commissioning sequence followed across 30+
PoPs during the district rollout.*
