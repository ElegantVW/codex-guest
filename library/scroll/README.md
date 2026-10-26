# Scroll — living book 📜

![Scroll hero](assets/hero/scroll.svg)

> **one page per app, Tab teaches faeOS — the last leaf opens PATH**

Scroll is how the house teaches itself. Each page is one creature: who she
is, how to live with her (keys included), which spells to type, and footer
runes that cast her. The last leaf is PATH — every tool on `$PATH`, printed
to your prompt so you may finish the line yourself.

For: faeOS onboarding, one page per app. The Rust build is standalone; no
Pixie or faeOS Python libraries are required. Python remains available as the
unchanged fallback while Rust parity is verified.

## Look

![Scroll summon page](assets/screenshots/scroll-summon.png)
![Scroll pixie page](assets/screenshots/scroll-pixie.png)

```
 ___
|---|
|---|
|___|
```

## Status

The book has 35 static pages plus the egg leaf (`hermetic` or `kur`, based on
runtime hatch state) and the virtual PATH leaf: 37 leaves in Tab order.

The staged Rust app is `scroll-rs`; the existing Python `scroll` executable
and `scroll_pages.py` are intentionally preserved as the fallback. Until the
faeOS launcher is deliberately switched, choose `scroll-rs` explicitly.

App information for Rust lives in `data/pages.json`. Keep it in curriculum
order with `src/model.rs`'s runtime egg pages; while the Python fallback is
retained, mirror curriculum updates in `scroll_pages.py` too.

## Use

```bash
cargo build --release
./target/release/scroll-rs              # open the book on page one
./target/release/scroll-rs --path       # PATH leaf (same as summon)
./target/release/scroll-rs list         # every page as text (for grepping)
./target/release/scroll-rs -x <cmd>     # run a PATH match without the TUI
```

Keys: `Tab` / `Shift-Tab` pages · `1–9` runes · `j/k` scroll · `g`/`G` jumps ·
`Ctrl-F` searchable app index / quick-jump · `m` ambience · `q` quit.
On PATH, type to filter, use arrows or `j/k`, then Enter to print the selected
command name. Double-click prints it too. `--refresh` refreshes the shared
six-hour PATH cache.

## Build and parity

Rust uses a standalone Cargo manifest and does not import Pixie internals.
Egg state is read from the standard faeOS egg JSON files. Ambience is optional:
it needs the chiptune track and `mpv`; its IPC socket is kept in
`$XDG_RUNTIME_DIR` (or `~/.cache/faeos/runtime` if unset), never Siren's socket.

```bash
cargo fmt --check
cargo test
cargo build --release
python3 -m pytest tests/ -q
```

Rust tests cover page inventory/content shape, runtime egg states, navigation
and search, PATH scanning/filtering/cache expiry, and rune argument parsing.
The legacy Python fallback still requires its existing faeOS `bin/` libraries.

## License

MIT — see [LICENSE](LICENSE).
