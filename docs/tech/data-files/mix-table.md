---
grand_parent: "Tech"
parent: "Data Files"
title: "Mix Table"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Mix Table files
The general data file mapping item combinations to Mix Overdrives is called `prepare.bin` and can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

### Block
The data block is 224 (0xE0) bytes long and consists of a short array of length 112.

{% for row in site.data.tech.data-files.mix_table_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

The block is repeated for each consumable item in the game. This effectively produces a `u16[112][112]` 2-dimensional array. The first index corresponds to the first item selected, and the second index corresponds to the second item selected. Each value of the array is the ID of the resulting Mix Overdrive.

Each block only has entries up to the combination of the item with itself, with all of the following entries being blank. So for example, block 0 only has an ID in its first index, corresponding to the combination of Potion \+ Potion, with the other 111 entries having a null value of `0x0000`.

Written by [{{ site.contributors.irin.name }}]({{ site.contributors.irin.url }})