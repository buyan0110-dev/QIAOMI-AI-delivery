# QIAOMI AI v0.4.0 完善版 — 日常生活、冷落与四次安抚

[打开完善版完整源码 ZIP 文件页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/QIAOMI-AI-v0.4.0-complete-source.zip)

在 Edge/Chrome 打开文件页，点击右上角 **Download raw file（向下箭头）**。若聊天内置浏览器打开下载链接会退出，请复制到外部浏览器。包约4.57 MB，构建标识 **v0.4.0-completion.1**，不是已构建Windows EXE。原v0.4.0包保持不变。

[安装与启动](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/INSTALL.md) · [逐项完成实况](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/FEATURE_STATUS.md) · [测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/TEST_REPORT.md) · [Windows验收](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/WINDOWS_TEST_STEPS.md) · [升级与数据保护](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/UPGRADE.md) · [Windows构建](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/WINDOWS_BUILD.md) · [修改清单](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/FILES_CHANGED.md) · [更新日志](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/CHANGELOG.md)

## 本轮实际实现

| 要求 | 状态 |
|---|---|
| 10/20/30分钟冷落 | 完成：单调时钟追踪、寻找/委屈/生闷气；游戏深眠冻结，离线不累计。 |
| 四次独立安抚 | 完成：1仍气、2心软、3蹭鼠标、4原谅；相邻至少0.65秒，快速三连击/空白/拖动不算。聊天/跳过不会直接原谅。 |
| 七类日常动作 | 完成初版：吃饭、点头瞌睡、侧卧蜷睡、金丝眼镜游戏机、洗脸、四足伸展、毛线球，各4张独立关键帧，不复用重逢冒充。 |
| 梦话 | 完成：普通睡觉3–7分钟低频随机文字、默认静音、无AI调用；醒来/隐藏/繁忙/深眠停止。 |
| 手动启动迎接 | 完成初版：工作区左边缘探头→眨眼→挥爪→跳出，结束恢复保存位置；自启动/深眠/重复激活不播放。 |
| 专业美术精修 | 部分完成：本轮整组素材无缺失，但每组仅4个关键帧，透明边缘、密集中间帧及衔接仍待精修。 |

新背身、抱尾、回头、心软和蹭鼠标都有独立姿态。第三下仅在画布内朝光标方向轻蹭，不移动/点击系统光标，不追逐窗口。生气状态可以在性格设置关闭，不阻断正常聊天。

新增52帧，保留原60帧，共112张WebP。下图是 **Linux实际Qt窗口渲染**，不是Windows截图；静态图仅用于检查可辨认姿态，不代替动画验收。

![日常、情绪与迎接姿态预览](https://raw.githubusercontent.com/buyan0110-dev/QIAOMI-AI-delivery/delivery/v0.4.0/completion/PREVIEW.png)

## 保留与使用

保留粉色睡衣/图标/托盘/GUI入口/单实例/游戏深眠/仅手动唤醒/重逢/长期记忆/语音/本地AI。SQLite、audio_capture.py、voice_worker.py、主配置与Ollama传输代码不变，无SQL迁移。新增性格开关和运行快照只写personality.json，旧字段/未知字段保留。

先完全退出旧版，备份原用户目录与模型/自定义素材；解压到新目录，start.bat准备依赖，install_voice.bat准备语音。日常用start.vbs或install_shortcut.vbs创建的图标，start.bat仍是带控制台的调试入口。不要复制移动旧.venv或把旧EXE当成新源码自动更新。旧自定义形象继续保留，要看新素材请主动恢复内置形象。

右键猫 → **敲咪的日常生活**，或托盘 → **性格与形象** 可逐个播放七类日常；主动撒娇与日常总开关、自动日常/冷落/梦话/迎接开关均可配置。工作/游戏眼镜造型暂停主动动作，但真正深眠才冻结冷落时间。只有“唤醒敲咪”能离开深眠。

## 验证范围

**317项自动化测试通过，0失败，新增42项；44状态Linux Qt离屏启动自检与pip check通过。** 覆盖真实Qt触摸/状态/进程main启动和退出，时间边界用注入时钟加速，音频和Windows接口包含模拟。没有将加速测试称为实际静待30分钟。

**Windows11实机、Windows GUI EXE、HyperX真实语音、RTX4070Ti/APEX/幻兽帕鲁并行性能未在本轮验证。** 原实验唤醒仍是默认关闭的可替换ASR方案，不是专用中文KWS。Ollama为共享独立服务，已发出的计算/权重驻留不保证立即终止。

约8秒Linux离屏单进程样本（无模型，单核口径）：待机CPU4.122%/RSS89.87MiB；深眠0.007%/86.33MiB；隐藏0.022%/86.34MiB。深眠冷落秒数保持不变，所有性格/动画timer停止、缓存0、麦克风inactive、语音PID0。不是Windows/游戏性能承诺。

[测试XML](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/TEST_RESULTS.xml) · [启动自检](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/SMOKE_RESULTS.json) · [性能原始数据](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/PERFORMANCE_LINUX.json) · [源码比对](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/SOURCE_DELTA.json) · [发布清单](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/release-manifest.json)

ZIP SHA-256：

```text
a22024f8ece2826a46af84a8f732ade18d601a5135c3f5b6e71f253001a59975
```

[校验文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/completion/QIAOMI-AI-v0.4.0-complete-source.zip.sha256)

[原v0.4.0源码ZIP（保留）](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/QIAOMI-AI-v0.4.0-source.zip) · [原v0.4.0报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/TEST_REPORT.md) · [v0.3.2](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.2) · [v0.3.1](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.1)
