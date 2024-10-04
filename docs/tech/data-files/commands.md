---
grand_parent: "Tech"
parent: "Data Files"
title: "Commands"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Command files
The files containing data for commands are `command.bin`, `item.bin`, `monmagic1.bin`, and `monmagic2.bin`. They can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive, though as they contain text data, there are copies in the `new_uspc` folder as well.

Every consumable item has an associated command, including those that cannot be used.

`monmagic1` contains commands used by regular enemies and optional bosses. `monmagic2` contains commands used in scripted encounters in the main campaign. Note that Ronso Rages used by the player have unique command blocks separate from those used by enemies.

### Standard Block
The standard command block is 96 (0x60) bytes long.

{% for row in site.data.tech.data-files.command_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

Status chances are in the following order: death, zombie, petrify, poison, power break, magic break, armor break, mental break, confuse, berserk, provoke, threaten, sleep, silence, darkness, shell, protect, reflect, NulTide, NulBlaze, NulShock, NulFrost, regen, haste, slow.

Status durations are in the following order: sleep, silence, darkness, shell, protect, reflect, NulTide, NulBlaze, NulShock, NulFrost, regen, haste, slow. 

Formula IDs can be mapped to the following values:

{% for row in site.data.tech.data-files.formula_table -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

Character IDs can be mapped to the following values:

{% for row in site.data.tech.data-files.character_table -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

Sphere Grid role IDs can be mapped to the following values:

{% for row in site.data.tech.data-files.sphere_role_table -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

### Monster Command Block
The monster command block is 92 (0x5B) bytes. It lacks the final 4 bytes of the standard command block (the `menu_idx`, `sg_role`, and final `unknown` variables), but is otherwise identical to the standard command block.

Written by [{{ site.contributors.irin.name }}]({{ site.contributors.irin.url }})