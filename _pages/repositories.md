---
layout: page
permalink: /repositories/
title: repositories
description: Software and open hardware I have built, or co-developed with the students I supervise — mostly low-cost instrumentation and appropriate technology for global health engineering.
nav: true
nav_order: 4
---

{% if site.data.repositories.github_users %}

## GitHub

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.repositories.github_users %}
    {% include repository/repo_user.liquid username=user %}
  {% endfor %}
</div>

{% if site.repo_trophies.enabled %}
{% for user in site.data.repositories.github_users %}

  <div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% include repository/repo_trophies.liquid username=user %}
  </div>
{% endfor %}
{% endif %}

---

{% endif %}

## Developed

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos_developed %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>

## Supervised &amp; co-developed

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos_supervised %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>
