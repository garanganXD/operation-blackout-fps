# OPERATION BLACKOUT — Entry Dossier (threejs-fps-01)

## Concept
A round-based tactical first-person shooter in the spirit Counter-Strike made famous,
with an original map, original names, original art and synth audio. Two teams —
**VIPERS** (player) vs **SERPENTS** (5 bots). Accuracy matters more than speed:
movement multiplies weapon spread, first-shot accuracy is king, and bots have
human-like reaction delays before engaging.

## Map: Container Yard
An 80×60 m freight yard at dusk. 8 corrugated shipping containers (4 colorways,
procedural canvas textures with ribs, grime and rust streaks), a central watchtower
that blocks the long lane, perimeter walls, gradient night sky, fog for depth.
Sightlines are broken on purpose so peeking and holding angles matter.

## Weapons (buy menu, economy)
| Name | Class | Damage | RPM | Mag | Cost |
|---|---|---|---|---|---|
| SIDEARM | pistol | 22 | 300 | 12 | free |
| HORNET | smg | 18 | 780 | 30 | $1200 |
| RAPTOR | rifle | 30 | 600 | 30 | $2700 |
| LONGSHADOW | sniper | 95 | 50 | 5 | $4750 |
| KEVLAR VEST | armor | — | — | — | $650 |

Headshots deal 2.5× damage. Kills pay $300; round win $3250, loss $1400.
Match is first to 8 rounds.

## Systems
- Round flow: buy phase (12 s, freeze-time style) → live round (1:55) → round end → next round.
- Bots: LOS checks, distance-scaled hit chance, reaction-time delay (350–850 ms),
  center-biased patrol + strafing during engagements.
- Gunplay: per-weapon spread; spread ×2.2 while moving, ×2.5 while airborne —
  rewards stop-and-shoot tactics. Reload with R, auto-reload on empty mag.
- Viewmodel: procedural first-person weapon with recoil kick and walk bob.
- Audio: fully synthesized via WebAudio (gunshots w/ lowpass noise burst, hitmarker,
  kill chime, round-start motif). No external assets anywhere.

## Tech
- three.js 0.187.0, kit build copied byte-for-byte (game/vendor/), loaded via the
  single import map in game/index.html.
- No build step: game/ is plain ES modules + index.html, opens in desktop Chrome (WebGL 2).
- Procedural textures (CanvasTexture), no network requests, deterministic seedless logic.
- Node 22 entrypoint main.ts verifies the bundle and can serve the game (--serve).

## Files
- main.ts — Node 22 entry (bundle check + optional static server)
- game/ — playable static bundle (index.html, main.js, vendor/three.module.min.js, vendor/three.core.min.js)
- vendor/makefun-threejs.ts — kit three.js build, unchanged
- screenshots/ — 4 real in-engine captures of the running game
