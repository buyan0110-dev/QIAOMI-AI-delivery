# Windows CI 与 EXE 实际交付证据

这是 **WindowsServer2025 / Python3.12 / Qt offscreen** 自动化结果，不是用户的 Windows11+HyperX+4070Ti 真实桌面/游戏验收。

- [完整 CI 运行](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/actions/runs/43609208848)：成功。
- 完整 pytest：**685 passed / 287.17秒**，0失败、0错误、0跳过；原始 `windows-full.xml`。
- PyInstaller `console=False` 实际构建成功；完整便携 ZIP 为209800069字节（约200MiB）。
- 实际运行打包 EXE 的离线自检：**91项检查通过**，`passed=true`，原始 `windows-frozen-smoke.json`。
- 下载便携包后二次检查：CRC正常、SHA256匹配、AMD64、PE子系统 **2 / Windows GUI**；264个运行资源与原项目逐文件一致，无用户数据库/语音配置/日志，见 `windows-binary-check.json`。
- [候选版发布页与下载](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/releases/tag/v0.6.0-world-candidate.2)。必须完整解压，运行 `QIAOMI-AI/QIAOMI-AI.exe`，不要单独复制EXE。

首轮 Windows CI 为675通过/6失败；真实布局与路径问题已修复，第二轮先跑旧失败项与新增门禁，再跑全部685项，没有跳过失败测试。首轮日志另存 `windows-first-failed.txt`。

## 构建可追溯性

构建代码提交 `b9b9498`，输入源码ZIP SHA256：

`231ffc332b0c9adf298b163ac5095cf5b285742ac7424e3f3e1d1087a30bab4d`

构建输入保留在该 Git 提交中。构建完成后，交付源码 ZIP 仅补录本页、Windows证据和说明；所有运行代码、脚本、测试、requirements、构建配置及 assets 均与 CI 输入逐字节一致，详见 `source-runtime-agreement.json`。交付 ZIP 新哈希见仓库 `WORLD-SHA256SUMS.txt`。

便携版 SHA256：

`c15f6aea705cd106b182613cfe7b1b1ff67cede59297c26e0fe353b17f14248f`

## 仍待实机

无瞬时控制台闪烁、Explorer托盘/自启、物理多屏与DPI、真实麦克风/Whisper/TTS/Ollama、Windows11下APEX/幻兽帕鲁资源占用，需要按 `WINDOWS_ACCEPTANCE.zh-CN.md` 实测。新增精绘动作/家具/插画仍为明确轻量占位。本候选版不宣称全部美术和硬件验收完成。
