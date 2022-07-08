# FFX Info
FFX game and speedrun information dump site.

# Docs
{% for page in site.pages -%}
{%- if page.title and page.url != "/" -%}
{%- assign link_text = page.title -%}
{%- if page.dir != "/" -%}
{%- assign link_text = page.dir | append: ": " | append: link_text -%}
{%- endif %}
[{{ link_text }}](.{{ page.url }})
{% endif -%}
{%- endfor %}
