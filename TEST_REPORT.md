# QIAOMI AI v0.4.1 测试报告

日期：2026-11-11（Asia/Shanghai）。基线：已发布v0.4.0完善版。本轮为增量升级，无SQL迁移。

## 最终自动化

**373项自动化测试通过，0失败，54.79秒；79状态Linux Qt离屏启动自检通过；pip check无依赖冲突。** 证据：docs/validation/tests-v0.4.1.xml、startup-v0.4.1.json。

最终仅提示文案更新后，记忆与输入UI的现有6项测试再次通过，证据ui-copy-v0.4.1.xml；这是复测，不另计为新案例。

Python3.12.14、PySide6/Qt6.8.3、Linux6.18.57、QT_QPA_PLATFORM=offscreen。原317项保留；按v0.4.1新语义更新触摸优先级/计时/动作名/隐藏HTML/素材数量/菜单文本断言，新增2个日常参数回归与test_v041.py的54个专项用例，共增加56个测试案例，没有删除旧测试。

- 实际Qt控件/事件/计时器：双主题×四字号、持久化/损坏备份、窄窗口紧凑导航/长行无横向溢出、弹窗滚动、欢迎无闲置timer、隐藏HTML延迟与显示恢复、代码块转义和复制。
- 实际状态机：十个部位、耳/肚连续反馈、动作收尾→基础坐姿→指定反馈、触摸优先于语音/任务视觉、忙碌恢复、重逢/深眠优先、延后的运动不能抢占重逢。
- 真实QVariantAnimation与几何：四边吸附/解除/关闭、负坐标屏幕矩形、位置保存、临时中央位置不覆盖家、一次爬行、触摸/关闭开关/深眠取消并恢复家。
- 模拟只读Win32：前台普通窗口允许、全屏/安全桌面禁止；非Windows或未知信息安全推迟。不是Windows实机API成功证明。
- 252张WebP真实Qt解码/不同帧/独立素材/有界缓存；原ASR/SQLite/IPC/退出/记忆确认/模型错误测试继续回归，部分设备/模型接口采用模拟。
- 冷落时间边界用注入单调时钟加速，不能等同于真实静待30分钟。普通手动/自启动/深眠重启的main入口使用真实Linux子进程测试。

测试增加DeferredDelete清理，避免测试夹具只调用processEvents导致关闭的Qt窗口积压；不将该测试内存积压称作生产正常待机实测。

## 实际预览

- docs/previews/butler-dark-100-v0.4.1-linux.png
- docs/previews/butler-light-100-v0.4.1-linux.png
- docs/previews/butler-light-150-v0.4.1-linux.png
- docs/previews/pet-v0.4.1-linux.png
- docs/previews/pet-animation-v0.4.1-linux.mp4：实际Qt资源渲染74帧、5fps、14.8秒、无音轨，展示姿态片段，不是完整自主流程或Windows录像。

预览由本次程序离屏渲染，非设计图。大字体需纵向滚动；所有窗口在每种Windows DPI下的布局仍待真机检查。生成式关键帧有清边/比例/衔接问题，见功能状态报告，解码成功不等于美术成片验收。

## 五状态性能短样本

隔离临时数据、离线provider、无ASR/LLM权重、无麦克风/GPU/游戏负载。每阶段约8秒，CPU为当前进程相对一个核心，不能与全机CPU百分比混用。采样误差和共享开发环境调度会影响数值。

| 状态 | 单核CPU | RSS | 线程 | 解码缓存字节 |
|---|---:|---:|---:|---:|
| pet_idle | 1.411% | 99.16 MiB | 4 | 1048576 |
| autonomous_read | 2.552% | 100.27 MiB | 4 | 1310720 |
| butler_open | 0.764% | 102.98 MiB | 4 | 1310720 |
| butler_hidden | 0.646% | 102.99 MiB | 4 | 1310720 |
| game_sleep | 0.105% | 101.04 MiB | 4 | 0 |

深眠阶段所有性格timer、Pet/Orb/位移timer/动画均停止，解码缓存0、麦克风false、语音进程PID0；必要托盘/退出事件仍存在，不承诺零CPU。管家隐藏时仍可有桌宠普通动画，二者资源管理分开。

GPU/显存字段为null（未测），Windows线程/任务管理器GPU计数需本机补验。短样本不能证明APEX/幻兽帕鲁性能或数小时内存无增长；提供measure_life.py的cycles参数延长测试，并明确此验收尚未完成。

## 数据保护与未验证

storage.py/audio_capture.py/voice_worker.py/config.py/ollama.py、ICO、start.bat/start.vbs与PyInstaller spec和基线字节一致；数据库结构不变。UI记忆编辑增加对话框释放，但不改变数据库操作。新增appearance.json和桌面/性格可兼容字段，未知字段保留。

**未生成Windows EXE；Windows11真机无黑窗/托盘/自启动/多DPI/多显示器/全屏/安全桌面、HyperX真实中文ASR/TTS、NVIDIA/GPU/显存及游戏并行性能均未在本轮实机验证。** 原实验唤醒不是专用KWS，本轮未实现专用检测。原用户旧版成功截图不充作v0.4.1实机验收。

缺失/部分完成：独立倒挂、毛线球专属收尾、逐帧精确命中多边形与专业美术修型，详见FEATURE_STATUS_V0.4.1.md。不能把这些标为全部完成。

## 复现

```bash
QT_QPA_PLATFORM=offscreen python -m pytest -q --junitxml=docs/validation/tests-v0.4.1.xml
QT_QPA_PLATFORM=offscreen python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.4.1.json
python -m pip check
QT_QPA_PLATFORM=offscreen python scripts/measure_life.py --output docs/validation/performance-v0.4.1-linux.json --seconds 8
```

Windows不设置offscreen，按WINDOWS_ACCEPTANCE_V0.4.1.md记录真实数据。源码不包含录音、用户数据库/配置、密钥、模型或虚拟环境。
