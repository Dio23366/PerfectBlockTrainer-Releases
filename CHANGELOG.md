# PerfectBlockTrainer Changelog

## V7.0.4 — Combat Reliability & Mixed-Threat Improvements

### Added

- Added validated direct-contact timing support for Black Ant projectiles.
- Added improved timing-prompt support for the Mysterious Stranger boss.
- Added stronger support for mixed melee and ranged combat.
- Added further coverage for previously problematic close-range attacks.

### Changed

- Improved QTE reliability during multi-enemy combat.
- Improved handling when melee, ranged, and projectile threats overlap.
- Improved multi-hit and special-attack timing behavior.
- Improved Earwig RockThrow prompt behavior during mixed combat.
- Improved handling of overlapping threats so active prompts are less likely to be visually displaced by another attack.
- Reduced redundant runtime processing to improve efficiency during normal gameplay.
- Updated compatibility and release validation for UE4SS_Grounded2 1.0.3.

### Fixed

- Fixed a mixed-combat prompt ownership issue that could cause an active ranged-attack QTE to be visually replaced by another incoming attack.
- Fixed the close-range Tick bite route that could be blocked in-game but previously fail to produce a QTE.
- Improved timing consistency for several Mysterious Stranger multi-hit and special attacks.
- Improved Black Ant projectile prompt timing and cleanup when the projectile misses or becomes invalid.
- Preserved validated blockable / unblockable warning behavior across the updated attack paths.

### Validated

- Normal melee combat — PASS
- Consecutive attacks — PASS
- Multi-hit attacks — PASS
- Multiple simultaneous threats — PASS
- Mixed melee and ranged combat — PASS
- Moving-body / charge attacks — PASS
- Ballistic projectile paths — PASS
- Black Ant direct-contact projectile timing — PASS
- Earwig RockThrow during mixed combat — PASS
- Mysterious Stranger boss timing prompts — PASS
- Previously problematic close-range attacks — PASS
- Blockable / unblockable warning behavior — PASS
- Save / map lifecycle — PASS
- Ring / Pointer cleanup — PASS
- Final public runtime acceptance — PASS
- Player-style clean-install release test — PASS
- Nexus download round-trip package identity — PASS
- Crash during accepted final release testing — NO

### Compatibility

- Grounded 2
- UE4SS_Grounded2 1.0.3

---

## V7.0.3 — Semantic Prediction & Coverage Expansion

### Added

- Expanded attack coverage across additional creatures and attack identities.
- Added validated ballistic projectile prediction.
- Added validated Earwig RockThrow support.
- Added stronger semantic separation between blockable attacks, unblockable warnings, and no-cue attacks.
- Added improved multi-phase handling for Mosquito DiveBomb.
- Added public release hardening for the distributed DLL.

### Changed

- Improved attack identity and semantic routing.
- Improved threat handling and cleanup when an attack becomes invalid or changes phase.
- Improved support for moving-body / charge attack behavior.
- Improved runtime stability and clean-install validation.
- Public distribution now removes nonessential development diagnostics and probe-only data.
- Public binary build-path information is sanitized.

### Fixed

- Preserved the real damaging first-pass QTE for normal Mosquito DiveBomb.
- Prevented the QTE from incorrectly reappearing during the post-first-pass non-damaging movement.
- Suppressed incorrect QTE behavior during Headless Cockroach phase 2.
- Preserved validated production behavior after Public Release Hardening.

### Validated

- Normal melee combat — PASS
- Consecutive attacks — PASS
- Multi-hit attacks — PASS
- Multiple simultaneous threats — PASS
- Moving-body / charge attacks — PASS
- Linear projectile paths — PASS
- Ballistic projectile paths — PASS
- Mosquito combat — PASS
- Mosquito DiveBomb segmentation — PASS
- Mosquito Combo — PASS
- Earwig RockThrow QTE / timing / Perfect Block — PASS
- Unblockable red warning behavior — PASS
- Mantis release smoke test — PASS
- Save / map lifecycle — PASS
- Ring / Pointer cleanup — PASS
- Clean-install release test — PASS
- Accepted final regression crash — NO

### Compatibility

- UE4SS_Grounded2 1.0.3

---

## V7.0.2 — Performance Fix

- Fixed the severe FPS drop that could occur while the QTE Pointer was active.
- Optimized runtime QTE Widget handling.
- Preserved gameplay timing, prediction behavior, UI, Blueprint assets, and LogicMods behavior from V7.0.1.
- Validated normal melee, consecutive attacks, multi-hit, multi-target combat, moving-body / charge attacks, linear projectiles, save / map reload, Ring / Pointer cleanup, and survival-map smoke testing.

---

## V7.0.1 — UE4SS_Grounded2 1.0.3 Compatibility Update

- Updated compatibility for UE4SS_Grounded2 1.0.3.
- Revalidated the established V7 gameplay baseline.
- Updated installation guidance and public packaging.

---

## V7.0 — First Public Release

- First public PerfectBlockTrainer release.
- Introduced the core runtime Perfect Block timing visualization workflow.
