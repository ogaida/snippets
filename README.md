
# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# Kategorien

<!-- found here https://blog.webjeda.com/jekyll-categories/ -->

{% for category in site.categories %}
  {% capture category_name %}{{ category | first }}{% endcapture %}
    <h4 class="category-head">{{ category_name }}</h4>
    <ul>
    {% for post in site.categories[category_name] %}
      <li><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></li>
    {% endfor %}
    </ul>
{% endfor %}

[https://snippets.schnatzefatt.de/](https://snippets.schnatzefatt.de/)
