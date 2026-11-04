# 1. CH341A Programmer Mod (3.3V)

## Steps
1. Added a jumper wire from the AMS1117 3.3V regulator output to the chip VCC pin (the kit shipped with the mod already done).
2. Verified the clip read ~3.3V with a multimeter before connecting it to the chip.

## Why
The stock CH341A drives the target at 5V. The W25Q128.V is a 3.3V part, and 5V can damage it. The mod forces the SOIC socket/clip rail to 3.3V.

## What I Learned
- Always confirm the programmer's output voltage with a meter before touching the chip — don't trust the board silkscreen.
- The red jumper routes the regulator's 3.3V to VCC; without it the stock board is 5V.

## Problems Encountered
- Had to confirm which header/jumper position was correct from the silkscreen before measuring.
