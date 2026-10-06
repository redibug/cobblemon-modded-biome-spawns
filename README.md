# Mel's Cobblemon Modded-Biome Spawns

A Cobblemon spawn datapack that adds wild Pokémon spawns to biomes from
three worldgen mods that ship with **no Cobblemon spawns of their own**:

| Mod | Biomes covered |
|---|---|
| **Dappled Up** (`dappled_up`) | Dappled Forest |
| **Blooming Biosphere** (`mr_blooming_biosphere`) | Autumnal Forest, Chaparral, Marsh, Oak Woodland, Rainforest, Snowy Cherry Grove, Tidepools |
| **Abyssaline Nether** (`mr_abyssaline_nether`) | Basalt Garden, Crimson Steppe, Distorted Wastes, Infected Valley, Nether Jungle, Overgrown Wastes, Scarlet Undergrowth, Twisting Thicket |

16 spawn files, 256 spawn entries — every biome has at least 4 Pokémon in
**each** rarity bucket (common / uncommon / rare / ultra-rare). Evolved
forms always sit a bucket above their base forms. Everything is **additive**
— it lives in its own `melspawns` namespace, so it never overrides or
blocks Cobblemon's default spawns (or other addons' files).

## Highlights

- **Dappled Forest** gets a spooky-autumn set: **Pumpkaboo** (common,
  day + night), **Phantump** (common, night), **Mimikyu** (rare), **autumn
  Deerling** (uncommon), plus Seedot, Shroomish, Pineco, Hoothoot (night)
  and Teddiursa — with Trevenant, Gourgeist, Nuzleaf, Noctowl, Shiftry,
  Ursaring and Forretress in the higher buckets.
- Blooming Biosphere biomes get themed sets (Wooper/Psyduck/Lotad in the
  Marsh, Snorunt/Swinub/Snover in the Snowy Cherry Grove, Krabby/Corphish/
  Wingull in the Tidepools, Tropius/Carnivine in the Rainforest, …).
- Abyssaline Nether biomes get fire/ghost sets (Vulpix, Growlithe, Houndour,
  Slugma, Numel, Torkoal, Gastly, Haunter, Litwick, Lampent, Magmar … up to
  Gengar, Chandelure, Magmortar and Typhlosion in ultra-rare).

## Install

**As a datapack (per-world):** drop this folder (or the zip) into
`<world>/datapacks/`.

**In a modpack (every world):** use the [Open Loader](https://modrinth.com/mod/open-loader)
mod and drop the folder/zip in `resources/openloader/datapack/`
(or `config/openloader/datapack/` on older versions) — it auto-applies to
every new world.

Cobblemon reads spawn files at world load — **`/reload` does NOT pick up
spawn changes**. Quit to the main menu and re-enter the world after editing.

## Test

In-game, stand in the biome and run `/checkspawns <bucket>`
(e.g. `/checkspawns rare`) — your new spawns should be listed.

## Tweaking

Spawn tables live in `data/melspawns/spawn_pool_world/<mod>/<biome>.json`.
Each entry is one Pokémon:

```json
{
  "id": "gastly-distorted_wastes-common",
  "pokemon": "gastly",
  "presets": ["natural"],
  "type": "pokemon",
  "spawnablePositionType": "grounded",
  "bucket": "common",
  "level": "6-31",
  "weight": 18,
  "condition": { "biomes": ["abyssaline:distorted_wastes"] }
}
```

- `bucket`: `common` / `uncommon` / `rare` / `ultra-rare`
- `weight`: relative chance *within* the bucket (0.1–10ish is normal)
- `condition.biomes`: biome IDs or tags (`#cobblemon:is_forest`, …)
- `condition.timeRange`: `"day"` / `"night"` / `"twilight"`
- `spawnablePositionType`: `grounded` (land), `seafloor` (underwater,
  pair with `"presets": ["water"]`), `surface` (water/lava surface),
  `underwater`, `lava`
- Forms use a space: `"pokemon": "deerling autumn"`
- Files are organized per-mod in subfolders — delete a mod's folder if you
  remove that mod.

Biome IDs were verified by inspecting the actual mod jars (Cobblemon 1.8.1,
MC 1.21.1, NeoForge). All 125 species IDs were verified against Cobblemon's
species data. Spawn JSON schema matches Cobblemon's `spawn_pool_world` format.

Regenerate everything with `python3 generate.py` (source of truth for the
tables lives at the top of that script).
