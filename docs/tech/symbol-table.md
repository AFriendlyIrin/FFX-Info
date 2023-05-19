---
parent: "Tech"
title: "Symbol table"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Symbol table
A list of all currently known symbols (function names, global variable names, and more) in FFX's Steam version. These are official function and variable names obtained by manually matching the decompilation with a version of the game that has unstripped symbols. The raw table in CSV format can be obtained from the Fahrenheit project [here](https://github.com/fkelava/fahrenheit/blob/master/Fahrenheit.Core.X/Data/FhXSymbolTable.csv).

Symbols mapped: {{ site.data.tech.symbol_table.size }} / 91537

{% for row in site.data.tech.symbol_table -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

Written by [{{ site.contributors.peppy.name }}]({{ site.contributors.peppy.url }})
