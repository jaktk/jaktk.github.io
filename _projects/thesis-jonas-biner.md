---
layout: page
title: "Design and Construction of a Black Soldier Fly Larvae Counting Machine"
description: "MSc thesis · Jonas Biner · 2025"
img: assets/img/projects/jonas-biner-bsf-counting.png
importance: 75
category: "Organic Waste"
student: "Jonas Biner"
degree: "MSc"
year: 2025
role: "Co-supervisor"
eth_collection:
repo:
tags: ["organic waste", "sensing & instrumentation", "prototyping / open hardware", "optimization"]
related_publications: false
---

This thesis addresses the need for reliable preprocessing and counting of Black Soldier Fly larvae (Hermetia illucens) to support process control in large-scale organic waste treatment facilities, where manual separation and counting are labor-intensive, error-prone, and unsuitable for scaling. A modular Black Soldier Fly Larvae Counting Machine was designed and built, combining sequential sieving, sedimentation, and machine-vision-based counting implemented on a Raspberry Pi 5 with a Pi Camera. Each module was experimentally tested with five-day-old larvae batches of 10-100 g, evaluating separation efficiency, processing time, counting accuracy, and throughput. Sieving reached roughly 25 g/min throughput, sedimentation removed fine frass at 6.7-14.3 g/min, and the vision-based counting module achieved 96.7-100% accuracy at about 30 larvae/min, establishing a low-cost, modular proof of concept for automated larvae processing.

<div style="margin-top:1.4rem;display:flex;flex-wrap:wrap;gap:.4rem">
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#ca8a04;display:inline-block;flex:0 0 auto"></span>organic waste</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>sensing & instrumentation</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>prototyping / open hardware</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>optimization</span>
</div>

{% if page.eth_collection %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.eth_collection }}" target="_blank">Thesis · ETH Research Collection</a>{% endif %}
{% if page.repo %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.repo }}" target="_blank">Code · GitHub</a>{% endif %}
