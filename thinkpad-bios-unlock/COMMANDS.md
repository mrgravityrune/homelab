# Command Reference (by phase)

## Phase 1 — CH341A mod
_No shell commands; hardware jumper + multimeter check (~3.3V)._

## Phase 2 — Dump & verify
```
sudo flashrom -p ch341a_spi -c "W25Q128.V" -r dump1.bin
sudo flashrom -p ch341a_spi -c "W25Q128.V" -r dump2.bin
sudo flashrom -p ch341a_spi -c "W25Q128.V" -r dump3.bin
sha256sum dump1.bin dump2.bin dump3.bin
cp dump1.bin dump1.backup.bin
```

## Phase 3 — First patch attempt (failed, signature mismatch)
```
git clone https://github.com/suds-mcduff/lenovo-bios-autopatcher
cd lenovo-bios-autopatcher
sudo dnf install qt5-qtbase        # fixes libQt5Core.so.5 missing
sh autopatch dump1.bin             # -> dump1_PATCHED.bin
sudo flashrom -p ch341a_spi -c "W25Q128.V" -w dump1_PATCHED.bin   # black-screened on boot
sudo flashrom -p ch341a_spi -c "W25Q128.V" -w dump1.bin           # recovery
```

## Phase 4 — Archived BIOS
```
ls -la ~/Downloads/*.bin
cp ~/Downloads/"t470 Orig..bin" t470_Orig.bin
```

## Phase 5 — Patch, inject, unlock
```
sh autopatch t470_Orig.bin         # -> t470_Orig_PATCHED.bin
sudo flashrom -p ch341a_spi -c "W25Q128.V" -w t470_Orig_PATCHED.bin
# boot it: Space -> Space once more -> "TPM certificate changed. Turn it off" -> power off
```

## Phase 6 — Restore & confirm
```
sudo flashrom -p ch341a_spi -c "W25Q128.V" -w dump1.bin
# boot -> "Bad CRC" -> enter ThinkPad Setup -> F9 load defaults -> F10 save & exit
# confirm no supervisor password prompt
```

## Troubleshooting commands used
```
lsusb                 # confirm the CH341A (1a86:5512) enumerates
lsmod | grep ch341
groups                # confirm user in wheel for sudo
```
