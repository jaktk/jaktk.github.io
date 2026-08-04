---
layout: page
title: projects
permalink: /projects/
description: My own engineering work, and a showcase of the student theses I have supervised at ETH Zürich. Every card is tagged by topic and method.
nav: true
nav_order: 3
display_categories: [Cryogenics, Biogas, Water & Sanitation, Anthropogenic Waste, Organic Waste, Air Quality, Energy & Mobility]
---

<style>
  .proj-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(270px, 1fr)); gap: 1.25rem; margin: 0.75rem 0 2.5rem; }
  .proj-card { display: flex; flex-direction: column; border: 1px solid rgba(127, 127, 127, 0.22); border-radius: 0.75rem; overflow: hidden; background: rgba(127, 127, 127, 0.03); transition: transform 0.15s ease, box-shadow 0.15s ease; }
  .proj-card:hover { transform: translateY(-3px); box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1); }
  .proj-link { color: inherit; text-decoration: none; display: flex; flex-direction: column; height: 100%; }
  .proj-link:hover { color: inherit; }
  .proj-thumb { aspect-ratio: 16 / 10; width: 100%; object-fit: cover; background: rgba(127, 127, 127, 0.1); display: block; }
  .proj-noimg { aspect-ratio: 16 / 10; display: flex; align-items: center; justify-content: center; background: linear-gradient(135deg, rgba(59, 130, 246, 0.12), rgba(22, 163, 74, 0.12)); color: rgba(127, 127, 127, 0.8); font-size: 0.85rem; letter-spacing: 0.04em; text-transform: uppercase; }
  .proj-body { padding: 0.85rem 1rem 1rem; display: flex; flex-direction: column; gap: 0.4rem; flex: 1; }
  .proj-title { font-weight: 600; font-size: 1rem; line-height: 1.3; }
  .proj-meta { font-size: 0.8rem; opacity: 0.7; }
  .proj-cat { margin: 1.75rem 0 0.75rem; font-size: 1.5rem; font-weight: 700; scroll-margin-top: 5rem; }
  .tag-row { display: flex; flex-wrap: wrap; gap: 0.35rem; margin-top: auto; padding-top: 0.5rem; }
  .tag-pill { display: inline-flex; align-items: center; gap: 0.3rem; font-size: 0.7rem; line-height: 1; padding: 0.26rem 0.5rem; border-radius: 999px; background: rgba(127, 127, 127, 0.12); border: 1px solid rgba(127, 127, 127, 0.26); }
  .tag-dot { width: 0.48rem; height: 0.48rem; border-radius: 50%; background: #9ca3af; flex: 0 0 auto; }
</style>

{% for cat in page.display_categories %}
{% assign items = site.projects | where: "category", cat | sort: "importance" %}
{% if items.size > 0 %}

<h2 class="proj-cat" id="{{ cat | slugify }}">{{ cat }}</h2>

<div class="proj-grid">
{% for p in items %}
  <div class="proj-card">
    <a class="proj-link" href="{{ p.url | relative_url }}">
      {% if p.img and p.img != "" %}
        <img class="proj-thumb" src="{{ p.img | relative_url }}" alt="{{ p.title | escape }}" loading="lazy" />
      {% else %}
        <div class="proj-noimg">{{ cat }}</div>
      {% endif %}
      <div class="proj-body">
        <div class="proj-title">{{ p.title }}</div>
        {% if p.student %}<div class="proj-meta">{{ p.degree }} · {{ p.student }} · {{ p.year }}</div>{% endif %}
        <div class="tag-row">
        {% for tag in p.tags %}
          {%- case tag -%}
            {%- when "cryogenics" %}{% assign c = "#3b82f6" -%}
            {%- when "thermodynamics" %}{% assign c = "#6366f1" -%}
            {%- when "biogas" %}{% assign c = "#16a34a" -%}
            {%- when "sanitation" %}{% assign c = "#0d9488" -%}
            {%- when "air quality" %}{% assign c = "#64748b" -%}
            {%- when "organic waste" %}{% assign c = "#ca8a04" -%}
            {%- when "anthropogenic waste" %}{% assign c = "#ea580c" -%}
            {%- when "water" %}{% assign c = "#0ea5e9" -%}
            {%- else %}{% assign c = "#9ca3af" -%}
          {%- endcase -%}
          <span class="tag-pill"><span class="tag-dot" style="background: {{ c }}"></span>{{ tag }}</span>
        {% endfor %}
        </div>
      </div>
    </a>
  </div>
{% endfor %}
</div>
{% endif %}
{% endfor %}
