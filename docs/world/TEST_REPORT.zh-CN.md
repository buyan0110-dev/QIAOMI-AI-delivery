# 验证记录

环境：Linux 容器 / Python3.12 / PySide6 6.8.3，`QT_QPA_PLATFORM=offscreen`。自动测试包含真实 Qt 控件、信号、计时器与生命周期，Windows 最近输入/前台、音频和模型接口使用模拟；不代表真实 Windows11 + HyperX/4070Ti 验证。

| 阶段 | 完整 pytest | 原始证据 |
|---|---|---|
| 基线 P0-fix.1 | 624 通过（上次交付记录） | docs/p0fix/tests.txt |
| 两项地基修正 | 629 通过 / 245.42秒 | docs/p1/fix2-tests.txt + XML |
| P1 实际生产者 | 651 通过 / 236.02秒 | docs/p1/full-tests.txt + XML |
| P2 收藏/相册/闯祸 | 658 通过 / 252.21秒 | docs/world/p2-full.txt + XML |
| P3 页面/家具/小游戏 | 666 通过 / 275.69秒 | docs/world/p3-full.txt + XML |
| CI前修订整套回归 | 681 通过 / 269.45秒 | docs/world/final-full.txt + XML |

最终 candidate.2 同一源码树整套回归 **685 通过 / 264.83秒**（final-full.txt/XML）。原681项记录另存 pre-ci-681-full。Windows 首轮实际675通过/6失败，原因与修正见 IMPLEMENTATION 末段；没有跳过旧断言。Windows风格Qt模拟复测17项通过。

P1 新增22项，P2新增7项，P3新增8项，P4新增19项；此前两项政策缺陷新增5项。P4 专项15项复测通过，最终整套结果另外记录，不将专项数充当完整回归数。

验证了：授权后 phase 转换不自取消；45秒/120秒长会话、过期与过期令牌拒绝；原摸头/前爪/拖拽优先；六梦与旧设置；七微动作；Windows闲置模拟与闷气计数保持；四闯祸中断；SQLite事务回滚/跨重启去重/收藏合并/删除/导出/相册关闭/每日上限；八家具槽位；三小游戏的关闭/Esc/超时/触摸/禁用/系统休眠/游戏模式清理；五新页与旧页共存；三主题四缩放真实Qt渲染；JSON和两个SQLite/WAL在线备份；完整旧功能测试。

发现并处理：同秒事件排序不稳定，时间戳改微秒且测试不依赖无定义同秒顺序；最初测试明确暴露该失败，修正后重跑。P3 后补充备份 source_version、房间等比预览及房间按钮窄屏换行，最终整套回归在这些修订后运行。

`final-smoke.json` 的 Linux 离线启动检查 passed=true，包含旧渲染、聊天持久化、记忆备份/导入、正常退出。截图为隔离演示数据的实际 Qt offscreen 输出。

未验证：Windows11/Explorer/自启动/真实全屏与输入时间、真实声卡/Whisper/TTS/Ollama、双屏物理DPI、真正游戏负载、GPU。Windows CI 构建如产生额外证据将单独附上，不冒充 Windows11用户实机测试。美术资源本次保持原样，格式/哈希测试不能证明角色解剖或动作已经精绘完成。


## Windows CI 第二轮实际结果

WindowsServer2025 / Python3.12：**685 passed / 287.17秒，0失败、0错误、0跳过**（windows-full.xml）。GUI EXE构建成功，打包程序91项启动检查全部通过（windows-frozen-smoke.json）。下载后二次ZIP CRC/SHA256检查、AMD64/GUI子系统2、原264资源一致性通过（windows-binary-check.json）。详见 WINDOWS_CI。源码ZIP只补录这些文档与证据，运行源码/测试/资源与CI输入逐字节一致。
