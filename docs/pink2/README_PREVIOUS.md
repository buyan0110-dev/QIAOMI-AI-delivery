# QIAOMI AI v0.5.0-pink.1 — 粉色管家整合候选

新增粉色默认主题、管家首页与主窗口内“照顾敲咪 / 洗澡澡 / 喂饭饭”。保留浅色/深色、对话、长期记忆、语音、桌宠互动及游戏深眠。

手动洗澡有女性手部拿海绵跟随页面鼠标，自动洗不显示人手；新增脱睡衣、泡泡、冲洗、浴巾和完整穿回睡衣关键帧。新增穿衣/喂食图集的胸饰为红白宝可梦球。喂食支持三次手动喂一口、自动与一键。全流程共用原生活状态机，暂停/继续/取消/完成可用。

[实际实现、安装与未完成项](docs/pink/IMPLEMENTATION.zh-CN.md) · [测试与Windows验收](docs/pink/TEST_REPORT.zh-CN.md) · [实际首页](docs/pink/previews/home.png) · [实际洗澡页](docs/pink/previews/bath.png) · [实际喂食页](docs/pink/previews/feed.png)

完整穿衣最后四帧和动画预览在docs/pink/previews。以上为Linux实际Qt运行抓图，不是Windows实机。当前没有已构建EXE；Windows构建脚本保留。首次start.bat，日常start.vbs或新快捷方式，旧托盘先完全退出。

**范围说明：** 大ZIP附件读取受32MiB工具限制，仍待独立完整需求书核对。本轮为关键帧＋程序效果，不是完整3D动画；原252张旧WebP中历史胸饰仍未全套统一，原美术待审项没有虚报完成。六个新美术资源加入，全部257个旧资源原样保留。
