# What to Upload to GitHub

## Upload (documentation only)
- `README.md` and the `01`–`06` phase docs
- `TOOLS.md`, `COMMANDS.md`
- Any sanitized photos of the setup (programmer, clip, chip) — optional
- A wiring/architecture diagram — optional

## Do NOT upload
- **`dump1.bin` / any BIOS dump** — contains your serial, UUID, and MAC address (and the archived one contains someone else's). These are private and are already excluded by `.gitignore`.
- `*_PATCHED.bin` images.
- Anything with real IPs, hostnames you don't want public, or credentials.

The included `.gitignore` already blocks `*.bin` so you can't accidentally commit a dump.
