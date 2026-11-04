# ThinkPad T470 Supervisor Password (SVP) Removal

A hands-on BIOS firmware project: removing a BIOS supervisor password from a legitimately-owned Lenovo ThinkPad T470 by externally reading, patching, and reflashing its SPI flash chip with a CH341A programmer.

## Why
_Fill in: why you did this (bought the laptop secondhand with an SVP set, learning firmware/security, etc.)._

## The Journey (read in order)
1. [CH341A Programmer Mod](01-ch341a-mod.md)
2. [BIOS Dump & Verify](02-bios-dump.md)
3. [First Patch Attempt & Signature Mismatch](03-patch-signature-mismatch.md)
4. [Archived BIOS from Badcaps](04-archived-bios.md)
5. [Patching & Injecting the Unlock Drivers](05-patch-inject.md)
6. [Restore Original & Confirm SVP Cleared](06-restore-confirm.md)

## Hardware & Tools
- ThinkPad T470 (Kaby Lake), Winbond W25Q128.V 16MB SPI flash
- CH341A SPI programmer + SOIC-8 clip (3.3V-modded)
- flashrom, Lenovo BIOS Auto-Patcher
- _Fill in: your host OS / machine_

## Disclaimer
_Fill in: this was done on hardware you own; note the safety/legal framing in your own words._
