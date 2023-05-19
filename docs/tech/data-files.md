---
parent: "Tech"
title: "Data Files"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Data Files
Data for FFX is stored in binary (.bin) files, which can be found in various folders in the VBF archive called FFX_DATA.  
General data is stored in `/FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel`.
Monster data is stored in `/FFX_Data/ffx_ps2/ffx/master/jppc/battle/mon`.
Unless otherwise stated, all data is writtein in little endian.

## General data files
### Header
{% for row in site.data.tech.data-files.general_headers -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% else -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endif -%}
{%- endfor %}

### Item Prices
<sup>Main article: [Item Prices](./data-files/item-prices.md)</sup>
Item prices are stored in the `item_rate.bin` file.

### Item Shops
<sup>Main article: [Item Shops](./data-files/item-shops.md)</sup>
Item shop data is stored in the `item_shop.bin` file.

### Customizations
<sup>Main article: [Customizations](./data-files/customizations.md)</sup>
Customization data is stored in the `kaizou.bin` file.