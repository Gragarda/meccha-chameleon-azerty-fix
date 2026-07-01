# MECCHA CHAMELEON — AZERTY Keyboard Fix

MECCHA CHAMELEON hardcodes WASD for movement and has no key rebinding option anywhere in the settings menu. On an AZERTY keyboard, the physical keys at the WASD position produce different characters, so the default controls are effectively unusable without a workaround. This mod patches the game's input assets directly so the controls match the AZERTY layout.

## Controls after installing

| Key | Action |
|-----|--------|
| Z Q S D | Move (was W A S D) |
| & | Provocation / whistle (was `1`) |
| é | Emote / action 2 |
| " | Emote / action 3 |
| ' | Emote / action 4 |
| ( | Emote / action 5 |
| - | Emote / action 6 |
| A | Clone / copy (was `Q`, now used for strafing) |

UI navigation is remapped to ZQSD as well. Everything else (mouse, Shift, Ctrl, E, F, R…) is untouched.

## Installation

Extract the zip into:

```
<game folder>/Chameleon/
```

That drops `AzertyFix_P.pak/.ucas/.utoc` into `Chameleon/Content/Paks/`, which Unreal loads automatically. To uninstall, delete those three files. Nothing else is touched — no save data or settings.

## Known limitation

- **Free camera (free view) moves with WASD.** The free/spectate camera is Unreal's built-in `SpectatorPawn`; its movement keys are hardcoded in the engine's C++ (`DefaultPawn` engine-defined axes), not an input asset or config value a mod can override.

## Important — game updates

This patch overrides cooked game assets (including character/controller blueprints for keys 2–6), so it is **tied to the exact game build it was made for**. After a game update it may need rebuilding, and **installing it on a different game version than it was built for can crash the game on load** (`Serial size mismatch`). If you crash after a game patch, delete the three `AzertyFix_P.*` files and wait for an updated release. This release was built for the current game version.

## How it works

The game ships its input bindings baked into Unreal Engine 5 IoStore assets (`.utoc`/`.ucas`/`.pak`), not as an editable `.ini`. This mod is a single override pak that ships patched copies of the affected `InputMappingContext` assets (movement/UI/whistle/clone) plus the cLeon character/controller/spectate blueprints (keys 2–6). Key names are swapped at the asset level (`W`→`Z`, `A`→`Q`, `Q`→`A`, `One`→`Ampersand`, `Two`→`E_AccentAigu`, `Three`→`Quote`, `Four`→`Apostrophe`, `Five`→`LeftParantheses`, `Six`→`Hyphen`); package offsets are recalculated automatically on re-serialization.

## Credits

Built with the community's Unreal Engine modding tools:

- [retoc](https://github.com/trumank/retoc) by trumank — converting the game's IoStore container to/from a legacy pak format
- [UAssetAPI / UAssetGUI](https://github.com/atenfyr/UAssetGUI) by atenfyr — reading and editing the game assets

Thanks to both for keeping these open-source.
