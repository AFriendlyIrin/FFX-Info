---
parent: "Tech"
title: "Frame counters"
---
# Frame counters
{: .no_toc }

## Table of contents
{: .no_toc }

1. TOC
   {:toc}

# Tracking in game time
External tools can track the passage of time in the game can by observing frame counters. These come in multiple varieties- 30 and 60FPS counters, and those that pause when the game does and those that don't.

# Frame counters
The following table represents the most common frame counters:

|  Memory address | FPS |     Timing start | Pausable |
| ---------------:| ---:| ----------------:| --------:|
|  FFX.exe+88FBAC |  30 |   First map load |       No |
|  FFX.exe+88FDD8 |  30 | Executable start |       No |
|  FFX.exe+F25D54 |  30 | Current map load |      Yes |
|  FFX.exe+EFB7A8 |  60 |              N/A |      Yes |
|  FFX.exe+EFB7AC |  60 |              N/A |      Yes |
|  FFX.exe+EFB87C |  30 |   First map load |       No |
|  FFX.exe+EFBBE8 |  60 |              N/A |      Yes |
| FFX.exe+1F328D0 |  30 |              N/A |      Yes |
| FFX.exe+1F328D4 |  30 |              N/A |      Yes |
| FFX.exe+1FCBBF0 |  30 |              N/A |      Yes |
