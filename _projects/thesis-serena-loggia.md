---
layout: page
title: "Testing, Calibration, and Three-Wavelength Adaptation of bcMeter, an Open-Source, Low-Cost Black Carbon Monitor"
description: "MSc thesis · Serena Gioia Loggia · 2025"
img: assets/img/projects/black-carbon-serena-loggia.png
importance: 75
category: "Air Quality"
student: "Serena Gioia Loggia"
degree: "MSc"
year: 2025
role: "Co-supervisor"
eth_collection:
repo:
tags: ["air quality", "sensing & instrumentation", "prototyping / open hardware", "mathematical modelling"]
related_publications: false
---

This thesis evaluates the bcMeter, an open-source, low-cost aethalometer for black carbon (BC), a major short-lived climate forcer and air pollutant that remains poorly monitored in resource-limited regions due to costly reference instruments. Three bcMeter units were co-located with an AE33 reference aethalometer across six tests at two Swiss sites, examining performance and the effects of filter loading, tubing material, and temperature fluctuations, with data calibrated via moving-average smoothing and multiple linear regression. The bcMeter reliably captured temporal BC trends, with regression fit improving from R² 0.59-0.74 to 0.74-0.85 after calibration; filter loading and temperature instability were the main error sources. A three-wavelength prototype for source apportionment failed to yield stable readings, so improvements were applied to the single-wavelength design, which showed strong potential as a low-cost monitor for low-income settings.

<div style="margin-top:1.4rem;display:flex;flex-wrap:wrap;gap:.4rem">
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#64748b;display:inline-block;flex:0 0 auto"></span>air quality</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>sensing & instrumentation</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>prototyping / open hardware</span>
  <span style="display:inline-flex;align-items:center;gap:.3rem;font-size:.75rem;line-height:1;padding:.3rem .6rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.28)"><span style="width:.5rem;height:.5rem;border-radius:50%;background:#9ca3af;display:inline-block;flex:0 0 auto"></span>mathematical modelling</span>
</div>

{% if page.eth_collection %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.eth_collection }}" target="_blank">Thesis · ETH Research Collection</a>{% endif %}
{% if page.repo %}<a class="btn btn-sm z-depth-0" role="button" href="{{ page.repo }}" target="_blank">Code · GitHub</a>{% endif %}
