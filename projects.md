---
layout: page
title: Projects
permalink: /projects/
show_title: false
wide: true
---

<!--
  Each project is a <tr> with two cells:
    .project-image-cell    → thumbnail (<img> or autoplay <video>)
    .project-content-cell  → .project-title, .skills pills, description <p>, .project-links

  Aim for ~300x225 (4:3) images. Copy a <tr> block to add a project.
-->

<table class="project-table">
  <tbody>
    <tr>
      <td class="project-image-cell">
        <img src="{{ '/images/talus-hillshade.png' | relative_url }}" alt="Hillshade of Foster Falls, TN rendered from a USGS DEM" class="project-image" onerror="this.style.display='none'">
      </td>
      <td class="project-content-cell">
        <p class="project-title"><strong>Talus</strong> — Rockfall hazard scoring for climbing areas</p>
        <div class="skills">
          <span class="skill">Go</span>
          <span class="skill">CUDA</span>
          <span class="skill">PostGIS</span>
          <span class="skill">Docker</span>
        </div>
        <p>
          End-to-end pipeline that turns a raw USGS elevation model into concrete
          rockfall risk scores for a climbing wall. GPU terrain kernels identify
          source zones above a route and combine with freeze-thaw windows to flag
          hazardous days. The Sobel slope/aspect kernel runs 10.6× faster on a
          GTX 1060 than a single-threaded CPU baseline (569&nbsp;ms vs 6,041&nbsp;ms over 116.9M cells).
        </p>
        <div class="project-links">
          [<a href="/projects/talus/">blog post</a>]
          [<a href="https://github.com/{{ site.github_username }}/talus">code</a>]
        </div>
      </td>
    </tr>
    <tr>
      <td class="project-image-cell">
        <img src="{{ '/images/proxmox-thumb.jpg' | relative_url }}" alt="Interior of a Dell PowerEdge R510 running the Proxmox homelab" class="project-image" onerror="this.style.display='none'">
      </td>
      <td class="project-content-cell">
        <p class="project-title"><strong>Proxmox Datacenter</strong> — Terraform-provisioned homelab on a Dell R510</p>
        <div class="skills">
          <span class="skill">Proxmox VE</span>
          <span class="skill">Terraform</span>
          <span class="skill">Cloud-Init</span>
          <span class="skill">k3s</span>
          <span class="skill">Tailscale</span>
        </div>
        <p>
          A decommissioned Dell PowerEdge R510 turned into a personal datacenter where 
          every VM is declared in Terraform and configures itself on first boot via 
          Cloud-Init. This hosts 5 nodes of my k3s cluster, with an always-on Raspberry 
          Pi 4 handling Tailscale subnet routing so the machine stays reachable even 
          when it is down. Roughly ten VMs share 16 Xeon threads and 64 GB ECC. 
        </p>
        <div class="project-links">
          [<a href="/projects/proxmox-datacenter/">blog post</a>]
          [<a href="https://github.com/{{ site.github_username }}/proxmox-data-center">code</a>]
        </div>
      </td>
    </tr>
    <tr>
      <td class="project-image-cell">
        <img src="{{ '/images/cegar-abstraction.png' | relative_url }}" alt="True-positive / false-negative / true-negative map over the (X1, X2) state space for the axis-aligned bounding-box abstraction" class="project-image" onerror="this.style.display='none'">
      </td>
      <td class="project-content-cell">
        <p class="project-title"><strong>CEGAR Abstraction</strong> — Conservative discrete abstractions for cyber-physical system verification</p>
        <div class="skills">
          <span class="skill">Python</span>
          <span class="skill">Formal Verification</span>
          <span class="skill">CTL Model Checking</span>
          <span class="skill">NumPy</span>
          <span class="skill">PyTorch</span>
        </div>
        <p>
          A worklist-based CEGAR (counterexample-guided abstraction refinement) tool
          that turns a continuous state space into a finite abstraction for formal
          verification. It partitions the space into cells (axis-aligned boxes or
          polytopes), builds conservative transitions between them, checks a CTL-style
          specification, and repeatedly refines cells left "unknown" until the
          classification converges. Three case studies exercise the pipeline: a 2D
          synthetic system, the 2D mountain-car problem, and a 3D unicycle model.
          Companion code for the arXiv paper, written with UF's Trustworthy Engineered
          Autonomy Laboratory.
        </p>
        <div class="project-links">
          [<a href="https://arxiv.org/abs/2608.10254">paper</a>]
          [<a href="https://github.com/{{ site.github_username }}/cegar-abstraction-tutorial">code</a>]
        </div>
      </td>
    </tr>
    <tr>
      <td class="project-image-cell">
        <img src="{{ '/images/omen-thumb.png' | relative_url }}" alt="Nextcloud and Immich running on the Omen Ubuntu server" class="project-image" onerror="this.style.display='none'">
      </td>
      <td class="project-content-cell">
        <p class="project-title"><strong>Ubuntu Server</strong> — Self-hosted cloud platform replacing paid subscriptions</p>
        <div class="skills">
          <span class="skill">Ubuntu Server</span>
          <span class="skill">Docker Compose</span>
          <span class="skill">LVM</span>
          <span class="skill">UFW</span>
          <span class="skill">Tailscale</span>
          <span class="skill">k3s</span>
          <span class="skill">Datadog</span>
          <span class="skill">Helm</span>
        </div>
        <p>
          An Ubuntu server running Immich, Nextcloud and a Minecraft server in Docker
          Compose across ~1.5&nbsp;TB of LVM-backed storage, cutting ~$150/yr in cloud
          subscriptions. Hardened with SSH key-only auth, a default-deny UFW firewall
          and a Tailscale WireGuard mesh, so nothing is exposed to the public internet.
          It was also the first node of what is now a 7 node k3s cluster and still runs
          the control plane, with a Datadog agent stack deployed via Helm for
          cluster-wide log collection and fault alerting.
        </p>
        <div class="project-links">
          [<a href="/projects/ubuntu-server/">blog post</a>]
        </div>
      </td>
    </tr>
  </tbody>
</table>
