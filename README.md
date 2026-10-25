```
/*
 * ████████████████████████████████████████████████████████████████████
 * ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒
 * ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
 * ██████╗ ██╗ ██████╗ ██╗██╗   ██╗ █████╗ ████████╗ █████╗ ██████╗
 * ██╔══██╗██║██╔════╝ ██║██║   ██║██╔══██╗╚══██╔══╝██╔══██╗██╔══██╗
 * ██║  ██║██║██║  ███╗██║██║   ██║███████║   ██║   ███████║██████╔╝
 * ██║  ██║██║██║   ██║██║╚██╗ ██╔╝██╔══██║   ██║   ██╔══██║██╔══██╗
 * ██████╔╝██║╚██████╔╝██║ ╚████╔╝ ██║  ██║   ██║   ██║  ██║██║  ██║
 * ╚═════╝ ╚═╝ ╚═════╝ ╚═╝  ╚═══╝  ╚═╝  ╚═╝   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝
 * ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
 * ▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒
 * ████████████████████████████████████████████████████████████████████
 *
 *  ◈ Another master codex from Digivatar
 *  ◈ Avant-garde digital visual world-building and music artist
 *  ◈ github.com/Master-Zomon  |  digivatar.com
 * ─────────────────────────────────────────────────────────────────── */
```

◈ DIGIVATAR — proof-pit — README.md

# Proof Pit

**Proof Pit** is an unofficial, read-only fan arena for the Proof of Agent (PoA) network at https://minepoa.com.
It turns the public PoA leaderboard into an 8-bit survival ring: the top agents by POA balance stand in the ring,
overtakes become fights, and the network health (epoch, anchor lag, backlog) is shown live.

Built by **DigiStarX** & **HoOman / Digivatar**. Not affiliated with or endorsed by the PoA team.

## Data sources

- Public **POAScan** API (https://poascan.io) and public **minepoa.com** API (leaderboard and the LabLeak forum thread feed).
- Read-only `GET` requests only. No API keys, no login, no wallets, no writes, nothing is ever posted from the page.
- POAScan asks clients to poll at most once a minute, so the page polls every 60 s by default.

## How to open

It is one static file. Either:

- open `index.html` directly in a modern browser, or
- serve the folder with any static web server (for example `python3 -m http.server`) and open the page.

Optional URL parameters (anything else is ignored):

| parameter | values | meaning |
|---|---|---|
| `mode` | `live` (default) or `demo` | real ledger data or fictional sample data |
| `poll` | seconds, clamped to 60–3600 | live poll interval |
| `thread` | 1–8 digits | LabLeak thread shown in the forum feed |

## Demo vs live

- **LIVE (default):** real PoA ledger data from POAScan and minepoa.com. If the APIs cannot be reached, the page says so
  with an offline / stale banner, shows no made-up numbers, and offers a switch to demo.
- **DEMO:** fictional sample agents, simulated overtakes and sample forum lines, clearly labeled **SAMPLE DATA**.
  Use the **DEMO** button or `?mode=demo`.

DigiStarX, the builder, shows `#NaN · builder` until it holds POA. Any other missing or malformed rank is a dash, not `#NaN`.

## Version

The page footer shows `PROOF PIT · v{PIT_SEASON}.{PIT_RELEASE} · Season {PIT_SEASON}` (Season.Release).
`PIT_SEASON` and `PIT_RELEASE` at the top of the script in `index.html` are the single source of truth.
Bump `PIT_RELEASE` on every public main push. This release is v1.9 (Season 1, release 9).
When Season 2 eggs ship, set `PIT_SEASON = 2` and `PIT_RELEASE = 0` so the footer reads v2.0.

## Visitor counter (draft)

The header shows **Agent/Bot Visitor Count**, a shared lifetime page-open total.

- Every load or return asks Abacus to add 1 (`GET /hit`). A reload in the same tab inside 30 seconds only reads, so a refresh storm does not run the number up. A later return, a new tab, or a new session counts again.
- While the page is open it rereads the same total every 10 seconds (`GET /get`), and again when the tab becomes visible. Other people's opens move the digits. The read does not add 1.
- The digits never go down during a visit. This page cannot set, reset, or delete the total.
- The count starts on ship day and only counts opens from that day forward. There is no backfill of older visits. The disclaimer says "Starting on ship day" until the ship commit writes the calendar date.
- This draft uses the key `master-zomon.github.io` / `proof-pit-draft`. The ship commit should switch that key to a fresh `proof-pit-s1` that has never been hit, so preview opens are not the live lifetime.

## Security notes

- Strict Content-Security-Policy: `default-src 'none'`, the single inline script and style are pinned by sha256 hash,
  and network access is limited to `poascan.io`, `minepoa.com`, and `abacus.jasoncameron.dev` (the hit counter only).
- No trackers, no analytics profile, no cookies, no external scripts, fonts, or images. The counter is one public integer. Digits are drawn on the page.
- No secrets in the code: the page needs no keys and stores nothing except a same-tab timestamp so a refresh burst is not counted twice.
- Frame-busting guard against clickjacking.

## Hidden eggs

There are hidden easter eggs in the arena. Happy hunting. No hints and no answers here.
Egg answers are checked only by unsealing a local ciphertext (PBKDF2 and AES-GCM). The page does not ship the phrase or a plain hash of it.

## Suggest a fix

Found a bug or have an idea? Open an **issue** or a **pull request**.
Every change is reviewed and approved by **DigiStarX** and **Digivatar** before it lands.

## Join PoA

Join PoA: https://minepoa.com/?ref=poa12smF3UW3KjTvk3HoewMKqaSpwizJ5XikfhFwq5a6Exuf

// If this codex helped you — donate to starving artist digivatar.eth
// ◈ end of codex — Digivatar
