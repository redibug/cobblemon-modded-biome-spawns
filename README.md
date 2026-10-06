# Mel's Cobblemon Modded-Biome Spawns

A Cobblemon spawn datapack that adds wild Pokémon spawns to biomes from
worldgen mods that ship with **no Cobblemon spawns of their own**:

| Mod | Biomes covered |
|---|---|
| **Dappled Up** (`dappled_up`) | Dappled Forest |
| **Blooming Biosphere** (`mr_blooming_biosphere`) | Autumnal Forest, Chaparral, Marsh, Oak Woodland, Rainforest, Snowy Cherry Grove, Tidepools |
| **Abyssaline Nether** (`mr_abyssaline_nether`) | Basalt Garden, Crimson Steppe, Distorted Wastes, Infected Valley, Nether Jungle, Overgrown Wastes, Scarlet Undergrowth, Twisting Thicket |
| **Enderscape** (`enderscape`) | Celestial Grove, Corrupt Barrens, Magnia Crags, Veiled Woodlands, Void Depths, Void Skies, Void Sky Islands |

23 spawn files, 368 spawn entries — every biome has at least 4 Pokémon in
**each** rarity bucket (common / uncommon / rare / ultra-rare). Evolved
forms always sit a bucket above their base forms. Everything is **additive**
— it lives in its own `melspawns` namespace, so it never overrides or
blocks Cobblemon's default spawns (or other addons' files).

## Highlights

- **Dappled Forest** gets a spooky-autumn set: **Pumpkaboo** (uncommon,
  day + night), **Phantump** (uncommon, night), **Mimikyu** (rare),
  **Hoothoot** (common, night), **autumn Deerling** (common), plus Seedot
  and Shroomish — with Trevenant, Gourgeist, Nuzleaf, Noctowl, Shiftry,
  Ursaring and Forretress in the higher buckets.
- Blooming Biosphere biomes get themed sets (Wooper/Psyduck/Lotad in the
  Marsh, Snorunt/Swinub/Snover in the Snowy Cherry Grove, Krabby/Corphish/
  Wingull in the Tidepools, Tropius/Carnivine in the Rainforest, …).
- Abyssaline Nether biomes get fire/ghost sets (Vulpix, Growlithe, Houndour,
  Slugma, Numel, Torkoal, Gastly, Haunter, Litwick, Lampent, Magmar … up to
  Gengar, Chandelure, Magmortar and Typhlosion in ultra-rare).
- **Enderscape** biomes are **Ultra Beast territory**: all 11 UBs are in
  base Cobblemon — Nihilego in the Corrupt Barrens, Pheromosa/Xurkitree in
  the Celestial Grove, Kartana/Buzzwole in the Veiled Woodlands, Stakataka
  in the Magnia Crags, Guzzlord/Naganadel/Blacephalon in the Corrupt Barrens
  and Void Depths, **Celesteela** soaring in the Void Skies, **Poipole** in
  the Corrupt Barrens, plus Necrozma, Lunala, Solgaleo, Marshadow and the
  Tapus in ultra-rare. All UBs spawn with 3 perfect IVs. The common/uncommon
  pools are filled with end-flavored base mons (Lunatone, Solrock, Elgyem,
  Sigilyph, Gothita line, Minior, …).

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
- Forms use a space: `"pokemon": "deerling autumn"`. Extra specs like
  `"nihilego min_perfect_ivs=3"` also work.
- Files are organized per-mod in subfolders — delete a mod's folder if you
  remove that mod.

Biome IDs were verified by inspecting the actual mod jars (Cobblemon 1.8.1,
MC 1.21.1, NeoForge). All species IDs were verified against Cobblemon's
species data plus the AllTheMons datapack's `species_additions`. Spawn JSON
schema matches Cobblemon's `spawn_pool_world` format.

Regenerate everything with `python3 generate.py` (source of truth for the
tables lives at the top of that script).
