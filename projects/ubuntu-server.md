---
layout: post
title: "Ubuntu Server"
subtitle: "A Self-Hosted Cloud Platform on Ubuntu"
date: 2025-05-15
permalink: /projects/ubuntu-server/
---

![Nextcloud and Immich open side by side, both served from the Ubuntu server]({{ '/images/omen-services.png' | relative_url }})

*Fig. 1 The two services that replace the subscriptions: Nextcloud (left) for files, Immich (right) for photos.*

---

<!-- ── LEAD ──────────────────────────────────────────────── -->

This is a single Ubuntu Server box called `omen-server`. This runs the paid cloud services I
used to rent. Immich replaces Google Photos, Nextcloud replaces Drive and Dropbox, and
a Minecraft server replaces a rented game host. All three run as Docker Compose stacks
on roughly 1.5&nbsp;TB of LVM-backed storage, and moving to self-hosted solutions has 
saved me about $150 a year.

This machine was also the first node of what is now a seven-node k3s cluster, and
it still runs the control plane. The [Proxmox Datacenter](/projects/proxmox-datacenter/)
VMs joined it later as workers. A Datadog agent stack, installed with Helm, collects
logs from every node and raises alerts when a node or pod goes unhealthy.

**What it replaced**

| Subscription                    | Replaced by            | Annual cost |
| ------------------------------- | ---------------------- | ----------- |
| [Google Photos](https://one.google.com/about/plans?g1_landing_page=60)    | Immich                 | $92.99      |
| [Google Drive](https://one.google.com/about/plans?g1_landing_page=60)       | Nextcloud              | $18.99         |
| [Minecraft Server Hosting](https://www.minecraft.net/en-us/realms)         | Minecraft container    | $95.88         |
| **Total**                       |                        | **~$150**   |

*Tab. 1 Final cost is calculated after subtracting ~$50 for electricity costs.*

---

<!-- ── SECTION 1 ──────────────────────────────────────────── -->

### Design Decisions

#### LVM for storage

The disks are pooled with LVM rather than partitioned directly. A logical volume spans
physical drives and resizes without repartitioning, so Immich's library volume can grow
as the photo count does instead of being sized once up front. This makes adding a disk 
simpler as you just need to extend the volume group instead of migrating data.

#### Docker Compose, not k3s, for the apps

Immich, Nextcloud and Minecraft each live in their own directory as a
`docker-compose.yml`. They are single-host services with no need for scheduling or
rolling updates, and Compose keeps backup easy.

#### Layered access with no public ports

Nothing is forwarded at the router. Remote access is three layers: SSH accepts keys
only, UFW denies inbound by default, and Tailscale puts the machine on a WireGuard mesh.
Every service is reachable only from inside the tailnet, so the exposed surface from the
public internet is a closed set of ports.

---

<!-- ── SECTION 2 ──────────────────────────────────────────── -->

### Implementation

![docker compose ls, ufw status, and the docker service status on omen-server]({{ '/images/omen-hardening.png' | relative_url }})

*Fig. 2 Left: `docker.service` up. Right: `docker compose ls` (Immich and Nextcloud shown) and `ufw status` active.*

#### The Compose layout

Each app is a directory with its `docker-compose.yml` and a bind mount onto the LVM
volume for its data:

```
/srv/
├── immich/       docker-compose.yml  →  /mnt/data/immich
├── nextcloud/    docker-compose.yml  →  /mnt/data/nextcloud
└── minecraft/    docker-compose.yml  →  /mnt/data/minecraft
```

#### k3s control plane on Omen

```
Internet
    │  (no port forwarding — access via Tailscale)
    ▼
Tailscale mesh (WireGuard)
    ▼
omen-server ── UFW ── static LAN IP
    ├── Docker Compose:  Immich · Nextcloud · Minecraft
    └── k3s control plane
          ├── Raspberry Pi 4        ARM worker
          └── 5× Proxmox R510 VMs   x86 workers
```

#### Observability with Datadog

As the cluster grew past one node, an observability stack (Datadog agents) was implemented.
The agent runs as a DaemonSet, so every node ships logs and metrics, and monitors 
when a node stops reporting or a pod crash-loops. This makes failures show up as an alert instead
of as a service that quietly went down.

---

<!-- ── SECTION 3 ──────────────────────────────────────────── -->

### Results

![kubectl get nodes showing seven nodes Ready]({{ '/images/omen-kubectl-nodes.png' | relative_url }})

*Fig. 3 `kubectl get nodes`, the control plane on `omen-server`, the Raspberry Pi, and five R510 VMs, all `Ready`.*

---

<!-- ── FUTURE WORK ────────────────────────────────────────── -->

### What's Next?

- Move Immich and Nextcloud from Compose onto k3s for automatic updates.
- GitOps for the Datadog values and the workload manifests.
