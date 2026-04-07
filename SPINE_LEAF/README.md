# SPINE_LEAF LAB

## Topology
A data center spine-and-leaf fabric using Cisco Nexus 9300v nodes.

**Topology:**
- 2 Spine switches (`spine1`, `spine2`)
- 4 Leaf switches (`leaf1`–`leaf4`) - paired into two MLAG domains
  - vPC Domain A: `leaf1` <-> `leaf2`
  - vPC Domain B: `leaf3` <-> `leaf4`
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
### IP Addressing Table

| Node   | mgt          | eth1/1 (->)    | eth1/2 (->)    | eth1/3 (->)    | eth1/4 (->)    | eth1/5 (->)     | eth1/6 (->)     |
| ------ | ------------ | ------------- | ------------- | ------------- | ------------- | -------------- | -------------- |
| spine1 | 172.20.20.2  | 10.1.1.1/30 (->leaf1) | 10.1.2.1/30 (->leaf2) | 10.1.3.1/30 (->leaf3) | 10.1.4.1/30 (->leaf4) | 10.0.0.1/30 (->spine2) | —      |
| spine2 | 172.20.20.3  | 10.2.1.1/30 (->leaf1) | 10.2.2.1/30 (->leaf2) | 10.2.3.1/30 (->leaf3) | 10.2.4.1/30 (->leaf4) | 10.0.0.2/30 (->spine1) | —      |
| leaf1  | 172.20.20.4  | 10.1.1.2/30 (->spine1) | 10.2.1.2/30 (->spine2) | —           | —             | L2 vPC PL (->leaf2) | L2 vPC PL (->leaf2) |
| leaf2  | 172.20.20.5  | 10.1.2.2/30 (->spine1) | 10.2.2.2/30 (->spine2) | —           | —             | L2 vPC PL (->leaf1) | L2 vPC PL (->leaf1) |
| leaf3  | 172.20.20.6  | 10.1.3.2/30 (->spine1) | 10.2.3.2/30 (->spine2) | —           | —             | L2 vPC PL (->leaf4) | L2 vPC PL (->leaf4) |
| leaf4  | 172.20.20.7  | 10.1.4.2/30 (->spine1) | 10.2.4.2/30 (->spine2) | —           | —             | L2 vPC PL (->leaf3) | L2 vPC PL (->leaf3) |

> **Subnet summary:**
> - Spine-to-spine: `10.0.0.0/30`
> - Spine1 -> Leaf*n*: `10.1.*n*.0/30` (spine1 = .1, leaf = .2)
> - Spine2 -> Leaf*n*: `10.2.*n*.0/30` (spine2 = .1, leaf = .2)
> - eth1/5 & eth1/6 on leaf pairs are L2 trunk port-channel members (vPC peer-link); no routed IP on individual ports.

### vPC Configuration Between Leaf Nodes
Configure vPC connections between node Leaf 1 <-> Leaf 2 and Leaf 3 <-> Leaf 4

[Cisco documenation](https://www.cisco.com/c/en/us/support/docs/switches/nexus-9000-series-switches/218333-understand-and-configure-nexus-9000-vpc.html "Cisco Nexus vPC Configuration") for vPC on Nexus switches is linked

### EIGRP or OSPF
[OSPF](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/6-x/unicast/configuration/guide/l3_cli_nxos/l3_ospf.html "OSPF") Configuration

[EIGRP](https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus9000/sw/6-x/unicast/configuration/guide/l3_cli_nxos/l3_eigrp.html "EIGRP") Configuration

**Note: For an additional change setup OSPFv3 in a dual stack Spine Leaf setup

## Verification
