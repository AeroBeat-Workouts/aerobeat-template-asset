# AeroBeat Internal Asset Template

This is the official template for creating **internal asset** repositories within the current AeroBeat v1 architecture.

It should be read against the locked product direction from `aerobeat-docs`:

- **Primary release target:** PC community first
- **Official v1 gameplay features:** Boxing and Flow
- **Official v1 gameplay input:** camera only
- **UI input stance:** mouse and touch remain valid for UI navigation, without implying equal-status gameplay input support
- **Asset-lane ownership:** shared internal assets, UI presentation assets, environments, and future controlled avatar/cosmetics surfaces belong here through `aerobeat-asset-core`
- **Downscoped customization truth:** this template is for internal/system asset work, not for reviving the older package-local gameplay asset swap story

## 📋 Repository Details

- **Type:** Internal asset template
- **License:** **CC BY-NC 4.0** (Attribution-NonCommercial)
- **Dependency contract:**
  - `aerobeat-asset-core` — required shared asset/resource contract for the asset lane
  - additional adjacent lane/core repos only when a concrete internal asset repo truly consumes them

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

That restores this repo's current dev/test manifest into `.testbed/addons/`. Canonically, this template should keep the baseline manifest narrow: `aerobeat-asset-core` plus test-only tooling.

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

- `assets/` - Root folder for internal runtime content owned by this package.
- `assets/ui/` - Icons, themes, and other shared UI-facing presentation assets.
- `assets/fonts/` - TTF/OTF files.
- `assets/mock/` - JSON/Resource data for testing and developer fixtures.
- `assets/prototypes/` - Greybox meshes, fallback art, and exploratory internal assets.

## Validation notes

- `.testbed/addons.jsonc` is the committed dev/test dependency contract.
- The canonical template manifest for this repo is `aerobeat-asset-core` + `gut`.
- Do **not** restore a universal `aerobeat-core` baseline here. Add adjacent repos only when a concrete asset repo truly needs them.
- Repo-local unit tests live under `.testbed/tests/` and currently validate repo metadata plus the manifest contract.
- This template is root-packaged (`subfolder: "/"`) and does not use a `.testbed/src` bridge; add real content directly under the repo root package boundary.

## Notes

- These assets are intended for internal AeroBeat assemblies, shells, and shared product surfaces.
- Environments remain in scope for the current product direction, but freeform package-local gameplay asset swap teaching does not.
- Helper scripts and shaders are allowed here when needed for system polish.
