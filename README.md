# QIAOMI AI v0.3.1 — Windows 语音修复与诊断交付

[打开 v0.3.1 源码 ZIP 文件页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/QIAOMI-AI-v0.3.1-source.zip)

建议在 Edge/Chrome 打开文件页，点击右上角 ↓ Download raw file 下载。避免在聊天内置浏览器直接打开 ZIP。

[安装/升级说明](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/INSTALL.md) · [语音操作](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/VOICE.md) · [根因分析](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/ROOT_CAUSE.md) · [文件变更清单](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/FILES_CHANGED.md) · [测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/TEST_REPORT.md) · [Windows 手测步骤](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/WINDOWS_TEST_STEPS.md) · [更新日志](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/CHANGELOG.md)

本版本基于 v0.3.0 增量修复，优先解决采集门控和诊断缺失：

- 默认手动录音：开始说话 → 实时音量/时长 → 结束并识别；不经过能量阈值或 Silero 门控。
- 三秒麦克风自检不加载模型；诊断显示真实设备、ID/接口、采样率、声道、RMS/峰值/阈值、时长和帧数。
- 原生格式采集，按整段能量选较强声道，再抗混叠重采样到 16 kHz float32；防止错误声道或反相平均抵消。
- 设备身份核验、请求 ID、重复点击保护、取消/超时恢复、模型错误和空结果提示。
- 单写入者轮转 voice.log，完整异常堆栈，不记录转写、录音或密钥。

旧版已确认有“未超过阈值就丢弃整段音频”的分支；这不证明 HyperX 现场的唯一根因。实际设备映射、信号幅度与中文识别质量仍需真机诊断。

## 升级后先做这三步

1. 完全退出旧版并备份用户数据目录；解压完整源码，执行 start.bat 与 install_voice.bat（新增 SciPy 依赖）。不要删除记忆数据库或个人配置。
2. 刷新设备、重新选择 HyperX QuadCast S，先运行三秒自检；选择原有完整 small 模型，保持 CPU int8。
3. 默认手动录音，讲话后点“结束并识别”。错误时查看诊断与“打开语音日志”。

**224 项自动化测试、Linux Qt 离屏启动自检和 pip check 通过；Windows 11 + HyperX QuadCast S、真实 Whisper 中文质量与游戏并行性能未实测。未提供 Windows EXE。** 没有数据库结构变化；桌宠、聊天、长期记忆、主配置和 start.bat 保持原实现。实验唤醒仍默认关闭，未升级为专用 KWS。

ZIP SHA-256：

```text
c7612457eefd09b2005a8d63cd5faed540c2966dec232fe3a47a26a621bab543
```

[校验文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.1/QIAOMI-AI-v0.3.1-source.zip.sha256) · [v0.3.0 原交付](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.0) · [v0.2.0 原交付](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.2.0)
