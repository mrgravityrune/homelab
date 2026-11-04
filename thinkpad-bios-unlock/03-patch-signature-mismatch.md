# 3. First Patch Attempt & Signature Mismatch (plan not applicable)

## Steps
1. Cloned the Lenovo BIOS Auto-Patcher and ran it on my own `dump1.bin` to inject the unlock DXE drivers → `dump1_PATCHED.bin`.
2. Flashed the patched own-dump:
   ```
   sudo flashrom -p ch341a_spi -c "W25Q128.V" -w dump1_PATCHED.bin
   ```
3. On boot: 8 fast beeps in different tones and a black backlit screen (error 0285) — would not POST.
4. Reflashed the original `dump1.bin` to recover a bootable (still locked) machine.

## Why It Failed
The T470 enforces an Insyde/Phoenix H2O firmware signature check backed by Intel Boot Guard, whose root key is fused into the PCH (inside the CPU package). Patching the *current* BIOS breaks the signature, and Boot Guard refuses to run it. Re-signing or hex-editing the image cannot defeat a fused root key, and the dkade `resign_bios.py` script is hardcoded for the T540p layout and can't find the key structure on Kaby Lake — so the re-sign "surgery" plan is **not applicable** on this platform.

## What I Learned
- Boot Guard is a hardware root of trust — you can't out-edit a fused key.
- The 8-fast-beeps-different-tones + black screen is the signature-failure signature; 1 beep is a healthy POST.
- Always keep the verified original handy: reflashing `dump1.bin` immediately recovered the machine.

## Problems Encountered
- Accidentally ran `-r` instead of `-w` at one point and overwrote `dump1_PATCHED.bin` with a fresh read (caught it because the sha256 matched dump1.bin); rebuilt it by re-running the patcher.
- `libQt5Core.so.5` missing made the patcher report "dump1.bin is corrupted" — the real cause was a missing Qt5 library, fixed with `sudo dnf install qt5-qtbase`.
- `uefitool` wasn't in the Fedora repos; not needed — the patcher bundles its own UEFIReplace in `tools/`.
- `autopatch` had to be run as `sh autopatch ...` (not executable directly).
