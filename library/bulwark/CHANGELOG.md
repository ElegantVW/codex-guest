# Bulwark changelog

## unreleased

- `bulwark router weave --iface <lan> --net <cidr>` / `unweave --net <cidr>`:
  extra LAN NAT (house AP `192.168.42.0/24`) remembered in `router/weaves.json`
  and rebuilt with speaker LAN on the next sync. No WAN → weave remembered,
  NAT waits. Ether asks; Bulwark still owns nf_tables.
- Masquerade uses kernel expr `masq` (`nft_masq`). `nat` type MASQUERADE is
  EOPNOTSUPP. Router batch failures stay router-voiced (not Aegis).

## v0.9.9 m4g1c_gl4d14t0r (2026-10-11)

- Numbered ward. Personal host only; not audited, no nation-state claims. Cargo 0.9.9.


## v0.1-house (2026-09-26)

- House (`house/`) + glass (`glass/`) workspace in one repo. Seal lock/greeter
  moves in from faeOS; privilege/state/units stay separate.
- Honest posture: missing/unknown wall is never SAFE.
- Evidence: `cargo test` — house 9 + glass 2 pass.
- Holes: cold professional review (path D) not started; see `house/docs/ADVERSARIAL.md`.
