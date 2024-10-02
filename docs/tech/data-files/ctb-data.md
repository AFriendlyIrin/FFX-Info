---
grand_parent: "Tech"
parent: "Data Files"
title: "CTB Data"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## CTB Data files
The general data file mapping CTB values to Agility values is called `ctb_base.bin` and can be found inside the `FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel` folder in the VBF archive.

The Agility stat determines two parameters used in the Conditional Turn-Based Battle system. The first is **Tick Speed**, and the second is **Initial Counter Value** (or **ICV**). Every action taken by a character generates a **Tick Counter** according to the following formula:

```Counter = TickSpeed * Rank * HasteStatus```

where `rank` is the move's rank (specified in command data) and `HasteStatus` is 0.5 when the character is under the Haste status, 2 when under Slow, and 1 otherwise. Non-integer results are rounded up. Every character's counter is reduced by 1 each "tick", and the character's next turn occurs when their counter reaches 0.

During a Pre-emptive Strike or Ambush, the disadvantaged side's counters are initialized to `TickSpeed * 3` at the start of battle. Otherwise, this is only the *maximum possible* initial counter value, and the ICV has a chance to be reduced by a number based on Agility. For enemies, `TickSpeed * 3` is instead the *minimum* possible ICV, and ranges are much greater; however, that data is not stored here.

The lowest possible tick speed is 3, which is achieved at 170 Agility. Agility has sharply diminishing returns above the value of 62, with extremely large gaps between further reductions in tick speed and some increments not even conferring a greater reduction in ICV.

### Block
The CTB data block is 2 (0x2) bytes long and consists of two 8-bit integers.

{% for row in site.data.tech.data-files.ctb_data_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

The block is repeated for every value of Agility, up to the stat maximum of 255.

Written by [{{ site.contributors.irin.name }}]({{ site.contributors.irin.url }})
