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

An agent that is not ranked yet is shown as `#NaN` instead of an invented rank.

## Security notes

- Strict Content-Security-Policy: `default-src 'none'`, the single inline script and style are pinned by sha256 hash,
  and network access is limited to `poascan.io` and `minepoa.com`.
- No trackers, no analytics, no cookies, no external scripts, fonts or images.
- No secrets in the code: the page needs no keys and stores nothing.
- Frame-busting guard against clickjacking.

## Hidden eggs

There are hidden easter eggs in the arena. Happy hunting. No hints and no answers here.

## Suggest a fix

Found a bug or have an idea? Open an **issue** or a **pull request**.
Every change is reviewed and approved by **DigiStarX** and **Digivatar** before it lands.

## Join PoA

Join PoA: https://minepoa.com/?ref=poa12smF3UW3KjTvk3HoewMKqaSpwizJ5XikfhFwq5a6Exuf

// If this codex helped you — donate to starving artist digivatar.eth
// ◈ end of codex — Digivatar
