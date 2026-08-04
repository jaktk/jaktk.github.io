---
layout: page
title: "Waste Logistics and Transport Modelling in Cape Maclear, Malawi"
description: "MSc thesis · Josch Stricker · 2024"
img: assets/img/projects/waste-collection-josch-stricker.png
importance: 76
category: "Anthropogenic Waste"
student: "Josch Stricker"
degree: "MSc"
year: 2024
role: "Co-supervisor"
eth_collection:
repo:
tags: ["anthropogenic waste", "mathematical modelling", "optimization", "field deployment"]
related_publications: false
---

This thesis addresses solid waste collection and transport logistics in Cape Maclear, Malawi, a rapidly growing lakeside community lacking organized waste management. The study quantified waste generators - lodges, businesses, and households - and developed three collection scenarios using four locally available vehicles: pickup truck, hand trolley, motorcycle, and small truck. A 2.5 km² map, built from drone imagery and on-site road surveys, was integrated with OpenStreetMap and QGIS routing to compute distances between collection points, with optimal routes found by solving the Travelling Salesman Problem; cost robustness was tested via Monte Carlo simulation. Results show Cape Maclear has roughly 15,000 residents, over 350 businesses, and 16 lodges. A motorcycle with trailer was most cost-effective for lodge-only collection, while a small truck was preferable when household waste was also included.

<div style="margin-top:1.4rem;display:flex;flex-wrap:wrap;gap:.4rem">
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#ea580c;display:inline-block;flex:0 0 auto"></span>anthropogenic waste</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>mathematical modelling</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>optimization</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>field deployment</span>
</div>

{% if page.eth_collection %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.eth_collection }}" target="_blank">Thesis · ETH Research Collection</a>{% endif %}
{% if page.repo %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.repo }}" target="_blank">Code · GitHub</a>{% endif %}
