# Linux 离屏短测，非 Windows 游戏性能认证

方法：同一容器，Python3.12/PySide6 offscreen，隔离数据，显示原猫并跳过启动欢迎；2 秒稳定后约 10 秒取 process CPU time / wall time，RSS 为进程启动后峰值。原基线 v0.6.0-P0-fix.1 对比本候选，未加载模型/开麦。测量脚本 `scripts/measure_world_linux.py`，原始 JSON 与 test-host.txt 同目录。

| 场景 | 基线 单核CPU% | 候选 单核CPU% | 基线峰值RSS MiB | 候选峰值RSS MiB |
|---|---:|---:|---:|---:|
| 普通待机 | 1.057 | 1.036 | 104.34 | 107.48 |
| 游戏深眠 | 0.015 | 0.010 | 99.97 | 102.91 |

深眠中 controller 保留一个 10 秒原托盘保活计时器；新增陪伴与小游戏计时器为零。普通模式增加一个 2 秒陪伴心跳；邻近跟踪仅临时 120 ms（约8fps）。无新增常驻线程/模型。

短测与回归任务可能共享宿主资源，单次样本不足以证明性能提升，也不能承诺“零影响”。RSS 增加约 3 MiB；未测 GPU、Windows 合成器、物理多屏、语音模型或真实游戏。需在用户的 4070 Ti Windows11 上按 WINDOWS_ACCEPTANCE 文档复测。
