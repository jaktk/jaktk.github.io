---
layout: page
title: "Design and Development of a Low-Cost Hydrogen Sulfide Sensor System for Biogas Monitoring"
description: "BSc thesis · Flurin Vital · 2026"
img: assets/img/projects/h2s-sensor-flurin-vital.png
importance: 74
category: "Biogas"
student: "Flurin Vital"
degree: "BSc"
year: 2026
role: "Co-supervisor"
eth_collection:
repo:
tags: ["biogas", "sensing & instrumentation", "prototyping / open hardware"]
related_publications: false
---

Biogas systems in low-resource settings often lack affordable tools for monitoring hydrogen sulfide (H2S), a toxic, corrosive gas produced during anaerobic digestion, since commercial instruments are costly and poorly suited to the required range. This thesis presents the design and development of a low-cost H2S sensor system for biogas monitoring, built around a three-electrode electrochemical sensor covering 0-2000 ppm. A custom PCB handles signal conditioning, analog-to-digital conversion, timekeeping, and battery power with USB-C charging; a diaphragm pump draws sampled gas through a 3D-printed flow chamber, with readings shown on an onboard display and firmware written in C++. All major subsystems integrated successfully, baseline noise over one hour stayed within 3.65 ppm, and the CHF 193.80 component cost was about 95% lower than a commercial reference instrument.

<div style="margin-top:1.4rem;display:flex;flex-wrap:wrap;gap:.4rem">
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#16a34a;display:inline-block;flex:0 0 auto"></span>biogas</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>sensing & instrumentation</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>prototyping / open hardware</span>
</div>

{% if page.eth_collection %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.eth_collection }}" target="_blank">Thesis · ETH Research Collection</a>{% endif %}
{% if page.repo %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.repo }}" target="_blank">Code · GitHub</a>{% endif %}
