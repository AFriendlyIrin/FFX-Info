---
grand_parent: "Tech"
parent: "Data Files"
title: "Equipment Data"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Equipment Data files
Equipment data is defined in three files: `buki_get.bin`, `shop_arms.bin`, and `weapon.bin`. These files can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive. `buki_get.bin` defines gear obtained from treasure chests, `shop_arms.bin` defines gear sold in shops, and `weapon.bin` defines other pre-existing gear (starting gear, gear obtained in scenes, Celestial weapons, etc.).

### Block
In each file the data block is 22 (0x16) bytes long.

{% for row in site.data.tech.data-files.gear_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

where `character_id` can be mapped to the following values:

{% for row in site.data.tech.data-files.character_table -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

and `damage_formula` can be mapped to the following values:

{% for row in site.data.tech.data-files.formula_table -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

Written by [{{ site.contributors.irin.name }}]({{ site.contributors.irin.url }})
