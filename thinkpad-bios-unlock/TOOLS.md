# Tools & Programs Used

| Tool | Purpose |
|------|---------|
| **CH341A SPI programmer** (3.3V-modded) | External read/write of the SPI flash chip |
| **SOIC-8 test clip** | Clamps onto the chip to connect it to the programmer |
| **Multimeter** | Verified the programmer outputs 3.3V before connecting |
| **flashrom** (v1.6.0) | Read, write, and verify the SPI flash from Linux |
| **Lenovo BIOS Auto-Patcher** (suds-mcduff/lenovo-bios-autopatcher) | Injects the SVP-unlock DXE drivers into a BIOS image |
| **UEFIReplace** (bundled in the patcher's `tools/`) | Does the actual volume/driver injection |
| **qt5-qtbase** | Runtime dependency for UEFIReplace |
| **sha256sum** | Verified dump integrity across three reads |
| **Badcaps forum** | Source of the archived 2018 T470 BIOS dump |

## Chip
- **Winbond W25Q128.V** — 16MB (16,777,216 bytes) SPI flash, 3.3V part, located under the drive bay.
