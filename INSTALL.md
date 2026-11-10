# QIAOMI AI v0.3.2 — Windows 桌面与托盘升级

在 v0.3.1 基础上增量实现完整桌面生命周期，保留已确认可用的 HyperX/WASAPI 语音采集算法、桌宠美术、文字聊天、Ollama、本地长期记忆和所有原配置。用户数据库结构不变，无需迁移。

**当前交付为源码 ZIP 和检查过的 Windows 构建脚本，尚未生成 Windows EXE，也未完成 Windows 11 新版实机验收。** Linux 自动化、模拟系统接口和性能测量均明确标记。

## 普通用户如何启动

优先使用 Windows 构建生成的 **QIAOMI-AI.exe**，或其桌面「敲咪」快捷方式：GUI/windowed EXE 不需要终端。

当前源码环境：

1. 完全退出旧版；备份 `%LOCALAPPDATA%\QIAOMI AI` 或既有 `QIAOMI_DATA_DIR`。保留 config.json、voice.json、qiaomi.db、原模型和自定义美术。
2. 解压到新的可写目录，用 start.bat 准备基础依赖；语音依赖仍用 install_voice.bat。已有完整模型可继续使用，无需重新下载。
3. 双击 **install_shortcut.vbs** 创建桌面 **敲咪.lnk**。脚本优先选择同目录/当前 dist 中的 GUI EXE，否则直接指向项目 .venv/Scripts/pythonw.exe + scripts/gui_entry.pyw，不经过 CMD 或 PowerShell。
4. 以后双击「敲咪」图标或 **start.vbs**。VBS 只启动独立 GUI 进程并立即返回，关闭启动器不影响 App。
5. 首次只显示小橘猫和托盘，不自动打开聊天主窗口，不自动探测或加载本地模型。双击猫咪打开聊天，右键猫咪保留互动与功能菜单。

start.bat 完整保留作安装/调试入口，使用它会有控制台；普通使用请选 GUI 入口。若源码目录内有旧版 dist/EXE，请先重建或移走旧构建，避免启动器优先打开旧 EXE。移动项目/虚拟环境后需重新准备 .venv 并重建快捷方式；旧快捷方式可手动移除。

本次声称的是 GUI 启动设计和静态检查，不是假称已在 Windows 目测“零黑窗”。Windows 真机还需检验 Explorer、Qt 插件、pythonw 与 EXE 行为。

## 托盘和关闭行为

原生 Qt QSystemTrayIcon 使用橘猫图标：左键/双击打开或恢复聊天，右键菜单提供：

- 打开敲咪；显示/隐藏桌面小猫。
- 语音设置；游戏模式；开机自启动。
- 桌面与启动设置；长期记忆；收起到托盘。
- **退出敲咪**：停止麦克风/TTS/工作进程、取消 AI 请求、完成数据库操作与桌面设置保存，再结束程序、移除托盘。

**聊天右上角 X 只关闭聊天视图**，保留猫咪当前显示状态和托盘；隐藏猫咪也不退出。聊天和宠物现在可以同时显示。要全部隐藏可用“收起到托盘”。

Windows Explorer 重启时接收 TaskbarCreated 后重新注册同一个托盘对象；另有每 10 秒一次的低频可用性恢复检查。不是每次检查都销毁/重建图标。非游戏模式且系统没有托盘时保留猫咪作为入口；游戏模式则保持隐藏，仍可通过再点桌面快捷方式唤回聊天。

## 位置和形象

宠物位置以 Qt 逻辑坐标保存在用户数据目录 **desktop.json**，移动后延迟合并写入，退出前再次保存。显示器/DPI/工作区变更后会将旧坐标夹回可见区域。

偏好设置新增“桌面 / 游戏模式 / 开机自启动”入口，可选择本地 SpriteLibrary JSON 形象清单，或恢复内置橘猫。路径保存在 desktop.json，默认仍兼容原 assets/cat/manifest.json。升级前若自定义资源放在旧项目中，请保留文件，并用此界面选择原清单；不要删除仍被引用的资源或模型目录。

形象缺失/损坏时记录错误并显示气泡/任务提示，回退内置绘制，避免无声退出。损坏 desktop.json 在重新保存前保留备份。主 config.json、voice.json 和 SQLite 不被桌面设置替换。

## 开机自启动：可选，默认关闭

在托盘或桌面设置里勾选。仅写入：

`HKCU\Software\Microsoft\Windows\CurrentVersion\Run` 中的 **QIAOMI AI** 值。

使用当前 GUI EXE，或 pythonw + GUI 脚本，加 `--autostart --data-dir "用户数据目录"`。不使用系统服务、管理员权限、计划任务或 CMD。登录时先显示猫咪与托盘，`--autostart` 优先于 --assistant；已运行时只 ping 现有实例，不打断前台游戏。

取消勾选只删除自己的这个值，不删除注册表键或其他启动项。此开关表示 Run 条目是否注册；Windows 任务管理器/系统策略仍可另外禁用启动。更换目录后界面会提示旧路径，需要取消再勾选以注册新 GUI 入口。禁用仍可在旧入口文件已经丢失时进行。

## 单实例

继续使用同一用户数据目录下的 qiaomi.lock，启动前取得锁；另用用户权限限制的本地管道传递固定 activate/ping 命令。锁失败时不创建第二个 Controller、不加载语音/AI 模型；手动重复启动恢复旧聊天窗口，自启动重复启动保持静默。

操作系统仍会短暂创建第二个启动请求进程，然后退出；不是两个常驻 App。不同显式 --data-dir 作为隔离环境可以独立运行。旧版只有锁、没有新激活协议时，提示使用旧托盘而不强行删除活锁。完全退出后释放锁与管道。

## 游戏模式

手动开关，重启默认关闭。启用时隐藏宠物/聊天/语音设置，停止宠物计时器并清空动画缓存、取消当前录音/TTS/AI 任务和待确认记忆、关闭持续唤醒、请求卸载本进程缓存的语音模型。没有增加任何后台记忆整理或自动 AI 推理任务。

仍可从托盘或快捷方式主动打开聊天，或点手动麦克风使用功能；显示猫咪时是静态且非置顶。关闭游戏模式恢复原宠物可见性和置顶偏好，但**不会自动重新开启麦克风唤醒**。

不扫描游戏进程、不截屏、不注入、不注册全局键盘钩子，也没有自动全屏检测。为了避免覆盖游戏，进入游戏前主动开启此模式即可。游戏期间没有自动弹窗/托盘气泡通知。Ollama 是独立服务，可能按自己的 keep_alive 策略保留 Qwen 权重；本程序不强制卸载共享 Ollama 模型，不能承诺游戏显存完全释放。

## 语音与隐私

v0.3.1 的手动录音、结束并识别、三秒自检、音量条、RMS/阈值诊断、CPU int8、WASAPI 名称/接口映射及本地转写保留。语音采集/处理算法不改；新增的是 Windows 工作进程使用 pythonw（或同一 windowed EXE）而非 python.exe，避免后台控制台。原中文 TTS 与记忆功能保持。

数据仍在用户持久目录，不在 PyInstaller 临时目录；自启动命令明确传入同一位置。日志在 logs/qiaomi.log、voice.log、startup.log、startup-fault.log，记录错误与堆栈，不记录密钥/转写原文。启动导入失败有 GUI 提示，原生崩溃尽可能由 faulthandler 留栈。模型路径继续用用户配置的本地绝对路径，不打进 EXE。

## Windows 构建

在 **Windows 11 x64 + Python 3.12** 运行 **build_windows.bat**。脚本准备依赖、生成多尺寸橘猫 ICO、运行 PyInstaller qiaomi.spec（console=False）、拷贝快捷方式脚本/指南，生成完整 onedir ZIP 与校验值。

输出 `dist/QIAOMI-AI/QIAOMI-AI.exe` 和 `dist/QIAOMI-AI-Windows-x64.zip`。要分发整个目录/ZIP，不能只拷贝 EXE；本地模型、Ollama、私人数据库、配置与 API Key 不包含在其中。普通用户解压后双击 EXE，再用同目录 install_shortcut.vbs 创建图标。

[构建说明](WINDOWS_BUILD.md) · [Windows 验收表](WINDOWS_TEST_STEPS.md)

## 测试与资源测量

见 [测试报告](TEST_REPORT.md)、[文件变更清单](FILES_CHANGED.md)。自动化覆盖真实 Qt、真实进程间激活和退出；Windows 注册表/Explorer 使用模拟 API，不能当成 Windows Shell 验证。

宠物待机刷新降至约 8 FPS，互动约 12 FPS，睡眠约 4 FPS，隐藏/游戏时无动画循环。完整绘制帧缓存按约 32 MB 像素预算限制，并按 DPI 降低缓存帧数；这是缓存预算，不是整个 App 内存承诺。

提供 `scripts/measure_idle.py --output 性能.json --seconds 8`：隔离临时数据、离线模式测实际进程 CPU/RSS。Windows 不设 offscreen 才能得到本机桌面样本；本次 Linux 离屏结果不代表 APEX/幻兽帕鲁并行性能。GPU 和游戏场景尚未测量，不承诺零影响。

[v0.3.1 完整功能说明（历史）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/INSTALL.md)
