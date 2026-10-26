# Scroll — living book (page carousel)

Canonical repo: `ElegantVW/scroll`. faeOS keeps only a thin launcher.

**Role:** One **page per app**; Tab teaches faeOS; last leaf is PATH (print to prompt).
**Status:** 35 static pages + egg leaf + PATH leaf = 37 leaves (switcher + tv added 2026-09-28).

## Navigation
- **Tab / Shift-Tab** — next / previous page (curriculum order)
- **1–9** — cast footer runes (**run** the spell)
- **g / G + digit** — vim-style page jump (11–20 / 21–30)
- **j/k · wheel** — scroll within a long page
- **PATH leaf** — filter · Enter → print name for shell `print -z`
- Layout: near-fullscreen panels with small margin so box edges show

## Curriculum
Python fallback order is in `CURRICULUM` in `scroll_pages.py`; Rust order and
app/command copy lives in `data/pages.json`. Both end with **switcher**, **tv**,
then the **Sealed Leaf** (or **Kur** if hatched), then **PATH**. Keep both
copies aligned until the faeOS launcher migration is approved. Appending new
pages at the end keeps existing g/G jump positions stable.

## Rust staging
- Build with `cargo build --release`; launch `target/release/scroll-rs`.
- `Ctrl-F` opens the searchable app index and quick-jump.
- The Rust app is self-contained: it reads faeOS egg state directly and
  optionally uses its own mpv ambience socket. It does not import Pixie
  internals or edit faeOS shared libraries.
- The Python `scroll` and `scroll_pages.py` files remain the untouched fallback
  until Rust parity is verified. No shared launcher has been switched yet.

## Sealed Leaf / egg
- Story: an **egg in the Menagerie** to hatch; points at **`murmur`** (babbling glass).
- No hand-holding, no true name, no solve path in docs.
- Leaf turns only after the player completes hatch tasks (not from murmur alone).

## Runtime deps (house libs, stay in faeOS)
`fae_termart` (frames), `fae_egg` (hatch state), `fae_ambience` (book music).
`scroll` puts its own dir first on `sys.path`, then `~/bin`.
