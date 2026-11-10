# QIAOMI AI v0.2.0 文件交付

本仓库用于交付已生成的 QIAOMI AI v0.2.0 源码 ZIP。

[下载源码 ZIP](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/raw/refs/heads/delivery/v0.2.0/QIAOMI-AI-v0.2.0-source.zip)

[查看交付分支](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.2.0)

ZIP 基于 v0.1.1 升级，保留桌宠、管家、聊天记录和长期记忆；增加本机 Ollama / qwen3:8b 检测、中文多轮、流式输出与取消。

Windows 11：先退出旧版并备份 `%LOCALAPPDATA%\QIAOMI AI`，解压源码 ZIP，确认 Ollama 中已安装 `qwen3:8b`，双击 `start.bat`。
详细说明见压缩包内 `docs/UPGRADE_V0.2.0.md`。

146 项自动化测试及启动自检已通过；真实 Windows、RTX 4070 Ti、Qwen3 推理仍需本机验证。此包为源码，不包含 Windows EXE。
