# QIAOMI AI v0.4.0 — 超级黏人性格系统

[打开 v0.4.0 完整源码 ZIP 文件页](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/QIAOMI-AI-v0.4.0-source.zip)

请使用 Edge/Chrome 打开文件页，再点右上角 **Download raw file（向下箭头）**。如果聊天内置浏览器打开下载链接会退出，请复制链接到外部浏览器。ZIP 约 2.69 MB，包含完整项目；这不是已构建的 Windows EXE。

[安装与启动](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/INSTALL.md) · [Windows 构建](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/WINDOWS_BUILD.md) · [升级/数据保护](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/UPGRADE.md) · [Windows 验收](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/WINDOWS_TEST_STEPS.md) · [测试报告](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/TEST_REPORT.md) · [动画素材实况](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/ASSETS_STATUS.md) · [修改文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/FILES_CHANGED.md) · [更新日志](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/CHANGELOG.md) · [语音配置](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/VOICE.md)

## 新增功能

- 粉色睡衣橘猫：摸头闭眼、肉垫缩爪、三连击打滚；本地有限动作与文字气泡配合，不调用 AI 主动生成撒娇。
- 手动“唤醒敲咪”后仅一次重逢：揉眼 → 惊喜 → 泪眼 → 迈步跑来 → 张爪求抱 → 短暂撒娇。可以跳过，不互动会逐渐恢复，不强制播放语音。
- 工作/游戏造型佩戴圆形金丝边框眼镜，配小电脑/手柄。陪伴与重逢使用普通造型。
- 撒娇/重逢/气泡可分别关闭，主动频率可调；默认高黏人，每 2–4 分钟一次短动作，任务繁忙/隐藏/眼镜造型时暂停主动撒娇。
- 游戏深度休眠停止动画与性格调度、释放动画缓存、停止自身语音进程并拦截新推理/录音；**只有“唤醒敲咪”恢复，切换窗口与重启不会自动恢复**。
- 延续 GUI 启动、托盘、单实例、自启动、长期记忆和 CPU int8 本地语音。新增独立 personality.json，原 SQLite 结构及语音采集算法未改动，无需数据库迁移。

## 启动与升级

先完全退出旧版并备份原用户数据目录；解压到新目录。start.bat 准备基础依赖，install_voice.bat 准备语音依赖；随后用 install_shortcut.vbs 创建“敲咪”桌面图标，日常双击图标或 start.vbs。start.bat 是有控制台的调试入口。模型保持原本地路径，不要移动旧虚拟环境，保留原数据库/配置/模型/自定义形象。

托盘 → “性格与形象”选择新造型。旧自定义形象继续保留；若想切换本次粉色睡衣素材，请在桌面设置主动恢复内置形象。缺失重逢动作会明确提示并跳过，不弹随机文字冒充动画。

## 已验证与尚未验证

**275 项自动化测试通过，31 状态 Linux Qt 离屏自检通过，pip check 通过。** Windows 系统接口/音频相关测试包含模拟，不能当成实机成功。**Windows EXE 未构建，Windows 11 + HyperX + RTX 4070 Ti + 游戏并行性能未实测。** 构建脚本使用 PyInstaller windowed/console=False，需在 Windows 完成构建和验收。

八组重逢各 6 帧、眼镜工作/游戏各 6 帧，共 60 张独立透明 WebP。属于 AI 初版美术：半透明粉边/局部矩形羽化及动作衔接仍待精修；九类主动行为复用这些帧与局部画布变换，不宣称九套独立绘制动画全部完成。

约 8 秒 Linux 离屏短样本（无模型，单核 CPU 口径）：普通待机 1.440% / 89.16 MiB；深度休眠 0.041% / 85.55 MiB；隐藏 0.076% / 85.58 MiB。休眠时动画/性格计时器停止、解码缓存 0、麦克风 inactive、语音进程 PID 0。**这不代表 Windows 或游戏零性能影响**。独立 Ollama 服务可能继续驻留模型，程序不强制终止共享服务。

[性能原始数据](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/PERFORMANCE_LINUX.json) · [自动化测试 XML](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/TEST_RESULTS.xml) · [启动自检](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/SMOKE_RESULTS.json) · [源码比对](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/SOURCE_DELTA.json) · [发布清单](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/release-manifest.json)

ZIP SHA-256：

```text
dab424a9a8377ce4a729a42b15347002496737413950e99ac9c1157077386cd0
```

[校验文件](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/blob/delivery/v0.4.0/QIAOMI-AI-v0.4.0-source.zip.sha256)

历史版本保持可用：[v0.3.2](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.2) · [v0.3.1](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.1) · [v0.3.0](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.3.0) · [v0.2.0](https://github.com/buyan0110-dev/QIAOMI-AI-delivery/tree/delivery/v0.2.0)
