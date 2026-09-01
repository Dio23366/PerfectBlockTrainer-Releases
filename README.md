<p align="center">
  <img src="media/cover.png" alt="PerfectBlockTrainer V7.0.4" width="100%">
</p>

<h1 align="center">PerfectBlockTrainer V7.0.4</h1>

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

## V7.0.4 Combat Reliability & Mixed-Threat Improvements / 实战可靠性与混合威胁改进

**PerfectBlockTrainer V7.0.4** focuses on improving QTE reliability during real combat, especially when multiple enemies, consecutive attacks, melee attacks, and ranged attacks overlap.

V7.0.4 also improves multi-hit and special-attack timing, expands validated projectile handling, and reduces unnecessary runtime work while preserving the core Perfect Block training workflow.

> **PerfectBlockTrainer V7.0.4** 重点提升复杂实战环境下的 QTE 提示可靠性，尤其针对多名敌人同时进攻、连续攻击，以及近战和远程攻击交错出现的情况。  
>
> 本版本同时改进多段攻击与特殊攻击的时机判断，扩展经过实战验证的射弹支持，并减少不必要的重复处理，同时保持原有的完美格挡训练与时机可视化体验。

### V7.0.4 highlights / 本次主要更新

- Improved QTE reliability in multi-enemy combat / 提升多敌人混战中的 QTE 提示稳定性
- Improved mixed melee and ranged attack handling / 改善近战与远程攻击同时出现时的提示处理
- Improved multi-hit and special attack timing / 改善多段攻击和特殊攻击的时机判断
- Added validated direct-contact timing for Black Ant projectiles / 增加黑蚂蚁射弹直接命中时的已验证时机支持
- Improved Earwig RockThrow prompts during mixed combat / 改善蠼螋投石在混战中的提示表现
- Improved several previously problematic close-range attacks / 改善多种此前容易漏提示或提示异常的近距离攻击
- Improved timing prompt support for the Mysterious Stranger boss / 改善神秘人 Boss 的攻击时机提示
- Reduced redundant runtime processing for better performance / 减少不必要的重复处理并改善运行效率
- Clean-install release validation / 玩家发行包全新安装验证

Compatible runtime:

- **UE4SS_Grounded2 1.0.3**
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

Representative validated V7.0.4 cases include:

- Multi-enemy combat
- Mixed melee and ranged combat
- Multi-hit and special attack sequences
- Mysterious Stranger boss attacks
- Black Ant direct-contact projectiles
- Earwig RockThrow during mixed combat
- Previously problematic close-range attacks
- Moving-body / charge attacks
- Multiple simultaneous threats
- Blockable / unblockable warning behavior

---

## Visual Semantics / 提示语义

PerfectBlockTrainer uses different visual cues depending on attack semantics:

- **Green QTE** — Perfect Block opportunity
- **Red warning** — Unblockable attack / dodge warning
- **No cue** — attacks that should not produce a Perfect Block prompt

> **绿色 QTE** 表示存在 Perfect Block 时机。  
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

Current demo version: **V7.0.3**

The current demo showcases:

- Multiple simultaneous threats / 多威胁同时预测
- Multi-hit prediction / 多段连击预测
- Timing mix-ups / 快慢刀
- Moving-body / charge prediction / 动态冲刺预测
- Projectile prediction / 飞行物预测
- Blockable vs. unblockable visual semantics / 可格挡与不可格挡提示
- Threat invalidation / 威胁失效
- Automatic Ring / Pointer cleanup / 自动清理提示

### Installation Video / 安装视频

▶ **[PerfectBlockTrainer Complete Installation Guide](https://www.bilibili.com/video/BV1ws4R6fEYL/)**

The installation video was originally recorded for an earlier V7 release, but the core installation flow remains applicable to V7.0.4 when using **UE4SS_Grounded2 1.0.3**.

Installation flow:

```text
Download
→ Install UE4SS_Grounded2 1.0.3
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

## V7.0.4 Runtime Validation / V7.0.4 运行验证

The final V7.0.4 public runtime passed automated release checks, manual gameplay acceptance, and a player-style clean-install test using the same final `RELEASE.zip` intended for public distribution.

Representative validated areas include:

- Normal melee combat — **PASS**
- Consecutive attacks — **PASS**
- Multi-hit attacks — **PASS**
- Multiple simultaneous threats — **PASS**
- Mixed melee and ranged combat — **PASS**
- Moving-body / charge attacks — **PASS**
- Ballistic projectile paths — **PASS**
- Black Ant direct-contact projectile timing — **PASS**
- Earwig RockThrow during mixed combat — **PASS**
- Mysterious Stranger boss timing prompts — **PASS**
- Previously problematic close-range attacks — **PASS**
- Blockable / unblockable warning behavior — **PASS**
- Save / map lifecycle — **PASS**
- Ring / Pointer cleanup — **PASS**
- Clean-install release test — **PASS**
- Crash during accepted final regression — **NO**

The final public `RELEASE.zip` was installed from a clean PerfectBlockTrainer state and tested as a player-distributed package before upload.

> 最终 V7.0.4 公开版不仅完成了发布前的运行验证和人工实战验收，还重新从玩家实际下载使用的 `RELEASE.zip` 进行了全新安装测试。  
>
> 正式发布包能够正常加载并进入游戏，代表性战斗场景中的 QTE、混战提示和基础稳定性均通过验收。

---

## Public Release Build / 公开发行版本

V7.0.4 uses a dedicated public release build that contains the gameplay functionality required by players without carrying unnecessary development-only diagnostics.

This does **not** change the validated attack-prediction or QTE behavior.

The final public build was built, checked, installed as the exact release package, and tested again before publication.

> V7.0.4 使用独立的公开发行版本，只保留玩家正常使用所需的功能。  
>
> 这不会改变已经验证过的攻击预测与 QTE 行为。最终公开包在发布前又以玩家实际安装方式进行了独立测试。

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

PerfectBlockTrainer V7.0.4 requires:

1. **Grounded 2**
2. **UE4SS_Grounded2 1.0.3**

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
PerfectBlockTrainer_V7.0.4_RELEASE.zip
```

Package structure:

```text
PerfectBlockTrainer_V7.0.4_RELEASE/
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
└─ RELEASE_MANIFEST_SHA256.txt
```

Validated installation flow:

```text
Install UE4SS_Grounded2 1.0.3
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

V7.0.4 was tested using a player-style clean installation.

The previous PerfectBlockTrainer installation was removed, and the final public `RELEASE.zip` was installed without using development build artifacts.

The clean-installed release successfully passed representative gameplay and basic runtime checks.

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

### PerfectBlockTrainer V7.0.4 Release ZIP

```text
PerfectBlockTrainer_V7.0.4_RELEASE.zip

SHA256
4A38939420C82F592E842B57B84CD931AFF689E0EF7F6BE4D0EDF737E364FDA4
```

### PerfectBlockTrainer V7.0.4 Runtime DLL

```text
main.dll

SHA256
84AF394E612F45C78E99EE6449F9AC2985353B4DC97E23A8CF97B75B17593037

Size
152064 bytes
```

### LogicMods

```text
PerfectBlockTrainer.pak

SHA256
D4D2572C2B17CCDD393A7A6826990ED01D518CE22057B9660FF48ECCB562FBE4
```

```text
PerfectBlockTrainer.utoc

SHA256
E724D71A8B113F7DD2B6E0FCF93F035153D6EE3DB0DB0B20E6A98AE440890393
```

```text
PerfectBlockTrainer.ucas

SHA256
4A4925F8FF8E9FC6AEDA041E9B33BBB78A1B1A8EAA10B62230DE9D0DFC144A4D
```

Modified or redistributed builds with different identities should be treated as **unofficial builds**.

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

**V7.0.4 — Combat Reliability & Mixed-Threat Improvements**

Current public runtime:

**UE4SS_Grounded2 1.0.3**

Current release channel:

**Stable**

Previous public releases:

```text
V7.0.3 — Semantic Prediction & Coverage Expansion
V7.0.2 — Performance Fix
V7.0.1 — UE4SS_Grounded2 1.0.3 Compatibility Update
V7.0   — First Public Release
```
