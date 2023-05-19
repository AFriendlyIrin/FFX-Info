---
parent: "Tech"
title: "Data Files"
has_children: true
---
# {{ page.title }}
Data for FFX is stored in binary (.bin) files, which can be found in various folders in the VBF archive called FFX_DATA.  
General data is stored in `/FFX_Data/ffx_ps2/ffx/master/jppc/battle/kernel`.  
Monster data is stored in `/FFX_Data/ffx_ps2/ffx/master/jppc/battle/mon`.  
Unless otherwise stated, all data is written in little endian.

General data files header:

{% for row in site.data.tech.data-files.general_headers -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

Written by [{{ site.contributors.evelyntsmg.name }}]({{ site.contributors.evelyntsmg.url }})
