# PerfectBlockTrainer — Product Case Study / 产品案例

**Making hidden combat timing understandable without playing the game for the player**

[← Project README](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/README.md) · [Gameplay Demo](https://youtu.be/ae4_FEjTbQI) · [Nexus Mods](https://www.nexusmods.com/grounded2/mods/198) · [Release History](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/CHANGELOG.md)

**Language / 语言：** [English](#english) · [简体中文](#简体中文)

> **Project:** PerfectBlockTrainer (PBT), a real-time Perfect Block timing assistant for *Grounded 2*  
> **Public release covered:** V7.0.7 · **Platform/runtime:** Grounded 2 PC, UE4SS_Grounded2 1.0.4  
> **My scope:** Product definition, interaction and runtime-system design, AI-assisted implementation, in-game validation, releases, and community support  
> **Project status:** Publicly distributed mod; ongoing maintenance. Multiplayer guest/client QTE support is not yet complete.

---

## English

## 1. The problem: a timing rule players cannot easily see

Perfect Block is a native *Grounded 2* combat mechanic. To execute it, players need to read enemy behavior and act within the game's timing window. This becomes harder to learn consistently when combat includes multiple enemies, multi-hit sequences, movement-based attacks, and projectiles.

The player sees animations and consequences, but not necessarily the underlying timing and threat state. An unsuccessful block does not, by itself, explain whether the player mistimed the input, misread the attack, reacted to the wrong enemy, or attempted to block an attack that should be dodged.

**Product opportunity:** turn otherwise implicit combat timing into useful, real-time training feedback—without removing the player's responsibility to react.

### Intended users and moments

| User situation | What makes it difficult | What PBT should provide |
| --- | --- | --- |
| Learning a creature's attack | Timing must be inferred from animation and repeated attempts | A readable Perfect Block timing window |
| Facing consecutive hits | The next hit may require a different timing decision | Distinct, correctly ordered upcoming-hit cues |
| Fighting multiple enemies | The most visually prominent enemy may not be the nearest threat | Threat-specific timing and stable prioritization |
| Facing charges or projectiles | Contact depends on movement, not only a fixed animation countdown | Updated contact predictions as the encounter changes |
| Facing unblockable or irrelevant actions | Showing a green prompt would teach the wrong action | Correct warning semantics—or no prompt |

## 2. Product goal and boundaries

PBT's central interaction contract is:

```text
System predicts
    ↓
UI explains
    ↓
Player decides
    ↓
Game validates
```

The system aims to make combat information **observable, actionable, and trustworthy**. It is a training and decision-support tool, not a combat autopilot.

**In scope:** attack interpretation, incoming-contact prediction, timing visualization, threat warnings, multi-threat handling, and player-controlled cue visibility.

**Out of scope:** automatic blocking, dodging, button presses, damage modification, and changing the game's Perfect Block rules.

This boundary was a product decision, not an implementation accident: if the tool performed the action, it would reduce the very timing and recognition skills it was intended to help players practice.

![PerfectBlockTrainer single-attack timing cue in actual gameplay](https://raw.githubusercontent.com/Dio23366/PerfectBlockTrainer-Releases/main/media/combat_single.png)

*The ring makes a timing opportunity visible. The player still chooses when to block.*

## 3. From a timing prompt to a threat decision system

A straightforward early approach is to identify an attack and display a fixed countdown. That approach becomes insufficient in real combat because an identified animation does not always remain an incoming threat to the local player.

As coverage grew, the product needed to answer several different questions, in order:

1. **What happened?** Capture an attack or movement event from the runtime.
2. **What does it mean?** Identify the source, current attack, hit, cue semantics, and target relationship.
3. **When could contact happen?** Select an appropriate prediction method and update its estimate.
4. **Is it actually a threat?** Check whether the candidate is relevant, valid, and still directed at the player.
5. **Which threat needs attention?** Resolve competing valid threats without unstable UI switching.
6. **What should the player see now?** Schedule a readable cue and clear it when no longer valid.

This produced a layered decision model rather than one large set of creature-specific countdown rules:

```text
Runtime observations
  → Attack meaning and prediction route
  → Contact-time estimate
  → Threat admission
  → Threat lifecycle / state ownership
  → Multi-threat arbitration
  → QTE scheduling and presentation
```

The key separation is:

> **Predicted contact ≠ eligible threat ≠ presentation owner ≠ visible QTE.**

A time estimate can be valid as a calculation yet still be inappropriate as player guidance. Making that distinction explicit was central to the product's reliability.

## 4. Four consequential product decisions

### Decision A — Preserve player agency instead of automating the response

**Alternative:** automatically issue a block input when a predicted timing window arrives.  
**Chosen:** display the window and let the player act.

This keeps PBT aligned with practice and learning. The product is responsible for the quality of its information, while the player remains responsible for execution. It also makes the UI's meaning more important: an incorrect recommendation would mislead a player even if the mod never touches the controls.

**Design consequence:** the green cue represents the game's recommended Perfect Block opportunity; it is not a promise that the enemy model will visually touch the player on exactly that frame.

### Decision B — Do not turn every detected attack into a QTE

**Simpler alternative:** show a cue whenever an attack event is observed or a contact time can be calculated.  
**Chosen:** separate attack identification, prediction, target verification, and **Threat Admission**.

Real attacks can be cancelled, interrupted, redirected, missed, or invalidated by the attacking creature's death. A single runtime event may also not reveal which player is being attacked.

The system therefore tracks the current attack instance and whether its state is still authorized to update the threat. It needs to remove obsolete cues and prevent older states from reappearing after an attack ends.

**User-facing benefit:** fewer misleading QTEs, fewer lingering indicators, and better stability during mixed combat.

**Conscious limitation:** full multiplayer guest/client QTE support is not yet implemented. Client-side attack and movement observations alone have not been sufficient to establish a consistently reliable attack-target signal. The product does not claim that unreliable guest-side prompts are supported.

### Decision C — Explain multiple valid threats without turning the screen into noise

**Simpler alternative:** display whichever attack was detected most recently.  
**Chosen:** maintain separate threats, prioritize them by relevant timing and validity, and stabilize transitions between displayed cues.

A player's next decision depends on which valid threat is approaching contact—not just which enemy is nearby or which event arrived last. Multi-hit attacks and simultaneous enemies also require the system to preserve distinct timing identities.

V7.0.6 added **GOLD overlap** when two independent blockable green windows share time. This is a visual explanation of overlap, not a merged attack and not a change to the game's Perfect Block windows.

![Multiple threats represented in the PerfectBlockTrainer UI](https://raw.githubusercontent.com/Dio23366/PerfectBlockTrainer-Releases/main/media/multi_threat.png)

*The interface represents more than one incoming threat while preserving the distinction between their timing windows.*

### Decision D — Give players control over guidance intensity

**Feedback:** a player requested a way to hide the QTE ring.  
**Chosen for V7.0.7:** an F8 display cycle: `FULL → DIM → HIDDEN → FULL`.

The original experience assumed the player always wanted the most visible guidance. That is useful while learning, but less appropriate once a player wants to practice without constant prompts or reduce screen obstruction.

Crucially, **the display mode changes presentation only**. Internal attack prediction and threat tracking continue while the ring is dimmed or hidden.

**Product lesson:** once core reliability improves, control over *how much* assistance to see becomes as important as expanding *what* the system can recognize.

## 5. UX semantics: one cue must mean one thing

The visual language is intentionally small and consistent:

| Visual state | Player-facing meaning | Boundary |
| --- | --- | --- |
| **White ring** | Timing-cycle frame | Its presence alone does not prove a valid green cue has been scheduled |
| **Green window** | Recommended Perfect Block opportunity | A timing window, not an exact animation-contact frame |
| **Red pointer** | Current position in the cue's timing cycle | Presentation of timing progress |
| **GOLD overlap** | Shared overlap of independent blockable windows | Does not change game rules or combine attacks |
| **Red warning** | Attack classified as unblockable / requiring dodge awareness | Not a generic “high damage” indicator |
| **No cue** | No ordinary Perfect Block prompt should be shown | Includes intentional `NO_CUE` and deferred special cases |
| **FULL / DIM / HIDDEN** | Player-selected cue visibility | Does not stop runtime threat processing |

The mod deliberately does not claim universal green-cue coverage. Some attacks are intentionally classified as warnings, `NO_CUE`, or deferred cases.

## 6. Iteration was driven by distinct kinds of evidence

PBT's releases reflect changes in what mattered most as the product matured.

| Stage | Main product concern | Representative response |
| --- | --- | --- |
| **V7.0–V7.0.1** | Initial public availability and compatibility | Establish a distributable release and supported runtime |
| **V7.0.2** | Severe usability/performance regression | Fix QTE-active FPS loss caused by repeated Widget rediscovery |
| **V7.0.3–V7.0.4** | More attack types and more reliable complex combat | Improve projectile/attack semantics and mixed-threat handling |
| **V7.0.5** | Incorrect or stale prompts in mixed encounters | Strengthen targeting, lifecycle cleanup, and threat stability |
| **V7.0.6** | Boss coverage and multi-threat readability | Expand validated boss/variant attacks; add GOLD overlap |
| **V7.0.7** | Dynamic prediction, broader coverage, and player choice | Improve moving-body/relative-motion/projectile cases; add F8 visibility control |

Detailed creature-by-creature changes remain in the [CHANGELOG](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/CHANGELOG.md) and [GitHub Releases](https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases). The purpose of this case study is to explain **why the priorities and design changed**, rather than repeat every patch note.

### Example: a performance complaint became a regression test

A public user reported that frame rate could fall from roughly **120 FPS to around 10 FPS** while the QTE pointer was active, then recover after the attack ended.

The investigation localized the issue to repeatedly finding the same UI Widget during active pointer updates. The scoped fix cached a valid Widget reference instead of continuously rediscovering it. It shipped in **V7.0.2**, and the player subsequently reported that the severe FPS drop was gone.

The important product practice was to treat the report as a **symptom requiring reproduction**, not as a request to rewrite unrelated rendering or prediction systems. The resolved failure pattern was retained for later regression checks.

### Example: advanced attack coverage exposed the limits of a fixed clock

Charge attacks, moving enemies, player retreat/approach, and projectiles can change expected contact timing during an attack. A single preconfigured number is not sufficient for these situations.

V7.0.7 strengthened second-layer dynamic prediction and relative-motion correction while retaining the established threat-admission and lifecycle rules. Representative cases include Mosquito, Wasp, Bee, Blue Butterfly, Ladybug, rolling/charge-style enemies, and validated projectile routes.

![Dynamic projectile/contact prediction displayed during gameplay](https://raw.githubusercontent.com/Dio23366/PerfectBlockTrainer-Releases/main/media/dynamic_prediction.png)

*The player sees a cue driven by an evolving prediction, not merely a static timer tied to the first observed animation frame.*

## 7. What counted as a successful feature?

**A successful compilation is not the same as a successful player experience.** PBT used separate checks for different failure classes:

| Acceptance layer | Question answered | Typical evidence |
| --- | --- | --- |
| **Build & deployment** | Did the intended build/package actually reach the test runtime? | Build status, DLL identity, package contents, deployment checks |
| **Runtime behavior** | Did attack identity, target relationship, contact prediction, threat state, and cue scheduling behave as intended? | Development-time runtime logs, traces, and focused diagnostic checks |
| **In-game experience** | Did the player actually see timely, readable, stable QTE behavior? | Manual in-game observation and captured gameplay footage |
| **Release acceptance** | Does the actual public package work without relying on development-only files? | Fresh-runtime and clean-install game testing, release manifest and SHA256 checks |

A runtime log saying a cue was scheduled does not, by itself, establish that the player saw it correctly. Conversely, an apparently good screenshot cannot prove the underlying target selection or lifecycle was correct. The acceptance decision must consider both.

**Example acceptance target:** for a dynamic charge attack, the cue should appear during the intended pre-contact phase, stay visually stable as the relative position changes, and clear when the threat is no longer valid. The actual result is checked against both runtime evidence and gameplay observation.

Public release builds intentionally exclude development-only probes and detailed diagnostic surfaces. Internal validation evidence is not presented here as an independently downloadable dataset.

## 8. Outcomes and what the numbers do—and do not—show

### Public distribution snapshot

| Public signal | Recorded value |
| --- | ---: |
| Stable public release | **V7.0.7** |
| Nexus unique downloads | **496** |
| Nexus total downloads | **749** |
| Nexus page views | **3,375** |
| Nexus endorsements | **7** |
| Public Bilibili video views | **10,000+ cumulative** |

*Snapshot: October 9, 2026; figures reported from the project's public-facing README/Nexus activity at the time of writing. These are distribution and discovery indicators—not active users, retention, conversion, or evidence that every installation works without issue.*

### What the project demonstrates

- A released game-facing product, not only a proof-of-concept prototype.
- A clear product boundary: explain and train rather than automate player actions.
- A shift from individual attack timers to a reusable, layered threat-decision architecture.
- Concrete iteration in response to performance reports, combat correctness issues, broader attack coverage, and a player-requested visibility control.
- An acceptance workflow that distinguishes build correctness, runtime semantics, visible experience, and public-package reliability.
- Public distribution, documentation, installation support, and ongoing feedback handling alongside development.

**Limitations still matter:** full guest/client multiplayer QTE support is not complete; future game updates may require adaptation; and verified creature coverage does not mean every possible attack should display a blockable cue. This case study describes the current released behavior, not future functionality as if it were finished.

## 9. Retrospective / Takeaways

The most significant change was conceptual: the product stopped treating **“an attack event happened”** as equivalent to **“show the player a countdown.”** Each intermediate question—meaning, predicted contact, target relevance, continued validity, priority, and presentation—became an explicit responsibility.

Three principles guide continued development:

1. **Preserve agency:** assist recognition and timing; let the player make the combat input.
2. **Earn the cue:** show guidance only when its semantics and current threat state support it.
3. **Validate the experience:** correct internal logs and correct visible gameplay must agree before a feature is considered accepted.

---

## 简体中文

**让隐藏的战斗时序变得易于理解，同时保留玩家自己的操作与判断**

> **项目：** PerfectBlockTrainer（PBT），《Grounded 2 / 禁闭求生 2》的实时完美格挡时机辅助 Mod  
> **本文对应公开版本：** V7.0.7 · **平台 / 运行环境：** PC 版 Grounded 2、UE4SS_Grounded2 1.0.4  
> **个人负责范围：** 产品定位、交互与运行时系统设计、AI 辅助实现、游戏内验证、版本发布及社区支持  
> **项目状态：** 已公开发布并持续维护；多人联机客机 / Client 端的 QTE 尚未完整支持。

---

### 1. 问题：玩家难以直观看到的格挡时机

Perfect Block（完美格挡）是《Grounded 2》原有的战斗机制。玩家需要观察敌人的行为，在游戏规定的时机窗口内执行格挡。面对多名敌人、多段连击、移动本体攻击及投射物时，这种时机更加难以稳定学习和掌握。

玩家能看见敌人的动作和格挡后的结果，却未必能直接理解背后的时序与威胁状态。一次失败的格挡，也无法单独说明究竟是按键太早或太晚、读错了招式、关注了错误的敌人，还是试图格挡本该闪避的攻击。

**产品机会：** 把原本隐含在游戏运行状态中的战斗时序转化为有用的实时训练反馈，同时不替玩家完成反应和操作。

#### 目标用户与使用场景

| 玩家场景 | 主要困难 | PBT 应提供什么 |
| --- | --- | --- |
| 学习某种生物的攻击 | 必须反复尝试，从动画中推断时机 | 清晰可读的 Perfect Block 时机窗口 |
| 面对连续多段命中 | 下一段攻击可能需要不同的格挡时机 | 彼此独立、按接触顺序排列的后续命中提示 |
| 同时面对多个敌人 | 画面最显眼的敌人不一定是最近的实际威胁 | 按具体威胁建立时机提示，并稳定决定优先级 |
| 面对冲刺或投射物 | 接触时间取决于运动状态，而不只是固定动画倒计时 | 随战况变化持续更新的接触时间预测 |
| 面对不可格挡或无关动作 | 错误的绿色提示会教会玩家错误操作 | 正确的危险提示语义，或者不显示提示 |

### 2. 产品目标与边界

PBT 的核心交互约定是：

```text
系统预测（System predicts）
    ↓
界面解释（UI explains）
    ↓
玩家决策（Player decides）
    ↓
游戏验证（Game validates）
```

系统的目标是让战斗信息**可观察、可用于判断，并且值得信任**。它是训练与决策辅助工具，而不是自动战斗工具。

**范围内：** 解释攻击、预测可能接触的时间、可视化格挡窗口、不可格挡警告、多威胁处理，以及由玩家控制提示的可见程度。

**范围外：** 自动格挡、自动闪避、自动按键、修改伤害，以及修改游戏原生 Perfect Block 规则。

这是一项主动的产品选择，而不是技术上碰巧没有实现的功能。如果工具替玩家执行了操作，就会削弱它原本希望帮助玩家练习的攻击识别与时机判断能力。

![真实游戏画面中的 PerfectBlockTrainer 单次攻击时机提示](https://raw.githubusercontent.com/Dio23366/PerfectBlockTrainer-Releases/main/media/combat_single.png)

*圆环把格挡时机变成可见信息，但何时按下格挡仍然由玩家决定。*

### 3. 从“时机提示”到“威胁决策系统”

一种直接的早期思路是：识别某个攻击，然后显示固定倒计时。但在实际战斗中，已经识别到的动画不一定始终对本地玩家构成威胁，因此这种方法并不足够。

随着攻击适配范围扩大，产品必须依次回答几个不同的问题：

1. **发生了什么？** 从游戏 Runtime 中捕捉攻击或移动事件。
2. **这意味着什么？** 确认攻击来源、具体招式、命中段、提示语义以及目标关系。
3. **什么时候可能发生接触？** 选择相应预测方法，并随运行状态更新估计值。
4. **它真的构成威胁吗？** 检查候选攻击是否与玩家相关、是否有效，以及是否仍然朝向玩家。
5. **哪个威胁更值得注意？** 在多个合法威胁之间选择优先级，同时避免界面不稳定地来回切换。
6. **玩家现在应该看到什么？** 按合适的时机显示易读提示，并在威胁失效后清除。

因此，系统逐渐形成了分层决策模型，而不是为每只虫子的每个攻击都单独堆叠倒计时规则：

```text
运行时观察（Runtime observations）
  → 攻击语义与预测路径
  → 接触时间估计
  → 威胁准入（Threat Admission）
  → 威胁生命周期 / 状态更新权
  → 多威胁仲裁（Arbitration）
  → QTE 调度与呈现
```

最关键的区分是：

> **预测到接触 ≠ 合法威胁 ≠ 当前展示所有者 ≠ 玩家可见 QTE。**

一个预测时间即使在计算上成立，也不一定适合成为对玩家的操作建议。把这几件事明确分开，是提高可靠性的核心。

### 4. 四项关键产品决策

#### 决策 A：保留玩家操作权，而不是自动执行格挡

**备选方案：** 预测时机窗口到来后，由 Mod 自动触发格挡输入。  
**最终选择：** 只显示时机窗口，由玩家自己操作。

这样 PBT 才能保持训练与学习工具的定位。系统负责提供可靠的信息，玩家负责执行操作。这也意味着 UI 提示的语义必须准确：即使 Mod 不碰玩家按键，错误的提示仍然可能误导玩家。

**设计结果：** 绿色区域代表游戏中推荐进行 Perfect Block 的时机窗口，而不是承诺敌人模型一定会在某一帧视觉上接触玩家。

#### 决策 B：不是每次检测到攻击都应该生成 QTE

**更简单的方案：** 只要检测到攻击事件，或者能计算接触时间，就显示 QTE。  
**最终选择：** 将攻击识别、接触预测、目标确认和 **Threat Admission（威胁准入）** 分成不同阶段。

真实战斗中的攻击可能被取消、打断、重定向、打空，也可能因为攻击者死亡而失效。而且，单个 Runtime 事件也不一定能直接告诉系统“这次攻击究竟在打哪个玩家”。

因此系统需要跟踪当前攻击实例，并判断哪些状态仍然拥有更新这一威胁的权限。已经过时的提示必须被移除，已结束攻击的旧状态也不能重新把 QTE 带回屏幕。

**玩家可感知的收益：** 减少误导性 QTE、攻击结束后残留的提示，以及混合战斗中的状态不稳定。

**明确保留的限制：** 多人联机客机 / Client 端尚未实现完整可靠的 QTE。虽然客户端能观察到部分攻击和运动数据，但目前还不能持续、可靠地确认攻击目标，因此不会把不可靠的客机提示描述为已支持功能。

#### 决策 C：解释多个有效威胁，而不是制造屏幕噪声

**更简单的方案：** 谁最后触发攻击事件，就显示谁的提示。  
**最终选择：** 分别维护不同 Threat，按有效性和预计接触时机确定优先级，并稳定处理提示之间的切换。

玩家的下一次操作取决于哪个有效攻击更接近实际接触，而不只是哪个敌人站得近、哪个事件刚刚被记录。多段连击和多个敌人同时攻击时，还必须保留每次命中的独立时机身份。

V7.0.6 加入了 **GOLD（金色重叠区域）**：当两个独立可格挡攻击的绿色时机窗口在时间上重叠时，使用金色解释这段公共区域。这只是视觉表达，并不把两次攻击合并，也不改变游戏原有的 Perfect Block 时间窗口。

![PerfectBlockTrainer 实际游戏界面中的多威胁提示](https://raw.githubusercontent.com/Dio23366/PerfectBlockTrainer-Releases/main/media/multi_threat.png)

*界面可以同时表达多个即将到来的威胁，并保留它们各自时机窗口的区别。*

#### 决策 D：允许玩家自行控制提示强度

**玩家反馈：** 有玩家希望通过快捷键隐藏 QTE 圆环。  
**V7.0.7 的选择：** 增加 F8 切换：`FULL → DIM → HIDDEN → FULL`。

最初的使用体验默认玩家始终希望看到最醒目的引导。这在学习阶段很有价值，但当玩家想减少视觉遮挡，或者尝试在较少提示下自主练习时，这种默认并不总是合适。

关键是：**显示模式只改变 Presentation（视觉呈现）**。即使圆环变暗或隐藏，内部攻击预测和 Threat 跟踪仍会继续运行。

**产品经验：** 当核心可靠性逐步提高之后，允许玩家决定“希望看到多少辅助”，也会成为与扩大“系统能够识别什么”同样重要的体验问题。

### 5. UX 语义：每一种提示都应表达明确含义

PBT 刻意保持一套较少、但一致的视觉语义：

| 视觉状态 | 玩家看到的含义 | 适用边界 |
| --- | --- | --- |
| **白色圆环** | 时机周期的基础框架 | 只看到白环，不代表绿色提示已被正确调度 |
| **绿色区域** | 推荐的 Perfect Block 时机窗口 | 表示时间窗口，而不是精确的动画接触帧 |
| **红色指针** | 当前 QTE 时机周期中的位置 | 用于呈现时机进度 |
| **GOLD 金色重叠区** | 不同可格挡窗口在时间上的公共部分 | 不改变游戏规则，也不合并攻击 |
| **红色警告** | 被归类为不可格挡、应注意闪避的攻击 | 不是泛指“高伤害攻击” |
| **无提示（No cue）** | 当前不应显示普通 Perfect Block 提示 | 包括有意设置的 `NO_CUE` 和延期处理的特殊攻击 |
| **FULL / DIM / HIDDEN** | 玩家选择的 QTE 可见程度 | 不停止内部威胁处理 |

本 Mod 并不宣称所有攻击都会显示绿色 QTE。部分攻击本来就应该采用警告、`NO_CUE` 或延期适配的处理方式。

### 6. 不同类型的证据推动不同阶段的迭代

PBT 的版本演进，体现的是随着产品成熟，开发优先级也在不断变化。

| 阶段 | 当时最重要的产品问题 | 代表性应对 |
| --- | --- | --- |
| **V7.0–V7.0.1** | 首次公开可用性与兼容性 | 建立可分发版本及受支持的运行环境 |
| **V7.0.2** | 严重影响使用的性能退化 | 修复 QTE 激活期间重复查找 Widget 导致的 FPS 大幅下降 |
| **V7.0.3–V7.0.4** | 更多攻击类型与复杂战斗的可靠性 | 加强投射物/攻击语义及混合威胁处理 |
| **V7.0.5** | 混合战斗中错误、过时或残留的提示 | 强化目标确认、生命周期清理和 Threat 稳定性 |
| **V7.0.6** | Boss 覆盖与多威胁提示可读性 | 扩大已验证的 Boss / 变体招式覆盖；加入 GOLD 重叠显示 |
| **V7.0.7** | 动态预测、覆盖扩展与玩家自主选择 | 优化移动本体、相对运动及投射物；加入 F8 显示控制 |

逐个生物和招式的详细更新保存在 [CHANGELOG](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/CHANGELOG.md) 与 [GitHub Releases](https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases)。这份案例的重点不是复述每条 Patch Note，而是解释：**为什么当时要调整产品优先级与设计方式**。

#### 案例：一次性能投诉如何变成长期回归检查项

一位公开用户反馈：当 QTE 指针激活时，帧率可能从约 **120 FPS 降到 10 FPS 左右**；攻击结束后帧率又恢复正常。

排查后，问题被定位到活跃指针更新期间反复查找同一个 UI Widget。最终采用范围受控的修复方案：缓存有效 Widget 引用，而不是每帧重新查找。修复随 **V7.0.2** 发布，玩家随后确认严重掉帧已经消失。

这里重要的产品实践是：先把玩家报告视作**需要复现和定位的症状**，而不是据此改写不相关的渲染或预测模块。修复后的故障模式也被保留，用于后续回归检查。

#### 案例：复杂攻击适配暴露固定倒计时的局限

冲刺、移动中的敌人、玩家前进或后退，以及投射物，都可能在一次攻击进行过程中改变预计接触时间。预先填入一个固定毫秒数，不足以覆盖这些情形。

V7.0.7 在保留既有 Threat Admission 和生命周期规则的基础上，进一步增强二层动态预测与相对运动修正。代表性案例包括蚊子、黄蜂、蜜蜂、蓝蝴蝶、瓢虫、滚动/冲刺类敌人，以及经过验证的投射物攻击路线。

![游戏内展示的动态投射物与接触预测](https://raw.githubusercontent.com/Dio23366/PerfectBlockTrainer-Releases/main/media/dynamic_prediction.png)

*玩家看到的是随实时预测更新的提示，而不只是根据首次检测到的动画帧启动的静态计时器。*

### 7. 怎样判定一个功能真正验收成功？

**编译成功不等于玩家体验已经通过验收。** PBT 将不同类型的问题交给不同的验证环节：

| 验收层 | 要回答的问题 | 常见证据 |
| --- | --- | --- |
| **编译与部署** | 正确的构建产物和安装包是否真的进入了测试运行环境？ | 编译状态、DLL 身份、包内文件、部署检查 |
| **运行时行为** | 攻击身份、目标关系、接触预测、Threat 状态和提示调度是否符合设计？ | 开发阶段的 Runtime 日志、Trace、针对性诊断 |
| **游戏内体验** | 玩家是否真的看到了及时、易读、稳定的 QTE？ | 人工实机观察和游戏录像 |
| **正式发布验收** | 玩家下载的公开安装包能否在不依赖开发专用文件的情况下正常工作？ | 新运行环境与干净安装实测、发布清单及 SHA256 校验 |

Runtime 日志说“已调度 QTE”，并不能单独证明玩家真正看到了正确的画面；反过来，某张看起来正常的截图，也无法证明内部目标判断或生命周期逻辑完全正确。最终验收需要同时考虑两类证据。

**验收目标示例：** 对于动态冲刺攻击，QTE 应在预定的接触前阶段出现，在玩家与敌人相对位置变化时保持视觉稳定，并在威胁失效后正确清除。实际结果需要同时对照 Runtime 证据和游戏内观察。

公开发布构建会有意移除开发专用的 Probe 与详细诊断能力。内部验收证据并未在这里作为独立数据集向外提供。

### 8. 项目成果：公开数字能够说明什么、不能说明什么

#### 公开分发数据快照

| 公开指标 | 记录值 |
| --- | ---: |
| 当前稳定公开版本 | **V7.0.7** |
| Nexus Unique Downloads（独立下载） | **496** |
| Nexus Total Downloads（总下载） | **749** |
| Nexus 页面浏览量 | **3,375** |
| Nexus Endorsements（认可数） | **7** |
| Bilibili 公开视频累计播放量 | **10,000+** |

*数据快照日期：2026 年 10 月 9 日；数字依据本文撰写时项目公开 README / Nexus 活动记录。它们属于发布、传播和发现指标，不等于活跃用户、留存、转化率，也不能证明每一次安装都完全没有问题。*

#### 这个项目体现了什么

- 它是已经正式发布、真实面向玩家的游戏内产品，而不只是概念原型。
- 产品边界明确：解释和训练玩家，而不是自动替玩家完成操作。
- 系统从单一攻击倒计时，演进为可复用的分层 Threat Decision 架构。
- 针对性能投诉、战斗判断正确性、攻击覆盖和玩家提出的显示控制需求，形成了实际版本迭代。
- 验收方法区分编译正确性、Runtime 语义正确性、游戏内可见体验以及公开包可靠性。
- 除开发工作外，还持续处理公开发布、安装说明、社区支持与反馈。

**当前限制同样重要：** 多人客机 / Client 的 QTE 还没有完整支持；未来游戏更新可能需要重新适配；已验证的生物覆盖也不意味着每一种攻击都应显示绿色可格挡窗口。本文只描述当前已经公开发布的能力，不把未来可能实现的功能当成既成事实。

### 9. 复盘与经验

最重要的变化其实是认识层面的：系统不再把**“检测到攻击事件”**直接等同于**“给玩家显示倒计时”**。攻击语义、接触预测、目标相关性、持续有效性、威胁优先级及最终呈现，逐步变成了各自明确的责任环节。

后续开发继续遵循三个原则：

1. **保留玩家决策权：** 帮助识别攻击和理解时机，但实际格挡仍由玩家完成。
2. **提示必须有依据：** 只有攻击语义与当前 Threat 状态成立时，才向玩家提供对应建议。
3. **同时验收系统与体验：** 内部日志正确、玩家画面正确，两者相互符合后，功能才算真正通过验收。

---

## Related materials / 相关资料

- [Project README & in-game preview / 项目首页与实机截图](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/README.md)
- [Detailed version history / 版本更新记录](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/CHANGELOG.md)
- [Installation instructions / 安装说明](https://github.com/Dio23366/PerfectBlockTrainer-Releases/blob/main/INSTALL.md)
- [Official release packages / 正式发布包](https://github.com/Dio23366/PerfectBlockTrainer-Releases/releases)
- [Real gameplay demo / 实机演示](https://youtu.be/ae4_FEjTbQI)
- [Nexus Mods community page / Nexus 社区页面](https://www.nexusmods.com/grounded2/mods/198)

*PerfectBlockTrainer is an independently maintained mod for Grounded 2. Grounded 2 is developed by Obsidian Entertainment and published by Xbox Game Studios.*

*PerfectBlockTrainer 是独立开发与维护的《Grounded 2》Mod。《Grounded 2》由 Obsidian Entertainment 开发、Xbox Game Studios 发行。*
