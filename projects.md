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
          Cloud-Init. This hosts a 5 node k3s cluster, with an always-on Raspberry Pi 4 
          handling Tailscale subnet routing so the machine stays reachable even when it is 
          down. Roughly ten VMs share 16 Xeon threads and 64&nbsp;GB ECC.
        </p>
        <div class="project-links">
          [<a href="/projects/proxmox-datacenter/">blog post</a>]
          [<a href="https://github.com/{{ site.github_username }}/proxmox-data-center">code</a>]
        </div>
      </td>
    </tr>
  </tbody>
</table>
