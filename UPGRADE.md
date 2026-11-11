# v0.4.0完善版 → v0.4.1

1. 从托盘完全退出旧版，备份原用户目录（默认 `%LOCALAPPDATA%\QIAOMI AI`，或已有 QIAOMI_DATA_DIR/--data-dir）。保留模型与旧自定义形象文件。
2. 新源码解压到新目录；不要覆盖正在使用的文件。原模型可沿用绝对路径，旧.venv不要直接移动，重新准备环境/快捷方式。
3. 原 qiaomi.db/config.json/voice.json 不迁移、不重置。storage/audio_capture/voice_worker/ollama字节不变，无SQL迁移。
4. appearance.json 是新增外观偏好：theme=dark、scale=100、welcome=true；损坏文件在保存前另存 appearance.invalid-随机值.json。desktop.json 新增 edge=null、snap_enabled=true、screen_name=''；personality.json新增seek_enabled=true。旧字段与未知字段保留。
5. 原冷落累计秒数/生气/安抚次数保留，不从聊天历史推断最后摸摸时间。v0.4.1运行期间只由有效鼠标触摸重置；想重新计时可由用户主动关闭再打开冷落。
6. 游戏深眠仍跨重启保留，只有“🐾 唤醒敲咪”恢复；重逢后重置计时，不重开持续麦克风监听。
7. 旧自定义形象优先保留；缺少新动作会提示。主动选择恢复内置后才使用新四边/身体/日常素材，勿删除仍引用的旧资源。
8. 源码start.vbs/pythonw与旧版EXE是不同入口。旧dist/EXE不会自动升级，需Windows重新build_windows.bat再重建快捷方式。

新ZIP不含数据库、私人配置、录音、模型、密钥、虚拟环境。Windows EXE尚未构建；先按WINDOWS_ACCEPTANCE_V0.4.1.md完成真机验收。
