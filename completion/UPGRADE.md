# v0.3.x → v0.4.0 安全升级

1. 从托盘完全退出旧版，备份 `%LOCALAPPDATA%\QIAOMI AI` 或既有 QIAOMI_DATA_DIR，并保留旧项目的 models/与自定义美术。
2. 将完整源码 ZIP 解压到新的可写目录。不要覆盖正在使用的目录或删除旧数据。虚拟环境不宜直接跨目录复制；用 start.bat 准备 Python 3.12 依赖，语音依赖用 install_voice.bat。
3. 使用原用户数据目录启动。默认目录不变；若曾使用 QIAOMI_DATA_DIR/--data-dir，继续设置同一路径。原数据库、config.json、voice.json、desktop.json 不迁移、不重置。新增 personality.json 只保存性格/造型/休眠状态，不包含聊天或记忆。
4. 模型仍使用原 faster-whisper-small 的本地绝对路径，CPU int8，Ollama/Qwen 不打包。模型安装和设备设置详见 VOICE.md；WASAPI 采集逻辑保留。
5. 普通 GUI 入口 start.vbs 或 install_shortcut.vbs 创建的“敲咪”；start.bat 保留调试控制台。旧 dist 中的 EXE 不会自动变成新版本，必须重新 Windows 构建并重建快捷方式。
6. 托盘“性格与形象”配置互动。旧自定义形象继续优先保留；要看新粉色睡衣形象，请在桌面设置主动选择恢复内置形象，勿删除原美术目录。
7. 游戏深度休眠跨重启保留；必须明确点“唤醒敲咪”恢复。工作/游戏眼镜造型只是外观，不代表进入休眠。

SQLite schema 未改，不需要 SQL 迁移。损坏 personality.json 在下次保存前另存 personality.invalid-随机值.json；不覆盖记忆数据库。

源码 ZIP 不含虚拟环境、录音、下载模型、用户数据库、API Key 或私人配置。Windows EXE 在本环境未构建；构建步骤见 WINDOWS_RELEASE.md。

## 本次完善版升级

使用新的 QIAOMI-AI-v0.4.0-complete-source.zip，原 v0.4.0 ZIP 保留。仍先完全退出、备份数据、解压新目录并重建环境/快捷方式。personality.json 新字段有默认值，未知字段保留；新增运行快照不影响任何长期记忆。不应将旧 EXE 当成本次源码自动更新。七项日常素材在 assets/personality，与原资源一同被现有 PyInstaller spec 收集。
