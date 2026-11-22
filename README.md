<div align="center">
  <h1 align="center">
    <img src="icons/icon.png" width="200" alt="ok-kes logo"/>
    <br/>
    ok-kes
  </h1> 
  
  <p>
    一个基于图像识别的卡厄思梦境自动化辅助工具，支持后台运行，基于 <a href="https://github.com/ok-oldking/ok-script">ok-script</a> 开发。
    <br />
    An image-recognition-based automation tool for Chaos Zero Nightmare (卡厄思梦境), with background mode support, developed with <a href="https://github.com/ok-oldking/ok-script">ok-script</a>.
  </p>
  
  <p><i>通过 Windows 接口模拟用户进行操作，无内存读取、无文件修改</i></p>
  <p><b>✅ 支持国际服繁体中文、国服 PC 客户端及安卓模拟器</b></p>
</div>

<!-- Badges -->
<div align="center">
  
![平台](https://img.shields.io/badge/platform-Windows-blue)
[![GitHub release](https://img.shields.io/github/v/release/azurplain/ok-kes)](https://github.com/azurplain/ok-kes/releases)

</div>

> 本仓库为 [baoxin1100/ok-kes](https://github.com/baoxin1100/ok-kes) 的增强复刻版（基于 `v1.4.17`，前期刻印刷取、特例神话装备、国服精密加工记忆等增强已随 PR #23 / PR #25 合入主仓库，本仓库持续提供最新修复与先行打包），打包安装包与轻量补丁请前往 [Releases](https://github.com/azurplain/ok-kes/releases) 下载。

### [English Readme](README_en.md) | 中文说明

> 📖 **第一次使用？请先阅读：[完整使用文档](docs/zh-CN/usage-guide.md)**

---

## ⚠️ 免责声明

本软件为外部辅助工具，旨在自动化《卡厄思梦境》的部分游戏流程。它完全通过模拟常规用户界面与游戏交互，遵循相关法律法规。本项目旨在简化用户的重复性操作，不会破坏游戏平衡或提供不公平优势，也绝不会修改任何游戏文件或数据。

本软件开源、免费，仅供个人学习与交流使用，请勿用于任何商业或营利性目的。开发者团队拥有本项目的最终解释权。因使用本软件而产生的任何问题，均与本项目及开发者无关。

**使用本软件即表示您已阅读、理解并同意以上声明，并自愿承担一切潜在风险。**

## 🚀 快速开始

1. **下载安装包或轻量补丁**：前往 [GitHub Releases](https://github.com/azurplain/ok-kes/releases) 下载最新的增强版完整安装程序；若已安装原版 `ok-kes`（v1.4.13 ~ v1.4.17），也可直接下载体积约 800KB 的 `ok-kes-patch-*.zip` 轻量补丁包，**先删除** `data\apps\ok-kes\working\ok_tasks` 旧文件夹，再将压缩包内的 `ok_tasks` 解压放入 `working\`（避免旧版残留文件如 `SortieModeExperimental.py` 报错）。
2. **安装并运行**：安装程序或覆盖补丁后重启，连接游戏窗口即可开始自动化。

## 🔥 本复刻版增强与最新修复（基于 v1.4.17）

### 1. 装备刻印刷取系统（光明 / 黑暗刻印）
- **新增配置**：`刻印刷取`（总开关）、`刻印优先级`、`首层未刷到刻印重开`、`最终战前已命中词条至少为多少`（0~3）。
- **智能识别与长文本自动翻页**：支持识别事件/战斗/商店装备的光明与黑暗刻印图标；遇到长描述 `▼` 按钮时自动翻页直到露出刻印词条，仅提取行内刻印图标及以下文本进行匹配。
- **3 槽位独立记录、过渡穿戴与保留刻印**：支持分别记录 1/2/3 号位刻印；词条优先级 > 装备优先级。非商店的白嫖**非优先级**装备在槽位尚未命中刻印时允许先穿戴过渡，保证局内战斗力；**特例神话装备**（`混沌之识/混沌指控`、`乱世之触/混沌触手`）未命中刻印时也允许正常穿戴与购买；**已命中目标刻印的槽位**允许被无刻印高优先级/高品质装备升级替换并**自动保留原有槽位刻印记录**，同时禁止被未命中刻印的带刻印装备覆盖。
- **德朗商店刻印识别与防抖**：支持识别商店 5 个槽位（含 1 号位特价上移位置及带空格/横线的特价价格）的刻印，自动预览词条并在未命中时点「取消」（不替队友购买）；仅在真正进入购买页后记录本页已检缓存，抗网络波动与 `+` 号 OCR 抖动。
- **局内重启无缝衔接**：每次局内启动进入战斗员信息页时，自动扫描目标主战员 3 个装备槽位并弹窗读取当前刻印词条记录。
- **双阶段保底删档重开**：支持「第一层通关未刷到刻印重开」以及「第 2 层最终 Boss 前（最后一个休息点后）已命中词条数不足 N 条重开」，触发后结算页无视 TB 阈值直接删档。

### 2. 命运选择优先级与黑名单
- **新增配置**：`命运优先级`、`拉黑命运`。
- **三卡区域 OCR 筛选**：完整识别命运卡标题与效果描述，先过滤命中 `拉黑命运` 的选项（若 3 个均被拉黑则自动跳过），再从安全命运中按 `命运优先级` 顺序选择。

### 3. 局内体验增强与稳定性修复
- **赛季卡厄思 / 零式系统刷新目标 pt**：支持自动刷新至目标 `pt`，并在货币不足或连续无变化时自动停止刷新并进入。
- **全局多行 OCR 文本阅读序排序**：`_get_region_text` 与刻印文本提取统一按纵向重叠行聚类（从左到右、从上到下）排序，解决人格面具/卡牌/事件描述偶发上下行错位问题。
- **记忆加工自动词条转换**：新增 `加工记忆` 开关与 `加工记忆词条` 配置，修复国服 `精密加工记忆` 界面被 `加工记忆` 误判死循环的问题，并采样按钮自身区域颜色独立判定左右按钮激活状态（注：简中服词条为「己方/伤害总量」，繁中服为「友军/伤害量」）。
- **不需要的装备直接提炼**：卡厄思模式下刷存档主战员不需要的装备直接点击「提炼」转化为信用点（商店内直接「取消」），不再塞给其他队友。
- **多项稳定性修复**：修复人格面具获取页 `>|` 跳过图标与左下角 `3/3` 刷新识别、卡牌分配页固定跳过坐标兜底、休息处冥想防死循环、宝箱/事件特征与记忆卡牌刷新检测等待时间。

## ✨ 主要功能

<img src="docs/images/image_1.png" alt="功能界面" />

### 自动出击模式
- 🎮 自动战斗：基于按键识别的智能出牌，支持玩家配置出牌优先级
- 🃏 自动选牌：自动获取、移除、复制、闪光卡牌
- ⚔️ 主战员选择：自动按优先级选择出站主战员
- 🛣️ 路线选择：智能识别节点类型，按优先级自动前进
- 🏪 商店处理：自动进入德朗商店移除卡牌
- 💊 以太补充检测：检测体力不足时自动退出
- 支持自定义卡牌优先级、移除/复制/闪光列表等配置

### 自动卡厄思模式
- 🃏 自动卡牌管理：移除、复制、闪光、赋予闪光、转换等
- 🛣️ 路线选择：自动识别休息/事件/boss/小怪节点
- 🏥 精神崩溃治疗：自动前往创伤中心治疗
- 📦 存储数据处理：自动删除存档（可配置保留）
- 🏪 商店处理：自动进入德朗商店
- 🌀 零式系统支持：自动处理法典搜索
- 更多功能持续开发中...

### 半自动剧情模式
- 💬 自动对话：跳过剧情对话
- ⚠️ 遇到战斗或卡厄思关卡时可手动切换对应模式

### 配置导入导出
- 📤 **导出配置**：一键将当前模式配置编码为文本并复制到剪贴板，可分享给他人
- 📥 **导入配置**：粘贴他人分享的配置编码即可应用配置，支持不同版本间互相导入

### 配置同步与热门配置 (v1.3.5+)
- 📡 **自动上传配置**：每5分钟自动上传匿名的配置信息和胜率到云端，帮助统计热门配置
- 🌟 **热门配置**：在卡厄思模式/出击模式的配置页中点击"热门配置"按钮
  - 浏览其他高胜率玩家分享的配置（支持按胜率或使用人数排序）
  - 一键应用热门配置到本地
  - 需开启配置上传功能才能使用（防止只下载不贡献）
- 🔒 **隐私说明**：不上传任何个人信息、游戏账号、截图、IP地址

### 通用功能
- 🖥️ **高分辨率支持**: 支持 1920x1080 / 1600x900 / 1280x720 等 16:9 分辨率
- 🔄 **后台模式**: 支持游戏窗口最小化或被遮挡时在后台运行
- 🌏 **多语言游戏支持**: 支持简体中文、繁体中文客户端（在自动模式配置中设置对应的“游戏语言”）

## 🔧 使用说明

1. **国际服玩家必读**：请在所使用的自动模式配置中将“游戏语言”设置为繁体中文
2. **自动战斗**：依赖按键识别，请在游戏设置中打开快捷键显示，提升出牌准确率
3. **卡厄思模式**：请主动打开游戏内自动战斗和自动剧情功能
4. **剧情模式**：战斗关卡可手动开启出击模式调用自动战斗功能；遇到卡厄思关卡请手动打开卡厄思模式；战斗关卡队伍需手动配置

## 🔧 疑难解答 (Troubleshooting)

如果遇到问题，请在提问前按以下步骤逐一排查：

1. **杀毒软件**：将软件所在目录添加到杀毒软件（包括 Windows Defender）的**信任区或白名单**中，以防文件被误删或拦截。
2. **显示设置**：
   * 关闭所有显卡滤镜（如 NVIDIA Game Filter）和锐化功能。
   * 使用游戏默认的亮度设置。
   * 关闭任何在游戏画面上显示信息的叠加层。
3. **游戏分辨率**：请确保游戏分辨率设置为 16:9 比例。
4. **软件版本**：检查并确保您使用的是最新版本。
5. **寻求帮助**：如果以上步骤都无法解决您的问题，请通过社区渠道提交详细的错误报告。

---

## 💖 赞赏支持

如果本分支新增的功能对你有帮助，欢迎自愿赞赏支持（项目免费开源学习交流，非商业售卖）~感谢

<p align="center">
  <img src="docs/images/my_wechat.jpg" alt="微信赞赏码" width="300">
  <img src="docs/images/my_alipay.jpg" alt="支付宝收款码" width="300">
</p>

---

## 💻 开发者专区

### 从源码运行 (Python)

```bash
# 安装或更新依赖
pip install -r requirements.txt --upgrade

# 运行 Release 版本
python main.py

# 运行 Debug 版本
python main_debug.py
```

本项目基于 [ok-script](https://github.com/ok-oldking/ok-script) 框架开发，简单易维护。欢迎有兴趣的开发者使用 [ok-script](https://github.com/ok-oldking/ok-script) 开发您自己的自动化项目。

## 🔗 使用ok-script的项目：

* 卡厄思梦境 [https://github.com/baoxin1100/ok-kes](https://github.com/baoxin1100/ok-kes)
* 鸣潮 [https://github.com/ok-oldking/ok-wuthering-wave](https://github.com/ok-oldking/ok-wuthering-waves)
* 少前2 [https://github.com/ok-oldking/ok-gf2](https://github.com/ok-oldking/ok-gf2)
* 星痕共鸣 [https://github.com/Sanheiii/ok-star-resonance](https://github.com/Sanheiii/ok-star-resonance)
* 二重螺旋 [https://github.com/BnanZ0/ok-duet-night-abyss](https://github.com/BnanZ0/ok-duet-night-abyss)
* 明日方舟：终末地 [https://github.com/AliceJump/ok-end-field](https://github.com/AliceJump/ok-end-field)
* 异环 [https://github.com/BnanZ0/ok-nte](https://github.com/BnanZ0/ok-nte)
* 阴阳师 [https://ok-script.com/ok-onmyoji](https://ok-script.com/ok-onmyoji)

## ❤️ 致谢

* [ok-script](https://github.com/ok-oldking/ok-script)
* [OnnxOCR](https://github.com/ok-oldking/OnnxOCR)
* [PyQt-Fluent-Widgets](https://github.com/zhiyiYo/PyQt-Fluent-Widgets)
