# QIAOMI AI v0.3.0 文件交付

[下载 v0.3.0 完整源码 ZIP](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/raw/refs/heads/delivery/v0.3.0/QIAOMI-AI-v0.3.0-source.zip)

[安装与本地 AI 配置](INSTALL.md) · [语音模型与中文声音安装](VOICE.md) · [测试报告](TEST_REPORT.md)

基于原 v0.2.0 整合升级，保留桌宠、Jarvis 管家界面、Ollama/Qwen3、长期记忆与原用户数据路径。新增 pythonw/VBS 无控制台启动、桌面快捷方式、自然语言记忆候选确认、本地语音输入/输出及实验转写唤醒。

Windows 首次执行 start.bat 准备依赖，之后使用 start.vbs；install_shortcut.vbs 创建桌面快捷方式。语音功能另执行 install_voice.bat，按说明安装本地模型和 Windows 中文声音。EXE 打包使用包内 build_windows.bat，Ollama/Qwen3/Whisper 模型不打进 EXE。

**169 项自动化测试与 Linux Qt 离屏启动自检通过。Windows 11 真机、中文音频质量、实际 Qwen3 提取和 RTX 4070 Ti 显存表现未验证；未生成 Windows EXE。**「敲咪」为默认关闭的实验本地转写匹配，不是专用唤醒词检测器，不承诺已验证的唤醒可靠性。

下载后先备份 %LOCALAPPDATA%\\QIAOMI AI，完全退出旧版，再解压完整项目；不要覆盖或删除自己的 qiaomi.db。

ZIP SHA-256：

```text
9e27d0353b5eccbcabc04a222b274e3e86beb581268db0e8e48acef5a046dcd5
```

[校验文件](QIAOMI-AI-v0.3.0-source.zip.sha256) · [保留的 v0.2.0 交付](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.2.0)
