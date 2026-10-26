---
layout: about
title: about
permalink: /
subtitle: Adventuring through life &middot; Radio Frequency Devices and Semiconductors

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular

selected_papers: false # set to true once _bibliography/papers.bib has entries marked selected={true}
social: true # includes social icons at the bottom of the page

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
---

<style>
  .container[role="main"] { position: relative; z-index: 1; }
  html, body { overflow-x: clip; }
  .hero-mountains {
    position: absolute;
    z-index: -1;
    top: -3rem;
    left: 50%;
    width: 100vw;
    height: 620px;
    transform: translateX(-50%);
    background: url("{{ '/assets/img/banner.jpg' | relative_url }}") center 35% / cover no-repeat;
    opacity: 0.5;
    -webkit-mask-image: linear-gradient(to bottom, #000 0%, rgba(0, 0, 0, 0.75) 45%, transparent 100%);
    mask-image: linear-gradient(to bottom, #000 0%, rgba(0, 0, 0, 0.75) 45%, transparent 100%);
    pointer-events: none;
  }
  html[data-theme="dark"] .hero-mountains { opacity: 0.35; }
</style>
<div class="hero-mountains" aria-hidden="true"></div>

This is my personal portfolio where I focus on outlining my current personal projects and detail my life in more detail. I'm an Indian who has spent a major part of his life in Tbilisi, Georgia and spent time working and studying in the United States.

I enjoy building things, and my ultimate goal here is to build multiple discrete RF components from discrete parts at WiFi ISM bands.
