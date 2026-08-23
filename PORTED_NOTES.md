# Ported notes (read me)

Corne config using [mctechnology17/zmk-config](https://github.com/mctechnology17/zmk-config)
as the base (its custom Corne shield + wireless/display setup), with
`config/corne.keymap` **replaced by a keymap ported from a MoErgo Go60 layout**.

## What changed vs. the base repo
- `config/corne.keymap` → the Go60 port (Colemak-DH base + Numbers layer done;
  all behaviors, macros, 13 combos carried over; other 30 layers are `&trans`
  placeholders to fill in). Go60 rows R2/R3/R4 map to the Corne's 3 rows.
- **RGB removed** — this Corne shield has no underglow LEDs, so every `&rgb_ug`
  was neutralized to `&none` (would not compile otherwise).
- `pointing.h` include dropped (unused).
- `build.yaml` trimmed to Corne-only targets (nice!view, nice!OLED, settings_reset).

## Secrets were REDACTED (repo is public)
The Go60 layout stored real credentials as keystroke macros. Those macros
(`mac_pass`, `dev_pass`, `migbyte_pass`, `apple_password`, and the phone/email
macros) now expand to `<&none>` — they type nothing. To use them, keep a
**local, un-pushed** copy of the keymap with the real values and build that
privately. **Rotate the previously-stored passwords** — they had been sitting
in plaintext in the Go60 editor and local file.

## Build & flash
Push triggers GitHub Actions → download firmware from the run's artifacts.
Flash the **pair matching your display** (`*_view` for nice!view, `*_oled` for OLED):
put each half in bootloader (double-tap reset), drag its `.uf2` onto `NICENANO`.
Flash `nice_settings_reset.uf2` to both halves first if they won't pair.
