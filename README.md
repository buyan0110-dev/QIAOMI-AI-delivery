# v0.6.0 小小世界 · P1–P3 功能候选版

**[下载完整源码 ZIP](QIAOMI-v0.6.0-P1-P3-CANDIDATE-source.zip)** · [修改文件](docs/world/CHANGED_FILES.md) · [逐项功能与素材缺口](docs/world/IMPLEMENTATION.zh-CN.md) · [测试报告](docs/world/TEST_REPORT.zh-CN.md) · [实际 Qt 截图](docs/world/screenshots/) · [Windows启动与验收](docs/world/WINDOWS_ACCEPTANCE.zh-CN.md)

已从真实 P0-fix.1 增量修正两项基础问题，并实现 F01–F10 的本地逻辑、五个新 PySide6 页面与小游戏。最终 Linux 完整回归 **681 passed / 269.45秒**；此前分阶段629/651/658/666项全量通过。原264运行资源哈希完全不变，没有包含私人数据库/模型/录音/配置。

**新增微动作/道具/家具含明确轻量占位，精绘未完成；Windows11真实麦克风/游戏/双屏/无黑窗与最终EXE实机验收未完成。** 新窗口沿用旧粉/浅/深主题，原功能保留。

Windows CI 将尝试在 GitHub Windows runner 上完整测试和构建 GUI EXE；只有实际成功产出才提供便携包，不把 CI 当作 Windows11+HyperX 真机验证。下载后完整解压，先退出旧托盘，保留原用户数据目录。首次 start.bat，日常 start.vbs；新收藏相册 sidecar 不修改旧记忆库Schema。

旧交付保留如下：

---

# v0.6.0-P0-fix.1 — 代码审查修正版（非完整v0.6.0）

**[下载P0修正版完整源码 ZIP（约26 MiB）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.6.0-p0-fix.1/QIAOMI-v0.6.0-P0-fix.1-source.zip)**

修正F03/F05/F09/F10分类门禁、旧身体反馈前置清理、观察/覆盖/视觉分渠道、generation token与优先级/取消/重入/超时，以及新P0快照版本标签；合法旧快照原样复用。264个运行资源不变，无数据库结构迁移。

**在修正后的同一源码树完整运行pytest：624项通过 / 222.75秒。** 不是引用旧578/94结果。Windows11实机/真实音频/DPI/游戏与EXE仍未验证，未提供新EXE。

**F01–F10具体玩法、五个新页面及P1–P4仍未完成。** 本包修复基础接口，不应作为十功能成品验收。

[逐条建议判断/修改文件行号/启动/未验证项](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.6.0-p0-fix.1/docs/p0fix/REPORT.zh-CN.md) · [完整测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.6.0-p0-fix.1/docs/p0fix/TEST_REPORT.zh-CN.md) · [原始测试输出](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.6.0-p0-fix.1/docs/p0fix/tests.txt) · [SHA256](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.6.0-p0-fix.1/SHA256SUMS.txt)

测试前先旧托盘完全退出，在新目录启动并保留原数据/模型。首次start.bat，日常start.vbs；换目录更新快捷方式/自启动路径。打包沿用Windows build_windows.bat。本包不含私人数据库、配置、录音、模型或虚拟环境；历史说明保留如下。

---

# 最新交付：QIAOMI AI v0.5.0-pink.2 — 比例、完整圆角与浴缸遮挡修复

**[下载修复后的完整源码 ZIP（约31 MiB）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/QIAOMI-AI-v0.5.0-pink.2-CANDIDATE-source.zip)**

> 开发进度：[v0.6.0 P0检查点](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.6.0-p0)已上传，仅审核/备份/事件门禁地基；**F01–F10和新页面尚未完成，不是完整v0.6.0**。当前pink.2可用版本下载保持不变。

用 Edge / Chrome 打开文件页，点击 **Download raw file（下载箭头）**。当前为候选源码，**没有已构建Windows EXE**。

- 右上角为最小化、最大化／还原、关闭三按钮，**保持原粉色底**，不改成灰色底；关闭仍只隐藏管家，托盘可真正退出。
- 角色按图集每帧真实宽高比绘制，不再把竖长图画成正方形；背景等比完整显示，原图片未压缩/替换。
- 外框四角固定完整透明圆角，只有内容滚动；1080×780标准字号下首页、概览、洗澡、喂食均完整显示。
- 所有洗澡状态共用浴缸前景遮挡，猫咪脚爪/尾巴不再压到浴缸前壁上。

[右上角粉色按钮](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/caption-normal.png) · [最大化后的还原图标](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/caption-restore.png) · [实际首页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/home-1080x780-100.png) · [实际洗澡](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/manual-bath-1080x780.png) · [实际喂食](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/manual-feed-1080x780.png)

**完整回归578项通过；最后保留粉色按钮底的调整，另跑92项按钮/几何专项通过。** 264个运行资源不变，生活/语音/记忆/游戏状态机原代码保留。截图为Linux真实Qt运行，不是Windows实机；Windows11/DPI/DWM/EXE仍待验证。历史胸饰逐帧统一与完整独立需求书核对等未完成项未虚报完成。

[修复原因/文件/安装](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/FIX_REPORT.zh-CN.md) · [测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/TEST_REPORT.zh-CN.md) · [修复前浴缸层次](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/before-bath.png) · [修复后待洗澡](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/docs/pink2/previews/bath-1080x780-100.png) · [SHA256校验](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.2/SHA256SUMS.txt)

先旧托盘完全退出，解压新目录，首次start.bat，日常start.vbs或新快捷方式；换目录需更新快捷方式/自启动路径。原用户数据和模型保留，无数据结构迁移。源码包不含私人数据库、配置、录音、模型或虚拟环境。历史对比媒体在旧交付分支保留，打包范围见docs/pink2/PACKAGING.zh-CN.md。

下面为历史交付记录，当前状态以pink.2报告为准。

---

# 最新交付：QIAOMI AI v0.5.0-pink.1 — 粉色管家整合候选

**[下载完整源码 ZIP（约36 MiB）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/QIAOMI-AI-v0.5.0-pink.1-CANDIDATE-source.zip)**

请用 Edge / Chrome 打开文件页，点右上角 **Download raw file（下载箭头）**。本包是源码，**没有已构建Windows EXE**。

新增粉色管家首页、主窗口“照顾敲咪 / 洗澡澡 / 喂饭饭”。妈妈帮洗有女性手部持海绵，随页面鼠标互动；自动洗无手部。补充完整穿回睡衣四帧，新图集胸饰为红白宝可梦球。保留手动/自动/一键、原记忆/语音/桌宠/主题与游戏深眠。

[实际首页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/previews/home.png) · [实际洗澡页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/previews/bath.png) · [实际喂食页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/previews/feed.png) · [完整穿衣收尾动画](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/previews/dressing-completion.mp4)

**完整回归486项通过，最后渲染专项35项通过；截图为Linux真实Qt运行，非Windows实机。** 尚待：整合包独立完整需求书核对、旧桌宠WebP历史胸饰逐帧统一、Windows实机及EXE构建。新动画为独立关键帧配合程序效果，不能称为完整3D布料动画或已全部验收。

[实现/安装/未完成项](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/IMPLEMENTATION.zh-CN.md) · [测试/性能/Windows步骤](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/TEST_REPORT.zh-CN.md) · [打包范围](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/docs/pink/PACKAGING.zh-CN.md) · [SHA256校验](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0-pink.1/SHA256SUMS.txt)

旧托盘先完全退出，解压到新目录；首次start.bat，语音install_voice.bat，日常start.vbs或新快捷方式。换目录须重新配置快捷方式/自启动路径。新版首次自动备份配置和SQLite，数据目录及数据库结构不变。包内不含私人配置、数据库、模型、录音或虚拟环境。全部257个旧运行资源保留；为缩小体积省略旧文档对比媒体，旧交付包仍保留。

以下为历史交付记录，当前状态以上方候选说明为准。

---

# 最新交付：QIAOMI AI v0.5.0 — 零负担自主生活

**[下载完整源码 ZIP（约91 MiB）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/QIAOMI-AI-v0.5.0-source.zip)**

用 Edge / Chrome 打开文件页，点击右上角 **Download raw file（下载箭头）**。本包是完整源码，**不是已构建的Windows EXE**。

新增喂食、五阶段洗澡、逗猫棒/毛线球/玩具老鼠、3–5分钟闲置摸鱼、四项生活数值及免费自主照顾。离线不扣分，不会病死；游戏深眠停止生活活动，仅托盘手动唤醒。保留原长期记忆、语音、互动、主题和全部257个原资源文件。

**455项自动化测试通过，Linux Qt流程通过；Windows11、真实麦克风、真实游戏和EXE运行未验证。** 新道具为程序绘制效果，部分猫姿复用旧动画，专用洗澡/捧鱼/追玩具精绘帧仍待补；原美术待审项未在本次重绘。

先从旧托盘完全退出，解压到新目录；首次`start.bat`安装，语音`install_voice.bat`。日常`start.vbs`或`install_shortcut.vbs`。换目录须重建快捷方式、关闭再开启自启动以更新路径。首次启动新版先备份用户配置和SQLite，生活值新增独立life.json，不改数据库结构。包内不含私人数据库、个人配置、录音、模型和虚拟环境。

[使用/升级/回滚与素材缺口](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/docs/v050/GUIDE.zh-CN.md) · [测试及Windows验收](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/docs/v050/TEST_REPORT.zh-CN.md) · [修改文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/docs/v050/FILES.zh-CN.md) · [实际洗澡截图](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/docs/v050/previews/bath-1.png) · [玩具截图](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/docs/v050/previews/wand.png) · [SHA256](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.5.0/SHA256SUMS.txt)

旧版本及原交付分支完整保留。下面为历史记录，本次状态以v0.5.0说明为准。

---

# 最新交付：QIAOMI AI v0.4.1 装饰尾巴与边界精修第2轮（候选）

**[下载完整源码 ZIP（约83 MB）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/QIAOMI-AI-v0.4.1-costume-tail.2-CANDIDATE-source.zip)**

使用 Edge / Chrome 打开文件页，点击右上角 **Download raw file（下载箭头）**。当前是完整源码，未构建 Windows EXE。

本轮精修21组98帧，原66张显著不透明边界警告清零；修改范围内低透明残留计数下降87.35%。摸头后三帧已去掉两只多余落地前爪，仅保留两只举起前爪和两只后爪。**404项自动化测试通过。全套透明羽化、连续动作与Windows11实机验收仍待完成。**

[实际摸头前后对比](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/touch-head-before-after.png) · [耳尖前后对比](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/ears-before-after.png) · [实际Qt动画预览](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/actions-before-after.mp4) · [修复报告与安装验收](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/REPORT.zh-CN.md) · [测试结果](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/TEST_RESULTS.txt) · [逐帧状态](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/frame-status.csv) · [SHA256校验](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1-costume-tail.2/SHA256SUMS.txt)

先从托盘完全退出旧实例，再于独立新目录测试并备份用户数据。图片、清单与绘制代码须一同更新；已有EXE需重建。旧版本保留：[artfix.1候选](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.4.1-artfix.1) · [原v0.4.1](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.4.1)。

## 原v0.4.1历史交付说明

以下为历史记录，最新精修状态以上方报告为准。

---

# QIAOMI AI v0.4.1 — 桌宠生命系统2.0 / AI管家界面2.0

[打开 v0.4.1 完整源码 ZIP 文件页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/QIAOMI-AI-v0.4.1-source.zip)

请用 **Edge/Chrome** 打开文件页，再点右上角 **Download raw file（向下箭头）**。如聊天内置浏览器打开下载会退出，请复制到外部浏览器。完整ZIP约8.84 MB，解压后再运行；**当前没有已构建Windows EXE**。原版本保留。

[安装与启动](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/INSTALL.md) · [逐项功能状态](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/FEATURE_STATUS.md) · [缺失素材](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/MISSING_ASSETS.md) · [测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/TEST_REPORT.md) · [Windows验收](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/WINDOWS_TEST_STEPS.md) · [Windows构建](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/WINDOWS_BUILD.md) · [升级与数据保护](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/UPGRADE.md) · [修改文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/FILES_CHANGED.md) · [更新日志](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/CHANGELOG.md) · [语音配置](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/VOICE.md)

## 本轮增量实现

- 四边独立姿态、约32个Qt逻辑像素边缘吸附、拖离解除、开关与位置保存；无手动保存位置时默认在边缘栖息。
- 十个部位互动：左右耳、头、下巴、肚子、左右前后爪、尾巴。自主动作被触摸时收尾→坐姿→部位反馈；触摸优先于任务视觉但不取消AI/语音数据任务。
- 看书翻页、金丝眼镜游戏机与胜负、毛线球、吃饭、瞌睡惊醒、趴睡、洗脸理帽、伸展，均由本地轻量调度器执行，梦话低频静音。
- 只有有效鼠标触摸重置本版本的冷落计时；聊天/语音/拖动不重置。10/20/30分钟寻找/委屈/生气，已吸附边缘时可临时爬中央，安全未知/全屏时延后，用户可中断或关闭。
- 独立四次摸摸哄好，至少间隔0.65秒，快速三连击不能替代。第四次专属转身举双爪和好；临时中央点不覆盖用户的家。
- 游戏深眠停止动画/位移/冷落/梦话/音频与新推理，跨重启保留，只能明确“🐾唤醒敲咪”。随后纸盒醒来和哭唧唧重逢一次，可跳过，不强制语音。
- 奶白浅色/原深蓝色，100/110/125/150%字体，立即应用保存；大字体窄窗紧凑导航/可滚动布局。欢迎区与聊天头像统一，本地随机欢迎语可关闭。
- 聊天气泡/输入/代码块/长行换行优化，隐藏后延迟HTML排版、闲置Orb无timer；主题字体不重载桌宠动画。

## 预览与真实边界

[浅色截图](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/previews/butler-light.png) · [深色截图](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/previews/butler-dark.png) · [150%字号](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/previews/butler-light-150.png) · [桌宠姿态图](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/previews/pet.png) · [静音动画预览MP4](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/previews/pet-animation.mp4)

预览是实际程序的 **Linux Qt离屏渲染**，不是Windows截图。MP4为74帧/14.8秒的姿态片段，无音轨，不是完整自主交互或真实跨桌面移动录像。

**新增140帧，总计252张WebP关键帧。** 四边不是同一图旋转。仍是生成式初版，比例、羽化边缘、道具消失与动作衔接待精修；**独立倒挂、毛线球专属收尾、逐帧精确命中标定尚未补齐**。基础姿态组命中不冒充每帧轮廓精确标定。

## 验证范围

**373项自动化测试通过，0失败；79状态Linux启动自检与pip check通过。** 末次提示文案更新后记忆/输入UI另复测6项通过（不是另算6个新案例）。时间边界为注入时钟测试，Windows/音频测试包含模拟。

**Windows11真机、GUI EXE、HyperX真实ASR/TTS、多显示器/多DPI、GPU/显存/游戏并行与数小时内存耐久未在本轮完成。** 没有用Linux代替Windows结论。专用中文KWS仍未实现，保留默认关闭的可替换ASR实验唤醒；共享Ollama模型驻留/已发出任务不保证被立即终止。

[自动化XML](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/TEST_RESULTS.xml) · [UI复测XML](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/UI_COPY_TEST_RESULTS.xml) · [启动自检](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/SMOKE_RESULTS.json) · [性能原始数据](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/PERFORMANCE_LINUX.json) · [源码比对](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/SOURCE_DELTA.json) · [发布清单](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/release-manifest.json)

## 安装与数据

先从旧托盘完全退出并备份原用户目录、模型与自定义形象。解压到新可写目录；start.bat准备基础依赖，install_voice.bat准备语音。日常用start.vbs或install_shortcut.vbs创建的“敲咪”图标，start.bat保留调试黑窗口。旧EXE不会自动变成新源码版本，需Windows重新构建并重建快捷方式。

SQLite结构不变、无SQL迁移；原采集/worker/Ollama/配置加载代码与GUI启动脚本/ICO保持。新增appearance.json与可兼容偏好字段，不覆盖数据库和个人语音配置。旧累计时间/安抚进度保留，不能追溯旧版真实最后摸摸时间。旧自定义形象继续保留；恢复内置形象后才使用新素材。

ZIP不含私人数据库/配置、录音、模型、密钥或虚拟环境；其中MP4仅为静音Qt资源渲染。

SHA-256：

```text
9c8d6f8d968621e50f23c6df1e1e21c4bf07e3c042592056828a03b2bb2bbdf6
```

[校验文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.1/QIAOMI-AI-v0.4.1-source.zip.sha256)

历史版本：[v0.4.0完善版](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.4.0/completion) · [原v0.4.0](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.4.0) · [v0.3.2](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.2) · [v0.3.1](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.1)
