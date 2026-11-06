# Ether — network creature

**Role:** House radio + weave face: bluetooth, wifi, lan; `veil` VPN toggle; `bridge` phone-hotspot client; `ap` house Wi-Fi access point; `bt` motherboard Bluetooth; `status` one-shot; `about`.

**Status:** one engine at `~/ether`

## Implementation

- Canonical crate: `~/ether`. ELF: `~/.local/lib/faeos/ether`. Public command: `ether` (thin launcher `~/bin/ether`).
- `./build.sh install --house` from `~/ether` is the only writer of that ELF. `faeOS/ether` is a retired kit tree and must not overwrite it.
- The launcher execs the ELF for every verb. No Python `ether-face`. Multi-call names (`whisper`, `listen`, `status`) ride `ETHER_INVOKED_AS`.
- `nether` is an alias to the same house ELF (`~/bin/nether` execs `~/.local/lib/faeos/ether`). It must never `cargo run` `~/faeOS/ether`.
- Wisp stays a separate creature that execs this ELF for `ap` / `bt` and Siren for HEOS.
- Unicode chrome default: `PIXIE_UNICODE=1`. Sitting TUI keeps alt-screen + CRLF row endings.

## Current

- `ether` — TUI: w/l weave, s scan (top 5), n new, d remove, R restart (soft), r refresh, q quit
- `ether status` — one-shot report (bt/wifi/lan)
- **Conjuring** — active downloads in the model dir, `~/Downloads`, `/tmp` (no pacman cache dump)
- `ether net` — connectivity diagnosis (IPv4 HTTPS for archive.org etc.)
- `ether veil on|off` — VPN toggle (`vpn`); still nmcli this cut
- `ether bridge` — phone hotspot CLIENT boot fallback (nmcli); env `~/.config/ether/netherweave.env` (chmod 600, never committed)
- `ether ap on|off|status|wps|nat` — house Wi-Fi AP: nl80211 START_AP + WPA2-PSK 4-way + DHCPv4 `192.168.42.1/24` + WPS PBC; Bulwark weave for optional NAT. No hostapd. No NetworkManager on the AP path.
- `ether bt status|scan|pair|connect|disconnect|forget` — BlueZ D-Bus (`org.bluez`); pairable only during scan. No bluetoothctl.
- `ether speakers` — `siren heos --json` (Siren owns :1255)
- `whisper ether` / `listen ether` — BT audio: ANC headphone / JBL Go 3 (each sets default sink)

## House AP vs phone bridge

- **House AP** (`ether ap`): the box SERVES Wi-Fi for lanterns/speakers. Raw nl80211 on `wlp41s0`. NetworkManager is never started or consulted for the house SSID.
- **Phone bridge** (`ether bridge`): the box CLIENTS to a phone hotspot when no real link is up. Still nmcli; left as-is on the phone-client path.
- Credentials: `~/.config/ether/ap.env` (0600) with `ETHER_AP_IFACE` / `ETHER_AP_SSID` / `ETHER_AP_PSK`; fallback `~/.config/wisp/ap.env`. The PSK is never printed — status only says `psk set`. `ap status` prints the gateway only while the daemon is alive (`ip idle` otherwise).
- Privilege: interactive `sudo -E ~/.local/lib/faeos/ether ap on` at the box, or user-installed caps. The sitting TUI never collects a sudo password.
- Wisp talks to the AP only through `ether ap …`.

## Next

- [ ] Wifi networks saved/prioritized; reconnect on boot
- [ ] LAN: show interfaces/IPs/mounts
- [ ] Bridge: wizard to write netherweave.env
- [ ] Profile "weaves" editor (named network setups)
- [ ] Whisper/listen via Pipewire without a BlueZ connect race

## Notes

- `ia.py` (Internet Archive engine) moved OUT of ether — ether is networking only.
- Tests must not raise a live AP or run a live BT inquiry.
