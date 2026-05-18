# Unity Project Setup Description

## Project Summary
This repository contains a Unity **2019.4.26f1** 3D platformer project with:
- A main menu and options flow
- Three playable levels
- Character movement, camera orbit, timer, pause/win UI, moving/rotating platforms, and audio mixing
- A WebGL build output under `docs/` for GitHub Pages deployment

## Root Structure
- `Assets/` — all game content (scenes, scripts, prefabs, models, materials, textures, audio, animation)
- `Packages/` — Unity package manifest and lockfile
- `ProjectSettings/` — Unity engine/project configuration
- `docs/` — built WebGL player files (`index.html`, `Build/`, `TemplateData/`)
- `readme_images/` — GIF/PNG assets for repository documentation
- `README.md` — project overview, controls, attribution, and installation notes

## Unity Version and Build Setup
- Unity version: `2019.4.26f1` (`ProjectSettings/ProjectVersion.txt`)
- Build scenes enabled (`ProjectSettings/EditorBuildSettings.asset`):
  1. `Assets/Scenes/MainMenu.unity`
  2. `Assets/Scenes/Level01.unity`
  3. `Assets/Scenes/Level02.unity`
  4. `Assets/Scenes/Level03.unity`
  5. `Assets/Scenes/Options.unity`

## Packages (`Packages/manifest.json`)
Key package dependencies include:
- `com.unity.textmeshpro` (UI text)
- `com.unity.ugui` (legacy Unity UI)
- `com.unity.timeline`
- `com.unity.test-framework`
- IDE integrations (`com.unity.ide.vscode`, `com.unity.ide.rider`)
- Unity built-in modules (audio, physics, animation, UI, etc.)

## Assets Overview
Top-level content folders in `Assets/`:
- `Animations/` — intro animation clips (`Intro01/02/03.anim`)
- `Animators/` — animator controllers (`CutsceneCamera.controller`, `ty.controller`)
- `Audio/` — BGM and SFX audio clips
- `Fonts/` — font assets (Changa family)
- `Materials/` — environment and skybox materials
- `Models/` — player model (`ty.fbx`), flag model, and large nature model library (`naturePack_*`)
- `Prefabs/` — reusable UI and gameplay prefab objects
- `Scenes/` — menu/options/level scene files plus baked lighting data
- `Scripts/` — gameplay and UI C# logic
- `Textures/` — texture assets including UI textures

## Scene and Flow Design
- **MainMenu**: Level selection, options navigation, and exit
- **Options**: Invert camera Y-axis and BGM/SFX volume settings persisted with `PlayerPrefs`
- **Level01/02/03**:
  - Intro cutscene camera
  - Playable character (`Player` prefab)
  - Pause menu
  - Timer and win condition logic
  - Environment obstacles/platform motion and rotation

## Prefabs
`Assets/Prefabs/` includes:
- `Player.prefab`
- `PauseCanvas.prefab`
- `TimerCanvas.prefab`
- `WinCanvas.prefab`
- Menu/button prefabs: `ApplyButton`, `BackButton`, `ExitButton`, `OptionsButton`, `MenuSFX`

## Script Responsibilities (`Assets/Scripts`)
- `PlayerController.cs` — character movement, jumping, gravity, rotation aligned to camera, respawn-on-fall, animator state updates
- `CameraController.cs` — third-person orbit camera controlled by right mouse drag, invert-Y support from saved prefs
- `MainMenu.cs` — main menu button behavior, scene loading, and menu button SFX events
- `OptionsMenu.cs` — options UI logic, mixer slider conversion between linear and dB, saving `PlayerPrefs`
- `PauseMenu.cs` — pause/resume flow, time scale control, pause canvas interactions, scene navigation
- `Timer.cs` — elapsed level timer and final-time handoff to win UI
- `TimerTrigger.cs` — enables timer once player exits start trigger
- `WinTrigger.cs` — handles level completion, stops gameplay/timer, shows win canvas, transitions music, pauses game
- `WinMenu.cs` — win screen buttons (main menu or next level)
- `CutsceneController.cs` — scene intro selection and handoff from cutscene to gameplay camera/player
- `MovePlatform.cs` — back-and-forth platform translation with delay and optional start delay
- `RotatePlatform.cs` — configurable axis-based rotation behavior
- `TyController.cs` — animation-event helpers and footstep/landing SFX switching based on surface material
- `ButtonSFX.cs` — reusable hover/click SFX trigger behavior for UI buttons
- `MainMenuBGM.cs` — persistent main-menu BGM singleton destroyed outside menu/options
- `MasterMixerManager.cs` — applies saved BGM/SFX mixer values at startup

## Audio Setup
- BGM clips include tracks like `CheeryMonday`, `Wallpaper`, `VictoryPiano`, etc.
- Mixer-controlled channels for:
  - `BGMVolume`
  - `SFXVolume`
- Audio settings are persisted via `PlayerPrefs` keys such as:
  - `dbBGMVolume`
  - `dbSFXVolume`
  - `InvertYToggle`

## Web Build Artifacts
The `docs/` folder contains WebGL output (`index.html`, build files, template files), enabling hosting directly from GitHub Pages.

## Notes
- The repository is organized as a standard Unity project, so `.meta` files are intentionally included and required for GUID consistency.
- Scenes also contain baked lighting and reflection probe assets under scene subfolders (e.g., `Assets/Scenes/Level01/LightingData.asset`).
