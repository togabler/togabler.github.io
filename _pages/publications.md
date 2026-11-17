---
layout: archive
title: "Veröffentlichungen"
permalink: /publications/
---

{% assign publications = site.publications | sort: "date" | reverse %}

<ul class="taxonomy__index">
  {% assign publications_by_year = publications
    | group_by_exp: "item", 'item.date | date: "%Y"'
  %}

  {% for year in publications_by_year %}
    <li>
      <a href="#{{ year.name }}">
        <strong>{{ year.name }}</strong>
        <span class="taxonomy__count">{{ year.items | size }}</span>
      </a>
    </li>
  {% endfor %}
</ul>

{% for year in publications_by_year %}
  <section id="{{ year.name }}" class="taxonomy__section">
    <h2 class="archive__subtitle">{{ year.name }}</h2>

    <div class="entries-list">
      {% for publication in year.items %}
        <article class="archive__item">
          <h2 class="archive__item-title">
            <a href="{{ publication.url | relative_url }}">
              {{ publication.title }}
            </a>
          </h2>

          <p>{{ publication.authors | join: ", " }}</p>

          {% if publication.venue %}
            <p><em>{{ publication.venue }}</em></p>
          {% endif %}

          {% if publication.doi %}
            <a href="https://doi.org/{{ publication.doi }}">DOI</a>
          {% endif %}

          {% if publication.paper_url %}
            | <a href="{{ publication.paper_url | relative_url }}">PDF</a>
          {% endif %}
        </article>
      {% endfor %}
    </div>

    <a href="#page-title" class="back-to-top">
      Back to Top &uarr;
    </a>
  </section>
{% endfor %}
