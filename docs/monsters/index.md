---
title: "Monsters"
nav_order: 1
---
# Monsters

{% for monster_page in site.monsters %}
[{{ monster_page.monster_data.name }}](./{{ monster_page.monster_id }})

{% endfor %}
