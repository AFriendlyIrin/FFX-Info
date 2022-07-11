---
parent: "RNG"
title: "Hit chance"
---
# Hit chance
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Mechanics
Hit chance uses RNG arrays 36-42 for for party members (RNG36 for Tidus, RNG37 for Yuna, etc.), 43 for Seymour and all Aeons, 44-51 for monsters (RNG44 for the monster in slot 1, RNG45 for the monster in slot 2, etc.). It's advanced once every time a character/monster uses an action that can miss (for characters its Attack and the Skills).

## Formula

### Characters
For characters the Hit chance is calculated as follows:
```
accuracy index = ((accuracy * 2 * 0x66666667) // 0xffffffff) // 2
(the above is similar to accuracy * 2 // 5)
hit chance index = accuracy index - enemy evasion + 10

if hit chance index < 0 then hit chance index = 0
else if hit chance index > 8 then hit chance index = 8
```

Then the game uses this table to find the Base Hit chance:

| Hit chance index | Base Hit chance |
| :--------------: | :-------------: |
| 0                | 25              |
| 1                | 30              |
| 2                | 30              |
| 3                | 40              |
| 4                | 40              |
| 5                | 50              |
| 6                | 50              |
| 7                | 80              |
| 8                | 100             |

```
hit rng = rng value MOD 101
hit chance = base hit chance + user luck - target luck
every aim on the user adds 10 to hit chance
every reflex on the target subtracts 10 from hit chance
if hit chance > hit rng then the action hits
```

### Monsters
For monsters the Accuracy Stat has no purpose, every monster action has an accuracy value that is used instead:
```
hit chance = action accuracy - target evasion + user luck - target luck
every aim on the user adds 10 to hit chance
every reflex on the target subtracts 10 from hit chance
if hit chance > hit rng then the action hits
```
