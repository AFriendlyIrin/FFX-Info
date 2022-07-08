# FFX Info
FFX game and speedrun information dump site.

# Docs
{% for page in site.pages -%}
{%- if page.title and page.url != "/" %}
[{{ page.title }}](.{{ page.url }})

{% endif -%}
{%- endfor %}
