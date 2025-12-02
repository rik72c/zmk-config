# ZMK Firmware Configuration - Agent Guide

## Build Commands
- **Build firmware**: GitHub Actions automatically builds on push (see `.github/workflows/build.yml`)
- **Local build**: Not typically done - firmware builds via zmkfirmware/zmk workflow
- **No traditional tests/linting** - ZMK configs use devicetree compilation validation

## Code Style & Structure

### File Organization
- Main keymap: `config/base.keymap` (shared base configuration)
- Board-specific: `config/cradio.keymap` (includes base + board definitions)
- Modular includes: `config/includes/*.dtsi` (behaviors, combos, macros, settings)
- Build config: `build.yaml` (defines board/shield matrix for CI)

### Devicetree Conventions
- Use `#include` for devicetree includes, not C-style imports
- Define behaviors in separate `.dtsi` files under `config/includes/`
- Use preprocessor defines for key position groups (KEYS_L, KEYS_R, KEYS_T)
- Layer numbers referenced by index (0=base, 1=nav, 2=numeric, etc.)

### Naming & Comments
- Behavior names: lowercase with underscores (e.g., `hm_s_l`, `gui_tab`)
- Visual keymap comments: Use box-drawing chars for layout visualization
- Configuration: Use `#define` for timing constants (HM_TAPPING_TERM, etc.)

### Configuration Files
- `.conf` files: Use CONFIG_ prefixed options for ZMK settings
- Comment out optional features with `#` prefix
