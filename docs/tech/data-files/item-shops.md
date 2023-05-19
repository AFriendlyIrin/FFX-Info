---
parent: "Data Files"
title: "Item Shops"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Item Shop files
The general data file containing item shops is called `item_shop.bin` and can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

### Block
The item price block is 34 (0x22) bytes long and consists of an unused short that if used would determine the multiplier of all prices in the shop, after which follow 16 shorts containing IDs of the items in the shop.

{% for row in site.data.tech.data-files.item_shop_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% else -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endif -%}
{%- endfor %}

The block is repeated for every existing shop. The only shop with a shopRatio different from 100 (100% of base price) is the Guadosalam item shop, which has 150 (150% of base price).