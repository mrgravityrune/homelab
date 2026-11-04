# 2. BIOS Dump & Verify

## Steps
1. Removed battery, SSD, and drive-bay cover; located the W25Q128.V (16MB) under the drive bay. (A smaller 25Q80 nearby is the Thunderbolt chip — ignored it.)
2. Seated the SOIC-8 clip with the red wire on the pin-1 dot corner.
3. Dumped the chip three times:
   ```
   sudo flashrom -p ch341a_spi -c "W25Q128.V" -r dump1.bin
   sudo flashrom -p ch341a_spi -c "W25Q128.V" -r dump2.bin
   sudo flashrom -p ch341a_spi -c "W25Q128.V" -r dump3.bin
   ```
4. Compared hashes; all three matched (`918a8d99a6daff6a36c184bd0478ceb1d5b73fe49cb44f58f3bfb97518fc9a0c`):
   ```
   sha256sum dump1.bin dump2.bin dump3.bin
   ```
5. Kept `dump1.bin` as the verified original / recovery floor (also backed up as `dump1.backup.bin`).

## Why
A triple-matched dump proves a clean read (solid clip contact). Keeping the original is the safety net to un-brick the machine at any point.

## What I Learned
- Three reads + matching sha256 is the real test of clip contact — a single read can look fine but be corrupt.
- Keep a second named backup of the original so a stray `-r` can't overwrite your only copy.

## Problems Encountered
- **"Couldn't open device 1a86:5512 / Programmer initialization failed"** — USB access issue; the programmer wasn't enumerating. Fixed by trying different USB ports until it appeared in `lsusb`.
- **"No EEPROM/flash device found"** — bad clip contact. Had trouble seating the clip ("how am I supposed to seat this thing"); fixed by pressing straight down, teeth aligned to the chip legs, firm steady pressure.
- **Clip was reversed** the first time — flipping it so the red wire sat on the pin-1 dot corner got the chip detected (16384 kB).
