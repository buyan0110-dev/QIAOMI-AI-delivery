# v0.4.0-completion.1 测试与交付报告

本次为已发布 v0.4.0 的增量完善，日期2026-11-11。未重写 GUI/数据库/语音采集。原公开 ZIP 保留，完善版使用新文件名。

## 实际结果

**317 项自动化测试通过，0 失败（25.09秒）；Linux Qt 离屏44状态启动自检通过；pip check 无依赖冲突。** 证据为 docs/validation/tests-v0.4.0-completion.xml、startup-v0.4.0-completion.json。原275项保留，素材总数断言60→112，以及随机动作测试隔离日常分支；新增42项test_lifestyle.py。

环境：Linux 6.18.57、Python3.12.14、PySide6 6.8.3，QT_QPA_PLATFORM=offscreen。

## 新增自动化覆盖

- 注入单调时钟验证599.99/600、1199.99/1200、1799.99/1800秒边界，游戏暂停/续计，离线时间不累计，生气进度持久化。
- 冷落寻找/委屈/鼓脸/背身/抱尾/回头状态；动画不会重置时钟；忙碌时延后展示，不丢失状态。
- 四次独立有效触摸与原三连击分离；快速连点不推进，聊天/跳过不直接原谅，真实Qt按下释放计数，空白/拖动/忙碌输入不冒充有效安抚。
- 第三下使用独立蹭鼠标帧，画布内轻蹭且OS光标未被移动；工作眼镜造型暂停生气画面但保留情绪。
- 七套独立日常帧真实Qt解码与渲染、无重逢文件别名、不同帧/透明度/LRU预算；打瞌睡转蜷睡。
- 普通睡觉低频随机本地梦话，醒来/关闭/游戏停止；无语音与模型调用。
- 手动迎接一次、临时边缘位置不写入desktop.json、跳过/任务打断恢复位置；缺素材明确提示。
- 真正启动独立Python进程执行main：普通手动迎接、自启动不迎接、深眠重启不迎接且不解码帧，均从正常退出路径结束。
- 性格设置按钮/开关同步，关闭冷落后保存已清除状态，旧偏好兼容；全部生活计时器在深眠停止。

时间边界测试使用可注入时钟加速，不能称为实际等待30分钟耐久测试。三条main入口是Linux真实子进程+真实Qt测试，不是Windows Shell验证。原Windows注册表/Explorer/音频测试包含模拟。

## 资源与视觉检查

新增52张WebP：七类日常28、迎接4、背身/抱尾/回头12、心软/蹭鼠标8。原60张保留，总计112张。实际Qt窗口渲染截图：docs/previews/lifestyle-v0.4.0-completion-linux.png。每个指定动作有独立可辨认画面；4帧生成式关键帧仍需密集中间帧、清边和修型，不等于专业动画成片。

逐项实际完成/部分完成/缺少素材报告见 FEATURE_STATUS_V0.4.0_COMPLETION.md。本轮指定七类日常无整组缺失素材；旧撒娇单爪挥动/肉垫特写等精修项尚未全部补绘。

## 基础性能（短样本）

隔离临时用户目录、离线provider、无模型/麦克风/游戏/GPU负载；每阶段约8秒，CPU为当前进程相对一个核心，短时样本存在调度误差。

| 场景 | 单核CPU | RSS | 累计冷落秒 | 冷落/梦话/情绪timer |
|---|---:|---:|---:|---|
| pet_idle | 4.122% | 89.87 MiB | 8.338 | True / False / False |
| game_mode | 0.007% | 86.33 MiB | 8.338 | False / False / False |
| hidden_idle | 0.022% | 86.34 MiB | 16.336 | True / False / False |

休眠累计值与进入前一致，动画/性格全部timer停止、动画解码缓存0、麦克风inactive、语音工作进程PID0。托盘/安全管理仍有事件循环，不承诺零CPU。隐藏时仍保留下一冷落截止点的单次timer但不展示动画，不是高频轮询。原始数据：docs/validation/performance-v0.4.0-completion-linux.json。

## 未验证

**Windows11实机、Windows GUI EXE、HyperX真实录音/中文转写/TTS、NVIDIA/GPU及APEX/幻兽帕鲁并行性能未在本轮验证。** 没有生成Windows EXE。没有实际等待30分钟或3–7分钟梦话的真机耐久测试；按WINDOWS_ACCEPTANCE_V0.4.0.md补验。

原专用中文KWS仍未实现，现有唤醒是默认关闭的可替换实验ASR方案。本次没有改名虚报。Ollama独立共享服务的已发出计算/权重驻留不保证立即终止。

## 数据保护

storage.py、audio_capture.py、voice_worker.py、主配置加载代码字节不变，SQLite结构不变。新增性格开关和运行快照只在personality.json，旧字段/未知字段保留。没有数据库迁移。ZIP不含私人数据库、个人配置、录音、模型、虚拟环境或密钥。脚本/GUI入口/托盘/图标继续保留。

## 复现

```bash
QT_QPA_PLATFORM=offscreen python -m pytest -q --junitxml=docs/validation/tests-v0.4.0-completion.xml
QT_QPA_PLATFORM=offscreen python -m qiaomi --smoke-test --smoke-report docs/validation/startup-v0.4.0-completion.json
python -m pip check
QT_QPA_PLATFORM=offscreen python scripts/measure_idle.py --output docs/validation/performance-v0.4.0-completion-linux.json --seconds 8
```

Windows真实桌面测试不要设置offscreen；构建使用现有build_windows.bat，需分发完整onedir。安装/升级详见README.md、QUICKSTART.txt与UPGRADE_V0.4.0.md。
