---
layout: page
title: "Status chance RNG"
permalink: /status-chance-rng/
---

# Formula
Status RNG is advanced before any check is performed.

The following checks are performed one after the other:
-   if the ability/item status landing chance is 255 the status always applies regardless of immunity;
-   if status resistance is 255 the status doesn't apply;
-   if the ability/item status landing chance is 254 the status is applied.

If all of the checks fail the game calculates the actual status chance and compares it to the RNG value:
```
status chance = ability/item status landing chance - target status resistance
status rng = rng value modulo 101
if status chance > status rng then apply the status
```

For abilities/items that apply multiple status effect the game checks them one by one, repeating the steps above; the order in which the statuses are checked is the following:
```
Death, Zombie, Petrify, Poison, Power Break, Magic Break, Armor Break, Mental Break, Confuse, Berserk, Provoke, Threaten, Sleep, Silence, Dark, Protect, Shell, Reflect, Nulblaze, Nulfrost, Nulshock, Nultide, Regen, Haste, Slow
```

# Notes
The RNG arrays used are 52-58 for party members (RNG52 for Tidus, RNG53 for Yuna, etc.), 59 for aeons, 60-67 for enemies (RNG60 for the enemy in slot 1, RNG61 for the enemy in slot 2, etc.).

For Break and Attack Skills and for -strike weapons the status landing chance is 100, and since the RNG value is a number between 0 and 100 there is a 1/101 chance for the status not to apply on enemies with 0 resistance.

For Buster Skills the status landing chance is 254 so they always apply unless the target is immune (255 resistance), even if the target resistance is 254 the status is applied.

Abilities and items that apply multiple statuses on multiple targets apply them in order (apply each status to the target on the first slot, then do the same for every other target).

Petrify Grenade and Stone Breath check for Petrify status chance and if the target is petrified a check for Shatter chance is performed (enemies always Shatter when petrified). For example, in the Wendigo fight using a Petrify Grenade when every enemy is alive advances status RNG 5 times: Petrify Chance for Guado A, Shatter chance for Guado A, Petrify Chance for Wendigo, Petrify Chance for Guado B, Shatter chance for Guado B.

Using Phoenix Downs on Undead enemies (like Fallen Monk and Evrae Altana) doesn't advance status RNG.
