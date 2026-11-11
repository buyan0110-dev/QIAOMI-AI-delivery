# v0.4.1 安装与启动

1. 从旧托盘“退出敲咪”，备份默认 %LOCALAPPDATA%\QIAOMI AI（或既有QIAOMI_DATA_DIR/--data-dir），保留模型/自定义美术。
2. 完整ZIP右键全部解压到新目录，进入内层QIAOMI-AI。不要在ZIP预览中运行，不要覆盖正在使用的目录。
3. Windows11 x64/Python3.12：start.bat准备基础环境，install_voice.bat准备语音；不要跨目录移动旧.venv。
4. 日常双击start.vbs，或install_shortcut.vbs创建“敲咪”快捷方式。start.bat是带控制台调试入口。当前没有已生成EXE；Windows构建按WINDOWS_BUILD.md。
5. 保持原用户目录和完整small模型绝对路径、CPU int8、原HyperX WASAPI设备配置；Ollama/Qwen/Whisper模型不在ZIP内。
6. 启动显示猫/托盘；聊天X隐藏，托盘退出才结束。只明确“🐾唤醒敲咪”能离开跨重启深眠。
7. 设置→外观切主题/字体/欢迎语；托盘桌面设置切吸附，性格设置切主动寻找/日常/梦话等。拖离边缘解除吸附。
8. 右键“敲咪的日常生活”或性格设置可手动预览；正常鼠标互动可中断自主活动。四次安抚至少相隔0.65秒，聊天/拖动不冒充摸摸。
9. 原SQLite无迁移，config/voice不替换，新增appearance.json；原累计时间与安抚进度保留。旧自定义形象不会被强制覆盖，主动恢复内置后才用新素材。
10. 真实完成/部分/缺失见FEATURE_STATUS.md与MISSING_ASSETS.md；Windows硬件验收按WINDOWS_TEST_STEPS.md。所有完整源码/旧文档/脚本都在ZIP里。

若源码旁仍有旧dist/EXE，启动器可能优先找到旧EXE；请重新构建或移走旧构建并重建快捷方式。升级不能把旧EXE当成自动更新。
