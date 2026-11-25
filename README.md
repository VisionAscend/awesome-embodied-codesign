# Awesome Embodied Co-Design

具身机器人软硬件协同设计精选。每条收录说明一项具体设计、与它配合的算法或控制方法，以及作者在实机上验证的能力。覆盖论文、技术报告、作者项目页和开源实现。

## 从这三篇开始

- **ALOHA** 把双臂遥操作采集与动作分段预测结合起来，用 50 条示教学装电池。[项目与视频](https://tonyzhaozh.github.io/aloha/)
- **UMI** 用手持夹爪采集腕部视角和相对轨迹，同一摆杯策略可以部署到 UR5e 和 Franka。[跨机械臂实验](https://umi-gripper.github.io/)
- **Flash ALOHA** 用可反驱机械臂直接采集高速示教，再平滑衔接策略输出的动作段，完成双臂抛接球。[项目与视频](https://johnyao93.github.io/flash-aloha/)

## 目录

- [双臂操作与遥操作](#双臂操作与遥操作)
- [夹爪与灵巧手](#夹爪与灵巧手)
- [足式运动](#足式运动)

## 双臂操作与遥操作

- **ALOHA / ACT，RSS 2023**　两台 WidowX 250 主臂映射到两台 ViperX 300 从臂。双腕加两个固定机位记录视觉，ACT 从多视角图像和关节位置预测成段的关节目标。每项任务用 50 条示教。论文把穿扎带等遥操作能力与自主执行分开呈现；自主实验包括开调料杯和装电池。适合对照阅读硬件教程、演示采集和策略回放。[项目与视频](https://tonyzhaozh.github.io/aloha/) · [ACT 代码](https://github.com/tonyzhaozh/act)
- **Mobile ALOHA，2024**　操作者双手控制双臂，用腰带牵引移动底盘，同时记录 14 维双臂及夹爪目标和 2 维底盘速度。训练时可以混入静态 ALOHA 数据。自主任务包括煎虾并装盘、打开双门吊柜收锅。底盘的作用和加入静态数据的收益是两个变量；论文的联合训练对照适合回答后一个问题。[作者项目](https://mobile-aloha.github.io/) · [论文](https://openreview.net/pdf?id=FO6tePGRZj)
- **ALOHA 2，2024**　给主从臂装低摩擦导轨夹爪，改进被动重力补偿，换用 D405 相机，并发布经过系统辨识的 MuJoCo 模型。实物、遥操工作站和仿真模型都有开放资料。它回答的是如何让人持续、稳定地采集演示；特定下游策略的增益仍需对应的任务实验。[技术报告与设计文件](https://aloha-2.github.io/) · [仿真模型](https://github.com/google-deepmind/mujoco_menagerie/tree/main/aloha)
- **ALOHA Unleashed，2024**　在 ALOHA 2 上组织规模化遥操采集，用基于 Transformer 的扩散策略学习双手的连续配合。系鞋带、挂衬衫、给另一台机器人更换手指都需要反复调整接触。结果反映平台、数据采集和策略的共同作用。[作者项目与逐任务视频](https://aloha-unleashed.github.io/)
- **AV-ALOHA，2024**　两条机械臂操作物体，第三条臂移动相机；VR 接口让示教者在操作时改变视角，策略也能控制视角。适合研究遮挡下“该往哪里看”。可对照论文里的视角配置，代码含实机和仿真环境。[论文](https://arxiv.org/abs/2409.17435) · [代码](https://github.com/Soltanilara/av-aloha)
- **ALOHA Lightning / Flash ALOHA，2026**　在可反驱双臂末端安装把手，人直接带动机械臂高速示教。训练时遮去入镜的人手，部署时平滑衔接重叠动作段。作者用 ARX 双臂收桌、插电池等，用 HESSIAN 双臂抛接球，每项采 50 条示教。抛接全流程在 arXiv v1 表 III 为 50%、1.85 秒，作者项目所链 PDF 表 III 为 80%、1.85 秒（两份公开版本的结果有差异）。[11 月 16 日预印本 v1](https://arxiv.org/html/2611.21919v1) · [作者 PDF 表 III](https://johnyao93.github.io/static/files/flash-aloha.pdf?v=2) · [硬件、视频和代码入口](https://johnyao93.github.io/flash-aloha/)

## 夹爪与灵巧手

- **Extrinsic Dexterity，ICRA 2014**　单执行器三指柔顺夹爪借助桌面等外部接触，配合机械臂运动完成换抓。值得看动作序列中物体何时由夹爪约束、何时由环境支撑。[论文与实机动作](https://publications.ri.cmu.edu/storage/publications/pub_files/2014/5/ICRA14_1887_FI.pdf)
- **Hardware as Policy，CoRL 2020**　单电机通过肌腱驱动多个关节。把滑轮半径、回位弹簧刚度和预紧角纳入可微计算，与抓取策略共同优化，再按所得参数制造机械手。实机既能指尖抓取也能包络抓取，是严格意义上的硬件与控制联合优化。[作者项目](https://roamlab.github.io/hwasp/)
- **Model W，Science Robotics 2021**　用势能模型与几何约束筛选双指结构，允许物体滚动、滑动以及部分接触断开。真机能连续重定向物体，并在包络握持和指尖捏持之间切换。[论文摘要](https://pubmed.ncbi.nlm.nih.gov/34043534/)
- **RBO 柔顺手，RSS 2021**　气动手指在接触时顺应物体形状，使一组开环动作可以反复串联。作者记录过连续旋转魔方 140 次后掉落的一次运行；这一数字描述该次运行的长度。[实机论文](https://www.roboticsproceedings.org/rss17/p089.pdf)
- **Touch Dexterity，2023**　Allegro Hand 在手掌和指节等处布置 16 个力敏电阻，将接触简化为易在仿真中对应的二值观测。实机策略利用这些信号转动训练中未见的物体，无需外部相机估计物体姿态。[作者项目](https://touchdexterity.github.io/)
- **UMI，RSS 2024**　示教者手持带 GoPro 的平行夹爪。腕部视角和相对末端轨迹把观测、动作与具体机械臂的关节布局解耦；部署时匹配传感与执行时延。摆杯实验同一策略跨 UR5e 和 Franka，动态抛物另有时延消融。摆杯采集速度为 UMI 每小时 111 次、SpaceMouse 遥操 35 次。[项目页的 Capability Experiments 与 Data Collection Methods](https://umi-gripper.github.io/)
- **DexUMI，CoRL 2025**　为 Inspire Hand 和 XHand 分别设计可穿戴外骨骼，使示教手势落在目标机械手的运动范围内。将视频里的人手和外骨骼替换为渲染的机械手，再训练扩散策略。作者报告两个平台多任务平均成功率 86%，两种手各有适配环节。[作者项目](https://dex-umi.github.io/)
- **House of Dextra，ICLR 2026**　搜索手掌几何、手指数目和关节构型，用以形态为条件的策略评估候选，再以模块化零件制造实物。四种设计用于实机迁移测试，包括在无视觉条件下旋转物体；实机验证的任务范围以论文为准。[作者项目与硬件指南](https://an-axolotl.github.io/co-design-for-dexterity.github.io/)
- **Tactile In-Hand Object Rotation，2026 年 10 月预印本**　仿人与对称布局的两款 LEAP Hand 都配 TacTip，按同一强化学习框架训练。10 个物体的实机测试中，对称布局平均旋转次数高 32.0%，整体转速高 25.8%。触觉相对仅本体感知的单项消融在仿真中完成。[预印本](https://arxiv.org/abs/2610.26759)

## 足式运动

- **McGeer，被动动态步行，1990；Collins 等，Science 2005**　早期实物利用腿的自然摆动、重力与惯性，在浅坡上形成稳定步态。后续机器人给步态补充少量能量以支持平地行走。两篇连读可以看出，先选身体的自然动力学，会怎样改变执行器要做的功。[McGeer 论文](https://doi.org/10.1177/027836499000900206) · [Collins 等论文](https://groups.csail.mit.edu/robotics-center/public_papers/Collins05.pdf)
- **MIT Cheetah 3，IROS 2018**　高带宽执行器提供本体感知，关节活动范围支持大步幅；接触检测和步态调度配合地面反力控制。实机仅凭本体感知登上踏步高度 17.8 cm 的楼梯，是传动设计与反馈控制相互支持的例子。[MIT 原论文](https://dspace.mit.edu/bitstream/handle/1721.1/126619/IROS.pdf)
- **Stanford Doggo，ICRA 2019**　3∶1 皮带准直驱配合并联连杆，以电机反馈实现虚拟刚度与阻尼。作者同时给出台架扭矩控制带宽和整机跳跃实验，便于从执行器读到整机行为。[原论文](https://arxiv.org/pdf/1905.04254)
- **PAWS，Nature Machine Intelligence 2025**　把动物的运动协同落实为柔顺的跨关节机械耦合，让四个执行器驱动多种动作。实机受扰时的被动响应，可用于观察哪些调整由身体直接完成。[原论文](https://www.nature.com/articles/s42256-025-00988-x)
- **Chen 与 Aukes，IJRR 2025**　小型四足平台可换腿长、传动比和串并联刚度。以跨形态策略筛选分别适合快速直行、转弯和低运输成本的设计，再制造三种腿并用动捕和电流验证。不同任务偏好不同结构。[论文](https://doi.org/10.1177/02783649251337110) · [项目与数据](https://idealab.asu.edu/curating-legs-web/)
- **Dogger，2026 年 11 月预印本**　先训练跨形态 PPO 策略，再用贝叶斯优化选三段腿长及膝部弹簧参数。相对连杆取中位长度、无弹簧的基线，作者报告巡检和负载 2 kg 搬运的实机运输成本分别下降 18.6% 和 35.7%。每种设计在各任务测四次；拆分几何和弹簧各自贡献的证据来自仿真。[实验与基线](https://arxiv.org/html/2611.02462v1)

## 补充条目

欢迎通过 issue 或 pull request 推荐工作。请附原论文或作者项目页，并用一两句话说明硬件设计、配套的软件方法和实机验证任务。
