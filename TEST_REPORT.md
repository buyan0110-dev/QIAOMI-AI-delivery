# QIAOMI AI v0.3.1 测试报告

日期：2026-11-11（Asia/Shanghai）。

## 结果

**224 项自动化测试通过，0 失败、0 错误、0 跳过；Qt 离屏启动自检通过；pip check 通过。** 最终全量测试耗时约 10.60 秒。这些均是 Linux 自动化/模拟结果；**Windows 11 + HyperX QuadCast S 真机未执行，真实中文模型识别质量未验证**。

环境：Linux、Python 3.12.14、PySide6/Qt 6.8.3、NumPy 2.5.4、SciPy 1.18.1。语音 Python 依赖可安装，实际设备环境缺少 PortAudio 系统库、HyperX 麦克风与 Whisper 模型。没有使用、上传或保存用户原始音频。

## 证据与复现

```bash
python -m pip install -r requirements-dev.txt
QT_QPA_PLATFORM=offscreen python -m pytest -q --junitxml=docs/validation/tests-v0.3.1.xml
QT_QPA_PLATFORM=offscreen python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.3.1.json
python -m pip check
```

Windows PowerShell 设置离屏变量可用 `$env:QT_QPA_PLATFORM='offscreen'`；这仍属于自动化而非真实桌面/麦克风验证。真实录音手测不应使用 offscreen。

- `docs/validation/tests-v0.3.1.xml`：224 项最终结果。
- `docs/validation/startup-v0.3.1.json`：实际 QApplication、桌宠/管家渲染、临时 SQLite、自检退出。
- `docs/validation/source-delta-v0.3.1.json`：与已交付 v0.3.0 ZIP 的源文件比较。
- `docs/validation/voice-panel-v0.3.1-linux.png`：Linux 离屏初始语音面板，未连接任何真实设备，不是 HyperX 验证截图。

原 v0.3.0 的 169 项回归测试全部保留。两项旧采集/缓存测试适配新内部 API，验证意图不变；原宠物 10 ms 定时器测试曾因固定等待 30 ms 出现调度偶发失败，改为最多 1 秒等待实际状态，不改产品动画或期望。新增 55 项采集、状态、IPC 与诊断测试。

## 用户要求覆盖

| 项目 | 自动化实际覆盖 | 真机状态 |
|---|---|---|
| 设备枚举 | 模拟设备列表排除输出，返回真实字段路径；真实子进程设备错误分支 | 未验证 HyperX 枚举 |
| 设备 ID 失效 | 名称+接口重定位、输出/消失/非法/歧义 ID 拒绝，不静默换输入 | 热插拔待测 |
| 类型/声道 | int16、uint8、float64 → float32；单声道/右声道/反相双声道；44.1k/48k/16k 重采样 | 设备实际格式待测 |
| RMS | 已知幅值计算、浮点累加、峰值、非有限值/空数组拒绝 | 实际输入幅度待测 |
| VAD | 同单位阈值边界、开始/0.9 秒结束、无语音超时；手动绕过两个门控 | 实际底噪阈值待测 |
| 手动开始停止 | 真实 Qt 按钮、真实 QProcess/认证 socket，测试进程内注入模拟设备/模型 | 实际录音待测 |
| 无声结束 | 手动静音返回实际帧，全零送 ASR 前报错，自动无声不加载模型 | 实际安静环境待测 |
| 模型加载失败 | 必需文件缺失、模拟 CPU 初始化失败、CUDA OOM 回退并复用 CPU | 真实模型加载待测 |
| 转写失败 | 包括惰性 segment 迭代异常，空结果提示，完整中文片段拼接 | 中文准确率待测 |
| 状态重置 | 异常/关闭/停止后进程崩溃/看门狗/取消超时恢复；保留具体终态错误 | Windows 驱动挂起待测 |
| 设备释放 | 正常/取消/读取异常/NaN/start 失败显式关闭；关闭失败致命路径 | 实际端点占用待测 |
| 多次操作 | 五轮开始/结束、重复点击、结束前取消、旧 request ID 丢弃 | 高频真实操作待测 |
| UI 同步 | 实际控件显示 RMS/阈值/电平/帧数/时长，按钮随状态变化，过期转写不入聊天 | Windows DPI/音量表现待测 |
| 日志异常 | 轮转数有界、创建/写入失败不抛出、动态提示、完整堆栈而不写成功转写文本 | 实际文件权限待测 |
| 三秒自检 | 模拟录制恰好三秒，不加载/调用 ASR；展示运行时采集参数 | 实际自检待测 |
| 旧功能 | 原桌宠/界面/聊天/本地请求/记忆 CRUD 与导入导出/托盘逻辑回归 | 真机回归待测 |

真实工作进程测试只验证协议和状态链路：设备与模型通过 **测试文件** 注入替身，产品代码没有虚假音频或模拟成功开关，不能把此测试称为真实 Whisper 中文识别通过。

## 数据与代码边界

经逐文件比较，qiaomi/app.py、storage.py、config.py、ui/pet.py、ui/assistant.py、start.bat 与 v0.3.0 完全一致。没有数据库结构变化，不需要迁移，未访问任何用户真实数据库或个人配置。配置新增字段在 voice.json 中向后兼容，旧字段值保留。

## 未验证事项

Windows 原生音频接口协商、HyperX 实际声道/采样率/信号、真实 small 模型输出和延迟、游戏同时运行的 CPU/RAM、Windows 设备占用与热插拔、打包 EXE 均未实测。本次没有重新验证本地 Qwen3 的真实生成，也没有提高实验唤醒的已验证等级。

确认的代码缺陷与现场待证假设见 `docs/ROOT_CAUSE_V0.3.1.md`；真机流程见 `docs/WINDOWS_ACCEPTANCE_V0.3.1.md`。不可因为模拟通过就写“Windows 语音已修好并验收”。
