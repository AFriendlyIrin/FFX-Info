---
grand_parent: "Tech"
parent: "Data Files"
title: "Aeon Growth"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Aeon Growth files
The data for aeon growth is split across three files: `sum_assure.bin`, `sum_grow.bin`, and `ply_rom.bin`. These files can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

Aeons can be taught abilities by consuming items once the player obtains the Summoner's Soul. This data is also stored in `sum_grow.bin`.

Aeon stats are determined by three factors: Yuna's stats, the number of battles fought by the player, and direct increments using the Aeon's Soul. Stats based on battles are defined in `sum_assure.bin`, and Aeon's Soul increments are defined `sum_grow.bin`. Yuna's stats are related to aeons' stats through the following formula:

```
	HP = a * Y + b * floor(Y_stat/100)
	MP = a * floor(Y/10) + b * floor(Y_stat/100)
others = floor(Y/a) + b * floor(Y_stat/10)
```

where `Y` is the sum of Yuna's stats (with HP and MP corrected with factors of 1/100 and 1/10 respectively) and `Y_stat` is Yuna's stat value for the specific stat being determined. `a` and `b` are factors defined in `ply_rom.bin`.

### sum_assure.bin Block
The data block is 12 (0x0C) bytes long and consists of data defining an aeon's stats at a given battle threshold.

{% for row in site.data.tech.data-files.sum_assure_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

The block is repeated 10 times, once for each aeon (with the three Magus Sisters counted separately). The set of 10 blocks is then repeated 20 times, once for each battle threshold.

### sum_grow.bin Block
`sum_grow.bin` features two different data blocks, one for abilities and one for stat improvements. Both are 8 (0x08) bytes long.

{% for row in site.data.tech.data-files.sum_grow_ability_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

This block is repeated 67 times, once for each ability that aeons can learn. It is then followed by stat blocks:

{% for row in site.data.tech.data-files.sum_grow_stat_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

This block is repeated 10 times, once for each stat. Stat IDs are as follows:

```
HP = 0,
MP = 1,
strength = 2,
defense = 3,
magic = 4,
magic_defense = 5,
agility = 6,
luck = 7,
evasion = 8,
accuracy = 9,
```

Note that the number of items required for stat increments depends on the stat in question. The formula for this calculation is not stored here.

### ply_rom.bin Block
The data block for growth coefficients is 18 (0x12) bytes long and is contained within a larger block 44 (0x2C) bytes long that contains additional data about the aeon. Only the growth data block is shown here. Aeon data blocks begin at address `0x0174` in `ply_rom.bin`, after the blocks for human data.

{% for row in site.data.tech.data-files.ply_rom_aeonGrowth_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

There is one of these blocks for every aeon (12 in total, including two dummy aeons).

Written by [{{ site.contributors.irin.name }}]({{ site.contributors.irin.url }})