<p align="center">
  <img src="media/cover.png" alt="PerfectBlockTrainer V7.0.6" width="100%">
</p>

<h1 align="center">PerfectBlockTrainer V7.0.6</h1>

<p align="center">
  <b>Real-time Perfect Block Timing Assistant for Grounded 2</b>
</p>

<p align="center">
  <a href="https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases"><b>⬇ GitHub Release</b></a>
  &nbsp;•&nbsp;
  <a href="https://www.nexusmods.com/grounded2/mods/198"><b>⬇ Nexus Mods</b></a>
  &nbsp;•&nbsp;
  <a href="https://www.bilibili.com/video/BV1wh8R6iESi/"><b>▶ Gameplay Demo</b></a>
  &nbsp;•&nbsp;
  <a href="https://www.bilibili.com/video/BV1ws4R6fEYL/"><b>▶ Installation Video</b></a>
  &nbsp;•&nbsp;
  <a href="INSTALL.md"><b>Installation Guide</b></a>
</p>

---

## V7.0.6 Expanded Combat Coverage & Boss Timing Improvements / 扩展攻击覆盖与 Boss 时序改进

**PerfectBlockTrainer V7.0.6** expands validated QTE coverage for more complex enemies and bosses while improving timing accuracy and readability in multi-threat combat.

The release builds on the stable V7.0.5 behavior. New changes are scoped to validated attacks and presentation cases instead of applying broad global rules.

> **PerfectBlockTrainer V7.0.6** 在 V7.0.5 稳定行为基础上，进一步扩展复杂敌人和 Boss 的 QTE 攻击覆盖，并提升复杂攻击时序与多威胁场景下的提示可读性。  
>
> 本次修改尽量限定在已经验证的敌人、攻击和显示场景中，避免为了修复单个特殊攻击而改变无关攻击的既有行为。

### V7.0.6 highlights / 本次主要更新

- Expanded Lizard boss QTE coverage and timing validation / 扩展并完善 Lizard Boss 多种攻击的 QTE 覆盖与时序验证
- Improved Lizard `Bite_01` double-contact handling and Combo3 follow-up timing / 改善 `Bite_01` 双接触判定与 Combo3 后续攻击时序
- Expanded validated ToeBiter family support, including key OGRE / Leviathan variants / 扩展 ToeBiter 家族及 OGRE / Leviathan 关键变体的已验证支持
- Completed representative AXL attack coverage / 完成 AXL 主要攻击路线的实战闭环
- Completed TayzT / RuzT / SphereBot combo third-hit timing / 补齐并验证 TayzT / RuzT / SphereBot 连击第三击时序
- Fixed Cockroach Queen and Berserker General Headless Spray timing / 修复 Cockroach Queen 与 Berserker General 无头喷射攻击时序
- Added **GOLD overlap QTE presentation** for overlapping green Perfect Block windows / 新增多个绿色 Perfect Block 窗口重叠时的 **GOLD / 金色重叠区域**
- Improved attack commitment / cancellation filtering without sacrificing normal player reaction time / 改善复杂攻击启动与取消判断，同时避免过滤机制吃掉正常反应时间
- Public release built with dedicated hardening and final clean-install runtime validation / 公开版本经过独立 Release Hardening 与最终 clean-install 实机验证

### GOLD overlap presentation / GOLD 重叠提示

When two independent blockable attacks have overlapping green Perfect Block windows, the shared overlap region is displayed in **GOLD**.

This is a readability improvement only. It does **not** change attack timing, window size, or Grounded 2's Perfect Block rules.

> 当两个独立可格挡攻击的绿色 QTE 时间窗口发生重叠时，公共重叠区会使用 **GOLD / 金色** 显示。  
>
> 这一变化只影响提示显示，不会修改攻击时机、Perfect Block 窗口大小或游戏自身的 Perfect Block 判定。

Compatible runtime:

- **UE4SS_Grounded2 1.0.4**
- UE4SS Git SHA: `c838a8acaade1a0f860bdf249f039e58f4e10088`

---

## Overview / 项目简介

**PerfectBlockTrainer** is a runtime combat-training and timing-visualization mod for **Grounded 2**.

It displays a timing ring when an incoming attack is detected, helping the player understand **when to perform a Perfect Block**.

This is not a simple fixed countdown.

Different attack types can use different prediction paths and runtime information. Predictions may update, retarget, or disappear when the threat changes.

The player still performs the actual block manually.

> **PerfectBlockTrainer** 是一个面向《Grounded 2 / 禁闭求生 2》的完美格挡训练与时机可视化 Mod。  
>
> 当系统检测到即将到来的攻击时，会显示时机提示环，帮助玩家理解什么时候应该执行 Perfect Block。  
>
> 它不是简单播放固定倒计时。不同攻击类型可以使用不同的预测路径与运行时信息，并且当威胁状态变化时，预测可以更新、重新定位或自动消失。  
>
> 最终格挡操作仍然由玩家本人完成。

---

## Highlights / 主要功能

PerfectBlockTrainer currently supports multiple production prediction paths:

- **Fixed single-hit attacks / 普通单段攻击**
- **Fixed multi-hit attacks / 多段连击**
- **Multiple simultaneous threats / 多威胁同时预测**
- **Moving-body / charge attacks / 冲刺与移动本体攻击**
- **Linear projectile attacks / 直线投射物**
- **Ballistic projectile attacks / 弹道投射物**
- **Blockable / unblockable semantic handling / 可格挡与不可格挡语义处理**
- **Multi-phase attack handling / 多阶段攻击处理**
- Runtime prediction correction
- Threat retargeting
- Automatic cleanup when a threat becomes invalid
- Chronological handling of upcoming multi-hit threats
- Save / map lifecycle handling
- QTE Ring / Pointer cleanup

Representative current production coverage includes:

- Multi-enemy and mixed-threat combat
- Mixed melee and ranged combat
- Multi-hit and special attack sequences
- Lizard boss representative attack routes
- ToeBiter family validated routes, including key OGRE / Leviathan variants
- AXL representative attack routes
- TayzT / RuzT / SphereBot combo coverage
- Cockroach Queen / Berserker General Headless Spray timing
- Mysterious Stranger boss attacks
- Black Ant direct-contact projectiles
- Earwig RockThrow during mixed combat
- Moving-body / charge attacks
- Multiple simultaneous threats
- Blockable / unblockable warning behavior

---

## Visual Semantics / 提示语义

PerfectBlockTrainer uses different visual cues depending on attack semantics:

- **Green QTE** — Perfect Block opportunity
- **GOLD overlap** — shared overlap area of two blockable green Perfect Block windows
- **Red warning** — Unblockable attack / dodge warning
- **No cue** — attacks that should not produce a Perfect Block prompt

> **绿色 QTE** 表示存在 Perfect Block 时机。  
>
> **GOLD / 金色重叠区域** 表示两个独立可格挡攻击的绿色时间窗口发生重叠。  
>
> **红色提示** 表示该攻击不可进行 Perfect Block，应作为闪避 / 危险警告理解。  
>
> 某些不需要提示的攻击不会生成 QTE。

Red does **not** mean "hard attack" or "high damage".

It specifically represents an **unblockable warning** in the current PerfectBlockTrainer semantic model.

---

## Demo / 演示

### Gameplay Demo / 功能演示

▶ **[Watch the PerfectBlockTrainer Gameplay Demo on Bilibili](https://www.bilibili.com/video/BV1wh8R6iESi/)**

This is the long-term PerfectBlockTrainer gameplay demo and will be updated as the mod evolves.

The long-term gameplay demo is maintained separately and may be updated alongside the current release.

The long-term demo focuses on:

- Multi-enemy mixed combat / 多怪物混合攻击
- Real-time projectile prediction / 投射物实时预测
- Real-time projectile tracking / 飞行物实时追踪
- Boss attack compatibility / Boss 攻击适配
- Unblockable attack warnings / 不可格挡攻击警告
- Dynamic charge attack prediction / 动态冲刺攻击预测

### Installation Video / 安装视频

▶ **[PerfectBlockTrainer Complete Installation Guide](https://www.bilibili.com/video/BV1ws4R6fEYL/)**

The installation video was originally recorded for an earlier V7 release, but the core installation flow remains applicable to V7.0.6 when using **UE4SS_Grounded2 1.0.4**.

Installation flow:

```text
Download
→ Install UE4SS_Grounded2 1.0.4
→ Verify UE4SS
→ Install PerfectBlockTrainerCpp
→ Install LogicMods
→ Edit mods.txt
→ Launch Grounded 2
→ Enter a save
→ Test Ring / Pointer / QTE
```

Bilibili creator page:

**[bili_55415870362](https://space.bilibili.com/3546748811217856)**

Nexus Mods page:

**[PerfectBlockTrainer on Nexus Mods](https://www.nexusmods.com/grounded2/mods/198)**

---

## Perfect Block UI / 界面说明

The timing UI uses:

- **White ring** — timing cycle
- **Green arc** — recommended Perfect Block timing window
- **GOLD overlap** — overlap between two independent green Perfect Block windows
- **Red pointer** — current timing position
- **Multiple rings** — upcoming multi-hit threats

> The green arc represents the **gameplay timing window**.  
> It does **not** necessarily represent the exact visual frame where the enemy model appears to touch the player.

For unblockable attacks, PerfectBlockTrainer can use a **red warning semantic** instead of the normal green Perfect Block cue.

---

## How It Works / 工作方式

At a high level, PerfectBlockTrainer follows this runtime flow:

```text
Attack Runtime Event
        ↓
Attack Identity
        ↓
Cue Semantic
        ↓
Collision / Attack Topology
        ↓
Prediction
        ↓
Threat
        ↓
Arbitration / Forecast
        ↓
Scheduler
        ↓
QTE Bridge
        ↓
PerfectBlockTrainer UI
```

Current production prediction families include:

```text
FIXED_SINGLE
FIXED_MULTI
MOVING_BODY
LINEAR_PROJECTILE
BALLISTIC_PROJECTILE
```

The runtime is event-driven.

```text
No valid incoming threat
→ No active QTE
```

If an attack becomes invalid, misses, changes target, or enters a phase that should not produce a Perfect Block prompt, the associated prediction can be removed automatically.

---

## V7.0.6 Release Testing / V7.0.6 发布测试

Before release, V7.0.6 completed final public-runtime acceptance and a player-style clean-install test using the formal release package.

Validated release scenarios include:

- Lizard boss representative attack routes — **PASS**
- Lizard `Bite_01` double-contact behavior — **PASS**
- Lizard Combo3 follow-up timing — **PASS**
- ToeBiter family / validated OGRE and Leviathan routes — **PASS**
- AXL representative attack routes — **PASS**
- TayzT / RuzT / SphereBot combo third hit — **PASS**
- Cockroach Queen Headless Spray — **PASS**
- Berserker General Headless Spray — **PASS**
- GOLD overlap QTE presentation — **PASS**
- Multi-threat QTE / UI smoke test — **PASS**
- Final release clean-install game test — **PASS**
- Independent release audit — **PASS**
- Fatal error during accepted final release testing — **NO**

The public DLL was also checked for development-only exposure before release.

> V7.0.6 在发布前完成了正式 Public Runtime 验收，并使用最终 Release 包执行玩家式 clean-install 实机测试。  
>
> Lizard Boss、ToeBiter 家族、AXL、TayzT / RuzT / SphereBot 连击第三击、Cockroach Queen / Berserker General 无头喷射、GOLD 重叠显示以及多威胁 QTE / UI 均完成最终验证。最终验收中没有发生 Fatal Error。

### Public Release Hardening / 公开版本硬化

The public DLL is built with the dedicated `PUBLIC_RELEASE_HARDENED` configuration. Development-only diagnostics, runtime probe surfaces, detailed development logging, and development-path exposure are removed while preserving accepted gameplay behavior.

> 公开 DLL 使用独立的 `PUBLIC_RELEASE_HARDENED` 构建配置，移除开发调试、runtime probe、详细开发日志和开发路径等暴露面，同时保持已经验收的 gameplay 行为。

---

## Release Package / 发布包

The V7.0.6 package provided to players is the same release package used for the final clean-install runtime test.

It contains the files required to run PerfectBlockTrainer and does not include development files.

> 玩家下载到的 V7.0.6 与最终 clean-install 实机测试使用的是同一个发布包。  
>
> 发布包只包含运行 PerfectBlockTrainer 所需的文件，不包含开发文件。

---

## Public Release Boundary / 公共版本能力边界

PerfectBlockTrainer is designed for:

- Combat training
- Timing visualization
- Attack prediction
- Attack warnings
- Perfect Block practice

PerfectBlockTrainer does **not** provide:

- Automatic blocking
- Automatic dodging
- Automatic player input
- Damage modification
- Inventory modification
- Save manipulation
- Network manipulation
- Remote-player manipulation
- Anti-detection or bypass functionality

The mod predicts and visualizes timing.

**The player always performs the actual combat input.**

---

## Requirements / 依赖

PerfectBlockTrainer V7.0.6 requires:

1. **Grounded 2**
2. **UE4SS_Grounded2 1.0.4**

Required entries in `mods.txt`:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

**No additional gameplay mod is required.**

> `BPML_GenericFunctions` and `BPModLoaderMod` are part of the supported UE4SS_Grounded2 setup and are used by the Blueprint UI lifecycle.

---

## Installation / 安装

Download the current release from:

- **[Nexus Mods — PerfectBlockTrainer](https://www.nexusmods.com/grounded2/mods/198)**
- **[GitHub Releases — PerfectBlockTrainer](https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases)**

Then follow:

**[INSTALL.md](INSTALL.md)**

Installation video:

**[PerfectBlockTrainer Complete Installation Guide](https://www.bilibili.com/video/BV1ws4R6fEYL/)**

Current release package:

```text
PerfectBlockTrainer_V7.0.6_RELEASE.zip
```

Package structure:

```text
PerfectBlockTrainer_V7.0.6_RELEASE/
├─ Mods/
│  └─ PerfectBlockTrainerCpp/
│     └─ dlls/
│        └─ main.dll
│
├─ LogicMods/
│  ├─ PerfectBlockTrainer.pak
│  ├─ PerfectBlockTrainer.ucas
│  └─ PerfectBlockTrainer.utoc
│
├─ INSTALL.txt
├─ VERSION.txt
├─ RELEASE_NOTES.md
└─ RELEASE_MANIFEST_SHA256.tsv
```

Validated installation flow:

```text
Install UE4SS_Grounded2 1.0.4
↓
Launch Grounded 2 once to verify UE4SS
↓
Install PerfectBlockTrainerCpp
↓
Install all three PerfectBlockTrainer LogicMods files
↓
Enable PerfectBlockTrainerCpp in mods.txt
↓
Launch Grounded 2
↓
Enter a save
↓
Test Ring / Pointer / QTE
```

---

## Clean Installation / 全新安装验证

V7.0.6 was tested using a player-style clean installation of the final public release package.

The previous PerfectBlockTrainer installation was removed, and the final public `RELEASE.zip` was installed without using development build artifacts.

The clean-installed exact release successfully passed representative mixed-combat, QTE, lifecycle, and basic runtime checks, then restored the pre-release development environment exactly.

This verifies that the public package itself contains the files required for normal installation and operation.

---

## Known Limitations / 当前限制

PerfectBlockTrainer does not claim complete validation of every creature and every attack in Grounded 2.

Current limitations include:

- Some uncommon or special attack patterns may still require dedicated runtime validation.
- Some projectile or special-topology attacks may not yet have a validated production prediction path.
- Different attacks from the same enemy can behave differently.
- Multiplayer validation has primarily focused on the **host-side** scenario.
- Future Grounded 2 updates may change runtime behavior or hooks and may require compatibility fixes.
- PerfectBlockTrainer is a training / visualization tool and does not change the game's actual Perfect Block rules.

If an attack produces no QTE, incorrect timing, or the wrong semantic warning, please report the specific enemy and attack.

---

## Community Testing / 社区测试

Community feedback is an important part of expanding PerfectBlockTrainer's attack coverage.

When reporting a problem, please include as much of the following as possible:

```text
Enemy / Creature
Attack / Move name if known
Single / Combo / Charge / Projectile
Blockable / Unblockable if known
Expected behavior
Actual behavior
Missing / Early / Late / Incorrect QTE
Game version
PerfectBlockTrainer version
UE4SS version
Video / GIF if possible
```

If the issue can be reproduced consistently but cannot be reproduced during development, `UE4SS.log` may also be helpful.

Recommended issue categories:

```text
BUG
ATTACK MISSING
TIMING WRONG
FALSE QTE
UNBLOCKABLE WARNING
PROJECTILE
UI
PERFORMANCE
COMPATIBILITY
```

Different attacks from the same creature are useful to report separately.

---

## Release Integrity / 发布校验

Only packages distributed through the official PerfectBlockTrainer channels should be considered official builds.

### PerfectBlockTrainer V7.0.6 Release ZIP

```text
PerfectBlockTrainer_V7.0.6_RELEASE.zip

SHA256
89363449D86CA6A92905BD681EF1AD48C4C77DB6124FD4AD20C068EC19F5AAD0
```

### PerfectBlockTrainer V7.0.6 Runtime DLL

```text
main.dll

SHA256
6D0316BEAD101BC8BC35981356022236A10AE7489215B2DD91C065579BEE241D
```

Modified or redistributed builds with different identities should be treated as **unofficial builds**.

The release ZIP SHA256 is the package-level identity. The release package also contains `RELEASE_MANIFEST_SHA256.tsv` for its packaged file manifest.

See [`SHA256SUMS.txt`](SHA256SUMS.txt) for the public release hash list.

---

## Repository / 仓库说明

This repository is the official **public distribution repository** for PerfectBlockTrainer.

Public content includes:

- Release documentation
- Installation documentation
- Changelogs
- Media
- Public release hashes
- Official binary release packages

Development source code, internal runtime evidence, development probes, build artifacts, backups, and Formal Freeze archives are maintained separately and are **not distributed through this repository**.

---

## Public Links / 公开页面

- **Nexus Mods:** [PerfectBlockTrainer](https://www.nexusmods.com/grounded2/mods/198)
- **GitHub Public Repository:** [PerfectBlockTrainer-Releases](https://github.com/Dio23366/PerfectBlockTrainer-Releases)
- **GitHub Releases:** [PerfectBlockTrainer Releases](https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases)
- **Gameplay Demo:** [BV1wh8R6iESi](https://www.bilibili.com/video/BV1wh8R6iESi/)
- **Installation Video:** [BV1ws4R6fEYL](https://www.bilibili.com/video/BV1ws4R6fEYL/)
- **Bilibili Creator Page:** [bili_55415870362](https://space.bilibili.com/3546748811217856)

---

## Credits

Built for **Grounded 2** using **UE4SS**.

Thanks to the UE4SS / RE-UE4SS project and community for the modding framework.

Grounded 2 is developed by **Obsidian Entertainment** and published by **Xbox Game Studios**.

---

## Version

**V7.0.6 — Expanded Combat Coverage & Boss Timing Improvements**

Current public runtime:

**UE4SS_Grounded2 1.0.4**

Current release channel:

**Stable**

Previous public releases:

```text
V7.0.5 — Combat Targeting & QTE Stability Improvements
V7.0.4 — Combat Reliability & Mixed-Threat Improvements
V7.0.3 — Semantic Prediction & Coverage Expansion
V7.0.2 — Performance Fix
V7.0.1 — UE4SS_Grounded2 1.0.4 Compatibility Update
V7.0   — First Public Release
```
