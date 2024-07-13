---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

<!-- {% if author.googlescholar %}
  You can also find my articles on <u><a href="{{author.googlescholar}}">my Google Scholar profile</a>.</u>
{% endif %} -->

You can also find my articles on <a href="https://scholar.google.com/citations?user=tfxCpGMAAAAJ&hl=en" target="_blank">my Google Scholar profile</a>.<br>
(* indicates equal contribution)

{% include base_path %}

{% assign publicationsByYear = site.publications | group_by_exp:"post", "post.date | date: '%Y'" %}
{% for year in publicationsByYear reversed %}
  <h1 style="margin: 1.5em 0px -0.5em; padding: 0px; color: brown;">{{ year.name }}</h1>
  {% assign publicationsByMonth = year.items | group_by_exp:"post", "post.date | date: '%B'" %}
  {% for month in publicationsByMonth reversed %}
    {% for post in month.items reversed %}
      {% if post.venue != "arXiv" and post.venue != "UCLA Electronic Theses and Dissertations" %}
        {% include archive-single.html %}
      {% endif %}
    {% endfor %}
  {% endfor %}
{% endfor %}

<hr>
<h1 style="margin: 1.25em 0px -0.5em; padding: 0px; color: brown;">Preprints</h1>
{% for post in site.publications reversed %}
  {% if post.venue == "arXiv" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

<hr>
<h1 style="margin: 1.25em 0px -0.5em; padding: 0px; color: brown;">Dissertation</h1>
{% for post in site.publications reversed %}
  {% if post.venue == "UCLA Electronic Theses and Dissertations" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}
