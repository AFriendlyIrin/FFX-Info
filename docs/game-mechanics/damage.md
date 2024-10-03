---
parent: "Game Mechanics"
title: "Damage"
---
# {{ page.title }}
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Mechanics
Every weapon and ability (magic, skills, etc.) is assigned one of several damage formulas to use. An ability's damage formula can be overridden by a weapon's if the ability has the `use_weapon_props` flag set (see Commands). Note that whether an attack is considered physical or magical is determined by a separate variable in the command data, *not* the formula.

The ID table for each formula is as follows:

{% for row in site.data.tech.data-files.gear_block -%}
{%- if forloop.first -%}
|{% for cell in row %} {{ cell[0] }} |{% endfor %}
|{% for cell in row %} :---: |{% endfor %}
{% endif -%}
|{% for cell in row %} {{ cell[1] }} |{% endfor %}
{% endfor %}

## Formulas
Several variables used in the following formula descriptions will be defined here:
- $d$ is damage.
- $u_{hp}$, $u_{maxHP}$, $u_{mp}$, $u_{maxMP}$, $u_{str}$, $u_{def}$, $u_{mag}$, and $u_{mdf}$ are the user's statistics.
- $u_{cheer}$ and $u_{focus}$ are the user's Cheer and Focus counts.
	- For simplicity, $u_{str} + u_{cheer}$ and $u_{mag} + u_{focus}$ will both be denoted with $x$.
	- The "buff factor" $b_{(cheer|focus)} = {15 - t_{(cheer|focus)} \over 15}$
- Target statistics are the same as user statistics, but are denoted with $t$ instead of $u$.
- $p$ is the move's power.
	- For simplicity, ${p \over 16}$ will be denoted with $p'$.
- $v$ is random variance, where $v = {k \over 256}$ and $k = \text{random}(240,271)$.

Additionally, some formulas use an additional factor $r$ calculated from the target's defense to reduce the damage taken:

$$ r = {730 - {t_{(def|mdf)} \cdot 51 - {t_{(def|mdf)}^2 \over 11} \over 10} \over 730} \cdot b_{(cheer|focus)} $$

Note that if the target is Armor Broken or Mental Broken, their defense or magic defense, respectively, are considered 0.

### STR vs. DEF
$$ d = \left({x^3 \over 32} + 30\right) \cdot r \cdot p' \cdot v $$

Neglect $r$ if defense is ignored.

### MAG vs. MDF
$$ d = \left({x^2 \over 6} + p\right) \cdot r \cdot 4p' \cdot v $$

Neglect $r$ if defense is ignored.

### Current or Max (Statistic)
$$ d = t_{stat} \cdot p' $$

### Multiple of 50
$$ d = 50 \cdot p $$

with variance:

$$ d = 50 \cdot p \cdot v $$

### Healing
$x$ is magical.

$$ d = (x + p) \cdot 8p' \cdot v $$

### Special Magic
$x$ is magical.

$$ d = \left({x^3 \over 32} + 30\right) \cdot p' \cdot v $$

### User Max HP
$$ d = {u_{maxHP} \over 10} \cdot p $$

### Celestial - High HP/MP
This damage formula uses an additional factor $c$, the celestial factor.
$x$ is physical.

$$ c = {{u_{(hp|mp)} \cdot 100 \over u_{(maxHP|maxMP)} + 10} \over 110} $$

$$ d = \left({x^3 \over 32} + 30\right) \cdot c \cdot p' \cdot v $$

### Celestial - Low HP
This damage formula uses an additional factor $c$, the celestial factor.
$x$ is physical.

$$ c = {{130 - {u_{hp} \cdot 100 \over u_{maxHP}}} \over 60} $$

$$ d = \left({x^3 \over 32} + 30\right) \cdot c \cdot p' \cdot v $$

### Chosen Gil
This damage formula uses an additional factor $g$, equal to the amount of gil chosen.

$$ d = {g \over 10} $$

### Target Kills
This damage formula uses the amount of enemies the target has killed, denoted with $k$. It only works against player characters.

$$ d = k \cdot p $$

### Multiple of 9999

$$ d = 9999 \cdot p $$

## Additional Modifiers
### HP Damage
Additional modifiers are applied to the calculated damage in the following order:
1. If the target is under the effects of the Shield command, the damage is multiplied by `0.25`.
2. If the target is under the effects of the Boost command, the damage is multiplied by `1.5`.
3. If the attack is magical and the target is under the effects of Shell, the damage is halved.
4. If the attack is physical and the target is under the effects of Protect, the damage is halved.
5. If the attack is a critical hit, the damage is doubled.
6. If the user is berserked, the damage is multiplied by `1.5`.
7. If the user has Magic Booster and the command is located in the black or white magic submenus, the damage is multipled by `1.5`.
8. If the user has Alchemy, the command is an item, is healing, and uses either the `Multiple of 50` or `Target Max HP` damage formulae, damage is doubled.
9. Apply Strength +%, Magic +%, Defense +%, and Magic Def +% auto-abilities accordingly. These multiply the raw damage, not the stats.
10. If the command uses either the `Target Max HP` or the `Current Statistic` damage formulae, and the target is immune to fractional damage, the damage is set to 0.
11. If the command makes the user absorb the damage and either user or the target (but not both) are under the effects of Zombie, the damage is negated (that is, multiplied by `−1`).
12. Elemental weaknesses and resistances are applied:
	– If the enemy is weak to any element of the attack, only weaknesses are considered: for each weakness that matches one of the attack’s elements, the damage is multiplied by `1.5`, then truncated to an integer.
	– If the enemy is neutral to any element of the attack, further steps are skipped.
	– If the enemy is resistant to any element of the attack, the damage is halved and further steps are skipped.
	– If the enemy is immune to any element of the attack, the damage is set to 0 and further steps are skipped.
	– If the enemy absorbs any element of the attack, the damage is negated.
13. If the attack is not piercing, the user's weapon does not have Piercing, and the target is armored, damage is divided by `3`.
14. If the attack is physical and target is defending, the damage is halved.
15. If the attack is physical and the user is under the effects of Power Break, the damage is halved OR if the attack is magical and the user is under the effects of Magic Break, the damage is halved.
16. If the attack is physical and the target is immune to physical damage, the damage is set to 0.
17. If the attack is magical and the target is immune to magical damage, the damage is set to 0.
18. If the target is invincible, the damage is set to 0.
19. If attack was an overdrive with a timed component an additional bonus is applied, derived from the remaining overdrive time (up to 50% at 100% time remaining).
### MP Damage
Additional modifiers are applied to the calculated damage in the following order:
1. If the user has Magic Booster and the command is located in the black or white magic submenus, the damage is multiplied by `1.5`.
2. If the user has Alchemy, the command is an item, is healing, and uses either the `Multiple of 50` or `Target Max HP` damage formulae, damage is doubled.
3. If the command makes the user absorb the damage and either user or the target (but not both) are under the effects of Zombie, the damage is negated (that is, multipled by `−1`).
### CTB Damage
An additional modifier is applied to the calculated damage:
1. If the command makes the user absorb the damage and either user or the target (but not both) are under the effects of Zombie, the damage is negated (that is, multipled by `−1`).

Written by [{{ site.contributors.evelyntsmg.name }}]({{ site.contributors.evelyntsmg.url }})
