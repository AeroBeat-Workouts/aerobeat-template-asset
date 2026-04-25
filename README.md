# AeroBeat Internal Asset Template

System assets (UI, Fonts, Mock Data) for AeroBeat internal use.

## 📋 Repository Details

*   **Type:** Internal Asset (System)
*   **License:** **CC BY-NC 4.0** (Attribution-NonCommercial)
*   **Dependencies:**
    *   `aerobeat-asset-core` (Canonical shared asset/resource contract)

## GodotEnv development flow

This repo uses the AeroBeat GodotEnv asset-package convention.

- Canonical dev/test manifest: `.testbed/addons.jsonc`
- Installed dev/test addons: `.testbed/addons/`
- GodotEnv cache: `.testbed/.addons/`
- Hidden workbench project: `.testbed/project.godot`
- Repo-local unit tests: `.testbed/tests/`

The repo root remains the package/published boundary for downstream consumers. Day-to-day development, import checks, and validation happen from the hidden `.testbed/` workbench using the pinned OpenClaw toolchain: Godot `4.6.2 stable standard`.

### Restore dev/test dependencies

From the repo root:

```bash
cd .testbed
godotenv addons install
```

That restores this repo's current dev/test manifest into `.testbed/addons/`. This repo is internal-only / system-facing Asset-lane work rather than a public workout-package template.

### Open the workbench

From the repo root:

```bash
godot --editor --path .testbed
```

Use this `.testbed/` project as the canonical direct-development and import-validation surface for internal asset work.

### Import smoke check

From the repo root:

```bash
godot --headless --path .testbed --import
```

### Run unit tests

From the repo root:

```bash
godot --headless --path .testbed --script addons/gut/gut_cmdln.gd \
  -gdir=res://tests \
  -ginclude_subdirs \
  -gexit
```

## 📂 Structure

*   `assets/` - Root folder for system-critical content.
*   `assets/ui/` - Icons and themes.
*   `assets/fonts/` - TTF/OTF files.
*   `assets/mock/` - JSON/Resource data for testing.
*   `assets/prototypes/` - Greybox meshes and fallback art.

## Validation notes

- `.testbed/addons.jsonc` is the committed dev/test dependency contract.
- The current manifest still pins the transition-era `aerobeat-core` package key to `v0.1.0` alongside GUT `main`. Canonical lane ownership is `aerobeat-asset-core`.
- Repo-local unit tests live under `.testbed/tests/`.
- This template is root-packaged (`subfolder: "/"`) and does not use a `.testbed/src` bridge; add real content directly under the repo root package boundary.

## Notes

- These assets are required by assemblies or UI shells and are not intended as mod-swappable UGC.
- Helper scripts and shaders are allowed here when needed for system polish.
