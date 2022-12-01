---
parent: "RNG"
title: "Damage, crit, escape and ICV"
---
# {{ page.title }}
{: .no_toc }

These mechanics are related because they use the same RNG arrays to determine their randomness, 20-26 for party members (RNG20 for Tidus, RNG21 for Yuna, etc.), 27 for Seymour and all Aeons, 28-35 for monsters (RNG28 for the monster in slot 1, RNG29 for the monster in slot 2, etc.).

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Damage Variance

### Mechanics
There are multiple formulas the game uses to calculate damage (including healing) using both the user's and the target's stats. Some damage formulas don't use stats at all, for example the ones used for damaging Items and Rikku Mixes, and some damage formulas don't take RNG into account (despite still advancing it), for example the one used to calculate healing from Items.

### Formula
Before doing any damage calculation the game advances damage RNG and after calculating the base damage value (the damage that would be dealt if there was no damage variance), it uses the RNG value to determine the exact amount of damage to deal:
```
damage rng = rng value MOD 31
damage roll = damage rng + 240
damage value = (base damage value * damage roll) // 256
```

## Critical chance

### Mechanics
The Attack command, all Skills, some Items and some Overdrives have a chance to deal double damage. Some actions use a bonus crit chance given by equipment, usually the ones that actually use the weapon to deal damage (but also actions like Sonic Wings and Impulse).

A lot of monster actions can potentially deal a critical hit but never do so because after calculations their critical hit chance is 0. Some monster action have a bonus crit chance added on top of the base critical chance.

### Formula
If the action is able to do a critical hit the game advances crit RNG before damage calculations:
```
crit rng = rng value MOD 101
crit chance = user luck - target luck
if the action uses the bonus equipment crit:
    crit chance += bonus equipment crit
if crit chance > crit rng then deal a critical hit
```

## Escape

### Mechanics
Every time the Escape command is used the game advances escape RNG.

### Formula
```
escape rng = rng value AND 255
if escape rng < 191 then escape
```

## ICV

### Mechanics
ICV stands for Initial Counter Value, it determines the initial amount of CTB ticks a character/monster needs to wait to take their first turn in battle. At the start of every fight every character (even the ones not in battle, Seymour and the Aeons) is assigned an ICV:
- if the battle is a Preemptive Strike every character is assigned an ICV of 0 and every monster an ICV equal to `Base CTB * 3`;
- if the battle is an Ambush every character is assigned an ICV equal to `Base CTB * 3` and every monster an ICV of 0;
- otherwise the game proceeds with ICV calculations normally, advancing RNG once for each character and each monster.

### Formula
You can find the Base CTB, ICV Variance and the ICV ranges [here](../game-mechanics/ctb.md#ctb-table).

For characters:
```
base ctb = base ctb array [character agility]
icv variance = icv variance array [character agility] + 1
icv rng = rng value MOD icv variance
icv = (base ctb * 3) + ctb rng
```

For monsters:
```
base ctb = base ctb array [monster]
ctb rng = 100 - (rng value MOD 11)
icv = (base ctb * 300) // ctb rng
```

### Notes
When there are multiple copies of the same monster some additional RNG advances are performed:
- the RNG array corrisponding to the first duplicate monster is advanced once for every duplicate monster
- the RNG array corresponding to the each duplicate monster is advanced once

It is currently not known how these RNG values are used.

While for characters every value in the range of ICV Values is equally likely, for monsters that is not the case: for example a monster with 15 Agility will have 3/11 chance of having 36 ICV, 3/11 chance of 37 ICV, 2/11 chance of 38 ICV, 2/11 of 39 ICV and 1/11 chance of 40 ICV.
