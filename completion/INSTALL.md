# v0.4.0-completion.1 完善版安装与启动

1. 从旧托盘“退出敲咪”，备份 `%LOCALAPPDATA%\QIAOMI AI`（或既有 QIAOMI_DATA_DIR）及旧项目 models/和自定义素材。
2. 下载完整源码 ZIP，右键“全部解压”到新的可写目录，进入内层 QIAOMI-AI。不要在 ZIP 预览里直接运行，也不要删除旧数据目录。
3. Windows 11 x64 / Python 3.12：双击 start.bat 准备基础环境，语音依赖运行 install_voice.bat；不要跨目录复制 .venv。
4. 源码普通入口为 start.vbs，或运行 install_shortcut.vbs 后双击桌面“敲咪”。调试入口 start.bat 有控制台。若要 EXE，按 WINDOWS_BUILD.md 在 Windows 本机构建，当前包没有已生成 EXE。
5. 保持原数据目录/环境变量/--data-dir，模型选择原 faster-whisper-small 完整绝对路径，CPU int8，HyperX 建议使用此前可用的 Windows WASAPI 设备。Ollama 与 Qwen 模型单独安装，不在源码包中。
6. 启动只显示猫和托盘，双击猫打开聊天，聊天 X 只隐藏窗口，托盘“退出敲咪”才完全结束。
7. 托盘“性格与形象”可调撒娇/重逢/气泡/频率，以及工作/游戏圆形金丝眼镜造型。旧自定义形象继续保留，选择恢复内置形象才切换新粉色睡衣。
8. 游戏深度休眠拦截录音和新推理；只有托盘“唤醒敲咪”恢复并播放一次重逢。重启也保留休眠。猫旁有跳过按钮。醒来不会自动打开主聊天或重开持续麦克风监听。
9. 原 config.json、voice.json、desktop.json、qiaomi.db 保持，新增 personality.json；无数据库迁移。ZIP 不含私人数据、录音、模型、虚拟环境。
10. 真机测试按 WINDOWS_TEST_STEPS.md；美术限制见 ASSETS_STATUS.md。完整 README/历史文档与脚本均在 ZIP 内。

若曾有旧 dist/EXE，启动器可能优先找到它；请重新构建/移走旧构建并重建快捷方式，确认运行版本。移动项目后必须重建虚拟环境和快捷方式。

## 本轮入口

右键猫→敲咪的日常生活，或性格设置手动选动作；冷落10/20/30分钟，生气需相隔至少0.65秒四次有效摸摸。睡觉时3–7分钟梦话，静音。手动普通启动边缘迎接，自启动/深眠不迎接。旧自定义形象若缺素材会明确提示，主动恢复内置才能看新形象。详见FEATURE_STATUS.md。
