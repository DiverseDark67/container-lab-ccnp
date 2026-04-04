# SPINE_LEAF LAB

## Topology
A data center spine-and-leaf fabric using Cisco Nexus 9300v nodes.

**Topology:**
- 2 Spine switches (`spine1`, `spine2`)
- 4 Leaf switches (`leaf1`–`leaf4`) - paired into two MLAG domains
  - MLAG Domain A: `leaf1` <-> `leaf2`
  - MLAG Domain B: `leaf3` <-> `leaf4`
- Each leaf has uplinks to both spines
- Spine-to-spine interconnect on `eth5`

**Concepts covered:** Spine-leaf architecture, MLAG (vPC), Layer 2/3 fabric

## Initial Deployment
From within any lab directory, deploy the topology with:

```bash
sudo clab deploy -t topology.clab.yml
```

SSH to the containers (admin|admin)
```bash
ssh admin@<mgmt-ip>
```

To destroy the lab:

```bash
sudo clab destroy -t topology.clab.yml
```

## Objectives

## Verification