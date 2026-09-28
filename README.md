<p align="center">
  <img src="media/cover.png" alt="PerfectBlockTrainer V7.0.6" width="100%">
</p>

<h1 align="center">PerfectBlockTrainer V7.0.6</h1>

<p align="center">
  <b>Real-time Combat Training & Threat Decision System for Grounded 2</b>
</p>

<p align="center">
  Turns hidden combat timing into observable, real-time player feedback without automating player input.<br>
  将隐藏的战斗时序转化为可观察的实时反馈，同时保留玩家自己的判断与操作。
</p>

<p align="center">
  <a href="https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases"><b>GitHub Releases</b></a>
  &nbsp;•&nbsp;
  <a href="https://www.nexusmods.com/grounded2/mods/198"><b>Nexus Mods</b></a>
  &nbsp;•&nbsp;
  <a href="https://www.bilibili.com/video/BV1wh8R6iESi/"><b>Gameplay Demo</b></a>
  &nbsp;•&nbsp;
  <a href="INSTALL.md"><b>Installation Guide</b></a>
</p>

---

## Product Overview / 产品概述

**PerfectBlockTrainer** started from a simple player problem: in complex combat, the timing behind Perfect Block opportunities is difficult to observe, understand, and practice reliably.

Instead of automating combat, the product converts hidden runtime timing into player-facing decision support:

```text
System predicts
→ UI explains
→ Player decides
→ Game validates
```

The system evolved from a simple timing assistant into a layered real-time threat decision system because increasingly complex combat scenarios exposed failure modes that simpler logic could not handle reliably.

**中文说明**

PerfectBlockTrainer 从一个真实玩家问题出发：复杂战斗中的完美格挡时序原本隐藏在动画和 Runtime 中，玩家很难稳定观察、理解和练习。

它不替玩家自动格挡，而是负责“预测并解释”，让玩家自己做决定，再由游戏结果验证判断是否正确。

随着多段攻击、冲刺、投射物、多敌人和攻击取消等场景不断出现，原本简单的 Timing 逻辑逐渐不足，因此系统才演进成后面的分层 Threat Decision System。

### Public release & usage / 公开发布与使用情况

- **Stable Public Release:** V7.0.6
- **435 Unique Downloads** on Nexus Mods
- **645 Total Downloads** on Nexus Mods
- **2,897 Nexus Views**
- **7 Endorsements**
- **8,138+ views** on the long-term Bilibili gameplay demo
- **6 public iteration rounds** after the initial V7.0 release
- Real-user feedback covering performance, compatibility, installation, attack coverage, and UX

> Nexus download and view counts reflect public distribution and discovery activity. They are not treated as DAU, retention, or active-user metrics.
>
> Nexus 的下载与浏览数据只作为公开发布和 Adoption 信号使用，不等同于 DAU、留存或活跃用户指标。

---

## Development Scope / 开发范围

PerfectBlockTrainer is independently designed, implemented, validated, released, and maintained as an end-to-end public project.

The project scope includes:

- Player problem discovery and product boundary definition
- Runtime decision-system architecture and interaction design
- AI-assisted implementation and iterative technical validation
- Runtime semantic reconstruction, state transitions, and threat lifecycle design
- Release prioritization across compatibility, performance, attack coverage, reliability, and UX
- Real-user issue reproduction, root-cause analysis, and regression validation
- Runtime validation, release hardening, clean-install acceptance, and public packaging
- Release documentation, demos, and community feedback maintenance

Rather than being maintained as a one-off prototype, the project follows a continuous product loop:

```text
Player Problem
→ System Design
→ Implementation
→ Runtime Validation
→ Public Release
→ User Feedback
→ Iteration
```

**中文说明**

这个项目不是一次性 Demo。开发范围同时覆盖产品问题定义、系统设计、AI-assisted implementation、运行时验证、公开发布、用户反馈和后续迭代。

重点不只是“功能能不能跑”，而是产品在真实发布后能否被安装、理解、稳定使用，并在出现问题后形成可重复验证的修复闭环。

---

## Product Problem / 产品问题

Perfect Block timing in Grounded 2 is often difficult to learn through visual animation alone, especially when combat includes:

- Multi-hit attacks
- Charge / moving-body attacks
- Linear or ballistic projectiles
- Multiple enemies attacking at the same time
- Target changes
- Interrupted or cancelled attacks
- Different blockable / unblockable semantics

A fixed countdown is not enough because the threat itself can move, disappear, become invalid, change target, or overlap with other threats.

The product therefore focuses on **decision support**, not automation.

**中文说明**

如果所有攻击都只是固定动画、固定时间，那么一个简单倒计时就足够了。

但真实战斗中，攻击可能移动、切换目标、被打断、失效、与其他攻击重叠，甚至不同攻击需要不同物理预测方式。因此产品真正解决的问题不是“显示一个倒计时”，而是持续判断：**当前什么攻击仍然构成威胁、什么时候可能接触玩家，以及哪些信息值得展示。**

---

## Concept Map / 核心概念速览

The following terms are used throughout the project as domain concepts rather than generic buzzwords.

| Concept | Meaning in PerfectBlockTrainer / 在 PBT 中的实际含义 |
|---|---|
| **Runtime Observation / 运行时观察** | Capture what actually happened in the game runtime：获取攻击、目标、位置、速度、投射物和结果等事实 |
| **Semantic Reconstruction / 语义重建** | Convert raw callbacks into attack meaning：把原始事件还原成“这是什么攻击、哪一段、什么语义” |
| **Prediction / 预测** | Estimate when and how a candidate may contact the player：估计攻击何时、以什么方式可能接触玩家 |
| **Threat Admission / 威胁准入** | Decide whether a predicted candidate is truly eligible to become a threat：判断预测结果是否真的有资格进入正式 Threat 系统 |
| **Threat Lifecycle / 威胁生命周期** | Manage creation, update, invalidation, expiration and cleanup：管理威胁从创建、更新到失效、过期和清理 |
| **Authority / 状态控制权** | Decide which state is still allowed to update the current threat：决定多个旧/新状态并存时谁仍有权更新当前 Threat |
| **Arbitration / 多威胁仲裁** | Decide which valid threats should receive priority when several exist：多个有效威胁同时存在时决定优先处理谁 |
| **Scheduler / 调度** | Convert changing threat states into stable show/update/retarget/clear behavior：把变化中的 Threat 状态转成稳定的显示、更新、切换和清理行为 |
| **Ground Truth / 实际结果** | Use real game outcomes to validate assumptions and regressions：用真实格挡、命中、Miss、取消等结果验证系统判断 |

---

## System Architecture / 系统架构

At a high level, the current production architecture is:

```text
Game Runtime
↓
Runtime Observation / 运行时观察
发生了什么？
Attack / Target / Position / Velocity / Projectile / Outcome
↓
Semantic Reconstruction / 语义重建
这是什么攻击？
Source / Montage / AttackGeneration / HitIndex / Cue
↓
Collision Topology / Algorithm Routing
碰撞拓扑与算法路由：这类威胁应该用哪种预测方式？
Fixed / Moving Body / Linear Projectile / Ballistic Projectile
↓
Topology-specific Prediction / 分类型预测
什么时候、以什么方式可能接触玩家？
↓
Threat Qualification / Admission / 威胁准入
它现在真的算有效威胁吗？
↓
Threat Lifecycle / Authority / 生命周期与状态控制权
它是否仍然有效？哪个状态仍有权更新它？
↓
Multi-threat Arbitration / 多威胁仲裁
多个有效威胁同时存在时先处理谁？
↓
Scheduler / 调度
什么时候显示、更新、切换或清除？
↓
QTE Presentation / 提示呈现
玩家最终看到什么？
↓
Player Decision / 玩家决策
↓
Game Outcome / Ground Truth / 游戏结果与真实验证
```

Current production prediction families include:

```text
FIXED_SINGLE
FIXED_MULTI
MOVING_BODY
LINEAR_PROJECTILE
BALLISTIC_PROJECTILE
```

The runtime is event-driven:

```text
No valid incoming threat
→ No active QTE
```

If an attack becomes invalid, misses, changes target, is interrupted, or enters a phase that should not produce a Perfect Block prompt, the corresponding threat can be revoked and removed.

**中文理解**

这条链路的核心不是把所有攻击塞进同一个算法，而是先区分“事实、语义、预测、资格、状态和展示”。这样某个 Case 出错时，可以判断到底是观察错了、理解错了、预测错了，还是预测虽然正确但根本不应该被展示。

---

## Why the Architecture Evolved / 为什么系统会演进成这样

The architecture was **not** designed for complexity. Each layer was introduced because a simpler assumption failed in real runtime scenarios.

> 复杂度不是设计目标，而是问题复杂度留下来的结果。只有当更简单的假设在真实 Runtime 中失败时，才增加新的机制。

### 1. Observation ≠ Meaning / 观察到事件 ≠ 理解事件含义

A runtime callback tells the system that something happened, but not necessarily what the attack means.

Therefore the system reconstructs semantic identity using information such as:

- Source
- Montage
- AttackGeneration
- HitIndex
- Cue semantics
- Target relationship

**Design consequence:** raw runtime events are separated from semantic interpretation.

**中文理解**

游戏告诉系统“发生了一个事件”，不代表系统已经知道“这是哪一次攻击、哪一段连击、是否可格挡、属于哪个目标关系”。

因此 Runtime Event 先作为事实进入系统，再由 Semantic Reconstruction 把它还原成可用于后续判断的攻击语义。

---

### 2. Attack ≠ Threat / 发动攻击 ≠ 始终构成有效威胁

An enemy starting an attack does not mean the attack remains a valid player threat.

The attack may later be:

- Interrupted
- Stunned
- Cancelled
- Invalidated by death
- Retargeted
- Physically missed

**Design consequence:** attack lifecycle, threat lifecycle, authority, revocation, and cleanup are explicit parts of the system.

**中文理解**

例如怪物已经发动攻击，但随后被打断、击晕、击杀，或者已经切换目标，那么原来的 QTE 就不能继续残留。

这就是 **Threat Lifecycle / 威胁生命周期** 存在的原因：它负责管理 Threat 从创建、激活、更新，到被撤销、失效、过期和清除的完整状态变化。

**Authority / 状态控制权** 则解决另一类问题：旧攻击、旧预测、新目标和新的 Runtime Event 可能同时存在，系统需要明确“哪个状态仍然有资格更新当前 Threat”，避免已经失效的旧状态重新覆盖新状态。

---

### 3. Prediction ≠ Admission / 能预测接触时间 ≠ 有资格成为正式威胁

A contact time can be mathematically predicted while the candidate is still not a legitimate threat to the player.

**Design consequence:** prediction and threat admission are separated so invalid or weak candidates do not automatically become player-facing prompts.

**中文理解**

“数学上能算出什么时候会碰到玩家”不代表这个候选攻击就应该进入正式 Threat 系统。

比如 Source、Target Relationship、当前攻击代次或物理关系已经失效，预测本身仍可能给出一个时间值。**Threat Admission / 威胁准入** 就是 Prediction 与正式 Threat 之间的资格门：先判断这个预测是不是一个真实、合法、仍与玩家相关的威胁，再允许它进入后续流程。

---

### 4. Admission ≠ Presentation / 是有效威胁 ≠ 一定立刻展示

Multiple valid threats can exist at the same time while player attention and visible UI capacity are limited.

**Design consequence:** multi-threat arbitration and scheduling determine what should be shown, updated, retained, or cleared.

**中文理解**

多个 Threat 可以同时全部“合法”，但玩家注意力和 UI 槽位是有限的。

因此 **Multi-threat Arbitration / 多威胁仲裁** 负责决定多个有效威胁中谁优先；**Scheduler / 调度** 再把持续变化的 Threat 状态转换成稳定的 show / update / retarget / clear 行为，避免 UI 因瞬时排序变化而频繁抖动或残留。

---

### 5. System Decision ≠ Player Action / 系统判断 ≠ 替玩家操作

The system decides what information should be shown, but it does **not** perform the block for the player.

**Design consequence:**

```text
System predicts
→ UI explains
→ Player decides
→ Game validates
```

This preserves player agency and keeps the product in the category of training / decision support rather than combat automation.

**中文理解**

PBT 的边界是“系统负责预测和解释，玩家负责决策和操作”。即使系统判断某个时间点值得提示，也不会自动执行 Block。

这保证了产品仍然是训练和 Decision Support，而不是 Combat Automation。

---

## Performance Incident: QTE-active FPS Drop / 性能问题与修复

One representative post-release incident came from real user feedback.

A user reported that while the QTE pointer was active during enemy attacks, frame rate could drop from roughly **120 FPS to around 10 FPS**, then recover after the attack ended.

The response was not to broadly rewrite the rendering or prediction system.

```text
User symptom / 用户现象
↓
Clarify trigger boundary / 明确触发边界
↓
Reproduce / 复现
↓
Collect runtime evidence / 收集运行时证据
↓
Find first responsible layer / 找到最早出错层
↓
Root cause / 根因
repeated Widget rediscovery while the QTE Pointer was active
QTE Pointer 激活期间重复查找 Widget
↓
Minimum fix / 最小修复
cache the valid Widget reference
缓存有效 Widget 引用
↓
Regression validation / 回归验证
↓
Public V7.0.2 release / 发布 V7.0.2
↓
User re-confirmed the FPS drop was gone
用户再次确认掉帧问题消失
```

This incident established a debugging and release principle used throughout later development:

> **User feedback is a symptom, not automatically a requirement. Reproduce first, locate the earliest wrong layer, apply the minimum responsible fix, then run regression.**
>
> **用户反馈首先是 Symptom，而不是自动变成 Requirement。先复现，再定位最早错误层，只修改最小责任范围，最后通过 Regression 确认修复没有破坏其他正常 Case。**

The fix was then retained as a regression case so later changes could be checked against the same failure pattern rather than relying on one-time confirmation.

---

## Product Evolution / 产品演进

PerfectBlockTrainer did not move through versions by adding features at random. Priorities changed with product maturity.

```text
V7.0.0
First public release / 首次公开发布
↓
V7.0.1
Compatibility / availability
兼容性与可用性
↓
V7.0.2
Severe performance badcase fix
严重性能 Badcase 修复
↓
V7.0.3
Coverage / semantics / projectile capability
攻击覆盖、语义与投射物能力
↓
V7.0.4
Complex-combat reliability turning point
复杂战斗可靠性转折点
↓
V7.0.5
Target authority / lifecycle / mixed-combat stability
目标控制、生命周期与混合战斗稳定性
↓
V7.0.6
Boss & variant coverage / readability / release hardening
Boss 与变体覆盖、可读性、发布硬化
```

Release priorities evolved roughly as:

```text
Availability / 可用
→ Correctness / 正确
→ Reliability / 可靠
→ Coverage / 覆盖
→ UX & Readability / 可读与易用
→ Release Quality / 发布质量
```

Later releases therefore focus less on simply adding features and more on stable behavior, failure boundaries, regression safety, and release confidence.

**中文说明**

版本优先级不是固定的。早期首先解决“能不能正常使用”，随后才逐渐转向正确性、复杂场景稳定性、覆盖、UX 和 Release Quality。

因此后期版本增加功能的同时，也会更严格地考虑 Failure Boundary、Regression Risk 和发布可信度，而不是单纯追求支持更多攻击。

Detailed per-version feature changes and player-facing patch information are maintained through **Nexus Mods** and **GitHub Releases** rather than duplicated here.

---

## Reliability & Release Engineering / 可靠性与发布

V7.0.6 completed a dedicated public-runtime acceptance process before release.

Representative accepted scenarios include:

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

**中文说明**

这里的“发布完成”不是只指代码编译成功。最终 Public Release 需要通过代表性攻击路线、多威胁 UI、clean-install 和独立 Release Audit，确认最终分发包本身能够正常运行。

### Public Release Hardening / 公开版本硬化

The public DLL is built using a dedicated `PUBLIC_RELEASE_HARDENED` configuration.

Development-only surfaces such as detailed diagnostics, runtime probes, development logging, and development-path exposure are removed while preserving accepted gameplay behavior.

**中文说明**

开发环境需要 Probe、详细日志和诊断能力，但玩家版本不应该携带这些开发暴露面。因此 Public Build 会在保留已验收 Gameplay 行为的前提下，移除仅用于开发的诊断、路径和日志信息。

### Clean-install Validation / 全新安装验证

The final public release package itself was used for player-style clean-install testing.

The process intentionally avoided relying on development build artifacts, so the accepted release package and the package distributed to players are the same release unit.

**中文说明**

最终验证使用的就是玩家实际下载到的 Release Package，而不是开发机上额外存在的文件。这样可以避免“开发环境能跑，但正式包缺文件”的发布问题。

---

## Product Boundary / 产品边界

PerfectBlockTrainer is designed for:

- Combat training / 战斗训练
- Timing visualization / 时序可视化
- Attack prediction / 攻击预测
- Threat warnings / 威胁提示
- Perfect Block practice / 完美格挡练习

PerfectBlockTrainer does **not** provide:

- Automatic blocking / 自动格挡
- Automatic dodging / 自动闪避
- Automatic player input / 自动玩家输入
- Damage modification / 伤害修改
- Inventory modification / 背包修改
- Save manipulation / 存档修改
- Network manipulation / 网络修改
- Remote-player manipulation / 远端玩家操控
- Anti-detection or bypass functionality / 反检测或绕过功能

**The player always performs the actual combat input. / 最终战斗操作始终由玩家本人完成。**

---

## Current Public Capabilities / 当前公开能力

PerfectBlockTrainer currently supports multiple production prediction and presentation paths:

- Fixed single-hit attacks / 固定单段攻击
- Fixed multi-hit attacks / 固定多段攻击
- Multiple simultaneous threats / 多威胁同时预测
- Moving-body / charge attacks / 冲刺与移动本体攻击
- Linear projectile attacks / 直线投射物
- Ballistic projectile attacks / 弹道投射物
- Blockable / unblockable semantic handling / 可格挡与不可格挡语义
- Multi-phase attack handling / 多阶段攻击
- Runtime prediction correction / 运行时预测修正
- Threat retargeting / 威胁重新绑定目标
- Automatic cleanup when threats become invalid / 无效 Threat 自动清理
- Chronological handling of upcoming multi-hit threats / 多段威胁按接触顺序处理
- Save / map lifecycle handling / 存档与地图生命周期处理
- QTE Ring / Pointer cleanup / QTE Ring 与 Pointer 清理

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

> Detailed creature- and attack-level patch information is maintained on Nexus Mods and GitHub Releases.
>
> 具体怪物、攻击路线和版本级 Patch 信息主要维护在 Nexus Mods 与 GitHub Releases；本 README 更关注产品工作方式和系统能力。

---

## Visual Semantics / 提示语义

PerfectBlockTrainer uses different visual cues depending on attack semantics:

- **Green QTE / 绿色 QTE** — Perfect Block opportunity / 存在 Perfect Block 时机
- **GOLD overlap / 金色重叠区** — shared overlap area of two blockable green Perfect Block windows / 两个独立可格挡窗口的公共重叠区域
- **Red warning / 红色警告** — Unblockable attack / dodge warning / 不可格挡攻击或闪避警告
- **No cue / 不显示提示** — attacks that should not produce a Perfect Block prompt / 不应产生 Perfect Block QTE 的攻击

Red does **not** mean "hard attack" or "high damage". It specifically represents an **unblockable warning** in the current PerfectBlockTrainer semantic model.

The GOLD overlap is a readability feature only. It does not change attack timing, Perfect Block window size, or Grounded 2 combat rules.

---

## Demo / 演示

### Gameplay Demo / 功能演示

▶ **[Watch the PerfectBlockTrainer Gameplay Demo on Bilibili](https://www.bilibili.com/video/BV1wh8R6iESi/)**

Current public demo signal: **8,138+ views**.

The long-term gameplay demo focuses on:

- Multi-enemy mixed combat
- Real-time projectile prediction
- Real-time projectile tracking
- Boss attack compatibility
- Unblockable attack warnings
- Dynamic charge attack prediction

### Installation Video / 安装视频

▶ **[PerfectBlockTrainer Complete Installation Guide](https://www.bilibili.com/video/BV1ws4R6fEYL/)**

The installation video was originally recorded for an earlier V7 release, but the core installation flow remains applicable to V7.0.6 when using **UE4SS_Grounded2 1.0.4**.

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

No additional gameplay mod is required.

`BPML_GenericFunctions` and `BPModLoaderMod` are part of the supported UE4SS_Grounded2 setup and are used by the Blueprint UI lifecycle.

---

## Installation / 安装

Download the current release from:

- **[Nexus Mods — PerfectBlockTrainer](https://www.nexusmods.com/grounded2/mods/198)**
- **[GitHub Releases — PerfectBlockTrainer](https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases)**

Then follow:

**[INSTALL.md](INSTALL.md)**

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

## Known Limitations / 当前限制

PerfectBlockTrainer does not claim complete validation of every creature and every attack in Grounded 2.

Current limitations include:

- Some uncommon or special attack patterns may still require dedicated runtime validation
- Some projectile or special-topology attacks may not yet have a validated production prediction path
- Different attacks from the same enemy can behave differently
- Multiplayer validation has primarily focused on the **host-side** scenario
- Future Grounded 2 updates may change runtime behavior or hooks and may require compatibility fixes
- PerfectBlockTrainer is a training / visualization product and does not change the game's actual Perfect Block rules

**中文说明**

项目不会把“已支持一部分代表性攻击”描述成“已经验证游戏里的所有敌人与所有攻击”。对于特殊攻击、特殊拓扑和未来游戏版本变化，仍可能需要单独 Runtime Validation。

If an attack produces no QTE, incorrect timing, or the wrong semantic warning, please report the specific enemy and attack.

---

## Community Testing / 社区测试

Community feedback is an important part of expanding attack coverage and validating regressions.

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

If an issue can be reproduced consistently but cannot be reproduced during development, `UE4SS.log` may also be useful.

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

## Repository Scope / 仓库说明

This repository is the public technical and distribution home of PerfectBlockTrainer.

The public surfaces are intentionally separated by purpose:

- **GitHub README** — product concept, system architecture, development evolution, validation, and release process
- **Nexus Mods** — player-facing release information, current downloads, version-specific changes, compatibility, and community distribution
- **GitHub Releases / INSTALL.md** — release packages and installation guidance

**中文说明**

不同页面承担不同职责：GitHub README 主要说明产品本身如何工作、为什么这样设计以及如何演进；Nexus 更适合维护玩家真正关心的版本更新、兼容性、下载和具体 Patch；GitHub Releases 与 INSTALL.md 则负责正式安装包和安装说明。

这样可以避免 README 变成重复的 Patch Notes，同时让产品结构保持相对稳定。

Public repository content includes:

- Product and architecture documentation
- Release documentation
- Installation documentation
- Media / demos
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

## Version / 当前版本

**V7.0.6 — Stable Public Release**

Current public runtime:

**UE4SS_Grounded2 1.0.4**

Previous public releases:

```text
V7.0.5 — Combat Targeting & QTE Stability Improvements
V7.0.4 — Combat Reliability & Mixed-Threat Improvements
V7.0.3 — Semantic Prediction & Coverage Expansion
V7.0.2 — Performance Fix
V7.0.1 — UE4SS_Grounded2 1.0.4 Compatibility Update
V7.0   — First Public Release
```
