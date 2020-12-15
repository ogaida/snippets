
# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# more

|--|--|--|
| [conditionals](./Conditionals.html)| [windows](./windows.html) | [bash](./bash.html) |
|[regex](./regex.html)|[jekyll](./jekyll.html)|[ruby](./ruby)|

# posts


  {% for cat in site.categories %}
    ## Category __{{ cat }}__
    <ul>
    {% for post in site.category[cat].posts %}
        <li>
        <a href="./{{ cat }}/{{ post.title }}">{{ post.title }}</a>
        </li>
    {% endfor %}
    </ul>
  {% endfor %}


## Demo

[http://snippets.schnatzefatt.de/](http://snippets.schnatzefatt.de/)
