---
layout: page
permalink: /impact/
title: Impact
description: Upstream fixes in open-source projects resulting from my research.
nav: true
nav_order: 4
---

{% assign d = site.data.merged_patches %}

<style>
  .impact-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 1rem;
    margin: 1.5rem 0 2rem;
  }
  .impact-stat {
    border: 1px solid var(--global-divider-color);
    border-radius: 0.5rem;
    padding: 1rem;
    text-align: center;
  }
  .impact-stat .num {
    font-size: 2rem;
    font-weight: 600;
    color: var(--global-theme-color);
    line-height: 1.1;
  }
  .impact-stat .label {
    font-size: 0.85rem;
    color: var(--global-text-color-light);
    margin-top: 0.25rem;
  }
  .impact-table td.bugtype .bug-type + .bug-type {
    margin-top: 0.25rem;
  }
  .impact-table td.bugtype .bug-type {
    white-space: nowrap;
  }
  .impact-table td.bugtype .bug-cwe {
    font-family: var(--font-family-monospace, monospace);
    font-size: 0.75rem;
  }
  .impact-table .badge-sec {
    font-size: 0.7rem;
    vertical-align: middle;
    background: var(--global-theme-color);
    color: #fff;
    border-radius: 0.25rem;
    padding: 0.1rem 0.35rem;
    margin-left: 0.3rem;
  }
  .impact-filters {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem 1.5rem;
    align-items: flex-end;
    margin-bottom: 1rem;
    font-size: 0.9rem;
  }
  .impact-filters label {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    margin: 0;
  }
  .impact-filters label.impact-check {
    flex-direction: row;
    align-items: center;
    gap: 0.4rem;
    padding-bottom: 0.4rem;
  }
  .impact-filters select {
    max-width: 18rem;
    padding: 0.3rem 0.5rem;
    border: 1px solid var(--global-divider-color);
    border-radius: 0.25rem;
    background: var(--global-bg-color);
    color: var(--global-text-color);
  }
  .impact-filters #impact-count {
    padding-bottom: 0.4rem;
  }
</style>

In [our ISSTA 2025 study](https://doi.org/10.1145/3728923), we applied CodeQL to 258 open-source embedded software projects and responsibly disclosed the defects it found. Maintainers confirmed {{ d.summary.defects_confirmed }} of the {{ d.summary.defects_discovered }} defects. Where possible, I submitted patches upstream; in other cases the maintainers fixed the bugs I reported themselves. This page lists only defects that were actually **fixed**: pull requests that were merged, and reported bugs that maintainers fixed.

<div class="impact-stats">
  <div class="impact-stat"><div class="num">{{ d.summary.patches_merged }}</div><div class="label">patches merged</div></div>
  <div class="impact-stat"><div class="num">{{ d.summary.issues_fixed }}</div><div class="label">reported bugs fixed by maintainers</div></div>
  <div class="impact-stat"><div class="num">{{ d.summary.repos }}</div><div class="label">open-source projects</div></div>
  <div class="impact-stat"><div class="num">{{ d.summary.defects_fixed }}</div><div class="label">defects fixed</div></div>
  <div class="impact-stat"><div class="num">{{ d.summary.security_defects_fixed }}</div><div class="label">security-relevant defects fixed</div></div>
</div>

## Upstream fixes

One row per merged pull request or fixed bug report, grouped by project and ordered by number of fixes per project. The bug type is the [CWE](https://cwe.mitre.org/) category of the defects, with descendants of CWE-119 grouped as buffer overflow; code-quality defects without a CWE are described in words. Bug types marked "security" are those we classified as security-relevant in the study.

<div class="impact-filters">
  <label>
    Project
    <select id="impact-filter-project">
      <option value="">All projects</option>
      {% for repo in d.repos %}
        <option value="{{ repo.name }}">{{ repo.name }} ({{ repo.fixes | size }})</option>
      {% endfor %}
    </select>
  </label>
  <label>
    My contribution
    <select id="impact-filter-kind">
      <option value="">All</option>
      <option value="patch">Patch, merged</option>
      <option value="issue">Bug report, fixed by maintainers</option>
    </select>
  </label>
  <label>
    Bug type
    <select id="impact-filter-rule">
      <option value="">All bug types</option>
      {% assign all_rules = "" | split: "" %}
      {% for repo in d.repos %}
        {% for p in repo.fixes %}
          {% assign all_rules = all_rules | concat: p.types %}
        {% endfor %}
      {% endfor %}
      {% assign all_rules = all_rules | uniq %}
      {% assign labels = "" | split: "" %}
      {% for r in all_rules %}
        {% if r contains "CWE-" %}
          {% assign cwe = site.data.codeql_rules.cwes[r] %}
          {% assign label = cwe.short | append: " (" | append: r | append: ")" %}
        {% else %}
          {% assign meta = site.data.codeql_rules.rules[r] %}
          {% if meta.primary %}
            {% assign label = meta.short | append: " (" | append: meta.primary | append: ")" %}
          {% else %}
            {% assign label = meta.name | default: r %}
          {% endif %}
        {% endif %}
        {% assign labels = labels | push: label %}
      {% endfor %}
      {% assign labels = labels | uniq | sort_natural %}
      {% for label in labels %}
        <option value="{{ label }}">{{ label }}</option>
      {% endfor %}
    </select>
  </label>
  <label class="impact-check">
    <input type="checkbox" id="impact-filter-security" />
    Security-relevant only
  </label>
  <span id="impact-count" class="text-muted"></span>
</div>

<div class="table-responsive">
  <table class="table table-sm impact-table" id="impact-table">
    <thead>
      <tr>
        <th scope="col">Project</th>
        <th scope="col">Bug type</th>
        <th scope="col" class="text-end">Defects</th>
        <th scope="col">My contribution</th>
        <th scope="col">Link</th>
      </tr>
    </thead>
    <tbody>
      {% for repo in d.repos %}
        {% for p in repo.fixes %}
          {% assign row_labels = "" | split: "" %}
          {% for r in p.types %}
            {% if r contains "CWE-" %}
              {% assign cwe = site.data.codeql_rules.cwes[r] %}
              {% assign label = cwe.short | append: " (" | append: r | append: ")" %}
            {% else %}
              {% assign meta = site.data.codeql_rules.rules[r] %}
              {% if meta.primary %}
                {% assign label = meta.short | append: " (" | append: meta.primary | append: ")" %}
              {% else %}
                {% assign label = meta.name | default: r %}
              {% endif %}
            {% endif %}
            {% assign row_labels = row_labels | push: label %}
          {% endfor %}
          {% assign row_labels = row_labels | uniq %}
          <tr data-project="{{ repo.name }}" data-types="{{ row_labels | join: '|' }}" data-security="{{ p.security }}" data-kind="{{ p.kind }}">
            <td><a href="{{ repo.url }}">{{ repo.name }}</a></td>
            <td class="bugtype">
              {% for label in row_labels %}
                {% assign parts = label | split: " (CWE-" %}
                <div class="bug-type">
                  {% if parts.size > 1 %}
                    {% assign cwe_num = parts[1] | remove: ")" %}
                    {{ parts[0] }} <a class="bug-cwe" href="https://cwe.mitre.org/data/definitions/{{ cwe_num }}.html">CWE-{{ cwe_num }}</a>
                  {% else %}
                    {{ label }}
                  {% endif %}
                  {% if p.security and forloop.first %}<span class="badge-sec">security</span>{% endif %}
                </div>
              {% endfor %}
            </td>
            <td class="text-end">{% if p.defects > 0 %}{{ p.defects }}{% else %}&ndash;{% endif %}</td>
            <td>{% if p.kind == "patch" %}Patch, merged{% else %}Bug report, fixed by maintainers{% endif %}</td>
            <td><a href="{{ p.url }}">{{ p.url | replace: 'https://github.com/', '' | replace: 'https://', '' | replace: repo.name, '' | remove_first: '/' }}</a></td>
          </tr>
        {% endfor %}
      {% endfor %}
    </tbody>
  </table>
</div>

<script>
  (function () {
    var project = document.getElementById("impact-filter-project");
    var rule = document.getElementById("impact-filter-rule");
    var kind = document.getElementById("impact-filter-kind");
    var security = document.getElementById("impact-filter-security");
    var count = document.getElementById("impact-count");
    var rows = Array.prototype.slice.call(document.querySelectorAll("#impact-table tbody tr"));

    function apply() {
      var shown = 0;
      rows.forEach(function (row) {
        var ok =
          (!project.value || row.dataset.project === project.value) &&
          (!kind.value || row.dataset.kind === kind.value) &&
          (!rule.value || row.dataset.types.split("|").indexOf(rule.value) !== -1) &&
          (!security.checked || row.dataset.security === "true");
        row.hidden = !ok;
        if (ok) shown++;
      });
      count.textContent = "Showing " + shown + " of " + rows.length + " fixes";
    }

    [project, kind, rule, security].forEach(function (el) {
      el.addEventListener("change", apply);
    });
    apply();
  })();
</script>
