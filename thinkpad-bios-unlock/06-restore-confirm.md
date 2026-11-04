# 6. Restore Original & Confirm SVP Cleared

## Steps
1. Flashed my own original BIOS back:
   ```
   sudo flashrom -p ch341a_spi -c "W25Q128.V" -w dump1.bin
   ```
2. Booted — hit "Bad CRC of security block."
3. Entered ThinkPad Setup, loaded defaults (F9), saved and exited (F10).
4. Confirmed the supervisor password prompt no longer appears.

## Why
Restoring `dump1.bin` puts my own serial/UUID/MAC back in place. The SVP-clear is written to the EC, not the BIOS flash file, so it persists even after flashing the original firmware back — which is what demonstrates the unlock actually succeeded.

## What I Learned
- The SVP state lives in the EC, not the BIOS image — that's why restoring the original dump keeps the machine unlocked.
- "Bad CRC" after a flash is a settings/NVRAM mismatch, cleared by loading setup defaults (F9) and saving (F10), not a brick.

## Problems Encountered
- "Bad CRC of security block" on first boot after restore — resolved by entering setup and loading defaults.
- A separate pre-existing "diag mode" black-screen-with-cursor-flash boot behavior appeared (from an earlier session), unrelated to the flash; confirmed 1 beep = healthy POST and the restored dump's sha256 matched the original, so the chip restore was perfect.
