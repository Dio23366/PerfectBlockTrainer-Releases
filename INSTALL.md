# PerfectBlockTrainer V7.0.8 — Native QTE Installation

[Project technical overview](README.md) · [Nexus download](https://www.nexusmods.com/grounded2/mods/198)

PerfectBlockTrainer V7.0.8 — Native QTE
INSTALLATION / 安装说明

IMPORTANT: REMOVE OLD PBT FILES BEFORE UPGRADING / 升级前先移除旧文件

中文版
安装过7.0.7或更早版本：保存并退出游戏，备份后移除
Grounded2\Augusta\Content\Paks\LogicMods 中的这三个旧PBT文件：
- `PerfectBlockTrainer.pak`
- `PerfectBlockTrainer.ucas`
- `PerfectBlockTrainer.utoc`
只移除这三个文件，不要删除整个LogicMods文件夹或其他模组。

安装过早期“独立EXE圆环版”7.0.8：退出游戏并确认PbtOverlay已退出，
将 ue4ss\Mods\PBTQteAutoStart 文件夹备份到游戏目录之外，再从Mods移除。
如修改过其中 overlay\config.json，请先保存，安装后复制为
ue4ss\Mods\PerfectBlockTrainerCpp\config.json。没有自定义配置可跳过。
新版使用游戏进程内的原生绘图，不再需要这个旧启动模组或其.NET文件。
不要移除其他模组的文件，也不要卸载其他程序使用的.NET。

## English
Upgrading from7.0.7 or earlier:save and close the game,back up and remove ONLY:
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.pak
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.ucas
Grounded2\Augusta\Content\Paks\LogicMods\PerfectBlockTrainer.utoc
Keep the LogicMods folder and all unrelated mods.

Upgrading from the earlier7.0.8 standalone-EXE renderer:close the game and
PbtOverlay.Back up ue4ss\Mods\PBTQteAutoStart outside the game,then remove
that old mod folder.If you customized overlay\config.json,save it and copy
it to ue4ss\Mods\PerfectBlockTrainerCpp\config.json after installing.
The native version no longer needs that companion or its bundled .NET files.
Do not remove other mods or uninstall .NET used by other applications.

---
## English
---
### 1. Requirements
Grounded2 UE5.7.4 on Windows x64,plus the tested UE4SS_Grounded2 1.0.6:
UE4SS_Grounded2 52 1.0.6 2026-10-24T21-32Z V7eYNegQ4.zip
Install that loader according to its own instructions.This package does not
include UE4SS.dll,dwmapi.dll or an installer.No separate .NET installation is
required.PBT uses native Windows drawing and the native C++ runtime used by
its UE4SS environment.If Windows reports a missing VCRUNTIME140*.dll,use the
official Microsoft Visual C++2015–2022 Redistributable x64;do not download
individual DLLs from third-party sites.

### 2. Locate the game
Steam > Grounded2 > Properties > Installed Files > Browse.
The game root contains Augusta,Engine and Grounded2.exe.
Paths in this guide start at that root.

### 3. Prepare UE4SS
Expected loader layout:
- `Augusta\Binaries\Win64\dwmapi.dll`
- `Augusta\Binaries\Win64\ue4ss\UE4SS.dll`
If the tested loader already works,keep it.Preserve all unrelated mods and
configuration.Do not replace a different graphics proxy blindly.

### 4. Install PBT
Save and fully exit the game.Complete the upgrade cleanup above.
Extract this ZIP.Open PerfectBlockTrainer_V7.0.8_RELEASE\Mods and copy the
ONE folder PerfectBlockTrainerCpp into:
- `Grounded2\Augusta\Binaries\Win64\ue4ss\Mods`
Replace the PBT main.dll when prompted.Do not copy an extra Mods folder
inside Mods,and do not place the DLL beside the game EXE.

### 5. Confirm these files
- `ue4ss\Mods\PerfectBlockTrainerCpp\enabled.txt`
- `ue4ss\Mods\PerfectBlockTrainerCpp\config.default.json`
- `ue4ss\Mods\PerfectBlockTrainerCpp\dlls\main.dll`
The empty enabled.txt enables the C++ mod.No manual mods.txt editing or
PerfectBlockTrainerCpp : 1 line is needed.Keep enabled.txt named exactly;
Windows may hide known file extensions.Do not overwrite other mods.txt files.

### 6. Start and play
Launch normally through Steam.The white ring and red pointer show a short
startup preview with green,red and gold hollow frames.Each frame clears
after the pointer passes.Combat cues appear automatically for supported
attacks and clear when finished.No separate QTE application needs starting.
There is no F8 full/dim/hidden cycle.

### 7. Cue meanings
White ring:timing reference.Green hollow frame:recommended Perfect Block
window.Red frame:danger warning;dodge rather than treating it as a normal
Perfect Block cue.Gold:shared time in overlapping block windows.
The mod gives timing cues;the player still performs the block or dodge.

### 8. Adjust appearance
To customize,copy config.default.json to config.json in PerfectBlockTrainerCpp.
Edit config.json with a text editor and restart the game.Parameters control
radius,stroke,frame width,pointer size,centerX/centerY and scale.
Default size is based on1080p height and scales with client height.Keep valid
positive values;center coordinates are normalized between0 and1.This release
does not ship a personal config.json,so updates preserve your custom file.

### 9. Recording with OBS
The ring is a separate transparent window even though its code runs inside
the game process.Game Capture or Window Capture may omit it.Display Capture
can include both the game and QTE;preview the recording before a full session.

### 10. If no ring appears
Check the startup preview and test a supported enemy.Check the exact folder
layout,enabled.txt and the tested UE4SS version.Close the game before changing
files.To test defaults,back up and temporarily rename your config.json.
UE4SS.log contains [PBTCPP][NativeQte] startup/state messages.If that log
reports an error,include it when requesting help.The old PbtOverlay.exe is
not required,and running it manually can produce duplicate rings.

### 11. Uninstall or roll back
Close the game.Back up your custom config,then remove only
ue4ss\Mods\PerfectBlockTrainerCpp.Leave other mods and UE4SS alone.
For rollback,restore a complete matching older PBT package and follow its
instructions;the old EXE version requires its old companion folder too.

### 12. Files and licenses
INSTALL.txt explains installation.RELEASE_NOTES.md lists changes.VERSION.txt
identifies the release.第三方许可_THIRD_PARTY_NOTICES.txt contains notices for native components.

---
## 简体中文
---
### 1. 运行要求
Grounded2 UE5.7.4，Windows x64，以及已测试的UE4SS_Grounded2 1.0.6：
UE4SS_Grounded2 52 1.0.6 2026-10-24T21-32Z V7eYNegQ4.zip
UE4SS请按其作者的说明安装。本包不含UE4SS.dll、dwmapi.dll或安装器。
不需要单独安装.NET。新版使用Windows原生绘图和UE4SS环境所需的C++运行库。
如果系统明确提示缺少VCRUNTIME140相关DLL，请安装微软官方Visual C++
2015–2022 x64运行库，不要从不明网站下载单个DLL。

### 2. 找到游戏根目录
Steam > Grounded2 > 属性 > 已安装文件 > 浏览。
根目录应包含Augusta、Engine及Grounded2.exe，下面路径均从这里开始。

### 3. 准备UE4SS
正确布局包括：
- `Augusta\Binaries\Win64\dwmapi.dll`
- `Augusta\Binaries\Win64\ue4ss\UE4SS.dll`
已经使用上述版本正常运行的用户无需重装。保留其他模组及配置，不要盲目
覆盖其他图形代理文件。UE4SS与PBT是分别安装的。

### 4. 安装PBT
保存并完全退出游戏，先完成本文开头的旧版文件清理。
解压本包，打开PerfectBlockTrainer_V7.0.8_RELEASE\Mods，只复制其中的
PerfectBlockTrainerCpp这一个文件夹到：
- `Grounded2\Augusta\Binaries\Win64\ue4ss\Mods`
升级时替换PBT自己的main.dll。不要放成Mods\Mods，也不要把DLL放在游戏EXE旁。

### 5. 核对文件
- `ue4ss\Mods\PerfectBlockTrainerCpp\enabled.txt`
- `ue4ss\Mods\PerfectBlockTrainerCpp\config.default.json`
- `ue4ss\Mods\PerfectBlockTrainerCpp\dlls\main.dll`
空白enabled.txt用于启用模组，无需编辑mods.txt，也无需添加
PerfectBlockTrainerCpp : 1。注意不要误存为enabled.txt.txt。
不要用其他包的mods.txt覆盖自己现有的模组配置。

### 6. 启动与使用
通过Steam正常启动。启动演示显示白环、红色指针及同时出现的绿、红、金
空心框；指针完整经过后框会逐个消失。支持的攻击自动显示战斗QTE，结束后
自动清理。无需另外启动圆环程序，也没有F8全显／半透明／隐藏切换。

### 7. 提示含义
白环：时机参照；绿色空心框：推荐完美格挡窗口；红框：危险警告，请考虑
闪避，不能当成普通完美格挡提示；金框：多个可格挡窗口的公共时间部分。
模组提供提示，仍需要玩家自己执行格挡或闪避。

### 8. 调整外观
将PerfectBlockTrainerCpp中的config.default.json复制一份，改名为config.json，
使用文本编辑器修改，重启游戏生效。可调整半径、线宽、框宽、指针大小、
centerX／centerY和scale。默认以1080高度为基准，随游戏客户区高度缩放。
数值保持合理正数，中心位置为0到1之间的比例。本包不提供个人config.json，
更新时保留你的自定义配置即可。

### 9. OBS录制
绘图代码虽然在游戏进程内，但圆环仍是独立透明窗口。游戏采集或窗口采集
可能只录到游戏。显示器采集可同时录入游戏和圆环，正式录制前请先预览。

### 10. 圆环没有出现
先观察启动演示，再让已支持的敌人攻击。检查目录层级、enabled.txt及
UE4SS版本。修改文件前退出游戏。测试默认配置时，先备份再暂时改名个人
config.json。UE4SS.log中的[PBTCPP][NativeQte]记录启动／状态，如有错误可
提供日志协助排查。不需要PbtOverlay.exe；手动运行旧程序可能产生双重圆环。

### 11. 卸载与回退
退出游戏，备份个人配置，只移除ue4ss\Mods\PerfectBlockTrainerCpp。
保留其他模组及UE4SS。回退时恢复完整匹配的旧版本，按旧说明安装；旧EXE
版还需要恢复对应的PBTQteAutoStart文件夹。

### 12. 包内文件
INSTALL.txt是安装说明，RELEASE_NOTES.md是更新内容，VERSION.txt标识版本，
第三方许可_THIRD_PARTY_NOTICES.txt保留原生组件的第三方许可文本。