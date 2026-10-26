# Scroll changelog

## v1.1.0 — staged Rust implementation (2026-10-26)

- Added standalone Rust TUI with embedded curriculum data, searchable app index and quick-jump.
- Reconciled Rust app pages with current faeOS app docs and command surfaces.
- Preserved PATH filtering, the shared six-hour cache format, name output, matching execution, runtime egg/Kur state, mouse input, and optional per-app ambience.
- Made cache replacement atomic and refresh/write failures visible; malformed or stale cache data is rebuilt.
- Kept the Python implementation and faeOS launcher unchanged as the rollback while integration and parity are verified.
- PTY check found Rust is not yet compatible with faeOS command-substitution launch: its non-TTY stdout path prints the book instead of drawing to `/dev/tty` and returning only the PATH selection.

## v1.0.0 1nk (2026-10-11)

- First stable number. Living book: 35 pages, Tab teaches, last leaf opens PATH. Read-only web reader on Grove.
