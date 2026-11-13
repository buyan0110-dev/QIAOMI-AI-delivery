# 修改文件清单

相对v0.4.1-costume-tail.2，原文件未删除。完整路径列表见`changed-files.json`。

## 新增运行文件

| 文件 | 作用 |
|---|---|
| qiaomi/upgrade.py | 读取旧数据前一次性配置及SQLite安全备份 |
| qiaomi/life_state.py | 四值、慢变化、边界验证、独立原子持久化 |
| qiaomi/care.py | 单活动协调、优先级、冷却、各生活阶段、暂停恢复 |
| qiaomi/power.py | Windows休眠/恢复通知适配，无轮询 |
| qiaomi/ui/life_panel.py | 数值、喂食、洗澡、玩具、手动流程与开关面板 |
| qiaomi/ui/care_effects.py | 局部程序道具效果，不重画猫咪部件 |

## 修改运行文件

- `qiaomi/app.py`：接入备份/生活协调器/面板/托盘、任务及退出生命周期、电源通知；只有托盘UI可唤醒游戏深眠。
- `qiaomi/personality.py`：生活协调器钩子、中断收尾、捕获反馈；保留原性格、冷落与四次安抚。
- `qiaomi/ui/pet.py`：生活菜单、道具绘制、局部指针与逆变换命中、菜单活动保护。
- `qiaomi/ui/assistant.py`：生活面板入口。
- `qiaomi/ui/desktop_settings.py`：仅托盘唤醒的提示文字。
- `qiaomi/__init__.py`：版本0.5.0，构建v0.5.0-life.1。

其余原语音、AI、长期记忆存储、配置、托盘基础设施、启动器、单实例、自启动及构建脚本均保持原代码。257资源逐字节不变，未新增或替换WebP/图标。

## 验证与交付

新增`tests/test_v050_life.py`（51项参数化实例），更新原`tests/test_costume_tail_assets.py`，仅为5个有意变更的旧运行文件核对“基线哈希→新版哈希”，其他旧模块继续严格校验未变。

新增`scripts/smoke_v050.py`：隔离Qt流程、截图和短时采样。更新README/QUICKSTART/CHANGELOG/TEST_REPORT，新增docs/v050内需求原文、计划、指南、报告、原始测试日志、截图及哈希范围记录。原README留档为README_PREVIOUS.zh-CN.md。

源码包保留全部项目功能、原图、测试和历史说明；排除缓存、虚拟环境、模型、运行日志、用户JSON/数据库及备份。包内`sample_memory.json`为原公开示例，不是私人数据；合成测试只使用临时目录。
