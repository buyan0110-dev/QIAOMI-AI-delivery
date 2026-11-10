# v0.3.1 文件修改清单

对比基线为已交付 v0.3.0 ZIP。未删除原文件。

## 修改已有文件

- `CHANGELOG.md`：版本说明、操作步骤、变更记录或本版测试报告。
- `QUICKSTART.txt`：版本说明、操作步骤、变更记录或本版测试报告。
- `README.md`：版本说明、操作步骤、变更记录或本版测试报告。
- `TEST_REPORT.md`：版本说明、操作步骤、变更记录或本版测试报告。
- `docs/VOICE.md`：版本说明、操作步骤、变更记录或本版测试报告。
- `qiaomi.spec`：打包声明新增 scipy.signal。
- `qiaomi/__init__.py`：版本号 0.3.1。
- `qiaomi/voice.py`：语音面板、实时诊断、手动控制、状态与请求 ID、日志与超时恢复。
- `qiaomi/voice_worker.py`：统一采集编排、异步停止/取消、本地模型校验及转写错误诊断。
- `requirements-voice.txt`：新增 SciPy，本地重采样依赖。
- `tests/test_pet.py`：将固定短等待改为有界等待定时器状态，不改变动画行为。
- `tests/test_voice_memory.py`：适配两项旧采集/缓存回归测试的新内部 API。

## 新增文件

- `docs/README_V0.3.0.md`：说明、历史快照、测试证据或验收文档。
- `docs/ROOT_CAUSE_V0.3.1.md`：说明、历史快照、测试证据或验收文档。
- `docs/VOICE_V0.3.0.md`：说明、历史快照、测试证据或验收文档。
- `docs/WINDOWS_ACCEPTANCE_V0.3.1.md`：说明、历史快照、测试证据或验收文档。
- `docs/validation/TEST_REPORT-v0.3.0.md`：说明、历史快照、测试证据或验收文档。
- `docs/validation/startup-v0.3.1.json`：说明、历史快照、测试证据或验收文档。
- `docs/validation/tests-v0.3.1.xml`：说明、历史快照、测试证据或验收文档。
- `docs/validation/voice-panel-v0.3.1-linux.png`：说明、历史快照、测试证据或验收文档。
- `qiaomi/audio_capture.py`：新增：设备核验/格式协商、声道与 RMS、统一录音和抗混叠重采样。
- `qiaomi/voice_logging.py`：新增：单写入者诊断转送、安全轮转与写入失败处理。
- `tests/test_audio_capture.py`：新增采集/设备/信号转换/释放测试。
- `tests/test_voice_diagnostics.py`：新增诊断、日志、Qt 状态与真实子进程 IPC 测试。

本清单与 source-delta-v0.3.1.json 为本次新增的交付清单文件。

## 明确保持不变

qiaomi/app.py、qiaomi/storage.py、qiaomi/config.py、qiaomi/ui/pet.py、qiaomi/ui/assistant.py、start.bat、start.vbs、主依赖 requirements.txt 及旧配置加载方式均保持原内容。无 SQLite 迁移。
