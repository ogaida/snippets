
# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# more

|--|--|--|
| [conditionals](./Conditionals.html)| [windows](./windows.html) | [bash](./bash.html) |
|[regex](./regex.html)|[jekyll](./jekyll.html)|[ruby](./ruby)|

# Categories

<!-- found here https://blog.webjeda.com/jekyll-categories/ -->

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>
    <p></p>

    <h3 class="category-head">{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
    <article class="archive-item">
      <h4><a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a></h4>
    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>

## Demo

[https://snippets.schnatzefatt.de/](https://snippets.schnatzefatt.de/)
