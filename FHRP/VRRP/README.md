# VRRP LAB

## Topology
A data center spine-and-leaf fabric using Cisco Nexus 9300v nodes.

**Topology:**
- 2 routers (`router1`, `router2`)
- 1 switch interconnecting the two routers and the linux pc
- 1 pc used to test and verify connectivity

**Concepts covered:** VRRP

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