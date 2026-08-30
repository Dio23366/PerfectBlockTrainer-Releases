# PerfectBlockTrainer Changelog

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
