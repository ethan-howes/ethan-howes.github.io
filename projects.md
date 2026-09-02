---
layout: page
title: Projects
permalink: /projects/
show_title: true
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
        <img src="{{ '/images/project1.png' | relative_url }}" alt="Project Name demo" class="project-image" onerror="this.style.display='none'">
      </td>
      <td class="project-content-cell">
        <p class="project-title"><strong>Project Name</strong> — Short Tagline</p>
        <div class="skills">
          <span class="skill">Python</span>
          <span class="skill">PyTorch</span>
          <span class="skill">CUDA</span>
          <span class="skill">Edge AI</span>
        </div>
        <p>
          One or two punchy sentences — what it does, the headline result
          (FPS, accuracy, speedup), and what makes it interesting.
        </p>
        <div class="project-links">
          [<a href="/projects/sample-project/">blog post</a>]
          [<a href="https://github.com/{{ site.github_username }}/project1">code</a>]
        </div>
      </td>
    </tr>
    <tr>
      <td class="project-image-cell">
        <img src="{{ '/images/project2.png' | relative_url }}" alt="Second Project demo" class="project-image" onerror="this.style.display='none'">
      </td>
      <td class="project-content-cell">
        <p class="project-title">Second Project — Another Tagline</p>
        <div class="skills">
          <span class="skill">C++</span>
          <span class="skill">SIMD</span>
          <span class="skill">Performance Engineering</span>
        </div>
        <p>
          What problem it solves, key results with numbers. Keep it under
          two sentences.
        </p>
        <div class="project-links">
          [<a href="https://github.com/{{ site.github_username }}/project2">code</a>]
        </div>
      </td>
    </tr>
  </tbody>
</table>
