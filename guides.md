---
layout: page
title: CloudUi Guides
---

# Guides

This is work in progress.

{% for guide in site.guides %}

<div>
{{ guide.title }}
Guide Place Holder

<a href="{{ guide.url | prepend: site.baseurl }}">
  <h2>{{ guide.title }}</h2>
</a>

<p class="post-excerpt">{{ guide.description | truncate: 160 }}</p>

</div>

{% endfor %}