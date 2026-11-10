# QIAOMI AI v0.3.0 — Windows 智能语音管家

在上传的 v0.2.0 源码基础上整合升级，保留 PySide6 Jarvis 界面、程序绘制桌宠、原有互动、聊天历史、Ollama 流式中文回复、记忆管理、导入导出、托盘、单实例和可取消请求。原用户数据库不会被交付包替换；长期记忆仅在明确确认后新增或修改。

**交付状态：源码与自动化测试可用；Windows 11 真机、RTX 4070 Ti、实际中文语音和唤醒可靠性尚未验收。没有提供伪造的 EXE。** 实验唤醒是本地转写匹配，不是专用 KWS。详见 [测试报告](TEST_REPORT.md)。

## Windows 11 快速开始

1. 从旧程序托盘完全退出。建议先备份 `%LOCALAPPDATA%\QIAOMI AI`；若使用 `QIAOMI_DATA_DIR`，备份该目录。新版使用相同数据路径。
2. 将完整源码 ZIP 解压到可写目录。保留系统现有 Python 3.12 64 位和 Ollama，无需重新下载 Qwen3。
3. 首次运行 `start.bat`，安装/更新项目内 `.venv` 基础依赖。此入口保留控制台用于安装和调试。
4. 以后双击 **`start.vbs`**：WScript 以隐藏方式运行 `.venv\Scripts\pythonw.exe`，正常运行不经过 CMD。它不会静默安装依赖；未准备好时会提示先运行 `start.bat`。
5. 双击 **`install_shortcut.vbs`** 创建桌面快捷方式。快捷方式指向项目内启动器，移动文件夹后需要重建。若系统移除了可选 VBScript 功能，可手工创建指向 `.venv\Scripts\pythonw.exe` 的快捷方式，参数为 `"项目绝对路径\scripts\gui_entry.pyw"`，起始位置为项目目录。
6. 桌宠双击打开管家；关闭管家只收起到托盘，托盘可恢复桌宠/管家。**托盘「退出 QIAOMI AI」才完全退出**。无托盘环境会保留桌宠，避免程序失联。

可直接运行 `.venv\Scripts\pythonw.exe scripts\gui_entry.pyw`。导入失败也会显示对话框并写入 `logs/startup.log`；运行日志为数据目录的 `logs/qiaomi.log`，轮转限制大小，记录错误类型和语音耗时，不记录录音、聊天内容或密钥。单实例锁沿用 Qt `QLockFile`。

## 本地 AI

Ollama 地址固定为 `http://127.0.0.1:11434`，本地请求不使用环境代理。默认模型 `qwen3:8b`，默认提供者 Ollama。打开 Ollama 或运行 `ollama serve`，用 `ollama list` 确认模型，管家设置页点击重新检测；没有安装时才主动执行 `ollama pull qwen3:8b`。

Qwen3 生成在后台 QThread 中运行，流式预览仅在完整成功后提交。语音与记忆解析都只使用本地服务。原 OpenAI 文字对话入口保留，只有用户主动选择/沿用该服务时才使用；语音转写不会发送到该入口。程序不提供实时天气来源，不会把模型猜测当作联网查询结果。

## 自然语言长期记忆

输入「敲咪，记住我最喜欢的选手是 Chovy 和 Doran」。程序先识别明确记忆意图，后台使用本机 Qwen3 生成结构化候选，严格校验字段。候选显示类型、名称、内容和同名替换警告，再问「妈妈，要把这件事保存到长期记忆吗？」。

点击「确认保存」或使用麦克风说「确认保存」后写入 SQLite；点击拒绝、说「不保存」、超时 60 秒、模型异常、取消解析，都不会保存候选。格式有效也可能含模型误解，所以必须核对可见内容；不会声称能自动证明 AI 提取正确。

原命令 `记住：名称=内容` 保留，改用同一非模态确认卡，以支持语音确认。普通聊天不会被自动提取为长期记忆；原聊天历史保存功能仍保留。重复检测针对同名及相同内容（去首尾空白、忽略大小写），不是语义向量去重。同名修改需再次确认。

「长期记忆」页原有查看、修改、指定删除、JSON 导入导出继续使用。新增类型放在附加的 `memory_categories` 表，既有 memories/messages 行、字段及 user_version=1 不变；删除记忆时触发器清除对应类型。原 version=1 导出格式保持 key/value 兼容（类型元数据不进入旧版备份）。

语音设置中的「启用长期记忆命令」可关闭提取、命令保存和对话引用，保留现有数据与管理入口。要让记忆参与后续对话，仍需在原偏好设置中勾选「允许将本地记忆用于 AI 对话」。

## 本地语音

运行 `install_voice.bat` 安装可选的本地语音依赖，再按 [语音模型与声音安装说明](docs/VOICE.md) 下载一次模型并选择目录。基础文字功能不依赖语音包。TTS 使用 Qt 调用 Windows 已安装的中文声音，无付费 API，无模型克隆，不依赖 ChatGPT。

默认不监听，手动点击麦克风才采集；原始音频仅在内存中，不保存文件。CPU int8 为默认，按需加载，空闲卸载；GPU 可选并支持 CPU 回退。语音采集/识别在独立进程，Qt GUI 不执行音频推理；语音子进程只有本机令牌认证控制通道。播报期间暂停麦克风以减少自身误触发。

唤醒默认关闭，每次重启也不恢复持续监听。用户主动启用后才循环采集并匹配「敲咪」转写。唤醒后回应，再听下一句；超时回待机。此方案准确率、噪声表现和待机 CPU 占用均待真机验证，优先推荐手动输入。

语音面板可选设备、调灵敏度、静音、取消/打断、开关 TTS、选声音、调音量和语速。语音输入结果可见，自动发往本地对话。取消同时停止识别、播报及 AI 请求；程序完全退出会停止语音并释放子进程和数据库。

桌宠沿用原绘制风格，补充唤醒标记、说话嘴部开合和错误提示；待机、抬头聆听与思考沿用原动画。状态枚举与 SpriteLibrary 保留后续美术替换接口，不声称具备完整新动作素材。

## Windows EXE 打包

在 Windows 11 x64 / Python 3.12 中运行 `build_windows.bat`。脚本安装 PyInstaller 和语音依赖，再用 `qiaomi.spec` 构建 `dist/QIAOMI-AI/QIAOMI-AI.exe`；`console=False`，使用 GUI 模式。分发时带上整个 onedir 文件夹或生成的 Windows ZIP，不可只拷贝 EXE。保留原 Windows CI，可在自己的仓库主动运行。

Ollama、Qwen3、Whisper 模型、私人数据都不包含在 EXE。中文系统声音由目标 Windows 提供。没有在本次 Linux 环境中生成或验证 Windows EXE；脚本与 CI 不是已执行成功的证据。

## 开发验证

```bash
python -m venv .venv
# Windows 使用 .venv/Scripts/python.exe；Linux 使用 .venv/bin/python
python -m pip install -r requirements-dev.txt
python -m pytest -q
python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.3.0.json
```

Linux 无显示服务时设置 `QT_QPA_PLATFORM=offscreen`。语音开发环境在 Linux 另需 PortAudio；本次环境未安装该系统库，因此设备枚举真实验证的是错误提示分支。运行模型和硬件测试需另行安装与配置，不能用模拟结果替代。

[v0.2.0 原说明（历史）](docs/README_V0.2.0.md) · [升级说明](docs/UPGRADE_V0.3.0.md) · [Windows 验收清单](docs/WINDOWS_ACCEPTANCE_V0.3.0.md)
