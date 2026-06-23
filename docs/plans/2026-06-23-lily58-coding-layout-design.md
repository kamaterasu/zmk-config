# Lily58 (54-key) Coding Layout — Design

Date: 2026-06-23

## Goal
Optimize a 54-key Lily58 (nice_nano_v2, nice_view) for writing + coding on Linux.
All-language coding: C/JS/TS, Python, web, shell. Ease of learning prioritized
over theoretical max ergonomics.

## Hardware
- Shield: `lily58_left` / `lily58_right` (firmware = 58 positions).
- Physical board = 54 keys: 6x4 grid + 3 thumbs per half.
- 4 firmware positions are unpopulated -> `&none`:
  - inner bottom keys: positions 42, 43
  - outermost thumb each side: positions 50, 57
- The 3 present thumbs map to the inner thumb positions (51/52/53 left,
  54/55/56 right). **Verify after flash** — if a thumb is dead, the missing
  thumb is a different position; shift the `&none`.

## Decisions
- **Base alpha: QWERTY** (no retrain; layers + HRM deliver most of the win).
- **Home-row mods**, standard GACS order, opposite-hand triggered:
  - Left: A=GUI, S=Alt, D=Ctrl, F=Shift
  - Right: J=Shift, K=Ctrl, L=Alt, ;=GUI
- 4 physical rows -> dedicated **number row** on the base layer.

## Layers
0. **BASE** — QWERTY + HRM + number row.
1. **NAV** (hold left SPACE or right BSPC) — right-hand arrows + Home/End/PgUp/PgDn;
   left-hand plain mods + undo/cut/copy/paste for one-handed select.
2. **SYM** (hold left TAB or right ENTER) — full coding symbol set across both
   hands; left home row keeps mods for symbol+mod combos.
3. **FUN** (tri-layer: NAV + SYM held together) — F1–F12, BT select/clear,
   media, ext_power, `&studio_unlock`, bootloader, sys_reset.

## Thumbs (3/side)
- Left: GUI · SPACE(hold→NAV) · TAB(hold→SYM)
- Right: ENTER(hold→SYM) · BSPC(hold→NAV) · DEL

## HRM tuning
hold-tap, `balanced` flavor: tapping-term 200ms, quick-tap 175ms,
require-prior-idle 150ms, hold-trigger-on-release, opposite-hand
`hold-trigger-key-positions`. Reduces misfires during fast rolls.

## Combos
- G + H -> `&studio_unlock` (unlock ZMK Studio without entering FUN layer).

## ZMK Studio
`CONFIG_ZMK_STUDIO=y` already set. Unlock via the G+H combo or FUN-layer key.

## Build / flash
Commit + push -> GitHub Actions builds both halves -> download `.uf2` ->
bootloader (double-tap reset) -> drag-drop each half.

## Follow-ups / risks
- Verify thumb position mapping after first flash (see Hardware).
- HRM timing may need per-finger tuning if pinky mods misfire.
- Optional later: bracket-pair macros/combos, Colemak toggle layer.
