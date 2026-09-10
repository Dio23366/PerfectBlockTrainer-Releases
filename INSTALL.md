# PerfectBlockTrainer V7.0.5

**Installation Guide / 安装指南**

---

# Part I — English

## 1. Before You Start

You need:

1. **Grounded 2**
2. **UE4SS_Grounded2 1.0.4**
3. **PerfectBlockTrainer V7.0.5**

## 2. Find the Grounded 2 Installation Folder

In Steam:

**Grounded 2 → Properties → Installed Files → Browse**

The game folder should look similar to:

```text
Grounded2
├─ Augusta
├─ Engine
└─ Grounded2.exe
```

All paths below start from this `Grounded2` folder.

## 3. Install UE4SS_Grounded2 1.0.4

Open:

```text
Grounded2\Augusta\Binaries\Win64
```

Extract **UE4SS_Grounded2 1.0.4**.

Copy:

```text
ue4ss
dwmapi.dll
```

into:

```text
Grounded2\Augusta\Binaries\Win64
```

The result should look similar to:

```text
Win64
├─ Grounded2Steam-Win64-Shipping.exe
├─ dwmapi.dll
└─ ue4ss
```

## 4. First Launch — Verify UE4SS

At this point, **do not install PerfectBlockTrainer yet**.

Launch **Grounded 2** and confirm that the game can reach the main menu normally.

Then completely exit the game.

## 5. Install PerfectBlockTrainerCpp

Extract:

```text
PerfectBlockTrainer_V7.0.5_RELEASE.zip
```

Open:

```text
Mods
```

Copy the entire:

```text
PerfectBlockTrainerCpp
```

folder into:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods
```

The final path must be:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp\dlls\main.dll
```

### Correct

```text
PerfectBlockTrainerCpp
└─ dlls
   └─ main.dll
```

### Wrong

```text
PerfectBlockTrainerCpp
└─ PerfectBlockTrainerCpp
   └─ dlls
      └─ main.dll
```

If you see two `PerfectBlockTrainerCpp` folders nested inside each other, the folder was copied one level too deep.

## 6. Install LogicMods

The release contains:

```text
LogicMods
├─ PerfectBlockTrainer.pak
├─ PerfectBlockTrainer.ucas
└─ PerfectBlockTrainer.utoc
```

Target location:

```text
Grounded2\Augusta\Content\Paks\LogicMods
```

If `LogicMods` does not already exist, copy the entire `LogicMods` folder from the release into:

```text
Grounded2\Augusta\Content\Paks
```

If `LogicMods` already exists, open the existing folder and copy these three files into it:

```text
PerfectBlockTrainer.pak
PerfectBlockTrainer.ucas
PerfectBlockTrainer.utoc
```

The final structure must be:

```text
Grounded2
└─ Augusta
   └─ Content
      └─ Paks
         └─ LogicMods
            ├─ PerfectBlockTrainer.pak
            ├─ PerfectBlockTrainer.ucas
            └─ PerfectBlockTrainer.utoc
```

> All three files must be installed together.

## 7. Install & Enable PerfectBlockTrainerCpp

Open:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\mods.txt
```

Confirm:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
```

Then add or confirm:

```text
PerfectBlockTrainerCpp : 1
```

Place it above:

```text
; Built-in keybinds, do not move up!
```

Example:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
jsbLuaProfilerMod : 0
PerfectBlockTrainerCpp : 1

; Built-in keybinds, do not move up!
Keybinds : 1
```

> Other entries in `mods.txt` may be different on your installation.  
> Do not copy the example line-for-line and do not change unrelated mods.

Save `mods.txt`.

## 8. Second Launch — Test PerfectBlockTrainer

Launch **Grounded 2**.

Enter a save.

Find a normal melee enemy and let it attack you.

A successful installation should show:

```text
Enemy prepares to attack
↓
QTE appears
↓
Ring appears
↓
Pointer moves
↓
Perfect Block timing is displayed
↓
UI disappears after the attack ends
```

If this works, installation is complete.

## 9. Troubleshooting

### Game Does Not Start

If the game cannot reach the main menu after installing UE4SS but before installing PerfectBlockTrainer, check the **UE4SS_Grounded2 1.0.4** installation first.

### PerfectBlockTrainer Does Not Appear

Check:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp\dlls\main.dll
```

Then confirm in `mods.txt`:

```text
PerfectBlockTrainerCpp : 1
```

### No Ring or QTE

Check that all three files exist in:

```text
Grounded2\Augusta\Content\Paks\LogicMods
```

```text
PerfectBlockTrainer.pak
PerfectBlockTrainer.ucas
PerfectBlockTrainer.utoc
```

Then confirm:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### Wrong Folder Structure

Wrong:

```text
...\Mods\PerfectBlockTrainerCpp\PerfectBlockTrainerCpp\dlls\main.dll
```

Correct:

```text
...\Mods\PerfectBlockTrainerCpp\dlls\main.dll
```

## 10. Update from an Older Version

Completely exit **Grounded 2** before updating.

### Updating from V7.0.3

V7.0.5 improves combat reliability, mixed melee/ranged handling, multi-hit and special-attack timing, projectile support, and runtime efficiency.

Replace the old:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

with the V7.0.5 `PerfectBlockTrainerCpp` folder.

The three LogicMods files in V7.0.5 have the same validated identities as V7.0.3, so they do not need to be replaced when updating directly from V7.0.3.

Then confirm:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### Updating from V7.0.2

V7.0.5 can also be installed directly over V7.0.2.

Replace the old:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

with the V7.0.5 `PerfectBlockTrainerCpp` folder.

The current three LogicMods files retain the same validated identities used by V7.0.2 / V7.0.3, so they do not need to be replaced if those exact files are already installed.

Then confirm:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### Updating from V7.0.1 or V7.0

Replace the old:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

with the V7.0.5 `PerfectBlockTrainerCpp` folder.

Then make sure all three current LogicMods files are installed together in:

```text
Grounded2\Augusta\Content\Paks\LogicMods
```

```text
PerfectBlockTrainer.pak
PerfectBlockTrainer.ucas
PerfectBlockTrainer.utoc
```

Finally, confirm:

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### Updating from an older development / test build

For a development or test build, a clean PerfectBlockTrainer reinstall is recommended.

Completely exit **Grounded 2**, remove the old:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

and remove the old PerfectBlockTrainer LogicMods files:

```text
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.pak
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.ucas
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.utoc
```

Then install V7.0.5 again using Sections 5–7 above.

## 11. Uninstall

Completely exit **Grounded 2**.

Delete:

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

Then delete:

```text
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.pak
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.ucas
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.utoc
```

Then remove or disable the `PerfectBlockTrainerCpp` entry in `mods.txt`.

Do not delete files belonging to other mods.

## 12. Official V7.0.5 Release Identity

Release package:

```text
PerfectBlockTrainer_V7.0.5_RELEASE.zip
```

SHA256:

```text
7F1A48CDDDA8CE3AF4C39540E4DA2A922990B613BD5F666F8E592951E456A541
```

Runtime DLL:

```text
main.dll
```

SHA256:

```text
50F6B6FAE66C772B772FD04783E4947394D6B86F5CD6D3D80442C7B848300ECD
```

Size:

```text
514560 bytes
```

Only packages distributed through the official PerfectBlockTrainer channels should be considered official builds.

## 13. Final Checklist

- [ ] UE4SS_Grounded2 1.0.4 installed
- [ ] Game reaches the main menu after UE4SS installation
- [ ] `PerfectBlockTrainerCpp\dlls\main.dll` is in the correct folder
- [ ] `PerfectBlockTrainer.pak` installed
- [ ] `PerfectBlockTrainer.ucas` installed
- [ ] `PerfectBlockTrainer.utoc` installed
- [ ] `BPML_GenericFunctions : 1`
- [ ] `BPModLoaderMod : 1`
- [ ] `PerfectBlockTrainerCpp : 1`
- [ ] Save loads normally
- [ ] QTE appears when an enemy attacks
- [ ] Ring appears
- [ ] Pointer moves
- [ ] UI disappears after the attack ends

---

# Part II — 中文

## 1. 安装前准备

你需要：

1. **Grounded 2 / 禁闭求生 2**
2. **UE4SS_Grounded2 1.0.4**
3. **PerfectBlockTrainer V7.0.5**

## 2. 找到 Grounded 2 安装目录

在 Steam 中：

**Grounded 2 → 属性 → 已安装文件 → 浏览**

打开后应该能看到类似：

```text
Grounded2
├─ Augusta
├─ Engine
└─ Grounded2.exe
```

后续所有路径都从这个 `Grounded2` 文件夹开始。

## 3. 安装 UE4SS_Grounded2 1.0.4

进入：

```text
Grounded2\Augusta\Binaries\Win64
```

解压 **UE4SS_Grounded2 1.0.4**。

把：

```text
ue4ss
dwmapi.dll
```

复制到：

```text
Grounded2\Augusta\Binaries\Win64
```

最终目录应类似：

```text
Win64
├─ Grounded2Steam-Win64-Shipping.exe
├─ dwmapi.dll
└─ ue4ss
```

## 4. 第一次启动 — 验证 UE4SS

此时**先不要安装 PerfectBlockTrainer**。

启动 **Grounded 2**，确认游戏可以正常进入主菜单。

然后完全退出游戏。

## 5. 安装 PerfectBlockTrainerCpp

解压：

```text
PerfectBlockTrainer_V7.0.5_RELEASE.zip
```

打开：

```text
Mods
```

把整个：

```text
PerfectBlockTrainerCpp
```

文件夹复制到：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods
```

最终路径必须是：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp\dlls\main.dll
```

### 正确

```text
PerfectBlockTrainerCpp
└─ dlls
   └─ main.dll
```

### 错误

```text
PerfectBlockTrainerCpp
└─ PerfectBlockTrainerCpp
   └─ dlls
      └─ main.dll
```

如果看到两层 `PerfectBlockTrainerCpp`，说明文件夹多套了一层。

## 6. 安装 LogicMods

Release 中有：

```text
LogicMods
├─ PerfectBlockTrainer.pak
├─ PerfectBlockTrainer.ucas
└─ PerfectBlockTrainer.utoc
```

目标位置：

```text
Grounded2\Augusta\Content\Paks\LogicMods
```

如果 Paks 下还没有 `LogicMods`，把 Release 中整个 `LogicMods` 文件夹复制到：

```text
Grounded2\Augusta\Content\Paks
```

如果已经存在 `LogicMods`，打开已有文件夹，只把这三个文件复制进去：

```text
PerfectBlockTrainer.pak
PerfectBlockTrainer.ucas
PerfectBlockTrainer.utoc
```

最终目录必须是：

```text
Grounded2
└─ Augusta
   └─ Content
      └─ Paks
         └─ LogicMods
            ├─ PerfectBlockTrainer.pak
            ├─ PerfectBlockTrainer.ucas
            └─ PerfectBlockTrainer.utoc
```

> 三个文件必须一起安装。

## 7. 安装并启用 PerfectBlockTrainerCpp

打开：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\mods.txt
```

确认：

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
```

然后新增或确认：

```text
PerfectBlockTrainerCpp : 1
```

把它放在：

```text
; Built-in keybinds, do not move up!
```

这一行的上面。

例如：

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
jsbLuaProfilerMod : 0
PerfectBlockTrainerCpp : 1

; Built-in keybinds, do not move up!
Keybinds : 1
```

> 不同玩家的 `mods.txt` 中其他内容可能不同。  
> 不要整段照抄示例，也不要修改与 PerfectBlockTrainer 无关的其他 Mod。

保存 `mods.txt`。

## 8. 第二次启动 — 测试 PerfectBlockTrainer

启动 **Grounded 2**。

进入一个存档。

找一个普通近战敌人，让它主动攻击你。

正确安装后应该看到：

```text
敌人准备攻击
↓
QTE 出现
↓
Ring 显示
↓
Pointer 运动
↓
显示完美格挡时机
↓
攻击结束后 UI 消失
```

如果这一整套流程正常，说明安装完成。

## 9. 常见问题

### 游戏无法启动

如果只安装 UE4SS、还没有安装 PerfectBlockTrainer 时，游戏就已经无法进入主菜单，请先检查 **UE4SS_Grounded2 1.0.4** 的安装。

### PerfectBlockTrainer 没有出现

检查：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp\dlls\main.dll
```

然后确认：

```text
PerfectBlockTrainerCpp : 1
```

### 没有 Ring 或 QTE

检查：

```text
Grounded2\Augusta\Content\Paks\LogicMods
```

里面是否同时存在：

```text
PerfectBlockTrainer.pak
PerfectBlockTrainer.ucas
PerfectBlockTrainer.utoc
```

然后确认：

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### 文件夹多套了一层

错误：

```text
...\Mods\PerfectBlockTrainerCpp\PerfectBlockTrainerCpp\dlls\main.dll
```

正确：

```text
...\Mods\PerfectBlockTrainerCpp\dlls\main.dll
```

## 10. 从旧版本更新到 V7.0.5

更新前请先完全退出 **Grounded 2**。

### 从 V7.0.3 更新

V7.0.5 主要提升混战中的提示稳定性，改善近战与远程攻击同时出现时的处理、多段与特殊攻击的时机判断、射弹支持以及运行效率。

把旧的：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

替换成 V7.0.5 的 `PerfectBlockTrainerCpp` 文件夹。

V7.0.5 中的三个 LogicMods 文件与 V7.0.3 使用的是同一组已经验证过的文件，因此如果你是从 V7.0.3 直接更新，不需要重新替换 LogicMods。

然后确认：

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### 从 V7.0.2 更新

V7.0.5 也可以直接从 V7.0.2 更新。

把旧的：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

替换成 V7.0.5 的 `PerfectBlockTrainerCpp` 文件夹。

当前三个 LogicMods 文件与 V7.0.2 / V7.0.3 使用的是同一组已经验证过的文件。如果你本地已经安装的是这些文件，就不需要再次替换。

然后确认：

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### 从 V7.0.1 或 V7.0 更新

把旧的：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

替换成 V7.0.5 的 `PerfectBlockTrainerCpp` 文件夹。

然后确认当前三个 LogicMods 文件都一起安装在：

```text
Grounded2\Augusta\Content\Paks\LogicMods
```

```text
PerfectBlockTrainer.pak
PerfectBlockTrainer.ucas
PerfectBlockTrainer.utoc
```

最后确认：

```text
BPML_GenericFunctions : 1
BPModLoaderMod : 1
PerfectBlockTrainerCpp : 1
```

### 从更早的开发版 / 测试版更新

如果你当前使用的是开发版或测试版，建议执行一次 PerfectBlockTrainer 的全新安装。

先完全退出 **Grounded 2**，删除旧的：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

并删除旧的 PerfectBlockTrainer LogicMods 文件：

```text
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.pak
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.ucas
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.utoc
```

然后按照上面的第 5–7 节重新安装 V7.0.5。

## 11. 卸载

先完全退出 **Grounded 2**。

删除：

```text
Grounded2\Augusta\Binaries\Win64\ue4ss\Mods\PerfectBlockTrainerCpp
```

然后删除：

```text
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.pak
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.ucas
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.utoc
```

最后从 `mods.txt` 中删除或禁用 `PerfectBlockTrainerCpp`。

不要删除其他 Mod 的文件。

## 12. V7.0.5 官方发行身份

Release 包：

```text
PerfectBlockTrainer_V7.0.5_RELEASE.zip
```

SHA256：

```text
7F1A48CDDDA8CE3AF4C39540E4DA2A922990B613BD5F666F8E592951E456A541
```

运行时 DLL：

```text
main.dll
```

SHA256：

```text
50F6B6FAE66C772B772FD04783E4947394D6B86F5CD6D3D80442C7B848300ECD
```

大小：

```text
514560 bytes
```

只有从 PerfectBlockTrainer 官方发布渠道获取的包应被视为官方版本。

## 13. 最终检查表

- [ ] 已安装 UE4SS_Grounded2 1.0.4
- [ ] 安装 UE4SS 后可以正常进入主菜单
- [ ] `PerfectBlockTrainerCpp\dlls\main.dll` 路径正确
- [ ] 已安装 `PerfectBlockTrainer.pak`
- [ ] 已安装 `PerfectBlockTrainer.ucas`
- [ ] 已安装 `PerfectBlockTrainer.utoc`
- [ ] `BPML_GenericFunctions : 1`
- [ ] `BPModLoaderMod : 1`
- [ ] `PerfectBlockTrainerCpp : 1`
- [ ] 可以正常进入存档
- [ ] 敌人攻击时出现 QTE
- [ ] Ring 正常显示
- [ ] Pointer 正常运动
- [ ] 攻击结束后 UI 正常消失
