# MECCHA CHAMELEON — AZERTY Keyboard Fix

MECCHA CHAMELEON hardcodes WASD for movement and has no key rebinding option anywhere in the settings menu. On an AZERTY keyboard, the physical keys at the WASD position produce different characters, so the default controls are effectively unusable without a workaround. This mod patches the game's Enhanced Input mapping assets directly so movement and UI navigation use ZQSD, matching the physical key layout AZERTY users expect.

It also remaps the number-row actions (provocations / emotes on `1`–`6`). On AZERTY those digits require holding Shift — but Shift is the Run key, so you couldn't trigger them cleanly. Each is rebound to the unshifted character on the same physical key, so they work on their own.

## Controls after installing

### Movement
| Key | Action |
|-----|--------|
| Z   | Move forward |
| Q   | Move left |
| S   | Move back |
| D   | Move right |

### Number-row actions (provocations / emotes)
| Press | Was |
|-------|-----|
| &     | 1 |
| é     | 2 |
| "     | 3 |
| '     | 4 |
| (     | 5 |
| -     | 6 |

All other bindings (mouse, Shift, Ctrl, E, F, R, etc.) are untouched.

## Installation

Download the latest release zip from the [Releases page](../../releases), then extract its contents into:

```
<game folder>/Chameleon/
```

The archive mirrors the game's folder structure, so the files land in the right place automatically.

### Uninstall

Delete the three `AzertyFix_P.*` files from `Chameleon/Content/Paks/`. Nothing else is touched: no save data or settings files are modified.

## Known issues

- **Free camera (free view) still moves with WASD.** The free-look/spectate camera uses its own movement input that isn't remapped yet. Identified; planned for a future update.

## How it works

The game ships its input bindings baked into Unreal Engine 5 IoStore assets (`.utoc`/`.ucas`/`.pak`), not as an editable `.ini`. This mod is a small override pak (`AzertyFix_P.pak/.ucas/.utoc`) containing patched copies of the affected assets:

- Movement / UI: the `Input Mapping Context` assets `IMC_Default_FirstPerson`, `IC_UINav_Custom`, `IC_UINav` (`W`→`Z`, `A`→`Q`, `Q`→`A`).
- Number row: `IMC_cLeonDefault` (the `1` provocation, Enhanced Input) plus the character/controller blueprints `BP_FirstPersonCharacter_cLeon_Character`, `BP_PlayerController_cLeon`, `BP_SpectatePawn_cLeon`, where the `2`–`6` actions are raw key events. The key names are swapped at the asset level to their AZERTY-unshifted equivalents (`One`→`Ampersand`, `Two`→`E_AccentAigu`, `Three`→`Quote`, `Four`→`Apostrophe`, `Five`→`LeftParantheses`, `Six`→`Hyphen`).

For the longer names the package offsets are recalculated automatically when the asset is re-serialized. Unreal Engine loads override paks automatically from `Content/Paks/`, so no installer or code injection is needed.

## Requirements

None. No other mods or tools are required to use this patch.

## Credits

This patch wouldn't have been possible without the Unreal Engine modding tools built by the community:

- [retoc](https://github.com/trumank/retoc) by trumank, for converting the game's IoStore (`.utoc`/`.ucas`) container to and from a legacy pak format
- [UAssetGUI / UAssetAPI](https://github.com/atenfyr/UAssetGUI) by atenfyr, for inspecting and editing the patched assets

Thanks to both for keeping these tools open-source and maintained.

## Compatibility note

This is a content override pak, not a save-file or settings change. It should be safe alongside other cosmetic/map mods, but may need updating if a game patch changes the base input assets or character blueprints.
