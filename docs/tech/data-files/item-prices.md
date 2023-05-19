---
parent: "Data Files"
title: "Item Prices"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Item Price files
The general data file containing item prices is called `item_rate.bin` and can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

### Block
The item price block is 4 (0x4) bytes long and consists only of a single integer determining an item's base price.
{% for row in site.data.tech.data-files.item_rate_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% else -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endif -%}
{%- endfor %}
The block is repeated for every existing item (and more if unmodified). The index of the block, that is, the point at which it appears in the file, determines which item it contains the base price for. The first block contains the base price of a Potion, the second contains the base price of a Hi-Potion, the third of an X-Potion, and so on.