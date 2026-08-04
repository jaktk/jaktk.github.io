---
layout: page
title: "Development of a Pay-As-You-Go Battery-Charging System for Electric Mobility in Nairobi, Kenya"
description: "MSc thesis · Patrick Fässler · 2026"
img: assets/img/projects/patrick-faessler-bike-charging.png
importance: 74
category: "Air Quality"
student: "Patrick Fässler"
degree: "MSc"
year: 2026
role: "Supervisor"
eth_collection:
repo:
tags: ["prototyping / open hardware", "field deployment", "sensing & instrumentation", "air quality"]
related_publications: false
---

Electric mobility adoption in Nairobi is constrained by high upfront costs and limited charging infrastructure. This thesis develops a pay-as-you-go (PAYG) battery-charging system for electric two-wheelers, in collaboration with the mobility company eWAKA. The system links a frontend interface and a Python-based backend to mobile payments processed through the Daraja (M-Pesa) API, so charging sessions start on confirmed payment and stop automatically once purchased energy is consumed. Two charging-control approaches were prototyped and field-tested: a hardware-based charger for e-bikes, and an API-based method using existing smart-battery communication for e-motorbikes. Both proved technically feasible; the API-based approach was found more scalable and cost-effective but dependent on battery-manufacturer API reliability, while the hardware approach offers greater independence but requires further development for large-scale deployment.

_MSc thesis · 2026 · Jakub Tkaczuk, supervisor_

<div style="margin-top:1.4rem;display:flex;flex-wrap:wrap;gap:.4rem">
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>prototyping / open hardware</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>field deployment</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>sensing & instrumentation</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#64748b;display:inline-block;flex:0 0 auto"></span>air quality</span>
</div>

{% if page.eth_collection %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.eth_collection }}" target="_blank">Thesis · ETH Research Collection</a>{% endif %}
{% if page.repo %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.repo }}" target="_blank">Code · GitHub</a>{% endif %}
