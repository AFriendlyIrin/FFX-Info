---
grand_parent: "Tech"
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
The general data file containing item shops is called `item_shop.bin`, and the file containing equipment shops is called `arms_shop.bin`. Equipment shops also reference `shop_arms.bin`. These files can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

### Block
The shop block is 34 (0x22) bytes long and consists of an unused short that if used would determine the multiplier of all prices in the shop, after which follow 16 shorts containing IDs of the items in the shop. For item shops, the ID corresponds to general item IDs (those in the `0x3000` range); for equipment shops, the ID corresponds to the index of entries in `shop_arms.bin`.

{% for row in site.data.tech.data-files.item_shop_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

The block is repeated for every existing shop. The only shop with a shopRatio different from 100 (100% of base price) is the Guadosalam item shop, which has 150 (150% of base price).

Written by [{{ site.contributors.evelyntsmg.name }}]({{ site.contributors.evelyntsmg.url }})
