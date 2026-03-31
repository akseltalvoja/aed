---
layout: Post
permalink: /
title: Natuke kõike
---


# External Memory

A digital repository of technical logs, creative experiments, and documented project cycles. This space serves as a centralized archive for research, random notes, modern aesthetics, and system architecture.

<div class="index-nav">
  <a href="/projects" class="nav-block">
    <span class="code-label">DIR_01</span>
    <span class="nav-text">Projects</span>
  </a>
  <a href="/library" class="nav-block">
    <span class="code-label">DIR_02</span>
    <span class="nav-text">Library</span>
  </a>
</div>

### Current Objectives
*   **Archive:** Documenting the evolution of personal and professional projects.
*   **Design:** Exploring the intersection of brutalist geometry and functional code.
*   **Logs:** Maintaining a persistent stream of thought on emerging technologies.

<div class="footer-joke">
  90% of this archive is held together by caffeine, low-level anxiety, and code I copied from someone who also didn’t know how it worked. But at least it looks cool and hacky, right?
</div>

<script>
    function updateClock() {
        const now = new Date();
        const timestamp = now.getFullYear() + '.' + 
            String(now.getMonth() + 1).padStart(2, '0') + '.' + 
            String(now.getDate()).padStart(2, '0') + '_' + 
            String(now.getHours()).padStart(2, '0') + ':' + 
            String(now.getMinutes()).padStart(2, '0') + ':' + 
            String(now.getSeconds()).padStart(2, '0');
        document.getElementById('clock').textContent = timestamp;
    }
    setInterval(updateClock, 1000);
    updateClock(); // Initial call
</script>