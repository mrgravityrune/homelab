# 5. Patching, Injecting & Successful TPM Unlock

## Steps
1. Patched the archived dump (injects two DXE drivers — BootOption + LenovoTranslateService — into the NVRAM volume at offset 0x800000):
   ```
   sh autopatch t470_Orig.bin
   ```
   → `t470_Orig_PATCHED.bin`
2. Flashed the patched archived image:
   ```
   sudo flashrom -p ch341a_spi -c "W25Q128.V" -w t470_Orig_PATCHED.bin
   ```
3. Booted it; the injected driver ran the unlock sequence on screen:
   - "Press Space..."
   - "Press Space once more..."
   - "TPM certificate changed. Turn it off"
4. Powered the machine off at that prompt.

## Why
The injected DXE drivers expose the SVP-clear routine. The older image boots because it isn't blocked by strict Boot Guard enforcement, and the "TPM certificate changed" message confirms the patched image booted and executed the unlock path.

## What I Learned
- A patched *older* image boots where a patched current image black-screens — that's the whole trick.
- The on-screen "Press Space / TPM certificate changed" prompts are the injected unlock driver doing its job.

## Problems Encountered
- **LIBUSB_TRANSFER_OVERFLOW** during the write — flaky USB/clip contact. Reseated the clip and retried until flashrom reported "verified."
