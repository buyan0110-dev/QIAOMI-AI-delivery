# QIAOMI AI v0.3.2 验证报告

日期：2026-11-11（Asia/Shanghai）。

## 结论

**255 项自动化测试通过，0 失败；隔离离屏启动自检通过；pip check 通过。** 最终测试约 16.37 秒。Linux 下已验证真实 Qt 控件、本地进程间激活和进程退出；Windows 注册表、Explorer 广播与前台授权仅用模拟 API 验证。

**Windows GUI EXE 尚未构建，Windows 11 新版实机验收尚未完成。** 用户之前提供的截图证明 v0.3.1 的 QuadCast S / WASAPI / 48k 双声道 / CPU int8 可转写并取得 Ollama 回复；本次没有把那次结果充作 v0.3.2 的无黑窗或系统托盘验证。

环境：Linux 6.18.57、Python 3.12.14、Qt/PySide6 6.8.3，QT_QPA_PLATFORM=offscreen。没有真实 Windows Shell、HyperX、游戏或 NVIDIA GPU 推理测试环境。

## 自动化证据

```bash
QT_QPA_PLATFORM=offscreen python -m pytest -q --junitxml=docs/validation/tests-v0.3.2.xml
QT_QPA_PLATFORM=offscreen python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.3.2.json
python -m pip check
QT_QPA_PLATFORM=offscreen python scripts/measure_idle.py --output docs/validation/performance-v0.3.2-linux.json --seconds 8
```

原 v0.3.1 的 224 项测试保留；对“聊天和猫必须互斥”的旧断言及冒烟检查按新需求改为共存，没有删测试。新增 31 项桌面生命周期测试（含参数化）。语音、记忆、配置及旧交互回归仍在最终结果中。

- tests-v0.3.2.xml：最终 255 项通过。
- startup-v0.3.2.json：实际 QApplication、13 种猫状态、聊天共存、临时 SQLite、干净退出。
- source-delta-v0.3.2.json：与 v0.3.1 交付 ZIP 的文件比对。
- pet-v0.3.2-linux.png / desktop-v0.3.2-linux.png：Linux 离屏截图，不是 Windows 截图。

以上文件均位于 docs/validation。旧版本证据仅为历史记录。

## 验收对应

| 用户要求 | 本次测试实际覆盖 | Windows 11 实机 |
|---|---|---|
| 无黑窗/桌面图标 | GUI spec console=False、ICO 目录、VBS 不含 CMD/PowerShell、pythonw 路径/缺失拒绝、frozen worker 路径、bootstrap 日志 | 未目测，无 EXE |
| 小橘猫启动 | 真实 Qt 渲染、坐标恢复/屏幕夹回、资产失效回退、形象保存与内置选择恢复、默认无大窗口 | 待测多屏/DPI/原生窗口 |
| 原生托盘 | QSystemTrayIcon 菜单/状态、单对象恢复、Trigger 激活；逻辑测试中模拟托盘可用性 | 待测 Windows 托盘显示 |
| 关闭聊天继续运行 | 关闭聊天后猫和托盘仍在，隐藏宠物与聊天独立，无托盘兜底 | 待测实际标题栏/Alt+F4 |
| 托盘恢复 | Qt 窗口恢复逻辑、真实本地激活 pipe；特定 PID 前台授权 API 模拟 | 待测 Windows 焦点策略 |
| 显示/隐藏猫 | 状态与入口保持、游戏下不置顶/无动画、无托盘游戏下不自动覆盖 | 待测游戏画面 |
| 自启动开关 | 模拟 HKCU Run，默认无写入、GUI 命令含固定数据目录、只删本值、其他值保留、缺失路径拒绝、权限失败回滚 UI | 待测真实注册表和登录 |
| 单实例 | 真实 QLockFile + QLocalServer；第二个真实进程 activate/ping；异常命令拒绝；完整 App 再次启动返回旧实例 | 待测 Windows named pipe |
| 托盘退出 | 完整 App 真实退出并释放锁；启动了真实语音工作进程后正常退出，Linux /proc 确认子 PID 不存在 | 待测 Windows 进程/设备 |
| 重启记忆 | 主 App 退出后重新打开同一 SQLite 验证既有记忆，旧配置/语音文件不因游戏模式被写改 | 系统重启待测 |
| 语音不受启动影响 | 原采集/转写/状态/IPC 测试保留，Windows worker GUI 解释器选择模拟，游戏手动录音可用 | 待测 GUI EXE + HyperX/TTS |
| 游戏低活动 | 真实 Qt 停表、隐藏、关闭 wake/follow、取消活动请求、保留手动入口；Linux 实际 CPU/RSS 测量 | 游戏/显存/帧率待测 |
| Explorer 恢复 | 模拟 TaskbarCreated MSG，延迟合并一次恢复，不增加控制器/托盘对象 | Explorer 重启待测 |

完整应用测试中的延时退出仅由测试子类注入；产品没有演示退出/虚假设备开关。原语音测试的设备/模型替身仍明确为模拟，不代表真实中文识别质量。

## 实际资源测量（仅 Linux）

每种状态采样约 8 秒，使用真实进程 CPU time / elapsed time 和 /proc RSS；离屏 Qt 软件绘制，托盘可用性被模拟，无 AI 权重、录音或语音子进程。CPU 百分比以**单个核心为 100%**，不是整机任务管理器总 CPU 百分比。

| 状态 | 实际时长 | CPU（单核口径） | RSS | 宠物动画 / 麦克风 |
|---|---:|---:|---:|---|
| 小猫待机（缓存后） | 7.963 秒 | 1.954% | 92.69 MiB | 动画开 / 麦克风关 |
| 游戏模式 | 8.051 秒 | 0.468% | 86.36 MiB | 动画关 / 麦克风关 |
| 隐藏待机 | 7.940 秒 | 0.074% | 86.36 MiB | 动画关 / 麦克风关 |

缓存前同环境一次 8.179 秒离屏样本的实时向量绘制为 84.504% 单核 CPU / 85.94 MiB，暴露了待机绘制问题；已用降帧与有界完整帧缓存处理。保留 performance-v0.3.2-before-cache-linux.json 作为发现依据。这是短时场景测量，不能推导 Windows 同比例改善、零性能影响、长时间稳定均值或游戏帧率。

测量脚本也提供 Windows GetProcessMemoryInfo 分支，但该分支未在本次环境实跑。GPU/VRAM、真正 Qwen/Whisper 加载后占用、APEX 和幻兽帕鲁并行占用全部未测。Ollama 服务可能自行保留 Qwen 模型，不在此进程 RSS 里。

## 数据与边界

qiaomi/storage.py、config.py、audio_capture.py、memory_intent.py、ollama.py 及 start.bat 与 v0.3.1 逐字节一致。没有数据库迁移，也没有访问用户真实数据。新增 desktop.json 与 HKCU Run（仅用户主动启用）是独立设置。模型、数据库、私人配置/日志不进入源包或默认 EXE 数据路径。

Windows 构建脚本、spec、快捷方式和图标经过路径/语法/结构检查，但 **没有执行 Windows 构建或 CI**。完整待测项目见 docs/WINDOWS_ACCEPTANCE_V0.3.2.md；打包操作见 docs/WINDOWS_RELEASE.md。
