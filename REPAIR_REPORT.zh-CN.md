# v0.4.1-artfix.1 专项修复候选 — 尚未完成全部美术验收

本包基于现有 v0.4.1 增量修改，版本仍为 0.4.1。不是 Windows 已验收正式版。

## 已确认根因

原始 edge_top/bottom/left/right 共16帧直接画有假边框、截断和杂点；原始 touch_tail-2/3 与 reunion_cuddle-2/3/4/5 可见后尾和前尾同时存在。主要问题已存在于原始素材。原渲染只绘制一个角色图，没有发现独立尾巴组件重复创建的证据。不能将用户现场的全部显示问题归因于图层残留。

## 实际改动与状态

- 已替换50张原始 WebP：16张 edge、16张 exit、4张 welcome、4张 touch_tail、4张 angry_tail、6张 reunion_cuddle。exit/welcome 含同类假边框，故一起修理。图片编辑工具重绘轮廓，未用模糊、矩形遮挡或阈值抠图冒充修复；导出仅统一画布和组内公共变换。
- 假横杆/假竖杆：候选素材中已去除。四边接触点使用真实窗口边界裁剪，资源中不再绘制屏幕道具。**实际 Windows 四边衔接仍待验收**。
- 双尾巴：本次候选 touch_tail/angry_tail/reunion_cuddle 逐帧缩略检查只见一条橘尾；保留粉色装饰尾。**尾根连接、完整摆尾运动及运行时所有切换仍部分完成，不能认证已经达到最终动画标准**。
- 尾巴播放：touch_tail 采用 0→1→2→3→2→1→0；抱尾巴别名使用同一资源。仅相关动作增加末帧保持，未更改四次安抚状态机。
- 渲染：每次以 Source 合成清除整个窗口透明缓冲，再绘制单帧，防止旧帧透明部分不能覆盖旧尾巴的风险。此为防御修正，未证明其是 Windows 现场第二根因。
- 命中：按实际绘制矩形、当前源帧姿势、组内交互范围映射；透明像素不响应，粉色装饰尾不作为橘尾。**四边高 DPI 和不同姿态边缘命中需实机验证**。
- 新增只读资源检查脚本，检查可解码、RGBA、尺寸、路径、孤立分量、低透明残留、接触点元数据及颜色重心跨度。不能自动判断尾巴数量、重复爪子或解剖正确性。

## 仍需人工精修的具体素材

以下目标帧仍触发透明残留/孤立像素诊断（可能含合法毛发和饰物，不能直接自动擦除）：

- angry_tail-1.webp
- edge_bottom-0.webp
- edge_bottom-1.webp
- edge_bottom-2.webp
- edge_bottom-3.webp
- edge_left-3.webp
- edge_right-0.webp
- edge_right-2.webp
- edge_top-1.webp
- reunion_cuddle-0.webp
- reunion_cuddle-1.webp
- reunion_cuddle-3.webp
- reunion_cuddle-4.webp
- reunion_cuddle-5.webp
- touch_tail-0.webp
- touch_tail-2.webp
- touch_tail-3.webp

此外，edge_top-0至3、edge_bottom-0至3、edge_left-0至3、edge_right-0至3 均需逐帧人工确认接触点和动作锚定；共享变换并不等于零抖动。touch_tail-0至3、angry_tail-0至3、reunion_cuddle-0至5 的角色占比与原素材有差异，尤其 cuddle 较小，必须精修占比、尾根和过渡后才能认定动画修复完成。没有通过逐帧独立缩放掩盖这些差异。

全252帧已作缩略图人工巡检和格式检测。另发现未在本次范围内修改的 working-0至5、game_preview-0至5 有矩形底色；angry_back-3、angry_peek-0至3 尾根关系仍需全尺寸人工复核。完整自动警告清单见 manual-review.csv 和 art-audit-after.json；不将未修改帧宣称为美术无缺陷。

## 数据与兼容性

未修改 app/personality/lifestyle/appearance 核心逻辑，未作数据库迁移；语音、聊天、存储、托盘、自启动模块不作本次重构。包不包含数据库、个人配置、模型、录音或虚拟环境。不要删除原安装目录，先备份用户数据，以新目录运行候选。原 start.bat 和 GUI 启动入口保留；只替换素材不会更新已有打包 EXE，EXE 必须重建。本环境未构建 Windows EXE。

## 测试与限制

Linux / Python 3.12 / PySide6 offscreen：原373项回归通过；新增13项接触点几何、RGBA、尺寸、只读审计、往返帧引用等测试通过。最终全量结果见 docs/validation/full-tests.txt 和 XML。252帧格式/路径检查无基本错误，236帧有启发式警告。它们是审查线索，不是236帧都存在错误的结论，也不证明其余16帧美术合格。

未进行 Windows 11 实机验证、真实桌面透明合成验证或高 DPI 多屏测试。预览由真实候选素材生成，不是 Windows 实机录屏；MP4不含语音，透明动画为 animated WebP。

## Windows 11 手动验收（尚未执行）

1. 备份现有用户数据和源码；在独立目录使用原安装步骤创建环境，start.bat 调试启动。确认记忆和配置路径仍指向原用户数据；不要复制候选包覆盖个人数据库。
2. GUI入口无黑窗启动；确认小猫、托盘、聊天和语音正常，退出无残留进程。
3. 四边分别拖动小猫，录制完整四帧循环；深浅桌面检查横线、竖线、透明杂点、底部截断和抖动。100%、125%、150% DPI及多屏重复。
4. 待机→尾巴单击→连续点击→抱尾巴→四次独立摸摸→待机；边缘姿态再触发尾巴互动。每帧只允许一条橘尾，保留粉色装饰尾；检查尾根、松爪和位置连贯。
5. 逐个点击头、脸、腹、爪、尾及透明区域；确认动作与部位匹配，不把装饰尾当真尾。
6. 游戏深度休眠期间确认无动画刷新；仅手动唤醒后重逢。验证冷落机制、四次哄好、主题、字体、长期记忆和语音回归。
7. 任一帧不合格，不可标记整体完成；在 manual-review.csv 标注帧名、DPI、方向、截图和复现步骤。

## 预览与文件

edges-before-after.png、tails-before-after.png 为实际前后资源对比；edge-frames-light.png 为浅底透明边缘检查；related-edge-frames.png 为相关 exit/welcome 帧；touch-tail-transparent.webp 为透明动画，touch-tail-preview.mp4 为不透明播放预览。changed-files.txt 为源代码与素材增量列表。

最终全量自动化结果：386 passed in 62.09s；仅 Linux/Qt offscreen，非 Windows 实机。edges-layout-simulation.mp4 使用实际接触点与 viewport 裁剪合成四边示意，非 Windows 录屏。
