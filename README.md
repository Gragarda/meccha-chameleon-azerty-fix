# MECCHA CHAMELEON — AZERTY Keyboard Fix

MECCHA CHAMELEON hardcodes WASD for movement and has no key rebinding option anywhere in the settings menu. On an AZERTY keyboard, the physical keys at the WASD position produce different characters, so the default controls are effectively unusable without a workaround. This mod patches the game's Enhanced Input mapping assets directly so movement and UI navigation use ZQSD, matching the physical key layout AZERTY users expect.

It also fixes the Provocation (whistle) key: the game binds it to `1`, which on AZERTY requires holding Shift — but Shift is the Run key, so you couldn't whistle without running. The patch rebinds it to the `&` key (the same physical key, but its unshifted character), so it works on its own.

## Controls after installing

| Key | Action |
|-----|--------|
| Z   | Move forward |
| Q   | Move left |
| S   | Move back |
| D   | Move right |
| &   | Provocation / whistle (was `1`) |

All other bindings (mouse, Shift, Ctrl, E, F, R, etc.) are untouched.

## Installation

Download the latest release zip from the [Releases page](../../releases), then extract its contents into:

```
<game folder>/Chameleon/
```

The archive mirrors the game's folder structure, so the files land in the right place automatically.

### Uninstall

Delete the three `AzertyFix_P.*` files from `Chameleon/Content/Paks/`. Nothing else is touched: no save data or settings files are modified.

## How it works

The game ships its input bindings baked into Unreal Engine 5 IoStore assets (`.utoc`/`.ucas`/`.pak`), not as an editable `.ini`. This mod is a small override pak (`AzertyFix_P.pak/.ucas/.utoc`) containing patched copies of the affected `Input Mapping Context` assets (`IMC_Default_FirstPerson`, `IC_UINav_Custom`, `IC_UINav` for movement/UI, and `IMC_cLeonDefault` for the whistle key). The key names are changed at the asset level (`W`→`Z`, `A`→`Q`, `Q`→`A`, and `One`→`Ampersand`); for the longer whistle name the package offsets are recalculated automatically when the asset is re-serialized. Unreal Engine loads override paks automatically from `Content/Paks/`, so no installer or code injection is needed.

## Requirements

None. No other mods or tools are required to use this patch.

## Credits

This patch wouldn't have been possible without the Unreal Engine modding tools built by the community:

- [retoc](https://github.com/trumank/retoc) by trumank, for converting the game's IoStore (`.utoc`/`.ucas`) container to and from a legacy pak format
- [UAssetGUI / UAssetAPI](https://github.com/atenfyr/UAssetGUI) by atenfyr, for inspecting and editing the Input Mapping Context assets

Thanks to both for keeping these tools open-source and maintained.

## Compatibility note

This is a content override pak, not a save-file or settings change. It should be safe alongside other cosmetic/map mods, but may need updating if a game patch changes the base Input Mapping Context assets.
