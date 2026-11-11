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
