---
layout: archive
title: "Conventions"
collection: conventions
permalink: /conventions/
author_profile: false
---
{% assign tags =  site.conventions | map: 'tags' | join: ','  | split: ',' | uniq %}

{% for tag in tags %}
    <section id="{{ tag[0] | slugify | downcase }}" class="taxonomy__section">
      <h2 class="archive__subtitle">{{ tag }}</h2>
      <div class="entries-{{ page.entries_layout | default: 'list' }}">
        {% for post in site.conventions %}
            {% if post.tags contains tag %}
                {% include archive-single.html type=page.entries_layout %}
            {% endif %}
        {% endfor %}
        </div>
        <a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
    </section>
{% endfor %}
