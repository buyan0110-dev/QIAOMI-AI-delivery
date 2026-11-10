# QIAOMI AI v0.3.2 — Windows 桌面与托盘升级

[打开 v0.3.2 完整源码 ZIP 文件页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/QIAOMI-AI-v0.3.2-source.zip)

请用 Edge/Chrome 打开文件页，再点击右上角 ↓ Download raw file。当前交付为完整源码与 Windows 构建脚本，**没有已构建的 Windows EXE**。

[安装与使用](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/INSTALL.md) · [Windows GUI 构建](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/WINDOWS_BUILD.md) · [Windows 验收表](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/WINDOWS_TEST_STEPS.md) · [测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/TEST_REPORT.md) · [变更文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/FILES_CHANGED.md) · [升级边界](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/UPGRADE.md) · [更新日志](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/CHANGELOG.md) · [Linux 测量原始数据](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/PERFORMANCE_LINUX.json)

## 这次升级

- 普通入口优先 windowed GUI EXE；源码备用用 pythonw，不经过 CMD/PowerShell。语音工作进程也使用 GUI 解释器/同一 windowed EXE。start.bat 保留调试。
- 桌面“敲咪”快捷方式与橘猫 ICO；启动只显示宠物/托盘，恢复保存的位置/形象。
- 聊天 X 只隐藏聊天，猫继续运行；托盘可恢复聊天、独立显示隐藏猫、打开语音设置和真正退出。
- 原生 QSystemTrayIcon、Explorer 重启恢复与低频兜底；单实例锁+本地激活管道，重复启动唤回旧窗口。
- 用户级 HKCU Run 自启动，默认关闭，固定原用户数据目录，无服务/管理员权限。
- 手动游戏模式隐藏猫、停止动画/自动唤醒、取消当前任务并卸载自身语音缓存；手动聊天/语音仍可用。
- 有界高 DPI 绘制缓存与降帧。原记忆数据库、主配置、音频采集算法、Ollama 传输与 start.bat 保持原内容，无数据库迁移。

## 如何打开

源码首次执行 start.bat 准备环境，语音另用 install_voice.bat；再运行 install_shortcut.vbs 创建“敲咪”桌面图标，日常使用该图标或 start.vbs。已在 Windows 构建时优先运行完整 dist/QIAOMI-AI 中的 QIAOMI-AI.exe。不要移动现有 .venv，使用新目录升级并重建快捷方式；保留用户数据库、配置、模型与形象文件。

设置页可打开“桌面 / 游戏模式 / 开机自启动”。游戏模式不扫描游戏、不截图、不注入、不装全局键盘钩子；进入游戏前手动开启。退出模式后麦克风唤醒仍关闭。独立 Ollama 服务的模型驻留按其自身策略管理，不承诺游戏显存完全释放。

## 验证范围

**255 项自动化测试、Linux Qt 离屏启动自检、pip check 通过。Windows 11 新版实机、GUI EXE 构建、登录自启动、Explorer 托盘与游戏并行性能未验证。** Windows API 仅模拟，不可等同于实机通过。

约 8 秒 Linux 离屏样本（单核口径、无 AI 权重）：猫咪待机 CPU 1.954% / RSS 92.69 MiB；游戏模式 0.468% / 86.36 MiB；隐藏待机 0.074% / 86.36 MiB。GPU 未测量，不能据此承诺 Windows/游戏零影响。

ZIP SHA-256：

```text
94bb81a9cbb9c32228565bf611cfb982561e5f4635f2972ea4e8312e9f48a528
```

[校验文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.3.2/QIAOMI-AI-v0.3.2-source.zip.sha256) · [v0.3.1](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.1) · [v0.3.0](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.0) · [v0.2.0](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.2.0)
