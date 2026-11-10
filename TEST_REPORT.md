# QIAOMI AI v0.3.0 测试报告

测试日期：2026-11-10（Asia/Shanghai）。

## 结论与环境

**169 项自动化测试通过；Linux Qt 离屏启动自检通过。Windows 11 真机测试未执行，Windows EXE 未生成。**

环境：Linux 6.18.57、Python 3.12.14、PySide6/Qt 6.8.3；无用户的 RTX 4070 Ti、Ollama/Qwen3、麦克风、Windows SAPI/WinRT 中文声音或真实 Whisper 模型。安装了语音 Python 依赖，`pip check` 通过；Linux 缺少 PortAudio 系统库，真实设备枚举测试因此验证的是错误提示分支，不是成功录音。

原 v0.2.0 的 146 项测试保留并通过。固定命令确认测试按新增非模态确认卡调整；完成动画期望改为待机；绘制数量从 10 更新为 13。新增 23 项（包含参数化案例），没有删除原测试以隐藏失败。

## 自动化证据

运行：

```bash
QT_QPA_PLATFORM=offscreen python -m pytest -q --junitxml=docs/validation/tests-v0.3.0.xml
QT_QPA_PLATFORM=offscreen python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.3.0.json
python -m pip check
```

证据：`docs/validation/tests-v0.3.0.xml`、`docs/validation/startup-v0.3.0.json`、`docs/validation/source-delta-v0.3.0.json`。历史 v0.1.1/v0.2.0 报告仅供溯源，不是本次 Windows 测试结果。

## 验收逐项区分

| 用户验收项 | 自动化 / 模拟结果 | Windows 11 真机 |
|---|---|---|
| 无控制台启动 | VBS/pythonw 路径与 EXE console=False 静态检查通过 | 未测，不能证明实际无窗口闪现 |
| 桌面宠物 | Qt 离屏创建、原互动回归、13 种状态渲染通过 | 未测 |
| 管家界面 | Qt 离屏打开、关闭/恢复、屏幕边界、输入回归通过 | 未测 |
| Ollama 连接 | 模拟 HTTP 传输、探测、超时/异常处理通过 | 无实际 Ollama，未测 |
| Qwen3 中文对话 | 模拟中文流式文本、提交与取消通过 | 无模型，未验证生成质量 |
| 自然语言记忆 | 意图门控、本地结构化请求、严格 JSON 校验、模拟候选通过 | 实际模型提取准确率未测 |
| 保存确认 | 按钮/文字/模拟语音信号、拒绝/超时/开关、不写库约束通过 | 实际语音确认未测 |
| 记忆修改删除 | 真实临时 SQLite CRUD、旧数据兼容、类型存储和 JSON 导入导出通过 | 原用户数据库未访问/改动 |
| 中文语音识别 | 模拟音频流结束、中文语言参数、VAD、取消、真实子进程 IPC 通过 | 无真实录音或模型推理 |
| 中文语音合成 | 模拟 TTS 音量/语速/播放/结束/停止编排通过 | Windows 发音质量、声音枚举未测 |
| 「敲咪」唤醒 | 转写匹配和唤醒→回应→下一句→超时状态机模拟通过 | 成功率、误报率和延迟未测；非专用 KWS |
| 麦克风静音 | 默认不监听、禁止静音录入、丢弃迟到文本通过 | 硬件占用/权限未测 |
| 语音打断 | 模拟 TTS 停止、识别结果失效与 AI 请求取消通过 | 扬声器与麦克风实测未测 |
| 托盘后台 | 原逻辑、无托盘兜底、关闭窗口与退出分离通过 | Windows 托盘实际交互未测 |
| 正常退出 | 真实子进程停止、QThread 请求结束、SQLite 关闭、离屏启动退出通过 | 设备/驱动释放未测 |
| 原功能回归 | 原 146 项测试保留并通过（对新交互调整预期） | 未测 |

模拟 GPU 加载 OOM 后 CPU 回退并复用模型的测试通过；这不是 RTX 真正显存耗尽测试。能量结束检测测试使用合成数值与模拟输入流，未使用私人音频。中文转写匹配单元测试不能当作声学唤醒率。

## 已知限制

- 实验唤醒为分段 Whisper 转写匹配，有间隙、延迟和罕见名称误识别问题；不应作为已可靠完成的专用唤醒方案。默认关闭，手动输入可用。
- ASR 默认 CPU int8，CUDA 可选。未测得目标 CPU 延迟、RAM/VRAM 峰值或后台 CPU 基准；日志记录推理/采集耗时以便真机评估。
- TTS 依赖目标 Windows 安装且 Qt 可见的中文声音。文字完成后开始播报，不提供逐词对齐。
- 提取严格校验只保证结构合法，不能证明 AI 语义正确；可见候选和明确确认是写入前置条件。重复检测为名称/内容规范化比较，不是语义去重。
- 无 Windows 构建环境，EXE 和更新的 Windows CI 均未执行。打包脚本存在不等于打包成功。
- 没有自动化天气联网工具，不会伪造天气查询能力。

真机流程见 `docs/WINDOWS_ACCEPTANCE_V0.3.0.md`，需要逐项填写实际结果后才能称为 Windows 验收通过。
