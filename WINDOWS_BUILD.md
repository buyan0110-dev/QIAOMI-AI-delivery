# v0.4.1 Windows GUI 构建与分发

当前 Linux 环境未生成 Windows EXE。以下脚本与路径经过静态/自动化检查，不能当作 Windows 编译、插件加载或无黑窗目测已通过。

## 在 Windows 构建

1. 准备 Windows 11 x64 和 Python 3.12 x64，项目解压至可写目录。
2. 双击 build_windows.bat。准备依赖/调试构建时出现终端属于开发流程。
3. 脚本先调用 start.bat --prepare-only，再安装 requirements-build.txt 与 requirements-voice.txt，执行 pip check。
4. scripts/make_icon.py 将当前粉色睡衣橘猫图标导出为含 16/32/48/256 像素图像的 ICO。
5. PyInstaller 使用 qiaomi.spec：onedir、console=False、嵌入橘猫图标，包含 Qt、语音 DLL/包与 Whisper 自带 Silero 资源，不包含用户 Whisper/Qwen 权重或 Ollama。
6. 完整分发目录为 dist/QIAOMI-AI，入口 QIAOMI-AI.exe。脚本加入 install_shortcut.vbs 与本指南，再用 scripts/build_release.py 验证完整目录、生成 ZIP 和 SHA-256。
7. 将整个 ZIP 解压至新目录，先完成下面真机验收再向用户称为“可直接运行版”。不要只发单个 EXE。

原 Windows CI 同步保留测试与 windowed 构建配置；本次没有触发或取得它的运行成功证据。

## 普通用户

双击 GUI EXE 或运行同目录 install_shortcut.vbs 创建“敲咪”桌面快捷方式。脚本以 GUI 方式执行，不调用 PowerShell/CMD。若 Windows 未安装可选 VBScript，可在资源管理器对 EXE 手动创建桌面快捷方式，无需另装脚本引擎。

源码备用入口为 pythonw.exe + scripts/gui_entry.pyw，start.vbs 不会静默安装缺失的 Python 或依赖；首次准备使用 start.bat。手工源代码快捷方式的目标为项目 .venv/Scripts/pythonw.exe，参数为 GUI 脚本绝对路径。普通使用不要指向 start.bat。

## 后台语音进程

源码模式下由已存在的同一虚拟环境 pythonw.exe 执行 -m qiaomi.voice_worker；打包模式使用同一 windowed EXE 的 --voice-worker 分支。该分支不创建 QApplication/主界面，不依赖 Python 标准输入输出，仍沿用经认证本机 socket。没有借助 cmd、start、PowerShell 或外部 ffmpeg 控制台。

## 持久数据

默认 %LOCALAPPDATA%\QIAOMI AI；继续支持 QIAOMI_DATA_DIR。数据库、config.json、voice.json、desktop.json、日志不进入临时 _MEIPASS。自启动 Run 命令固定 --data-dir，登录后读取同一数据库。

外部模型与自定义图像清单用用户配置路径，不从临时打包目录下载或生成。移动/删除旧目录前，确认配置不再引用旧模型/图像。源代码中的 assets 是内置界面资源，不是用户数据目录。构建时不要手工向分发目录加入私人数据库、日志、密钥或模型。

## 自启动与更新

设置只写当前用户 HKCU Run 的 QIAOMI AI 值，取消时只删除这个值。默认关闭，无服务或管理员权限。Windows 任务管理器/安全策略可额外禁止登录启动，应在真机检查。程序移动后，自启动界面会提示旧目录；取消再启用以更新路径。

使用独立新目录升级，完全退出旧进程，重建桌面快捷方式。旧版与新版共享锁/数据库路径，但旧版不支持激活协议；先从旧托盘退出。数据库无需迁移，长期记忆不会由新源码包覆盖。

## 启动排查

启动异常看数据目录 logs/startup.log、startup-fault.log 和 qiaomi.log。普通日志轮转；故障栈日志启动时超限换为 .old。日志不包含聊天内容或密钥。启动导入失败尽可能使用 Windows MessageBox 显示提示，原生 Qt/运行库错误可能在主循环前中止，需根据故障栈定位。

## Windows 真机待验收

无短暂黑窗、桌面快捷方式/登录启动、Qt 托盘/Explorer 重启、焦点激活、音频工作进程不弹窗、子进程正常终止、跨重启记忆、游戏占用与 DPI 坐标等，均需填写 WINDOWS_ACCEPTANCE_V0.3.2.md。Linux 离屏与模拟注册表不能替代它们。EXE 未签名；本次不声称已有签名、安装包或升级服务。

新增 assets/personality 清单与全部 WebP 通过 spec 的 assets 目录整体打包；独立 personality.json 仅在用户数据目录生成，不打包私人设置。模型与数据库继续排除。

本版新增appearance/body/habitat模块由collect_submodules(qiaomi)收集；assets整体包含252张WebP、原ICO和头像。无需新增大型依赖；本地语音/LLM权重仍排除。需在Windows验证Qt WebP插件、DPI及全屏/安全桌面API，不能将Linux源码测试当成EXE验证。
