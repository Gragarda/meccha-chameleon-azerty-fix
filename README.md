# MECCHA CHAMELEON — AZERTY Keyboard Fix

MECCHA CHAMELEON hardcodes WASD for movement and has no key rebinding option anywhere in the settings menu. On an AZERTY keyboard, the physical keys at the WASD position produce different characters, so the default controls are effectively unusable without a workaround. This mod patches the game's Enhanced Input mapping contexts directly so movement, UI navigation and the main actions match the AZERTY layout.

## What the main patch does

| Key | Action |
|-----|--------|
| Z Q S D | Move (was W A S D) |
| & | Provocation / whistle (was `1`) |
| A | Clone / copy (was `Q`, which ZQSD now uses for strafing) |

UI navigation is remapped to ZQSD as well. Everything else (mouse, Shift, Ctrl, E, F, R…) is untouched.

The main patch overrides only `InputMappingContext` assets (Enhanced Input). It contains **no blueprint or gameplay-class data**, so it is safe and robust across game builds.

## Optional add-on — number-row actions 2–6

A **separate optional download** remaps the emote/provocation keys `2 3 4 5 6` to their AZERTY-unshifted characters:

| Key | Action |
|-----|--------|
| é | 2 |
| " | 3 |
| ' | 4 |
| ( | 5 |
| - | 6 |

> [!WARNING]
> These actions live in the character/controller **blueprints**, which embed game-specific compiled data tied to one exact game build. This add-on is built for the **current** game version. On a **different game build it will crash on load** (`Serial size mismatch` in the async loader). Only install it if your game is up to date, and **remove it if you crash** — the base game keeps working without it. It also needs rebuilding after most game updates.

## Installation

Extract the main zip into:

```
<game folder>/Chameleon/
```

For the number-row add-on, extract its zip the same way (it adds a second `AzertyFix_Digits_P.*` pak alongside the main one).

### Uninstall

Delete the `AzertyFix_P.*` (and `AzertyFix_Digits_P.*` if installed) files from `Chameleon/Content/Paks/`. Nothing else is touched.

## Known limitations

- **Free camera (free view) moves with WASD.** The free/spectate camera is Unreal's built-in `SpectatorPawn`; its movement keys are hardcoded in the engine's C++ (`DefaultPawn` engine-defined axes) and are not an input asset or a config value the mod can override. Not fixable from a content mod.

## Compatibility & game updates

The mod overrides cooked game assets, so it is tied to the game version it was built from. The **main patch** (Enhanced Input contexts) is robust and usually survives updates. The **optional 2–6 add-on** (blueprints) is version-locked — after a game update it may need rebuilding, and players on an older/newer build than it was built for will crash. Keep your game updated and remove the add-on if you ever crash after a patch.

## How it works

The game ships its input bindings baked into Unreal Engine 5 IoStore assets (`.utoc`/`.ucas`/`.pak`), not as an editable `.ini`. This mod is a small override pak containing patched copies of the affected `InputMappingContext` assets (`IMC_Default_FirstPerson`, `IC_UINav`, `IC_UINav_Custom`, `IMC_cLeonDefault`, `IMC_MoverMappingContext`), with key names swapped at the asset level (`W`→`Z`, `A`→`Q`, `Q`→`A`, `One`→`Ampersand`). Package offsets are recalculated automatically on re-serialization. Unreal loads override paks automatically from `Content/Paks/`, so no installer or code injection is needed. The optional add-on does the same for the digit key events in the cLeon blueprints.

## Credits

Built with the community's Unreal Engine modding tools:

- [retoc](https://github.com/trumank/retoc) by trumank — converting the game's IoStore container to/from a legacy pak format
- [UAssetAPI / UAssetGUI](https://github.com/atenfyr/UAssetGUI) by atenfyr — reading and editing the input assets

Thanks to both for keeping these open-source.
