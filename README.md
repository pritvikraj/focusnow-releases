# FocusNow for macOS

FocusNow is a menu-bar time tracker for macOS. This repository contains the
official FocusNow downloads and the update feed used by the app.

## Before you install

- FocusNow requires **macOS 14 Sonoma or newer**.
- Current builds are made for **Apple silicon Macs** (M1, M2, M3, M4, and
  newer).
- FocusNow is not yet notarized by Apple. The first installation therefore
  needs one Terminal command, explained below. Future in-app updates do not
  need this step.

## Install FocusNow

1. Open the [latest FocusNow release](https://github.com/pritvikraj/focusnow-releases/releases/latest).
2. Under **Assets**, download the file named `FocusNow-<version>.zip`.
3. Open the downloaded ZIP, then drag `FocusNow.app` into your Mac's
   **Applications** folder.
4. Open **Terminal** (press Command-Space, type `Terminal`, and press Return),
   paste the following command, and press Return:

   ```sh
   xattr -dr com.apple.quarantine /Applications/FocusNow.app
   ```

   This removes the download quarantine that macOS applies to apps that are
   not Apple-notarized. Only run this command for FocusNow downloaded from
   this official repository.
5. Open **Applications** and double-click **FocusNow**. Its icon will appear
   in the menu bar.

## Getting future updates

After the first installation, FocusNow checks this repository for new
versions using its built-in Sparkle updater. When an update is available, the
app will offer to download, verify, install, and relaunch it for you.

You can also check manually from FocusNow's menu-bar menu by selecting
**Check for Updates…**. You do not need to download another ZIP or repeat the
Terminal command for an in-app update.

## Why the Terminal step is necessary

FocusNow is currently ad-hoc signed rather than Developer ID signed and
notarized. macOS therefore quarantines a copy downloaded through a browser.
Removing that quarantine allows the first launch.

Every update delivered inside the app is separately signed with an EdDSA
(ed25519) key. Sparkle verifies that signature before installing the update
and rejects a changed or substituted download.

## What this repository contains

- `appcast.xml` is the public Sparkle update feed.
- Each GitHub Release contains a versioned `FocusNow-<version>.zip` download.

Releases are built, signed, and published manually by the project owner. They
are not published automatically when a source-code tag is pushed. FocusNow's
source code remains in a separate private repository; this public repository
contains only the files required for downloading and updating the app.
