# FocusNow releases

This repository exists for one reason: it is the **public** side of a private
project. FocusNow's source lives in a private repo, but Sparkle — the
in-app updater — has to fetch its appcast feed anonymously, with no token and
no login. A private repo cannot serve that. So the source stays private and
this repo carries only what has to be publicly readable: the update feed and
the build artifacts it points at.

## What's here

- `appcast.xml` — the Sparkle feed. The running app polls this to learn
  whether a newer build exists.
- Release assets — each version's `FocusNow-<version>.zip`, attached to a
  GitHub Release in this repo.

Both are published automatically when a `v*` tag is pushed in the source repo.

## Verifying a download

Every zip referenced by the appcast is signed with an EdDSA (ed25519) key.
Sparkle checks that signature before it will install anything, so a tampered
or substituted zip is rejected by the app even though the build itself is not
Developer ID signed or notarized.

The public half of that key is baked into the app's `Info.plist` as
`SUPublicEDKey`. The private half is never in either repository.

## Installing for the first time

Because these builds are ad-hoc signed rather than notarized, macOS Gatekeeper
will quarantine a manually downloaded copy. First installs need
`--no-quarantine` (the Homebrew cask handles this). Updates delivered through
Sparkle are unaffected — the app validates them itself.
