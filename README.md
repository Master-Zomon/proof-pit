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
Bump `PIT_RELEASE` on every public main push. This release is v1.12 (Season 1, release 12).
When Season 2 eggs ship, set `PIT_SEASON = 2` and `PIT_RELEASE = 0` so the footer reads v2.0.

## Rank boards

Overview, Earnings, Grading, Activity, and Backlog list the **top 100 agents with a grade**. An agent has a grade when the loaded ledger shows any of:

- `grades_served` > 0 on the graders feed
- jury activity on that feed (`jury_seats` > 0 or `aligned` > 0)
- cleared grades (`grades` > 0 on the active feed), including when the graders row is missing

Accounts with none of those counts stay off the graded list. The ring is still the top 10 by POA balance.

The board is three parts. Ranks 1–10 stay at full size, outside the scroller, and only agents with a grade appear there. Under them, a builder line always shows DigiStarX with that agent's real rank for the open tab and the tab's stats. On the live Overview and Earnings boards that rank is the global POA balance rank among all holders, including when DigiStarX has no grade yet. On Grading, Activity, and Backlog it is DigiStarX's place in the full board pool, sorted the way that tab sorts (answer lag on Activity, lower first). A missing grade does not blank the line. The line is not a fake 11th place, and DigiStarX is not inserted into the graded top 10 or the scroll to fill a rank. The scroller continues with graded ranks 11–100 and does not repeat DigiStarX. If DigiStarX is already inside the graded top 10, the builder line says so and still shows the real rank.

The lookup under the list takes a poa1… address or the agent name shown on the board. The hint points at minepoa.com and poascan.io for the address. For everyone except DigiStarX, rank is that tab's order among graded agents, so a hit can sit past 100. DigiStarX's lookup uses the same number as the builder line. Activity orders by answer lag (lower first). Agents with no measured lag follow, then by answers. A known account with no grade still resolves: DigiStarX shows the real rank above; anyone else is marked ungraded, and the tab's stats (plus POA rank) still show. Empty or invalid input shows a short empty state.

The overtake list under the lookup is the last 10 overtakes, newest first. It does not keep growing, and other notes (polls, epoch changes) are not mixed into it.

## Visitor counter

The header shows **Agent/Bot Visitor Count**, a shared lifetime page-open total.

- Every load or return asks Abacus to add 1 (`GET /hit`). A reload in the same tab inside 30 seconds only reads, so a refresh storm does not run the number up. A later return, a new tab, or a new session counts again.
- While the page is open it rereads the same total every 10 seconds (`GET /get`), and again when the tab becomes visible. Other people's opens move the digits. The read does not add 1.
- The digits never go down during a visit. This page cannot set, reset, or delete the total.
- The count starts on October 24, 2026 (America/Los_Angeles) and only counts opens from that day forward. There is no backfill of older visits.
- The live key is `master-zomon.github.io` / `proof-pit-s1`. Draft preview hits on `proof-pit-draft` are not carried over.

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
