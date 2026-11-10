# v0.3.2 文件清单

基线：已交付的 v0.3.1。未删除任何原文件。

## 修改

- `.github/workflows/windows.yml`：完整打包时加入快捷方式脚本；本次未运行 CI。
- `CHANGELOG.md`：本版说明、测试报告或操作指南更新。
- `QUICKSTART.txt`：本版说明、测试报告或操作指南更新。
- `README.md`：本版说明、测试报告或操作指南更新。
- `TEST_REPORT.md`：本版说明、测试报告或操作指南更新。
- `build_windows.bat`：Windows 平台检查、图标生成、GUI 构建与快捷方式复制。
- `docs/WINDOWS_RELEASE.md`：本版说明、测试报告或操作指南更新。
- `install_shortcut.vbs`：创建“敲咪”图标，优先 GUI EXE，否则 pythonw。
- `qiaomi.spec`：console=False 保留，新增 EXE 图标声明。
- `qiaomi/__init__.py`：版本号 v0.3.2。
- `qiaomi/__main__.py`：接入共用启动器。
- `qiaomi/app.py`：托盘、桌面设置、窗口独立关闭、游戏模式、位置恢复、退出与单实例接入。
- `qiaomi/smoke.py`：冒烟检查改为聊天与宠物共存。
- `qiaomi/ui/assistant.py`：聊天 X 只隐藏、新增桌面设置入口，保留原布局。
- `qiaomi/ui/pet.py`：有界高 DPI 绘制缓存、低功耗计时器、位置事件、内置形象选择。
- `qiaomi/voice.py`：Windows GUI 工作进程路径、暂停自动语音与卸载模型命令。
- `qiaomi/voice_worker.py`：仅新增 unload 控制命令，采集/转写流程不变。
- `scripts/frozen_entry.py`：windowed EXE 入口接入共用启动器。
- `scripts/gui_entry.pyw`：pythonw 入口接入共用启动器。
- `start.vbs`：GUI EXE 优先，否则 pythonw，不经控制台。
- `tests/test_app.py`：按新要求更新聊天/猫共存断言。

## 新增

- `assets/qiaomi.ico`：新增多尺寸橘猫图标。
- `docs/README_V0.3.1.md`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/UPGRADE_V0.3.2.md`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/WINDOWS_ACCEPTANCE_V0.3.2.md`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/TEST_REPORT-v0.3.1.md`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/desktop-v0.3.2-linux.png`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/performance-v0.3.2-before-cache-linux.json`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/performance-v0.3.2-linux.json`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/pet-v0.3.2-linux.png`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/startup-v0.3.2.json`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `docs/validation/tests-v0.3.2.xml`：本版说明、历史快照、Linux 测量/截图或验证证据。
- `qiaomi/desktop.py`：新增独立位置/形象配置、原子写与坏文件备份。
- `qiaomi/instance.py`：新增带锁的用户级本地激活管道。
- `qiaomi/launcher.py`：新增共用 GUI bootstrap、早期错误与故障栈日志。
- `qiaomi/ui/desktop_settings.py`：新增可选游戏/自启动/形象设置面板。
- `qiaomi/windows.py`：新增 GUI 解释器、用户级 Run、Explorer 消息与前台激活授权。
- `scripts/make_icon.py`：新增复用原橘猫绘制的多尺寸 ICO 生成器。
- `scripts/measure_idle.py`：新增离线隔离数据的 CPU/RSS 实测脚本。
- `tests/test_desktop_lifecycle.py`：新增 31 项桌面/IPC/GUI/Windows 模拟与退出测试。

另新增本清单与 docs/validation/source-delta-v0.3.2.json。

数据库/主配置/记忆解析/Ollama 传输/音频采集算法/start.bat 逐字节保持；requirements.txt、requirements-voice.txt、requirements-build.txt 和 requirements-dev.txt 不增加依赖。无数据库迁移。
