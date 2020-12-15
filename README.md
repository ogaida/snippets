
# Snippets

Ein paar CODE-Schnipsel zum stöbern.

Es handelt sich hier um eine statische Website auf jekyll-BASIS. jekyll wird von github gut unterstützt, wodurch es relativ einfach ist, hier Informationen zu veröffentlichen.

# more

|--|--|--|
| [conditionals](./Conditionals.html)| [windows](./windows.html) | [bash](./bash.html) |
|[regex](./regex.html)|[jekyll](./jekyll.html)|[ruby](./ruby)|

# posts

<ul>
        {% for cat in site.categories %}
        <li>
                {% assign cat_name = cat[0] %}
                <h2> Category __{{ cat_name }}__ </h2>
                <ul>
                {% for post in site.categories[cat_name] %}
                    <li>
                    <a href="./{{ cat_name }}/{{ post.title }}">{{ post.title }}</a>
                    </li>
                {% endfor %}
                </ul>
        </li>
        {% endfor %}
</ul>

## Demo

[http://snippets.schnatzefatt.de/](http://snippets.schnatzefatt.de/)
