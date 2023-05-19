---
parent: "Data Files"
title: "Customizations"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Customization data files
The general data file containing item prices is called `kaizou.bin` and can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

### Block
The customization block is 8 (0x8) bytes long and consists of four shorts.

{% for row in site.data.tech.data-files.kaizou_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% else -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endif -%}
{%- endfor %}

The block is repeated for every existing customization. The `appliesTo` field is 1 if the customization can be applied to weapons, 2 if it can be applied to armor, or 3 if it can be applied to both. In other words, the first bit determines whether the customization can be applied to weapons, and the second bit determines whether the customization can be applied to armor.
