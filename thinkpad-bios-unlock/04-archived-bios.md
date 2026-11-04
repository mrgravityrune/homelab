# 4. Archived (Older) BIOS from Badcaps

## Steps
1. Sourced an archived 2018-era locked T470 BIOS dump from the Badcaps forum.
2. Verified the file was exactly 16,777,216 bytes (16MB).
3. Copied it to a clean filename (the download had spaces and a double dot, `t470 Orig..bin`):
   ```
   cp ~/Downloads/"t470 Orig..bin" t470_Orig.bin
   ```

## Why
Older T470 firmware predates the strict Boot Guard signature enforcement, so a patched *older* image can actually boot and run the unlock routine where the current firmware can't. This is the route that replaced the dead-end re-sign plan.

## What I Learned
- The platform's signature enforcement tightened over firmware revisions — an older archived image is a viable bypass path.
- Watch out for odd filenames: quote the path or rename to avoid "file not found."

## Problems Encountered
- The download's real name had spaces and two dots, so `cp ~/Downloads/t470_Orig.bin .` failed with "No such file or directory" until I quoted the actual filename.
- **Caveat:** this archived dump carries someone else's serial/UUID/MAC, which is exactly why restoring my own `dump1.bin` at the end is mandatory.
