---
grand_parent: "Tech"
parent: "Data Files"
title: "Equipment Prices"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Equipment Price files
Equipment price is partially determined by its auto-abilities, each of which have an associated gil value. The general data file containing the value of each auto-ability is called `arms_rate.bin` and can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

The full formula for determining equipment price is:

```(50 + sum(ability_value)) * slots_factor * empty_slots_factor```

where `slots_factor` and `empty_slots_factor` are arrays with indices corresponding to the number of filled and empty slots, respectively. The values for each are as follows:

```
EQUIPMENT_SLOTS_GIL_MODIFIERS = (1, 1, 1.5, 3, 5)
EQUIPMENT_EMPTY_SLOTS_GIL_MODIFIERS = (1, 1, 1.5, 3, 400)
```

The location of the formula data is currently unknown.

### Block
The gear price block is 4 (0x4) bytes long and consists only of a single integer determining an auto-ability's value.

{% for row in site.data.tech.data-files.gear_rate_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

The block is repeated for every existing auto-ability (and more if unmodified). The index of the block, that is, the point at which it appears in the file, determines which auto-ability it contains the value for. The first block contains the value of Sensor, the second contains the value of First Strike, the third of Initiative, and so on.

Written by [{{ site.contributors.irin.name }}]({{ site.contributors.irin.url }})
