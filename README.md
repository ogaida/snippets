---
layout: default
---


# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# Kategorien

<!-- found here https://blog.webjeda.com/jekyll-categories/ -->

{% for category in site.categories %}
{% capture category_name %}{{ category | first }}{% endcapture %}
## {{ category_name }}
{% for post in site.categories[category_name] %}
- [{{ site.baseurl }}{{ post.url }}]({{post.title}})
{% endfor %}
{% endfor %}

[https://snippets.schnatzefatt.de/](https://snippets.schnatzefatt.de/)
