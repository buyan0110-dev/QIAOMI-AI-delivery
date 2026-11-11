# QIAOMI AI v0.4.0 测试报告

日期：2026-11-11。平台：Linux 6.18.57、Python 3.12.14、PySide6 6.8.3、QT_QPA_PLATFORM=offscreen。

## 自动化结果

**275 项自动化测试通过，0 失败；31 状态离屏启动自检通过；pip check 通过。** 全套测试最终耗时 19.14 秒，证据位于 docs/validation/tests-v0.4.0.xml 与 startup-v0.4.0.json。XML 为最终源码测试结果。

保留 v0.3.2 全部 255 项测试，其中游戏模式断言更新为严格休眠/显式唤醒；缓存键与渲染状态数量跟随新增造型更新，没有删除旧测试。新增 test_personality.py 20 项：

- 有限重逢顺序/不重复、休眠构造不调用形象加载器、缓存释放/停止计时。
- 头/肉垫/身体触摸、三连击、跳过、禁用重逢/气泡、忙碌保护、隐藏时停止。
- 工作/游戏眼镜状态暂停主动行为、关闭主动行为即时生效。
- 配置未知字段保留/损坏备份、普通退出不擅自开启休眠。
- 60 张素材实际解码/透明通道/不同帧、LRU 预算/释放、非法路径及损坏帧提示一次。
- Controller 休眠拦截麦克风/新推理/延迟回复，只有明确唤醒恢复。

真实 Qt 控件/计时器与原有 IPC/退出测试使用 Linux 本机运行；Windows 注册表、Explorer 与部分音频设备/模型接口采用模拟。模拟成功不等于 Windows 真机成功。

## 基础性能样本（不是 Windows 游戏性能）

隔离临时用户目录、离线 provider，不加载 ASR/LLM 模型，无麦克风/游戏/GPU 压测，每阶段约 8 秒。CPU 为当前进程相对一个核心的占用；短样本存在调度误差，不能推导长期峰值。

| 场景 | 单核 CPU | RSS | 动画解码缓存字节 |
|---|---:|---:|---:|
| pet_idle | 1.44% | 89.16 MiB | 1048576 |
| game_mode | 0.041% | 85.55 MiB | 0 |
| hidden_idle | 0.076% | 85.58 MiB | 0 |

休眠阶段宠物动画、性格两个计时器均停止，缓存 0，麦克风 inactive，语音工作进程 PID 0。托盘监测/退出安全事件仍可运行，不承诺零 CPU。完整原始样本：docs/validation/performance-v0.4.0-linux.json。

## 未验证项目与限制

**没有 Windows 11 实机、没有构建 Windows EXE、没有本轮 HyperX 麦克风真实采集/中文转写/TTS 验证，也没有 RTX 4070 Ti/APEX/幻兽帕鲁性能数据。** 用户以前 v0.3.1 的成功截图不充作本版本实机验收。本轮保留 audio_capture.py / voice_worker.py，不改动已验证的 WASAPI 采集算法。

Windows 无黑窗、托盘 Explorer 恢复、自启动、DPI/置顶/焦点、PyInstaller WebP 插件、真实录音/语音和游戏性能均需执行 docs/WINDOWS_ACCEPTANCE_V0.4.0.md。美术有粉边/动作衔接待精修，见 ASSETS_V0.4.0.md。没有将“解码成功”称为“美术验收通过”。

## 复现

```bash
QT_QPA_PLATFORM=offscreen python -m pytest -q --junitxml=docs/validation/tests-v0.4.0.xml
QT_QPA_PLATFORM=offscreen python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.4.0.json
python -m pip check
QT_QPA_PLATFORM=offscreen python scripts/measure_idle.py --output docs/validation/performance-v0.4.0-linux.json --seconds 8
```

在 Windows 使用虚拟环境 python；不要设置 offscreen，测量结果另存，完整分发目录必须本机构建。
