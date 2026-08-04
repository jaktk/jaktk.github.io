---
layout: page
permalink: /publications/
title: publications
description: Publications in reverse-chronological order; my name is emphasised, and each entry is tagged by topic and method.
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography %}

</div>

<script>
  (function () {
    var T = {"schweizer2026wastebin": [["anthropogenic waste", "#ea580c"], ["optimization", "#9ca3af"], ["mathematical modelling", "#9ca3af"]], "madikeri2025autocrime": [["machine learning", "#9ca3af"], ["sensing & instrumentation", "#9ca3af"]], "abgottspon2025willingness": [["anthropogenic waste", "#ea580c"], ["field deployment", "#9ca3af"]], "tilley2024capemaclear": [["anthropogenic waste", "#ea580c"], ["field deployment", "#9ca3af"]], "tkaczuk2021thesis": [["cryogenics", "#3b82f6"], ["thermodynamics", "#6366f1"], ["equations of state", "#9ca3af"]], "tkaczuk2020eos": [["cryogenics", "#3b82f6"], ["thermodynamics", "#6366f1"], ["equations of state", "#9ca3af"], ["optimization", "#9ca3af"]], "fccphysics2019": [["particle physics", "#9ca3af"]], "fccee2019": [["cryogenics", "#3b82f6"], ["particle physics", "#9ca3af"]], "fcchh2019": [["cryogenics", "#3b82f6"], ["particle physics", "#9ca3af"]], "helhc2019": [["cryogenics", "#3b82f6"], ["particle physics", "#9ca3af"]], "tkaczuk2017magnetic": [["cryogenics", "#3b82f6"], ["thermodynamics", "#6366f1"], ["mathematical modelling", "#9ca3af"]]};
    function pill(label, color) {
      var s = document.createElement('span');
      s.style.cssText = 'display:inline-flex;align-items:center;gap:.3rem;font-size:.7rem;padding:.24rem .5rem;border-radius:999px;background:rgba(127,127,127,.12);border:1px solid rgba(127,127,127,.26);margin:.15rem .35rem .15rem 0';
      var d = document.createElement('span');
      d.style.cssText = 'width:.45rem;height:.45rem;border-radius:50%;display:inline-block;flex:0 0 auto;background:' + color;
      s.appendChild(d);
      s.appendChild(document.createTextNode(label));
      return s;
    }
    function run() {
      Object.keys(T).forEach(function (k) {
        var el = document.getElementById(k);
        if (!el || el.querySelector('.pub-tag-row')) return;
        var row = document.createElement('div');
        row.className = 'pub-tag-row';
        row.style.cssText = 'display:flex;flex-wrap:wrap;align-items:center;margin-top:.5rem';
        T[k].forEach(function (t) { row.appendChild(pill(t[0], t[1])); });
        el.appendChild(row);
      });
    }
    if (document.readyState !== 'loading') run();
    else document.addEventListener('DOMContentLoaded', run);
  })();
</script>
