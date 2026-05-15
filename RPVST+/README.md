# RPVST+ LAB

![RPVST+ Topology Diagram](diagram/topology.png)

## Topology
A Layer 2 Rapid Per-VLAN Spanning Tree Plus (RPVST+) lab using Cisco Nexus 9300v nodes.

**Topology:**
- 4 Switches (`switch1`, `switch2`, `switch3`, `switch4`)
- 2 Linux computers (`computer1`, `computer2`) used to test and verify end-to-end connectivity
- Redundant links between switches to create Layer 2 loops and trigger Spanning Tree reconvergence

**Concepts covered:** RPVST+, Root Bridge election, Port Roles (Root, Designated, Alternate), Port States, Spanning Tree priority, and Path Cost manipulation.

## Initial Deployment
From within the lab directory, deploy the topology with:

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
### Configuration & Verification Tasks
1. **Enable RPVST+**: Ensure Rapid PVST+ is enabled globally on all switches.
2. **Root Bridge Election**: 
   - Configure `switch1` as the primary Root Bridge for VLAN 10.
   - Configure `switch2` as the secondary Root Bridge for VLAN 10.
3. **Verify Port Roles**: Inspect the topology to identify which switch ports are blocking (Alternate) and which are forwarding (Root/Designated).
4. **Path Cost Manipulation**: Adjust the spanning-tree port cost on `switch4` to change its Root Port election and force traffic over a specific path.
5. **End-to-End Connectivity**: Verify that the Alpine hosts can successfully ping each other once the STP topology has converged.