# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# Kategorien

<!-- found here https://blog.webjeda.com/jekyll-categories/ -->

{% assign sorted_site_categories = site.categories | sort %}
{% for category in sorted_site_categories %}
{% capture category_name %}{{ category | first }}{% endcapture %}
## {{ category_name }}
<ul>
{% for post in site.categories[category_name] %}
<!-- - [{{post.title}}]({{ site.baseurl }}{{ post.url }}) -->
<li><a href="{{ site.baseurl }}{{ post.url }}?version={{post.version}}">{{post.title}}</a></li>
{% endfor %}
</ul>
{% endfor %}

[https://snippets.schnatzefatt.de/](https://snippets.schnatzefatt.de/)
