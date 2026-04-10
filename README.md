# MMMerge 4.0 Workspace

This repository is a working **Might and Magic 6/7/8 Merge** game directory built on the **MM8** runtime, extended with **GrayFace's MM8 Patch** and **MMExtension**, then customized with additional Lua systems, data-table edits, map overrides, localization work, and bundled modding resources.

It is not a minimal source-only repo. It is a full mod workspace that mixes:

- game runtime files and patch DLLs
- live mod content used by the current build
- optional presets and one-file mods
- backup/export material for text and LOD assets
- personal work/reference folders

At the moment, the active gameplay configuration is the **Revamp** variant:

- `Data/Tables/ModSettings.txt` identifies the live preset as `Revamp`
- `Scripts/Structs/10_MergeSettings.lua` reports `Merge.VariantVersion = "20220618-revamp"`

## What Lives Where

### Runtime and entry files

- `mm8.exe`: base executable used to run the merged game
- `mm8.ini`: GrayFace patch configuration, renderer/UI/input options
- `MMMergeSettings.lua`: user override file for merge settings and logging
- `MM8Patch ReadMe.TXT`: bundled patch reference
- `MMExtension.htm`: bundled MMExtension reference

### Live gameplay logic

- `Scripts/Core/`: MMExtension core/runtime bootstrap
- `Scripts/Structs/`: low-level hooks, limits removal, merge settings, engine extensions
- `Scripts/General/`: global gameplay systems driven by tables and settings
- `Scripts/Global/`: shared quest logic, utilities, editor support, custom mechanics
- `Scripts/Maps/`: per-map scripts for specific locations across MM6/MM7/MM8 content
- `Scripts/Modules/`: helper modules used by the rest of the Lua code

### Live data and assets

- `Data/Tables/`: main editable text tables for balance, races, classes, items, spells, travel, UI, and other systems
- `Data/`: active LOD archives, localization files, UI assets, imported resources, and backup/export folders
- `DataFiles/`: binary tables and classic text files such as `class.txt` and `roster.txt`
- `Maps/`: loose map data overrides (`.dat`, `.odt`, backups)
- `Data/Games/`: loose exported map content (`.blv`, `.dlv`, `.odm`, `.ddm`)

### Optional presets and reference content

- `Extra/Revamp/`: source copy of the active Revamp preset
- `Extra/BaseDefault/`, `Extra/CommunityDefault/`, `Extra/Extended/`: alternate table/data snapshots
- `Extra/1FileMods/`: small targeted overrides such as alternate race skills or character selection data
- `Docs/`: changelogs and a small developer note set
- `language/`: language-pack related files
- `【魔法门678攻略宝典】/`: bundled Chinese guide/reference material
- `mywork/`: personal working area, experiments, saves, tools, and notes

## How The Project Is Structured

The project follows the usual Merge pattern:

1. `mm8.exe` starts the MM8-based runtime.
2. GrayFace patch settings are read from `mm8.ini`.
3. MMExtension loads Lua from `Scripts/`.
4. `Scripts/Structs/10_MergeSettings.lua` initializes default merge settings, then loads user overrides from `MMMergeSettings.lua`.
5. Table-driven systems read from `Data/Tables/`.
6. Loose files in `Data/`, `Maps/`, and related folders override packed assets when present.

In practice, most gameplay edits fall into one of these buckets:

- **Lua behavior**: edit `Scripts/General/`, `Scripts/Global/`, or `Scripts/Maps/`
- **Balance/data definitions**: edit `Data/Tables/`
- **Roster/class baselines**: edit `DataFiles/`
- **Map content**: edit `Maps/` and/or `Data/Games/`
- **UI/localization/assets**: edit files in `Data/`

## Recommended Editing Workflow

Because this repo is a full game tree, the safest way to work is:

1. Treat the repository root as a runnable installation, not just source code.
2. Prefer editing **loose text/Lua/table files** before touching packed LOD archives.
3. Keep `Extra/` as reference presets and donor content unless you intentionally want to promote changes into the live tree.
4. Preserve backup/export folders in `Data/`; many of them exist specifically to round-trip assets out of LODs.
5. Use logs for debugging:
   - `MMMergeLog.txt`
   - `MMMergeLog.1.txt`, `MMMergeLog.2.txt`
   - `ErrorLog.txt`
   - `MMExtensionLog.txt`

## Important Config Files

### `mm8.ini`

Controls patch/runtime behavior such as:

- UI layout
- fullscreen/windowed behavior
- mouse look and input
- hardware rendering settings
- quality-of-life patch options

### `MMMergeSettings.lua`

Controls merge-specific behavior such as:

- logging level and log file name
- character creation/autobiography options
- conversion/promotion behavior
- other merge-specific toggles exposed by the Lua side

If `MMMergeSettings.lua` is missing, `Scripts/Structs/10_MergeSettings.lua` can seed it from `Extra/MMMergeSettings.lua`.

### `Data/Tables/ModSettings.txt`

Defines the active variant-level settings. In this workspace it points at:

- `Name = Revamp`
- `Directory = Extra/Revamp`

## Folder Guide For Contributors

If you need to find the right place to make a change:

- new gameplay rule or scripted mechanic: `Scripts/General/` or `Scripts/Global/`
- map-specific quest/object/NPC logic: `Scripts/Maps/`
- race/class/spell/item progression: `Data/Tables/`
- starting party or class roster: `DataFiles/`
- custom textures/UI art/localization assets: `Data/`
- alternate presets to compare against: `Extra/`
- history/background on upstream Merge behavior: `Docs/ChangeLog.md`, `Docs/ChangeLogBase.md`

## Notes And Caveats

- This repository already contains generated logs, backups, exported assets, and personal working material. Do not assume every folder is meant for shipping.
- Some directories and files use Chinese names and GB2312/legacy encodings; use an editor that handles them cleanly.
- The tree contains both live files and historical copies of the same resources. Check whether you are editing the active path or a backup first.
- Asset packaging is LOD-based. For bitmap import workflow, see `Data/如何添加自定义BMP到游戏.md`.

## Useful References In The Repo

- `Docs/ChangeLog.md`: community branch history
- `Docs/ChangeLogBase.md`: upstream/base Merge history
- `Docs/Developer Manual/MMExtension.md`: small project note on MMExtension additions
- `MM8Patch ReadMe.TXT`: GrayFace patch reference
- `MMExtension.htm`: local MMExtension documentation

## Short Description

If you need a one-line summary for the project:

> A customized MM8-based Might and Magic 6/7/8 Merge workspace with Revamp as the active variant, combining Lua gameplay code, editable data tables, loose map overrides, localization work, and bundled modding resources inside a runnable game directory.
