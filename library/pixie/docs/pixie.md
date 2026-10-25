# Pixie — local AI assistant

**Role:** Local AI familiar with tools (files, shell, house spells), fully offline. `pixie` / `pixie "…"`; llama-server on `127.0.0.1:8080` via `menagerie`.

**Status:** Rust engine (v0.2.5). Python `bin/pixie` retired. Menagerie / ask / imp stay Python in this pass.

## Current

- Engine: Rust ELF `~/.local/lib/faeos/pixie`, thin launcher `~/bin/pixie`. Build: `./build.sh install --house`.
- Model: Huihui Qwen3-8B abliterated v2 Q4_K_M on this box (menagerie). CPU default (`-ngl 0`).
- Bare `pixie` → bubbled TUI, Runes **Tab / Shift-Tab** (Ctrl-R alias):
  - **Chat** (12) — house, remember, search_house, wiki, list_dir, grep_files, bash (`sh -c`, confirm), files, systemd, mail. **No Magpie search**.
  - **Deep** (20) — light DDG HTML `web_research`, `fetch_web_page`, wiki, search_house, list_dir, grep_files. Never `menagerie ensure magpie`.
  - **Build** (20) — inspect `~/pixie` first; `edit_local_file` / `write_local_file`; search_house.
  - **Plan** (20) — read-only bash allowlist + inspect + `write_plan` (cache only). Overlay shows the plan. y → Build in `~/pixie`.
- Tool results are tagged `<tool_result>` (not llama `role: tool`). SmolLM on kur `:8081` adds the cute line; the 8B does JSON and facts.
- You/Pixie sit in content-sized bubbles (right blush / left pink). House star splash on launch; wait spinner is the star’s own rows (`*` `\|/` `---*---` `/|\`), not a generic ticker. Prompt box grows with wrapped text (same wrap for height, paint, and cursor).
- File cards: green `+` / red `−` on writes; **C-l** look · **C-o** open · **C-p / C-n** cycle. **C-h** help · **C-v** verbose · **C-q** quit. Bare letters always type.
- Host card every turn (OS, zsh, CPU, GPU, RAM, term, session). House pack in `config/pixie/context/`.
- Barge-in: type + Enter aborts the in-flight reply. Quiet hides `<think>` but jsonl stores it.
- `look` stub: eye still sleeping (vision Pass 2).
- `menagerie ensure pixie` on demand. Quit keeps the server warm unless `PIXIE_STOP_LLM_ON_EXIT=1`.

## Files

| Path | Role |
|------|------|
| `src/` | Rust engine |
| `scripts/pixie` | launcher |
| `build.sh` | release + install |
| `config/pixie/spells.toml` | kit spellbook |
| `config/pixie/context/` | always-on house pack |
| `~/.local/share/pixie/memory.md` | durable memory |
| `~/.cache/pixie/sessions/*.jsonl` | transcripts |

## Later

- **#4 Vision** — menagerie app `pixie-eye`, `look` via Reflection shots.
- **#5 Image gen** — Imp / later menagerie app.
- **Pass 3 Menagerie** — Rust steward in `~/menagerie`. llama-server is a guest. Pixie no longer sends OpenAI `tools` on the wire; house JSON parser owns calls.

## Tests

`cargo test` (no llama). Gate: host-card Arch vs Debian, Chat has no `web_research`, Plan refuses `rm`, path gate, spells, think strip.
