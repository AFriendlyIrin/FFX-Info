---
parent: "RNG"
title: "Yojimbo (PS2 version)"
---
# Yojimbo
{: .no_toc }
**Important note**: the information in this page are based on the PS2 version, you can find information based on the HD version [here](./yojimbo-hd).

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Mechanics
Yojimbo RNG (RNG17) is advanced once at the start of every Yojimbo turn (before the command menu comes up) and either once or twice after paying him at least 1 Gil.

### Compatibility
An hidden value called Compatibility is used to determine if Yojimbo will perform an action at the start of his turn for free and it's used in the Motivation calculations to determine what action he's going to perform after the payment.

Compatibility starts at 50, it can't go below 0 and above 255, it's modified by these actions:

| Action                                 | Compatibility modifier |
| :------------------------------------: | :--------------------: |
| Daigoro                                | -1                     |
| Kozuka                                 | 0                      |
| Wakizashi (single target)              | +1                     |
| Wakizashi (multi target)               | +3                     |
| Zanmato                                | +4                     |
| Dismiss (after at least 1 turn)        | 0                      |
| First turn Dismiss (before any action) | -3                     |
| Yojimbo Death                          | -10                    |
| Autodismiss (pay Yojimbo 0)            | -20                    |

### Zanmato Level
Every monster has a property called Zanmato Level, its a value between 0 and 4: it's used as part of the free action calculation and for the Motivation calculation.

From the Zanmato Level and based on what option has been picked when Yojimbo asks "What do you want of me?" while recruiting him a Zanmato Resistance is calculated: if option 1 ("To train as a summoner.") or option 2 ("To gain the power to destroy fiends.") have been picked, these are the Zanmato Resistances:

| Zanmato Level | Zanmato Resistance |
| :-----------: | :----------------: |
| 0             | 1                  |
| 1             | 1/2                |
| 2             | 1/3                |
| 3             | 1/4                |
| 4             | 1/5                |

if option 3 has been picked ("To defeat the most powerful of enemies."), these are the Zanmato Resistances:

| Zanmato Level | Zanmato Resistance |
| :-----------: | :----------------: |
| 0             | 4/5                |
| 1             | 4/5                |
| 2             | 4/5                |
| 3             | 2/5                |
| 4             | 2/5                |

## Formula
To check if Yojimbo will do a free action at the start of his turn:
```
free action rng = rng value AND 255
if (compatibility // 4) > free action rng then perform a free action
```

If the previous check is successful Yojimbo will always perform an action:
```
motivation rng = rng value AND 63
motivation = (compatibility // 4) + motivation rng
if motivation < 32 use daigoro
else if motivation < 48 use kozuka
else if motivation < 63 use wakizashi (single target)
else if motivation < 80 use wakizashi (multi target)
else if zanmato level > 0 use wakizashi (multi target)
else use zanmato
```

If no free action has been used, you can either Dismiss (lowering Compatibility by 3 if it's Yojimbo's first turn), pay him 0 (lowering Compatibility by 20 and dismissing Yojimbo) or pay him any amount between 1 and 999.999.999 (the max amount of Gil a player can hold is 999.999.999), letting Yojimbo choose what action to use:

```
gil motivation = FLOOR(LOG2(gil amount / 2)) * 2
base motivation = (compatibility // 30) + gil motivation
motivation rng = rng value AND 63
motivation = (base motivation * zanmato resistance) + motivation rng
if yojimbo has overdrive then add 2 to motivation
(overdrive bar is consumed after yojimbo performs an action)

if zanmato level = 0
    if motivation < 32 use daigoro
    else if motivation < 48 use kozuka
    else if motivation < 63 use wakizashi (single target)
    else if motivation < 80 use wakizashi (multi target)
    else use zanmato

if zanmato level > 0
    if motivation >= 80 use zanmato
    else recalculate motivation using zanmato level = 0
    (the above step will advance yojimbo rng again)
    if motivation < 32 use daigoro
    else if motivation < 48 use kozuka
    else if motivation < 63 use wakizashi (single target)
    else use wakizashi (multi target)
```

## Gil motivation sheet
This sheet shows how much Base Motivation certain amounts of Gil will add based on the formula above (`FLOOR(LOG2(gil amount / 2)) * 2`), any amount of Gil between 2 values will add as much Motivation as the lower one (for example, 100.000 Gil is between 65.536 and 131.072 and will add 30 Motivation, as much as 65.536 would).

| Gil           | Gil Motivation |
| :-----------: | :------------: |
| 0             | Dismiss        |
| 1             | 0              |
| 4             | 2              |
| 8             | 4              |
| 16            | 6              |
| 32            | 8              |
| 64            | 10             |
| 128           | 12             |
| 256           | 14             |
| 512           | 16             |
| 1.024         | 18             |
| 2.048         | 20             |
| 4.096         | 22             |
| 8.192         | 24             |
| 16.384        | 26             |
| 32.768        | 28             |
| 65.536        | 30             |
| 131.072       | 32             |
| 262.144       | 34             |
| 524.288       | 36             |
| 1.048.576     | 38             |
| 2.097.152     | 40             |
| 4.194.304     | 42             |
| 8.388.608     | 44             |
| 16.777.216    | 46             |
| 33.554.432    | 48             |
| 67.108.864    | 50             |
| 134.217.728   | 52             |
| 268.435.456   | 54             |
| 536.87.0912   | 56             |
