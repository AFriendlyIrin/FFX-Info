---
parent: "RNG"
title: "Encounters"
---
# Encounters
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Encounter formation and condition

### Mechanics
When an encounter is triggered the game uses RNG1 to determine both the monster formation and the encounter condition (Normal, Ambush or Preemptive Strike).

If the encounter triggered has a forced formation (for example a boss) RNG is only advanced to determine the encounter condition. Most bosses and some random encounters force a specific encounter condition (usually Normal), in that case RNG is still advanced but the result is not used.

Triggering an encounter advances damage RNG to determine ICVs, you can find more details [here](./damage-crit-escape-icv#icv).

### Formula
The game determines the formation first:
```
formation rng = rng value MOD # of formations in the zone
```
The formation used will be the Nth formation in the zone, where N is Formation RNG.

The encounter condition is determined as follows:
```
condition rng = rng value AND 255
if a character in the active party has an initiative weapon equipped:
    condition rng -= 33

if condition rng < 32 the condition is preemptive
else if condition rng < 223 the condition is normal
else the condition is ambush

if the encounter has a forced condition use that instead
```

## Encounter checks

### Mechanics
Every 10 units of movement in an hostile zone an encounter check is generated, RNG0 is advanced and the RNG value is checked against a check counter determining if an encounter is triggered or not; when an encounter is triggered or the zone changes both the distance counter and the check counter are reset to 0.

Every hostile zone has a Danger Value that determines the Grace Period, how many encounter checks to skip when entering the zone and after every encounter, and the Threat Modifier, used to determine how fast a counter that is compared to the RNG Value increases. The bigger the Danger Value is the longer the Grace Period is gonna be and the slower is the counter is gonna increase.

### Formula
The Grace Period and Threat Modifier are calculated as follows:
```
grace period = danger value // 2
threat modifier = danger value * 4
```

At every encounter check the game performs the following calculations:
```
check rng = rng value AND 255
check value = (check counter * 256) // threat modifier
if check rng < check value then trigger an encounter and reset the counters
else increase the check counter by 1
```
