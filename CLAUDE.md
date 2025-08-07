# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a ZMK (Zephyr Mechanical Keyboard) firmware configuration repository for a Corne keyboard with Nice!View displays. ZMK configs use GitHub Actions to automatically build firmware when changes are pushed.

## Architecture

- **build.yaml**: Defines the build matrix for GitHub Actions, specifying board/shield combinations to build (Nice Nano V2 with Corne split keyboard and Nice!View displays)
- **config/corne.conf**: Keyboard configuration settings (Bluetooth power, sleep timeout)
- **config/corne.keymap**: Device tree overlay defining the keymap with 3 layers (default, symbols/numbers, navigation/media)
- **config/west.yml**: West manifest pointing to the ZMK firmware repository

## Build System

The firmware is built automatically via GitHub Actions when changes are pushed. The workflow uses ZMK's build-user-config.yml workflow. Built firmware artifacts are available as GitHub Actions artifacts after each successful build.

To download firmware:
1. Go to Actions tab on GitHub
2. Select the latest successful workflow run
3. Download the firmware artifact
4. Flash the .uf2 files to your keyboard halves

## Keymap Modifications

When modifying the keymap in config/corne.keymap:
- The file uses Device Tree format (.dtsi)
- Three layers are defined: default_layer, layer_below (layer 1), layer_above (layer 2)
- Custom behaviors are defined in the behaviors section
- Key positions follow the Corne 42-key layout (3x6 + 3 thumb keys per side)

## Common ZMK Keycodes

- Basic keys: &kp KEY_NAME (e.g., &kp A, &kp SPACE)
- Modifiers: &kp LCTRL, &kp LSHFT, &kp LALT, &kp LGUI
- Layer switching: &mo LAYER_NUMBER (momentary), &lt LAYER_NUMBER KEY (layer-tap)
- Bluetooth: &bt BT_CLR (clear), &bt BT_SEL N (select profile)
- Media: &kp C_PP (play/pause), &kp C_NEXT, &kp C_PREV, &kp C_VOL_UP, &kp C_VOL_DN