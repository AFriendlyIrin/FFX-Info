---
parent: "Game mechanics"
title: "CTB"
---
# {{ page.title }}
{: .no_toc }

CTB stands for Conditional Time Battle, it's the system the game uses to determine turn order in battle.

## Table of contents
{: .no_toc }

1. TOC
{:toc}

## Mechanics
Each character and monster has a Base CTB, the higher their Agility, the lower their base CTB. At the start of an encounter each character and monster is assigned a CTB Value (you can find a detailed explanation [here](../rng/damage-crit-escape-icv.md#icv)), then the game starts decreasing everyones CTB Value until someone has a CTB Value of 0, then that character/monster takes their turn and their CTB Value is set to `Base CTB * Action Rank`, continuing the process until the encounter is over.

If more than one character/monster has a CTB Value of 0, characters get priority over monsters; if there is still a tie (meaning multiple characters or monsters or both have 0 CTB) they get ordered based on their Agility stat (who has higher Agility goes first) and lower indexes have priority over higher indexes: Tidus (character index 0) has priority over everyone else, Wakka (4) has priority over Lulu (5) and Rikku (6); the monster in slot 1 has priority over the other monsters, the monster in slot 3 has priority over monsters in slots 4 to 8.

If an action is performed under the Haste status the CTB Value is divided in half, rounding up; under the Slow status the CTB Value is doubled.

When a character is revived or is cured from the Petrify status their CTB Value is set to `Base CTB * 3`, even if under the Haste or Slow status.

## CTB Table
Each possible value of the Agility stat and its corresponding Base CTB and ICV Variance:

| Agility | Base CTB | ICV Variance |
| ------: | -------: | -----------: |
| 1       | 28       | 1            |
| 2       | 26       | 1            |
| 3       | 24       | 1            |
| 4       | 20       | 1            |
| 5       | 16       | 1            |
| 6       | 16       | 2            |
| 7       | 15       | 1            |
| 8       | 15       | 2            |
| 9       | 15       | 3            |
| 10      | 14       | 1            |
| 11      | 14       | 2            |
| 12      | 13       | 1            |
| 13      | 13       | 2            |
| 14      | 13       | 3            |
| 15      | 12       | 1            |
| 16      | 12       | 2            |
| 17      | 11       | 1            |
| 18      | 11       | 2            |
| 19      | 10       | 1            |
| 20      | 10       | 2            |
| 21      | 10       | 3            |
| 22      | 10       | 4            |
| 23      | 9        | 1            |
| 24      | 9        | 2            |
| 25      | 9        | 3            |
| 26      | 9        | 4            |
| 27      | 9        | 5            |
| 28      | 9        | 6            |
| 29      | 8        | 1            |
| 30      | 8        | 2            |
| 31      | 8        | 3            |
| 32      | 8        | 4            |
| 33      | 8        | 5            |
| 34      | 8        | 6            |
| 35      | 7        | 1            |
| 36      | 7        | 2            |
| 37      | 7        | 3            |
| 38      | 7        | 4            |
| 39      | 7        | 5            |
| 40      | 7        | 6            |
| 41      | 7        | 7            |
| 42      | 7        | 8            |
| 43      | 7        | 9            |
| 44      | 6        | 1            |
| 45      | 6        | 1            |
| 46      | 6        | 2            |
| 47      | 6        | 2            |
| 48      | 6        | 3            |
| 49      | 6        | 3            |
| 50      | 6        | 4            |
| 51      | 6        | 4            |
| 52      | 6        | 5            |
| 53      | 6        | 5            |
| 54      | 6        | 6            |
| 55      | 6        | 6            |
| 56      | 6        | 7            |
| 57      | 6        | 7            |
| 58      | 6        | 8            |
| 59      | 6        | 8            |
| 60      | 6        | 9            |
| 61      | 6        | 9            |
| 62      | 5        | 1            |
| 63      | 5        | 1            |
| 64      | 5        | 1            |
| 65      | 5        | 1            |
| 66      | 5        | 2            |
| 67      | 5        | 2            |
| 68      | 5        | 2            |
| 69      | 5        | 2            |
| 70      | 5        | 3            |
| 71      | 5        | 3            |
| 72      | 5        | 3            |
| 73      | 5        | 3            |
| 74      | 5        | 4            |
| 75      | 5        | 4            |
| 76      | 5        | 4            |
| 77      | 5        | 4            |
| 78      | 5        | 5            |
| 79      | 5        | 5            |
| 80      | 5        | 5            |
| 81      | 5        | 5            |
| 82      | 5        | 6            |
| 83      | 5        | 6            |
| 84      | 5        | 6            |
| 85      | 5        | 6            |
| 86      | 5        | 7            |
| 87      | 5        | 7            |
| 88      | 5        | 7            |
| 89      | 5        | 7            |
| 90      | 5        | 8            |
| 91      | 5        | 8            |
| 92      | 5        | 8            |
| 93      | 5        | 8            |
| 94      | 5        | 9            |
| 95      | 5        | 9            |
| 96      | 5        | 9            |
| 97      | 5        | 9            |
| 98      | 4        | 1            |
| 99      | 4        | 1            |
| 100     | 4        | 1            |
| 101     | 4        | 1            |
| 102     | 4        | 1            |
| 103     | 4        | 1            |
| 104     | 4        | 1            |
| 105     | 4        | 1            |
| 106     | 4        | 2            |
| 107     | 4        | 2            |
| 108     | 4        | 2            |
| 109     | 4        | 2            |
| 110     | 4        | 2            |
| 111     | 4        | 2            |
| 112     | 4        | 2            |
| 113     | 4        | 2            |
| 114     | 4        | 3            |
| 115     | 4        | 3            |
| 116     | 4        | 3            |
| 117     | 4        | 3            |
| 118     | 4        | 3            |
| 119     | 4        | 3            |
| 120     | 4        | 3            |
| 121     | 4        | 3            |
| 122     | 4        | 4            |
| 123     | 4        | 4            |
| 124     | 4        | 4            |
| 125     | 4        | 4            |
| 126     | 4        | 4            |
| 127     | 4        | 4            |
| 128     | 4        | 4            |
| 129     | 4        | 4            |
| 130     | 4        | 5            |
| 131     | 4        | 5            |
| 132     | 4        | 5            |
| 133     | 4        | 5            |
| 134     | 4        | 5            |
| 135     | 4        | 5            |
| 136     | 4        | 5            |
| 137     | 4        | 5            |
| 138     | 4        | 6            |
| 139     | 4        | 6            |
| 140     | 4        | 6            |
| 141     | 4        | 6            |
| 142     | 4        | 6            |
| 143     | 4        | 6            |
| 144     | 4        | 6            |
| 145     | 4        | 6            |
| 146     | 4        | 7            |
| 147     | 4        | 7            |
| 148     | 4        | 7            |
| 149     | 4        | 7            |
| 150     | 4        | 7            |
| 151     | 4        | 7            |
| 152     | 4        | 7            |
| 153     | 4        | 7            |
| 154     | 4        | 8            |
| 155     | 4        | 8            |
| 156     | 4        | 8            |
| 157     | 4        | 8            |
| 158     | 4        | 8            |
| 159     | 4        | 8            |
| 160     | 4        | 8            |
| 161     | 4        | 8            |
| 162     | 4        | 9            |
| 163     | 4        | 9            |
| 164     | 4        | 9            |
| 165     | 4        | 9            |
| 166     | 4        | 9            |
| 167     | 4        | 9            |
| 168     | 4        | 9            |
| 169     | 4        | 9            |
| 170     | 3        | 1            |
| 171     | 3        | 1            |
| 172     | 3        | 1            |
| 173     | 3        | 1            |
| 174     | 3        | 1            |
| 175     | 3        | 1            |
| 176     | 3        | 1            |
| 177     | 3        | 1            |
| 178     | 3        | 1            |
| 179     | 3        | 1            |
| 180     | 3        | 1            |
| 181     | 3        | 1            |
| 182     | 3        | 1            |
| 183     | 3        | 1            |
| 184     | 3        | 1            |
| 185     | 3        | 1            |
| 186     | 3        | 2            |
| 187     | 3        | 2            |
| 188     | 3        | 2            |
| 189     | 3        | 2            |
| 190     | 3        | 2            |
| 191     | 3        | 2            |
| 192     | 3        | 2            |
| 193     | 3        | 2            |
| 194     | 3        | 2            |
| 195     | 3        | 2            |
| 196     | 3        | 2            |
| 197     | 3        | 2            |
| 198     | 3        | 2            |
| 199     | 3        | 2            |
| 200     | 3        | 2            |
| 201     | 3        | 2            |
| 202     | 3        | 3            |
| 203     | 3        | 3            |
| 204     | 3        | 3            |
| 205     | 3        | 3            |
| 206     | 3        | 3            |
| 207     | 3        | 3            |
| 208     | 3        | 3            |
| 209     | 3        | 3            |
| 210     | 3        | 3            |
| 211     | 3        | 3            |
| 212     | 3        | 3            |
| 213     | 3        | 3            |
| 214     | 3        | 3            |
| 215     | 3        | 3            |
| 216     | 3        | 3            |
| 217     | 3        | 3            |
| 218     | 3        | 4            |
| 219     | 3        | 4            |
| 220     | 3        | 4            |
| 221     | 3        | 4            |
| 222     | 3        | 4            |
| 223     | 3        | 4            |
| 224     | 3        | 4            |
| 225     | 3        | 4            |
| 226     | 3        | 4            |
| 227     | 3        | 4            |
| 228     | 3        | 4            |
| 229     | 3        | 4            |
| 230     | 3        | 4            |
| 231     | 3        | 4            |
| 232     | 3        | 4            |
| 233     | 3        | 4            |
| 234     | 3        | 5            |
| 235     | 3        | 5            |
| 236     | 3        | 5            |
| 237     | 3        | 5            |
| 238     | 3        | 5            |
| 239     | 3        | 5            |
| 240     | 3        | 5            |
| 241     | 3        | 5            |
| 242     | 3        | 5            |
| 243     | 3        | 5            |
| 244     | 3        | 5            |
| 245     | 3        | 5            |
| 246     | 3        | 5            |
| 247     | 3        | 5            |
| 248     | 3        | 5            |
| 249     | 3        | 5            |
| 250     | 3        | 6            |
| 251     | 3        | 6            |
| 252     | 3        | 6            |
| 253     | 3        | 6            |
| 254     | 3        | 6            |
| 255     | 3        | 6            |
