
# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# more

|--|--|--|
| [conditionals](./Conditionals.html)| [windows](./windows.html) | [bash](./bash.html) |
|[regex](./regex.html)|[jekyll](./jekyll.html)|[ruby](./ruby)|

# posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

## Demo

[http://snippets.schnatzefatt.de/](http://snippets.schnatzefatt.de/)
