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

A fixed countdown is not enough once combat includes multi-hit attacks, charge / moving-body attacks, projectiles, multiple simultaneous threats, target changes, interrupts, cancellations, and different blockable / unblockable semantics. The system therefore evolved into a stateful real-time decision system that continuously decides **what an observed event means, whether it still constitutes a valid threat, and whether that threat should be shown to the player now**.

**中文说明**

PerfectBlockTrainer 从一个真实玩家问题出发：复杂战斗中的完美格挡时序原本隐藏在动画和 Runtime 中，玩家很难稳定观察、理解和练习。

它不替玩家自动格挡，而是负责预测和解释，让玩家自己判断与操作，再由游戏结果验证。随着多段攻击、冲刺、投射物、多敌人、目标切换、攻击取消等情况出现，系统真正需要解决的也不再只是“倒计时”，而是持续判断：**发生了什么、它意味着什么、是否仍然构成威胁，以及当前是否值得展示。**

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

## Runtime Decision Flow / 实时决策流程

The product is not a fixed sequence of steps. During combat, the system repeatedly decides whether an observed attack is relevant, whether it is still valid, which threat matters most, and whether the player should see a cue now.

> 这不是“事件进来以后一路执行到底”的线性 Workflow。系统会持续重新判断：这个攻击候选是否真的与玩家有关、是否仍然有效、多个有效威胁谁更优先，以及当前到底要不要显示。

```mermaid
flowchart TD
    A["Game Runtime Signals<br/>游戏运行时信号<br/>攻击 / 目标 / 位置 / 投射物"] --> B["Capture Runtime Facts<br/>获取运行时事实<br/>先记录发生了什么"]
    B --> C["Identify Current Attack<br/>识别当前攻击<br/>哪次攻击？哪一段？<br/>目标是谁？"]
    C --> D["Choose Prediction Method<br/>选择预测方式<br/>近战 / 冲刺 / 直线投射物 /<br/>弹道投射物"]
    D --> E["Predict Contact Timing<br/>预测接触时机<br/>什么时候可能碰到玩家？"]

    E --> F{"Is It a Real Threat?<br/>是否真的构成威胁？"}
    F -- "No / 否" --> F0["Ignore Candidate<br/>忽略候选<br/>不生成提示"]
    F -- "Yes / 是" --> G["Create or Update Threat<br/>创建或更新威胁"]

    G --> H["Track Current Threat State<br/>跟踪当前威胁状态<br/>处理中断 / 取消 / 切目标 / 过期"]
    H --> I{"Still Valid?<br/>现在仍然有效吗？"}
    I -- "No / 否" --> I0["Remove Threat & Clear Cue<br/>移除威胁并清理提示"]
    I -- "Yes / 是" --> J["Choose Which Threat<br/>Comes First<br/>决定先处理哪个威胁<br/>多个有效威胁竞争有限 UI"]

    J --> K{"Show It Now?<br/>现在应该提示玩家吗？"}
    K -- "No / 否" --> K0["Keep State<br/>Do Not Show Yet<br/>保留状态，暂不显示"]
    K0 -. "Re-check as combat changes<br/>战斗变化后重新判断" .-> J
    K -- "Yes / 是" --> L["Update On-screen Cue<br/>更新屏幕提示<br/>显示 / 更新 / 切换 / 清理"]

    L --> M["QTE Cue<br/>玩家可见提示"]
    M --> N["Player Decision & Input<br/>玩家判断并操作"]
    N --> O["Validate with Actual<br/>Game Outcome<br/>用实际游戏结果验证<br/>Block / Hit / Miss / Cancel"]
    O -. "Evidence for later validation<br/>作为后续验证证据" .-> B
```

The important part of the flow is not the number of boxes, but the **decisions that can stop, revoke, delay, or redirect the flow**:

- Capturing runtime facts does not mean the system already knows what attack they represent.
- Predicting a contact time does not mean the candidate is a real threat to the player.
- A previously valid threat can become invalid and must be removed.
- Several valid threats can exist at once, so the system must choose what deserves limited UI attention first.
- A displayed cue is only information; the player still performs the action.

**中文理解**

这张图最重要的不是“步骤很多”，而是系统在不断做取舍：

- 先获取游戏正在发生的事实，再判断这些信号到底代表哪次攻击；
- 即使算出了接触时间，也要再判断它是不是真的会威胁当前玩家；
- 已经成立的威胁，也可能因为打断、击晕、击杀、切换目标或已经打空而被撤销；
- 多个威胁同时成立时，需要决定谁应该优先占用有限的 UI 注意力；
- 最终提示只是帮助玩家理解时机，系统不会替玩家执行格挡。

---

## Key Concepts in the Flow / 流程中的核心概念

The flowchart uses plain action-oriented names first. The original technical terms are kept in parentheses only where they help deeper implementation discussions.

> 为了让第一次接触项目的人直接看懂，流程图优先写“这一层具体做什么”。原来的技术术语只保留在这里，方便后续深入讨论实现。

| What this stage does / 这一层在做什么 | Meaning in PerfectBlockTrainer / 在 PBT 中的实际含义 |
|---|---|
| **Capture Runtime Facts / 获取运行时事实** *(Runtime Observation)* | Read raw facts from the running game：攻击事件、来源与目标、位置、速度、投射物状态、格挡/命中/Miss 等。这里只回答“发生了什么”，暂不解释这些信号代表哪次攻击。 |
| **Identify Current Attack / 识别当前攻击** *(Semantic Reconstruction)* | Turn raw callbacks into an understandable attack identity：判断这是哪个敌人、哪一次攻击、哪一段连击、是否可格挡、当前目标是谁。 |
| **Choose Prediction Method / 选择预测方式** *(Collision Topology / Routing)* | Different physical attack types need different prediction methods：固定接触、移动本体/冲刺、直线投射物、弹道投射物分别进入合适的预测路径。 |
| **Predict Contact Timing / 预测接触时机** *(Prediction)* | Estimate when a candidate attack may contact the player：根据对应的运动/攻击模型估计可能接触时间，并允许运行时持续修正。 |
| **Is It a Real Threat? / 是否真的构成威胁？** *(Threat Admission)* | Check whether a mathematically predictable attack is actually relevant to the current player：确认攻击来源、目标关系、攻击状态和物理关系仍然成立，过滤不应该进入后续流程的候选。 |
| **Track Current Threat State / 跟踪当前威胁状态** *(Threat Lifecycle / State Authority)* | Keep the active threat state consistent：处理打断、击晕、击杀、取消、切目标、过期；当旧状态和新状态同时存在时，只允许当前有效状态继续更新威胁。 |
| **Choose Which Threat Comes First / 决定先处理哪个威胁** *(Multi-threat Arbitration)* | When several threats are valid at once, choose which ones deserve the limited UI slots first：依据接触时间、优先级和稳定性规则决定展示顺序。 |
| **Update On-screen Cue / 更新屏幕提示** *(Scheduler)* | Turn changing threat state into stable UI behavior：决定什么时候显示、更新、切换、保持或清理提示，避免 UI 因瞬时变化频繁抖动或残留。 |
| **Validate with Actual Game Outcome / 用实际游戏结果验证** *(Ground Truth)* | Compare system decisions with real combat outcomes：用真实 Perfect Block、普通格挡、命中、Miss、取消等结果检查判断，并作为后续回归证据。 |

Current production prediction families include:

```text
FIXED_SINGLE         — fixed single-hit timing / 固定单段攻击
FIXED_MULTI          — fixed multi-hit timing / 固定多段攻击
MOVING_BODY          — charge / moving attacker / 冲刺或移动本体攻击
LINEAR_PROJECTILE    — straight-line projectile / 直线投射物
BALLISTIC_PROJECTILE — arcing projectile / 弹道投射物
```

---

## Development Scope / 开发范围

PerfectBlockTrainer is independently designed, implemented, validated, released, and maintained as an end-to-end public project.

The project scope includes:

- Player problem discovery and product boundary definition
- Runtime decision-system architecture and interaction design
- AI-assisted implementation and iterative technical validation
- Runtime fact capture, attack identification, state transitions, and threat-state tracking
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

## Design Decisions Behind the Flow / 流程背后的设计判断

The architecture was **not** designed for complexity. Each separation exists because a simpler assumption failed in real runtime scenarios.

> 复杂度不是设计目标，而是问题复杂度留下来的结果。只有当更简单的假设在真实 Runtime 中失败时，才增加新的机制。

### 1. Raw Event ≠ Attack Meaning / 捕捉到事件 ≠ 已经理解攻击含义

A runtime callback tells the system that something happened, but not necessarily what the attack means.

Therefore the system reconstructs the attack meaning using information such as:

- Source — which enemy / attack source
- Montage — which animation / attack sequence
- AttackGeneration — which specific attack instance
- HitIndex — which hit inside a multi-hit sequence
- Cue semantics — blockable / unblockable / no cue
- Target relationship — who the attack is currently aimed at

**Design consequence:** raw game events are captured first; attack meaning is reconstructed only after enough context is available.

**中文理解**

游戏告诉系统“发生了一个事件”，不代表系统已经知道“这是哪一次攻击、哪一段连击、是否可格挡、属于哪个目标关系”。

因此系统先记录“发生了什么”，再通过 **Identify Current Attack / 识别当前攻击** 判断“这是哪次攻击、哪一段、是否可格挡、当前目标是谁”。

---

### 2. Attack Started ≠ Still Threatening the Player / 攻击已经发动 ≠ 现在仍然威胁玩家

An enemy starting an attack does not mean the attack remains a valid player threat.

The attack may later be:

- Interrupted
- Stunned
- Cancelled
- Invalidated by death
- Retargeted
- Physically missed

**Design consequence:** the system explicitly tracks whether each threat is still valid, removes invalid threats, and controls which current state is allowed to update them.

**中文理解**

例如怪物已经发动攻击，但随后被打断、击晕、击杀，或者已经切换目标，那么原来的 QTE 就不能继续残留。

这就是 **Track Current Threat State / 跟踪当前威胁状态**（技术上对应 Threat Lifecycle）存在的原因：系统持续判断威胁从创建、更新到失效、过期和清除的状态变化。

**Control Which State May Update / 控制哪个状态还能更新**（技术上对应 State Authority）解决另一类问题：旧攻击、旧预测、新目标和新的 Runtime Event 可能同时存在，系统必须明确“哪个状态现在还能更新这个威胁”，避免已经失效的旧状态重新覆盖新状态。

---

### 3. Predictable Contact ≠ Valid Threat / 能算出接触时间 ≠ 当前真的构成有效威胁

A contact time can be mathematically predicted while the candidate is still not a legitimate threat to the player.

**Design consequence:** contact-time prediction is separated from the valid-threat check, so a mathematically plausible result does not automatically become a player-facing prompt.

**中文理解**

“数学上能算出什么时候会碰到玩家”不代表这个候选攻击就应该进入正式 Threat 系统。

例如攻击来源已经失效、目标已经切换，或者当前攻击实例/物理关系已经不再成立，系统仍可能数学上算出一个时间值。因此 **Is It a Real Threat? / 是否真的构成威胁？**（技术上对应 Threat Admission）会再确认：这个预测现在是否真的与玩家有关，只有通过后才进入后续流程。

---

### 4. Valid Threat ≠ Show It Now / 确实是威胁 ≠ 现在就一定要展示

Multiple valid threats can exist at the same time while player attention and visible UI capacity are limited.

**Design consequence:** when several threats are valid at once, the system first chooses priority, then controls when each cue should be shown, updated, retained, or cleared.

**中文理解**

多个 Threat 可以同时全部“合法”，但玩家注意力和 UI 槽位是有限的。

因此 **Choose Which Threat Comes First / 决定先处理哪个威胁**（技术上对应 Multi-threat Arbitration）先决定多个有效威胁中谁更应该占用有限 UI；随后 **Update On-screen Cue / 更新屏幕提示**（技术上对应 Scheduler）把持续变化的状态转换成稳定的显示、更新、切换和清理行为，避免 UI 因瞬时变化频繁抖动或残留。

---

### 5. System Recommendation ≠ Player Action / 系统给出提示 ≠ 替玩家完成操作

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
Target switching / stale-state cleanup / mixed-combat stability
目标切换、旧状态清理与混合战斗稳定性
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
- Blockable / unblockable attack classification / 可格挡与不可格挡攻击分类
- Multi-phase attack handling / 多阶段攻击
- Runtime prediction correction / 运行时预测修正
- Threat target update / 威胁目标变化后的更新
- Automatic cleanup when attacks stop being valid threats / 攻击不再构成威胁时自动清理提示
- Chronological handling of upcoming multi-hit threats / 多段威胁按接触顺序处理
- Save / map transition cleanup / 存档与地图切换时的状态清理
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

Red does **not** mean "hard attack" or "high damage". It specifically means **this attack cannot be Perfect Blocked and should be treated as a dodge / danger warning** in the current product rules.

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

`BPML_GenericFunctions` and `BPModLoaderMod` are part of the supported UE4SS_Grounded2 setup and support Blueprint UI creation, update, and cleanup.

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
- Some projectile or unusual physical attack types may not yet have a validated production prediction path
- Different attacks from the same enemy can behave differently
- Multiplayer validation has primarily focused on the **host-side** scenario
- Future Grounded 2 updates may change runtime behavior or hooks and may require compatibility fixes
- PerfectBlockTrainer is a training / visualization product and does not change the game's actual Perfect Block rules

**中文说明**

项目不会把“已支持一部分代表性攻击”描述成“已经验证游戏里的所有敌人与所有攻击”。对于特殊攻击、特殊物理运动方式和未来游戏版本变化，仍可能需要单独 Runtime Validation。

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
