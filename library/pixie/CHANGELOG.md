# Pixie changelog

## v0.2.6 keep the thread (2026-10-25)

- Bare `pixie` resumes the latest jsonl. `pixie --new` (`-n`) starts a blank session. C-s lists chats (enter load, n new).
- On quit, kur recaps 4–8 durable bullets into `memory.md` if the mouth is already up. Never blocks the glass; skips radio/secrets.
- Memory inject 6k, file 24k. LLM history is a 24k-char window (oldest tools drop first), not a magic 14 entries.
- Pixie mouth ctx **16384** in the house registry (GPU). 32k/40k stays a later CPU/KV-quant pass.

## v0.2.5 think + tool (2026-10-25)

- Each round's `<think>` is committed on the tool card. A tool call no longer wipes the thought.
- Verbose paints two tracks: `think 1`, `think 2`, … and `tool 1 · name`, `tool 2 · name`, … both stay in the chat.

## v0.2.4 TUI replies (2026-10-25)

- Clip bubbles that start above the viewport. A verbose think/tool taller than the pane no longer paints an empty chat (replies vanishing).
- Footer labels **C-v verbose** (pink when on). C-v works while she is busy. C-h stays help.
- Live JSON hide only when the speech *is* a tool object. A normal reply that mentions a tool stays visible.
- SmolLM sparkle runs on the worker thread so the TUI does not freeze on Done.

## v0.2.3 harness (2026-10-25)

- TUI glass: file cards teach C-o/C-l/C-n/C-p. Quiet tools show the tool name. Live JSON is `calling {name}…`, not a Pixie speech bubble.
- Typing: key Press only; SGR mouse CSI stripped from insert/paste. sudo cannot paint on the alternate screen (`setsid` + `SUDO_ASKPASS=/bin/false`).


- Tool results are `<tool_result>` on `role: user`, never llama `role: tool`. Harness nudges tagged `<harness>`.
- Chat 12 rounds; Build/Deep/Plan 20. `list_dir $HOME` / `.config` capped. Inspect Pixie in `~/pixie`.
- Chat/Build `execute_bash` uses `sh -c` so `&&` works. Plan stays argv allowlist.
- Plan writes cache only; overlay shows the full plan. Approve → Build in `~/pixie`.
- Keys: no bare letters. C-h help, C-o open, C-l look, C-v verbose, C-q quit, C-n/C-p files. Type `ok` without opening a file.
- SmolLM (kur :8081) writes the one-line sparkle. 8B stays JSON/facts.
- Host card: OS, zsh, CPU, GPU driver, RAM, term, session.
- Restored `faeOS/faeOSplan.md`; removed junk `~/.config/plan/*.sh`.
- Evidence: `cargo test --offline` 49 pass.

## v0.2.2 tools (2026-10-16)

- Native llama tool_calls: keep up to 4, not only the first.
- JSON Schema arrays stay arrays. History keeps every tool result in the window.
- `list_dir` and `grep_files` (in-process walk, no rg/grep binary). `edit_local_file` unique replace. Build gets `search_house`.
- `apply_patch` / `str_replace` alias to edit, not a full-file clobber.
- Evidence: `cargo test` 44 pass (no llama).

## v0.2.1 TUI feel (2026-10-16)

- Splash holds 1.5s (star poses ~350 ms). Wait lines rotate every 5s.
- Prompt box grows with wrapped text; left/right/home/end move the cursor.
- Prompt wrap is display-width (one wrap for height, paint, and cursor) so a second line no longer stomps the first.
- Content-sized chat bubbles (you right / Pixie left).
- Tab / Shift-Tab cycle Runes; digits `1`–`4` type into the prompt.
- Launch splash and wait spinner are frames of the house star (`assets/sigils/pixie.txt`).
- File cards: green `+` / red `−`, `l` look, `o` open in `$EDITOR`.
- Evidence: `cargo test` 38 pass (no llama).

## v0.2.0 rust familiar (2026-10-16)

- Pixie engine is Rust (`src/`, `./build.sh install --house`). Python `bin/pixie` retired.
- Host card from `/etc/os-release` + package manager so she stops inventing `apt` on Arch.
- Chat rune has no Magpie search (GPU + time). Deep uses light DDG HTML + `magpie browse --dump`.
- Barge-in, verbose think (`v` / `-v`), Plan bash allowlist, path gate on read and write.
- Evidence: `cargo test` 23 pass (no llama).

## v1.1.2 nap (2026-10-11)

- Numbered nap. Offline-first local AI agent stack, source-only kit.


## v0.1-stack (2026-09-26)

- Initial public stack: pixie + ask + imp + menagerie (ports 8080/8090/8082).
- Seeds sanitized (no host/user/PII). Models + libs stay on-machine.
- Evidence: unittest 41 pass; 1 pytest-only file (`test_imp.py`) needs pytest.
