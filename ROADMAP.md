# Android Builder Lab Roadmap

## Project Goal
Build a system-first, phone-friendly Android Builder / Editor / Installer Lab that helps manage Android projects from a mobile device.

Primary goal:
- make Android app development, inspection, building, signing, and installing practical from a phone

## Locked Design Principles

### 1. System-first Android behavior
Use Android's own systems wherever possible:
- `ACTION_OPEN_DOCUMENT_TREE` for folders
- `ACTION_OPEN_DOCUMENT` for files
- persistent URI permissions
- `DocumentFile` / content URI workflow
- `FileProvider` for APK handoff
- system package installer for installs

### 2. Workspace-based model
Do not rely on random absolute file paths.
The app should support importing/staging projects into an app-controlled workspace when needed.

### 3. Termux is required, but not the main UX
The app is the control center.
Termux is the execution backend for anything heavy or awkward to do natively.

### 4. Minimum permissions first
Avoid broad permissions unless absolutely necessary.
Prefer:
- SAF / picker access
- FileProvider
- targeted package visibility

Avoid by default:
- `MANAGE_EXTERNAL_STORAGE`
- `QUERY_ALL_PACKAGES`
- legacy broad storage permissions

### 5. Phone-first workflow matters most
Priority order:
1. Best for phone-only workflow
2. Modularity / future-proofing
3. Reliability
4. Speed
5. Broad project support
6. Ease of use

## Supported Inputs and Project Types

### Accepted inputs
- Folder
- ZIP
- APK
- APKS / split package
- Anything the user selects, with autodetect

### Recognized project/package types
- Classic raw-source Android projects
- Gradle Android projects
- Decoded APK / apktool-style projects
- ZIP archives containing any of the above
- APK / APKS packages for inspection/import/install routing

## What Build Means
Build should mean:
- compile
- sign
- install
- save logs/history

## Build Ladder

### BUILD 1 — Foundation Shell
Type: FULL

Includes:
- classic raw-source Android project structure
- modular package layout
- Home/Dashboard screen
- picker hooks (folder, file, ZIP/APK/APKS import)
- project intake/detection engine v1
- project classification UI
- workspace/staging skeleton
- Termux presence/status checker
- basic settings screen
- basic logs screen shell
- basic file browser shell
- docs describing structure

Goal:
- open something
- detect what it is
- stage it if needed
- show the recommended path

### PATCH 1A — Intake / Detection Fix Pack
Type: PATCH

### BUILD 2 — Build Profile + Termux Bridge
Type: FULL

Includes:
- build profile screen
- per-project build configuration
- debug/release selection
- Termux command bridge v1
- command generation layer
- live log capture v1
- build history model v1
- output discovery logic v1

### PATCH 2A — Termux / Logging Fix Pack
Type: PATCH

### BUILD 3 — First Real Build Success Milestone
Type: FULL

Includes:
- first-class Gradle build path
- first-class raw-source build path
- build result screen
- output file detection
- improved diagnostics
- clearer fix suggestions

### PATCH 3A — Build Success Stabilizer
Type: PATCH

### BUILD 4 — Signing + Install Milestone
Type: FULL

Includes:
- existing keystore selection
- alias entry
- signing flow
- signed output verification
- install button
- FileProvider handoff
- system installer integration

### PATCH 4A — Signing / Install Fix Pack
Type: PATCH

### BUILD 5 — Editor + Repair + Diagnostics
Type: FULL

Includes:
- file browser
- basic text editor
- save support
- project health panel
- suggested fixes
- export/copy logs
- better history screen

### PATCH 5A — Editor / Diagnostics Fix Pack
Type: PATCH

### BUILD 6 — APK / APKS / Decoded Project Support
Type: FULL

Includes:
- APK/APKS intake
- ZIP extraction refinement
- decoded/apktool project classification
- smarter routing
- more advanced project detection logic

## Delivery Rules

### FULL build
Use when:
- architecture changes
- screens/modules are added
- file structure changes
- detection/build flow changes
- anything core is refactored

### PATCH build
Use when:
- change is isolated
- only a few files change
- no major restructuring

### WIPE / RESET build
Use when:
- current base becomes structurally wrong
- too many patches stack up
- architecture proves bad

## Recommended naming pattern
- `BuilderLab_FULL_v1`
- `BuilderLab_PATCH_v1a`
- `BuilderLab_FULL_v2`
- `BuilderLab_PATCH_v2a`
- reset example: `BuilderLab_FULL_v3_RESET`
