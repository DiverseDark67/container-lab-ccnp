# Container Lab CCNP

A collection of CCNP-level network labs using [Containerlab](https://containerlab.dev/) and virtualized Cisco images via [vrnetlab](https://github.com/hellt/vrnetlab).

## Prerequisites

Labs require the following licensed Cisco images:
- **Nexus 9300v** — used for data center/spine-leaf labs
- **CSR 1000v** — used for routing labs (BGP, FHRP)

## Server Setup

### Recommended Instance
| Setting | Value |
|---|---|
| Image | Debian 13 |
| Instance Type | c8a.4xlarge |
| Storage | 150 GB gp3 |

### Base Packages

Run the startup script to install Docker, Containerlab, QEMU, and vrnetlab:

```bash
bash start-script.sh
```

Or add it to your cloud instance's user data / startup scripts for automated provisioning.

### Initializing Container Images

Copy your Cisco images to the appropriate vrnetlab build directory, then build the Docker image.

**Example — Nexus 9300v:**

```bash
sudo mv /path/to/nexus9300v64.10.5.5.M.qcow2 /opt/vrnetlab/cisco/n9kv/n9kv-10.5.5.qcow2
cd /opt/vrnetlab/cisco/n9kv/
sudo make docker-image
```

Verify the image was built:

```bash
docker images | grep n9kv
```

The expected image tag is `vrnetlab/cisco_n9kv:10.5.5`. You may need to adjust version tags in topology files to match your image.

## Running a Lab

From within any lab directory, deploy the topology with:

```bash
sudo clab deploy -t topology.clab.yml
```

To destroy the lab:

```bash
sudo clab destroy -t topology.clab.yml
```

## Labs

Labs can be found in there respective folder locations :)
