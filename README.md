# YUNG's Better Nether Fortresses — a Horizon port

**YUNG's Better Nether Fortresses** is a Minecraft mod. A complete overhaul to vanilla Nether Fortesses!. This repository is a **port of it to [Horizon](https://github.com/horizon-rust/horizon)**, the Rust engine for Minecraft Java 26.3. It carries the complete source of the port plus the content files it ships, and installs as a single `.hmod` package.

Upstream: [YUNG-GANG/YUNGs-Better-Fortresses](https://github.com/YUNG-GANG/YUNGs-Better-Fortresses) — licence **LGPL-3.0-only**.

| | |
|---|---|
| Upstream mod | YUNG's Better Nether Fortresses ([source](https://github.com/YUNG-GANG/YUNGs-Better-Fortresses)) |
| Ported to | Horizon 0b14f8a, Minecraft Java 26.3, mod API `0.2` |
| Package | `betterfortresses.hmod` (install it with the Horizon launcher) |
| Licence | **LGPL-3.0-only** — the upstream mod's licence; see [Licence and credit](#licence-and-credit) |

## What this port implements

### What it implements

- `betterfortresses:fortress`, a Nether fortress of a keep, halls, bridges and
  blaze towers, assembled by the pin's YUNG's-API jigsaw (`yungsapi:yung_jigsaw`)
  with its own terrain kernel.
- Its structure set (spacing 30 / separation 20, a 10-chunk exclusion zone around
  vanilla's nether complexes) so it generates in the Nether next to vanilla's
  fortresses.
- 167 of the jar's 169 templates, the nine chest loot tables and the three lang
  files.

## Not yet ported

- **Vanilla fortresses are not disabled.** The mod's
- **The six Java processors are not carried** (pillars under bridges and keeps,
- **Element `condition`s are not run** (92 in the jar: 90 `yungsapi:depth`,
- **Element `modifiers` are not run** (8 elements).
- **Structure `spawn_overrides` are not read for mod structures.** The pin's
- **`size` 20 instead of 46** (patch 3): the fortress is shallower than the
- **The `yungsapi:` structure tags are not carried** (`remove_basalt_columns_feature_in`,
- **`data/minecraft/advancement/nether/find_fortress.json` is not carried**: a

## Installing

1. Install the [Horizon launcher](https://github.com/horizon-rust/horizon/releases) (0.2.70 or newer).
2. Add `betterfortresses.hmod` to the instance's mods.
3. The package is pinned to a specific Horizon build; the launcher checks that pin.

## Licence and credit

YUNG's Better Nether Fortresses was created by its upstream authors; the code, models and assets in the original mod
remain theirs and are used here under **LGPL-3.0-only**. The Rust in this repository is a clean-room
rewrite for Horizon, not a translation of the original source.

- `LICENSE` — the upstream licence text.
- `LICENSE-NOTICE.md` — what this port carries and where it came from.
- The upstream project: https://github.com/YUNG-GANG/YUNGs-Better-Fortresses

## Technical details

```
horizon-mod.toml   package manifest (id, version, api, [native] pin)
Cargo.toml         the crate; depends on `horizon-mod-api` from the fetched SDK
src/               lib.rs (the one `impl Hooks`), runtime.rs (pure logic + tests), glue
assets/ data/      the content the package ships
tools/             content generators and the e2e scenario
```

- Build: `cargo horizon-mod build` (packages; it does not compile against the game).
- Test: `cargo test`, `cargo clippy --all-targets -- -D warnings`.
- In-game: `ports/tools/launcher-game.sh run betterfortresses` in the campaign tree, or install the
  `.hmod` and play; the harness scenario is `tools/e2e.sh`.

This repository is generated from the campaign's port at `ports/betterfortresses/`; the port's own
`notes.md` is the full record (decisions, traps, evidence).
