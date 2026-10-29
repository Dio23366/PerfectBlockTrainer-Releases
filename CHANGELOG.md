# PerfectBlockTrainer Changelog

## V7.0.8 — Native Presentation Architecture & UE5.7 Migration

### Architecture / 架构

- Retained the C++ attack-prediction, threat-admission, arbitration and scheduling core.
- Added a versioned copied QTE snapshot boundary carrying world/attack/hit identities and assigned visual windows.
- Replaced the UE5.6 Widget/material/LogicMods display with a native C++ GDI+ drawing thread inside main.dll.
- Removed the intermediate companion EXE and bundled .NET runtime from the final package.
- 保留成熟预测核心，通过值快照连接 DLL 内原生绘图，不再依赖旧 UE5.6 显示资产。

### Combat and UX / 战斗与交互

- Added supported Termite-family melee and explosion warnings, plus Centipede combo, slam, emergence and follow-up routes.
- Preserved core-defined green/red/gold semantics with hollow frames and a red Bézier spindle.
- Added a loading preview with immediate green/red/gold frames and clearance-based cleanup.
- Replaced the historical F8 visibility cycle with automatic attack-driven display and cleanup.
- 白蚁与蜈蚣新增路线、原生圆环及启动演示；游走/冲刺头部接触提示仍延期。

### Distribution / 分发

- One PerfectBlockTrainerCpp folder with enabled.txt, default visual config and main.dll; no manual PBT mods.txt edit.
- Final native package: 223,237 bytes (about 218 KiB); old EXE/runtime package was about 66.9 MiB.
- Includes one combined third-party notice, not a player-facing checksum manifest.
- 升级移除旧 PBT LogicMods；中间 EXE 版另需清理 PBTQteAutoStart 并迁移个人配置。

### Verification scope / 验证范围

Native rendering passed offline core/renderer checks, display comparisons, window lifetime tests and a user-confirmed basic gameplay session. ZIP extraction, installed DLL identity and a legacy-free native host were checked separately. This does not relabel the historical V7.0.7 full-roster/clean-install results as a complete UE5.7 regression; broader multiplayer, long-run and final clean-package game testing retain their own scope.

### Compatibility

- Grounded 2 UE5.7.4, Windows x64
- Tested UE4SS_Grounded2 1.0.6 distribution

---



## V7.0.7 — Broader QTE Coverage, Dynamic Prediction & Visibility Control

### Added

- Added **F8 QTE visibility control** with three display states:
  - `FULL`
  - `DIM`
  - `HIDDEN`
- Added validated attack coverage for **Garden Masked Fighter / Mysterious Stranger**.
- Added validated attack coverage for **O.R.C. Broodmother**, including representative:
  - Slow 5-Combo
  - Fast 5-Combo
  - Fast 3-Combo
- Expanded the current known-creature QTE adaptation pass for the tested Grounded 2 version.

### Improved

- Improved second-layer dynamic prediction for complex moving threats.
- Improved relative-motion correction when the player approaches or moves away from an incoming attack.
- Improved representative charge / moving-body behavior for creatures including Mosquito, Wasp, Ladybug, and other charge-style enemies.
- Improved representative projectile prediction behavior for Black Ant and other validated projectile cases.
- Improved dynamic prediction behavior for additional creatures including Blue Butterfly and Bee.
- Improved long-range world-boss FixedContact handling so validated boss attacks are not delayed by ordinary-creature distance admission rules.
- Improved late-stage timing stability for O.R.C. Broodmother combo sequences.

### Behavior Boundary

- V7.0.7's coverage pass does **not** mean every animation should generate a normal blockable QTE.
- `NO_CUE`, attacks that are not handled as ordinary Perfect Block attacks, and explicitly deferred special attacks remain intentional exceptions.
- The new F8 visibility control changes presentation only; prediction and threat tracking continue while the UI is dimmed or hidden.

### Public Release Hardening

- Built the public release from a dedicated hardened public configuration.
- Excluded development-only diagnostic probes, shadow-observation surfaces, detailed development logging, and development-path exposure from the public build.
- Preserved promoted production logic for timing, resolver behavior, dynamic prediction, and attack-target authority.

### Validated

- Garden Masked Fighter / Mysterious Stranger representative attacks — **PASS**
- O.R.C. Broodmother representative attacks — **PASS**
- O.R.C. Broodmother Slow 5-Combo — **PASS**
- O.R.C. Broodmother Fast 5-Combo — **PASS**
- O.R.C. Broodmother Fast 3-Combo — **PASS**
- F8 `FULL → DIM → HIDDEN → FULL` cycling — **PASS**
- Representative Mosquito charge behavior — **PASS**
- Representative rolling / charge-style enemy behavior — **PASS**
- Release-package clean-install game test — **PASS**
- Fresh public runtime smoke test — **PASS**
- Fatal error during accepted final release testing — **NO**

### Compatibility

- Grounded 2
- UE4SS_Grounded2 1.0.4

---

## V7.0.6 — Expanded Combat Coverage & Boss Timing Improvements

### Added

- Expanded validated QTE coverage for additional complex enemies, bosses, and special variants.
- Added broader validated support for the ToeBiter family, including key OGRE / Leviathan variant attacks.
- Added validated AXL attack coverage for the main tested combat routes.
- Added and validated missing combo coverage for TayzT / RuzT / SphereBot, including the third combo hit.
- Added **GOLD overlap visualization** when the green Perfect Block windows of two independent blockable threats overlap.

### Improved

- Improved Lizard boss QTE admission, presentation, and contact timing across multiple attacks.
- Improved `Bite_01` double-contact handling so a correct first Perfect Block is not incorrectly contradicted by a later physical contact.
- Improved later-hit timing for Lizard Combo3 sequences.
- Improved long-range boss attack handling so QTE visibility is based on attack semantics and contact authority rather than a simple boss-root distance check.
- Improved attack commitment and cancellation handling to reduce both premature prompts and prompts that appear too late to react to.
- Preserved player reaction time while filtering short-lived or cancelled attack states.
- Increased GOLD overlap contrast to improve readability during multi-threat combat.

### Fixed

- Fixed `AM_Cockroach_Attack_Spray_Headless` timing for Cockroach Queen and Berserker General.
- Corrected the Headless Spray contact timing so the QTE aligns with the validated runtime contact window.
- Kept the Headless Spray correction scoped to the verified attack/source instead of applying a broad rule to unrelated Cockroach attacks.

### Release Hardening

- Built the public DLL with the dedicated `PUBLIC_RELEASE_HARDENED` configuration.
- Removed development-only diagnostics, runtime probes, detailed development logging, and development-path exposure from the public build.
- Preserved the accepted gameplay behavior while reducing public development observability.

### Validated

- Lizard boss representative attack routes — **PASS**
- Lizard `Bite_01` double-contact behavior — **PASS**
- Lizard Combo3 follow-up timing — **PASS**
- ToeBiter family / validated OGRE and Leviathan routes — **PASS**
- AXL representative attack routes — **PASS**
- TayzT / RuzT / SphereBot combo third hit — **PASS**
- Cockroach Queen Headless Spray — **PASS**
- Berserker General Headless Spray — **PASS**
- GOLD overlap QTE presentation — **PASS**
- Complex / overlapping threat presentation — **PASS**
- Fresh public runtime acceptance — **PASS**
- Final release clean-install runtime test — **PASS**
- QTE / UI runtime smoke test — **PASS**
- Fatal error during accepted final release testing — **NO**

### Compatibility

- Grounded 2
- UE4SS_Grounded2 1.0.4

---

## V7.0.5 — Combat Targeting & QTE Stability Improvements

### Improved

- Improved QTE reliability when several enemies attack at the same time.
- Improved prompt targeting during mixed Wasp + Mosquito combat.
- Improved handling when an enemy briefly changes target state during an attack, reducing cases where a valid QTE could disappear or switch to the wrong attack.
- Improved QTE cleanup for charge and movement-based attacks.
- Reduced unnecessary background checks when there is no active incoming threat.
- Kept the existing projectile timing and prediction behavior unchanged.

### Fixed

- Fixed rare mixed-combat cases where the correct QTE could be suppressed by another nearby attack.
- Fixed rare cases where a charge / movement attack could leave its QTE visible after the attack had already ended.
- Fixed an edge case where an old QTE could reappear after the corresponding attack was already over.
- Fixed a rare long-lasting stuck-QTE case caused by an attack ending without the usual cleanup event.

### Tested

- Wasp + Mosquito mixed combat — **PASS**
- Normal melee attacks — **PASS**
- Charge / movement attacks — **PASS**
- Projectile attacks — **PASS**
- QTE cleanup after attacks end — **PASS**
- Multiple overlapping threats — **PASS**
- Fresh-install release test — **PASS**
- General performance check — **PASS**
- Crash during accepted final release testing — **NO**

### Compatibility

- Grounded 2
- UE4SS_Grounded2 1.0.4

---

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
- Updated compatibility and release validation for UE4SS_Grounded2 1.0.4.

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
- UE4SS_Grounded2 1.0.4

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

- UE4SS_Grounded2 1.0.4

---

## V7.0.2 — Performance Fix

- Fixed the severe FPS drop that could occur while the QTE Pointer was active.
- Optimized runtime QTE Widget handling.
- Preserved gameplay timing, prediction behavior, UI, Blueprint assets, and LogicMods behavior from V7.0.1.
- Validated normal melee, consecutive attacks, multi-hit, multi-target combat, moving-body / charge attacks, linear projectiles, save / map reload, Ring / Pointer cleanup, and survival-map smoke testing.

---

## V7.0.1 — UE4SS_Grounded2 1.0.4 Compatibility Update

- Updated compatibility for UE4SS_Grounded2 1.0.4.
- Revalidated the established V7 gameplay baseline.
- Updated installation guidance and public packaging.

---

## V7.0 — First Public Release

- First public PerfectBlockTrainer release.
- Introduced the core runtime Perfect Block timing visualization workflow.
