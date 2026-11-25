# Awesome Embodied Co-Design

截至 2026 年 11 月 25 日，收录 99 个条目，覆盖 1982 年的工业装配到近期的高速双臂与形态搜索。每条给出机构或接口、与其配合的控制或学习方法，以及论文实际测过的任务。

## 阅读路线

| 想弄清的问题 | 建议先读 | 看哪组证据 |
|---|---|---|
| 示教器会改变机器人学到的动作吗？ | [ALOHA](https://tonyzhaozh.github.io/aloha/) → [Flash ALOHA](https://johnyao93.github.io/flash-aloha/) | 从主从关节映射到直接拖动双臂。对照装电池的成功率与耗时，再单看动作块平滑消融。 |
| 同一个策略换硬件还能用吗？ | [UMI](https://umi-gripper.github.io/) → [Mirage](https://robot-mirage.github.io/) → [AnySkin](https://any-skin.github.io/) | 依次换机械臂、重绘输入画面以适配新臂、换同型触觉皮肤。三者对相机、动作和传感几何的要求不同。 |
| 一部分控制能否交给机构？ | [Whitney 的插销实验](https://doi.org/10.1115/1.3149634) → [SNAG 栖停实验](https://pubmed.ncbi.nlm.nih.gov/34851710/) | 前者让偏心接触产生纠正力，后者让撞击本身启动抓合。读插入力曲线和着枝后平衡对照。 |
| 如何证明算法选出的形态值得制造？ | [Hardware as Policy](https://roamlab.github.io/hwasp/) → [House of Dextra](https://an-axolotl.github.io/co-design-for-dexterity.github.io/) → [Dogger](https://arxiv.org/abs/2611.02462) | 看哪些传动、手形和腿长真正做出了实物，再核对每个候选是否重训，以及单因素消融在哪完成。 |

## 目录

[双臂操作、遥操作与示教](#s1) · [手持采集与跨本体示教](#s2) · [跨硬件部署与家庭机器人](#s3) · [装配、触觉与被动机构](#s4) · [抓具与灵巧手](#s5) · [步行、四足与人形](#s6) · [空中运动与栖停](#s7) · [软体与水下机器人](#s8) · [传感器布局与形态估计](#s9) · [形态搜索与可微设计](#s10) · [人机协作与特殊作业环境](#s11)

<a id="s1"></a>

## 双臂操作、遥操作与示教

- **ALOHA / ACT，RSS 2023**　两台 WidowX 250 主臂映射到两台 ViperX 300 从臂。双腕加两个固定机位记录视觉，ACT 从多视角图像和关节位置预测成段的关节目标。每项任务用 50 条示教。论文把穿扎带等遥操作能力与自主执行分开呈现；自主实验包括开调料杯和装电池。适合对照阅读硬件教程、演示采集和策略回放。[项目与视频](https://tonyzhaozh.github.io/aloha/) · [ACT 代码](https://github.com/tonyzhaozh/act)

- **Mobile ALOHA，2024**　操作者双手控制双臂，用腰带牵引移动底盘，同时记录 14 维双臂及夹爪目标和 2 维底盘速度。训练时可以混入静态 ALOHA 数据。自主任务包括煎虾并装盘、打开双门吊柜收锅。底盘的作用和加入静态数据的收益是两个变量；论文的联合训练对照适合回答后一个问题。[作者项目](https://mobile-aloha.github.io/) · [论文](https://openreview.net/pdf?id=FO6tePGRZj)

- **ALOHA 2，2024**　给主从臂装低摩擦导轨夹爪，改进被动重力补偿，换用 D405 相机，并发布经过系统辨识的 MuJoCo 模型。实物、遥操工作站和仿真模型都有开放资料。它回答的是如何让人持续、稳定地采集演示；特定下游策略的增益仍需对应的任务实验。[技术报告与设计文件](https://aloha-2.github.io/) · [仿真模型](https://github.com/google-deepmind/mujoco_menagerie/tree/main/aloha)

- **ALOHA Unleashed，2024**　在 ALOHA 2 上组织规模化遥操采集，用基于 Transformer 的扩散策略学习双手的连续配合。系鞋带、挂衬衫、给另一台机器人更换手指都需要反复调整接触。结果反映平台、数据采集和策略的共同作用。[作者项目与逐任务视频](https://aloha-unleashed.github.io/)

- **AV-ALOHA，2024**　两条机械臂操作物体，第三条臂移动相机；VR 接口让示教者在操作时改变视角，策略也能控制视角。适合研究遮挡下“该往哪里看”。可对照论文里的视角配置，代码含实机和仿真环境。[论文](https://arxiv.org/abs/2409.17435) · [代码](https://github.com/Soltanilara/av-aloha)

- **ALOHA Lightning / Flash ALOHA，2026**　在可反驱双臂末端安装把手，人直接带动机械臂高速示教。训练和部署时使用相同的几何遮罩，部署时平滑衔接重叠动作段。作者用 ARX 双臂收桌、插电池等，用 HESSIAN 双臂抛接球，每项采 50 条示教。抛接全流程在 arXiv v1 表 III 为 50%、1.85 秒，作者项目所链 PDF 表 III 为 80%、1.85 秒（两份公开版本的结果有差异）。[11 月 16 日预印本 v1](https://arxiv.org/html/2611.21919v1) · [作者 PDF 表 III](https://johnyao93.github.io/static/files/flash-aloha.pdf?v=2) · [硬件、视频和代码入口](https://johnyao93.github.io/flash-aloha/)

- **Grasping with Chopsticks（2020 预印本）**。定制筷子末端与人示范匹配，算法处理行为克隆协变量漂移。在该实物抓取协议下，作者报告从 37.3% 到 80%，操作者专家 82.6%。机械选择和策略共同完成闭环，成功率差值反映论文算法/训练处理，不能单独当作筷子形态收益。 [论文](https://arxiv.org/abs/2011.06719)

- **GELLO（2023 预印本，2024 IROS）**。3D 打印件与现成电机复制目标臂运动学，操作者在关节空间示范，Franka、UR5、xArm 均有实现；用户研究与 VR 手柄和 3D 鼠标对比。作者的低于 300 美元口径仅含主端零件，每种目标臂仍需要对应机构。 [项目及论文](https://wuphilipp.github.io/gello_site/)

- **DROID（2024，RSS）**。将 Franka Panda、两路可调外部立体相机、腕部立体相机和 Quest 2 遥操作组合为标准实机工作站，18 套设备、50 名采集者、564 场景得到约 7.6 万条演示。标准化降低跨点异质性，仍需要真实机器人，且该数据规模主要覆盖单臂同类本体。 [论文](https://jiajunwu.com/papers/droid_rss.pdf) [搭建和数据入口](https://droid-dataset.github.io/)

- **HALO（2026-11，预印本，HKUST/Robbyant）**。人直接引导真实双臂末端并推动低阻平台，训练时校准/时间对齐人与真实部署底座的响应差，同时移除视频中示教者手部。相对于 Mobile ALOHA 与 VR，作者报告最高 2.9 倍采集速度，并报告六阶段长任务 73.3% 成功。需区分采集速度与训练后成功率，两项都受任务和操作员影响。 [论文](https://arxiv.org/abs/2611.16439) [项目](https://robbyant-research.github.io/Lingbot-ALOHA/)

- **FACTR，2025**　将从臂受到的外力反馈给示教者，再用课程训练让策略在面团擀压、搬盒等接触任务中利用力信号。作者分别评估人遥操时的表现与自主策略在未见物体上的表现，两组对照回答不同问题。[论文与对照](https://arxiv.org/abs/2502.17432)

- **Reachy 2，工程文档**　人形上身和移动底盘配有可通过 VR 遥控的双臂与头部。LeRobot 文档展示如何选择参与录制的机体部位、读取顺应主臂的当前关节位置并回放，用来核对示教接口的动作语义。[硬件](https://pollen-robotics.com/reachy-2/) · [录制与部署文档](https://huggingface.co/docs/lerobot/reachy2)

<a id="s2"></a>

## 手持采集与跨本体示教

- **UMI，RSS 2024**　示教者手持带 GoPro 的平行夹爪。腕部视角和相对末端轨迹把观测、动作与具体机械臂的关节布局解耦；部署时匹配传感与执行时延。摆杯实验同一策略跨 UR5e 和 Franka，动态抛物另有时延消融。摆杯采集速度为 UMI 每小时 111 次、SpaceMouse 遥操 35 次。[项目页的 Capability Experiments 与 Data Collection Methods](https://umi-gripper.github.io/)

- **DexUMI，CoRL 2025**　为 Inspire Hand 和 XHand 分别设计可穿戴外骨骼，使示教手势落在目标机械手的运动范围内。将视频里的人手和外骨骼替换为渲染的机械手，再训练扩散策略。作者报告两个平台多任务平均成功率 86%，两种手各有适配环节。[作者项目](https://dex-umi.github.io/)

- **DexCap（2024）**。胸部 RGB-D/LiDAR 相机、SLAM 相机与手部动作捕捉用于记录人手操作，DexIL 把人体运动/场景信息转为机器人技能，附带人与机器人交互纠正。可扩展到真实环境，但重定向与两侧接触属性差异仍由系统承担。 [项目及论文](https://dex-cap.github.io/)

- **FastUMI（2025，CoRL）**。采集器机械结构与专有夹爪解耦，保留视觉视角一致性，以商品跟踪设备替换原 UMI 的复杂视觉惯性追踪环节，并自动质检。硬件独立性来自模块和视觉接口约束，跨设备部署仍需坐标与机械安装适配。 [正式论文](https://proceedings.mlr.press/v305/zhaxizhuoma25a.html)

- **TacUMI（2026-01，预印本）**。同步集成视触觉、力/力矩、位姿和 RGB；电缆上夹任务比较阶段识别的多模态输入，测试不同机器人，采集器扳机动作会引入力污染并需处理。阶段识别准确率与端到端任务完成率分开读，任务面目前较窄。 [论文](https://arxiv.org/abs/2601.14550)

- **RoboPocket（2026-03，预印本）**。手机兼任传感器与 AR 屏幕，把远程策略的预测轨迹投回采集现场，引导操作者收集纠偏轨迹并异步更新策略。所测任务报告最高约两倍样本效率；依赖远程推理与跟踪链路，其纠偏信号也不同于真机接触失败。 [论文](https://arxiv.org/abs/2603.05504) [项目](https://robo-pocket.github.io/)

- **HoMMI（2026-03，预印本）**。为 UMI 加头部第一视角，学习跨本体视觉与放宽的头部动作表示，再以具物理约束的全身控制器协调底座、手和视线。验证需要主动感知和导航的长时多阶段移动操作，人的移动/视线到机器人可行轨迹的映射仍依赖部署控制。 [论文](https://arxiv.org/abs/2603.03243)

- **YUBI（2026-06，预印本）**。手指直接驱动、柔顺的指向对齐夹爪与 VR 六自由度轨迹结合，作者报告 8,434 小时、120 万条演示及 119 项任务；同一策略在 UR、Franka、ELEY 双臂部署时将匹配夹爪安装在各本体。跨臂迁移证据成立于共享末端形态及所测任务。 [论文](https://arxiv.org/abs/2606.10244) [硬件与数据](https://yubi.airoa.io/)

- **HiFi-UMI（2026-07，预印本）**。头戴式双目/惯性 SLAM、共用 GPIO 微秒触发、每手双广角和相对姿态共同设计，报告工作区内约 3 mm 末端误差。在三个基座上，仅用采集器数据后训练与同场景实机遥操作后训练的成功率差异为 −2.5、+3.1、−0.6 个百分点。论文称差异在其协议采样噪声内。所报为特定基座和任务，公开 2,000 小时与完整采集口径分列。 [论文](https://arxiv.org/abs/2607.25895)

- **Koala Gripper（2026-08，预印本，RAI Institute）**。共同设计采集端手指扳机、机器人可反驱执行器，以及共享的欠驱动指与可转动双拇指，捕获装置和执行装置一开始便一起迭代。作者演示更丰富的包络抓、捏持和单件分离，及从两种采集方式训练并实机执行。属于最直接的机构共同设计，但仍是特定抓具、任务和原型。 [论文](https://arxiv.org/abs/2608.20546) [机构图和视频](https://koalagripper.rai-inst.com/)

- **UMI-Live（2026-10，预印本）**。把相机、LiDAR/IMU、机载计算、电池和任务录制界面集成到双持设备，异步处理 SLAM 与数据输出。公布完整搭建资料和三任务 40 小时数据；两种策略在一项双臂抓放上分别成功 10/10 和 8/10，样本小且不代表三任务都完成实机验证。 [论文](https://arxiv.org/abs/2610.39385) [项目](https://umi-live.github.io/)

- **GR00T 2 / UMIverse（2026-11，NVIDIA 技术报告）**。共享目标机器人腕部视角与动作接口的手持 GEAR UMI 和复现 XHAND1 Pro-U 运动学/接触面的 GEAR DexUMI 用于不同阶段，另发布跟随操作者头显的三轴相机颈及原型 BOM、CAD 和组装软件。系统规模与复现资料支撑工程参考，技术报告的模型成绩不能视为任一硬件独立增益。 [白皮书附录 E](https://research.nvidia.com/labs/gear/gr00t-2/assets/gr00t2_whitepaper.pdf) [设计资料](https://research.nvidia.com/labs/gear/hardware-prototypes/)

<a id="s3"></a>

## 跨硬件部署与家庭机器人

- **Mirage，RSS 2024**　换机械臂之后，策略看到的手臂外观也变了。作者用标定和机器人几何模型把画面中的目标臂替换为训练时的源臂，再用目标臂跟踪源策略给出的末端动作。实机分别换夹爪、换整臂，适用范围受工作空间和抓具几何约束。适合与 UMI 对读，一篇在部署时重绘图像，一篇在采集时就把相机绑到夹爪上。[论文与实机对照](https://robot-mirage.github.io/)

- **ViNT，CoRL 2023**　相机输入、相对路点输出构成导航接口。路点按车速归一化，由各底盘自己的控制器恢复尺度并跟踪。作者给出跨平台部署和长距离导航，后者额外用图搜索与子目标选择。可据此区分局部模型、底盘跟踪器和全局规划器各自负责什么。[项目与演示](https://general-navigation-models.github.io/vint/) · [作者技术报告](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2024/Archive/EECS-2024-166.pdf)

- **Stretch，ICRA 2022**　窄底盘、伸缩臂和升降柱让机器人贴着台面移动。作者用机械模型和实测权衡可达范围、体积与稳定性，展示室内取放、递物；读 Dobb·E 时，这篇能解释底座和机械臂怎样分工。[原论文](https://pmc.ncbi.nlm.nih.gov/articles/PMC10710733/)

- **Dobb·E，2023**　把 iPhone 装到手持取物器采示教，再把相机装到 Stretch 上复现近似视角。作者在 22 户采预训练数据，在 10 户评估 109 个任务，报告 81% 成功率；新任务有约 5 分钟示教和 15 分钟适配。项目还记录了阴影、示教质量等真实家庭里的失败原因。[项目、数据与逐任务视频](https://dobb-e.com/)

<a id="s4"></a>

## 装配、触觉与被动机构

- **Whitney，ASME 1982**　插销偏心时，接触力可能把销推正，也可能让它卡死。论文从力平衡推导远心柔顺装置的柔顺中心与刚度如何选，再用插入力实验核对模型。它给出了改变手腕就能改变装配容差的经典基线。[原论文](https://doi.org/10.1115/1.3149634)

- **颗粒阻塞抓手，PNAS 2010**　软袋先贴合物体，再抽气让颗粒锁紧，控制器用一次压力切换即可抓取多种形状。作者通过拉脱实验分析摩擦、吸附和形状咬合的贡献；物体能否被包住、表面能否密封都影响结果。[原论文](https://doi.org/10.1073/pnas.1003250107)

- **GelSight 理线夹爪，2020**　夹得太紧，线缆滑不动；太松，触觉图像又读不出线的位置。作者用指腹图像估计摩擦力和线缆朝向，分别闭环控制握力和夹爪姿态。实机可经两三次换抓沿一米长的线摸到末端，并演示插入耳机插头。[论文、控制对照与演示](https://gelsight.csail.mit.edu/cable/)

- **GelSight Wedge，ICRA 2021**　把照明和光路折进接近人指尺寸的指尖，配合从凝胶图像重建三维接触面的算法。作者对比一、二、三路照明并展示物体位姿跟踪，证据落在重建和跟踪精度。[项目与论文](https://gelsight.csail.mit.edu/wedge/)

- **AnySkin，2024**　把可磨损的磁性软皮与磁力计分开，使新皮能以可重复的方式套回同一位置。用一块皮训练的策略换皮后仍能刷卡、插插头和插 USB。这里更换的是同型传感皮，任务证据最适合回答维护后能否复用策略。[作者项目与跨实例对照](https://any-skin.github.io/)

- **DIGIT**（2020 年预印本）— 公开紧凑型高分辨率视触觉传感器设计，以机械手手内操作验证组件可用性。传感证据集中于装有 DIGIT 的局部接触面和给定操作任务。 [论文](https://arxiv.org/abs/2005.14679)

- **GelSight EndoFlex**（2023 年，IEEE RoboSoft）— 将柔性内骨骼与曲面光学触觉结合，在手指沿长度方向提供高分辨率接触图。论文的实物结果集中在原型的抓持和传感表征。 [论文](https://arxiv.org/abs/2303.17935)

- **eFlesh**（2025 年 6 月预印本）— 利用可打印的顺应微结构和磁场读出构建贴合不同外形的触觉传感器，项目提供设计与学习实例。结果对应论文所用微结构、装配与操作条件。 [论文](https://arxiv.org/abs/2506.09994) · [项目](https://e-flesh.com/)

<a id="s5"></a>

## 抓具与灵巧手

- **Extrinsic Dexterity，ICRA 2014**　单执行器三指柔顺夹爪借助桌面等外部接触，配合机械臂运动完成换抓。值得看动作序列中物体何时由夹爪约束、何时由环境支撑。[论文与实机动作](https://publications.ri.cmu.edu/storage/publications/pub_files/2014/5/ICRA14_1887_FI.pdf)

- **Hardware as Policy，CoRL 2020**　单电机通过肌腱驱动多个关节。把滑轮半径、回位弹簧刚度和预紧角纳入可微计算，与抓取策略共同优化，再按所得参数制造机械手。实机既能指尖抓取也能包络抓取，是严格意义上的硬件与控制联合优化。[作者项目](https://roamlab.github.io/hwasp/)

- **Model W，Science Robotics 2021**　用势能模型与几何约束筛选双指结构，允许物体滚动、滑动以及部分接触断开。真机能连续重定向物体，并在包络握持和指尖捏持之间切换。[论文摘要](https://pubmed.ncbi.nlm.nih.gov/34043534/)

- **RBO 柔顺手，RSS 2021**　气动手指在接触时顺应物体形状，使一组开环动作可以反复串联。作者记录过连续旋转魔方 140 次后掉落的一次运行；这一数字描述该次运行的长度。[实机论文](https://www.roboticsproceedings.org/rss17/p089.pdf)

- **Touch Dexterity，2023**　Allegro Hand 在手掌和指节等处布置 16 个力敏电阻，将接触简化为易在仿真中对应的二值观测。实机策略利用这些信号转动训练中未见的物体，无需外部相机估计物体姿态。[作者项目](https://touchdexterity.github.io/)

- **House of Dextra，ICLR 2026**　搜索手掌几何、手指数目和关节构型，用以形态为条件的策略评估候选，再以模块化零件制造实物。四种设计用于实机迁移测试，包括在无视觉条件下旋转物体；实机验证的任务范围以论文为准。[作者项目与硬件指南](https://an-axolotl.github.io/co-design-for-dexterity.github.io/)

- **Tactile In-Hand Object Rotation，2026 年 10 月预印本**　仿人与对称布局的两款 LEAP Hand 都配 TacTip，按同一强化学习框架训练。10 个物体的实机测试中，对称布局平均旋转次数高 32.0%，整体转速高 25.8%。触觉相对仅本体感知的单项消融在仿真中完成。[预印本](https://arxiv.org/abs/2610.26759)

- **A Detachable Crawling Robotic Hand**（2026 年 1 月，Nature Communications）— 用对称布局与可双向弯曲手指，在同一机构上实现双面抓取和脱离机械臂爬行。五指、六指原型验证了多物取回和重新对接，证据来自实验室任务。 [论文](https://doi.org/10.1038/s41467-025-67675-8) · [EPFL 存档](https://infoscience.epfl.ch/entities/publication/f8013182-c0ca-4073-af77-a1c7f8c757ab)

- **Yale OpenHand Project**（2017 年，IEEE Robotics & Automation Magazine）— 发布可快速制造和改装的欠驱动机器人手，包括配置和制造说明。各型号的自由度、驱动方式与抓持能力不同，选型时可按型号查看。 [项目](https://www.eng.yale.edu/grablab/openhand/) · [论文](https://www.eng.yale.edu/grablab/pubs/Ma_RAM2017.pdf)

- **Fit2Form**（2020 年，CoRL）— 用学习得到的抓持评价网络指导生成平行夹爪的两片指面几何。论文和项目展示目标物体的实物抓取，设计范围限于平行夹爪指面。 [论文](https://proceedings.mlr.press/v155/ha21b.html) · [项目](https://fit2form.cs.columbia.edu/)

- **RBO Hand 3**（2022 年，IEEE Transactions on Robotics）— 用软气动执行器、柔顺结构和对掌拇指实现 16 个主动自由度，发布了从零件到模具与装配的教程。实物实验建立在气源和具体软体制造流程上。 [论文](https://arxiv.org/abs/2201.10883) · [构建教程](https://www.tu.berlin/robotics/forschungsgebiete/infrastruktur-and-tutorials/offene-ressourcen/building-your-own-rbo-hand-3)

- **LEAP Hand**（2023 年，RSS）— 开放低成本的仿人灵巧手设计，展示真实硬件的遥操作、从视频学习和仿真迁移。论文覆盖指定操作任务，可用于与形态优化手做固定平台对照。 [论文](https://arxiv.org/abs/2309.06440)

- **Open Parametric Hand**（2025 年 5 月，Science Robotics）— 发布可调整骨架与肌腱参数的可打印机械手案例，便于用同一制造方法对照不同的手形与抓握行为。实验覆盖研究者制作的形态，开放参数空间还包含大量未测试组合。 [论文](https://infoscience.epfl.ch/entities/publication/ad0430e1-0d8f-4ada-b5f4-98366e7f91d2) · [项目](https://sites.google.com/view/open-parametric-hand/home)

- **ORCA Hand**（2025 年，IROS）— 公布 17 自由度肌腱驱动灵巧手、集成触觉与装配资料。论文给出的材料成本与装配时间基于作者公布的版本和物料条件。 [论文](https://arxiv.org/abs/2504.04259) · [ETH 项目](https://www.orcaprd.ethz.ch/)

- **Data-Driven Inverse Design Enables a Dexterous Hand**（2026 年 6 月，Biomimetics）— 通过已有手部设计与性能数据建立关联，再按目标动态性能设计实物。与人手的比较来自节奏游戏等指定结构化任务，样本量限制了关联模型的外推。 [论文](https://www.mdpi.com/2313-7673/11/6/434)

<a id="s6"></a>

## 步行、四足与人形

- **McGeer，被动动态步行，1990；Collins 等，Science 2005**　早期实物利用腿的自然摆动、重力与惯性，在浅坡上形成稳定步态。后续机器人给步态补充少量能量以支持平地行走。两篇连读可以看出，先选身体的自然动力学，会怎样改变执行器要做的功。[McGeer 论文](https://doi.org/10.1177/027836499000900206) · [Collins 等论文](https://groups.csail.mit.edu/robotics-center/public_papers/Collins05.pdf)

- **MIT Cheetah 3，IROS 2018**　高带宽执行器提供本体感知，关节活动范围支持大步幅；接触检测和步态调度配合地面反力控制。实机仅凭本体感知登上踏步高度 17.8 cm 的楼梯，是传动设计与反馈控制相互支持的例子。[MIT 原论文](https://dspace.mit.edu/bitstream/handle/1721.1/126619/IROS.pdf)

- **Stanford Doggo，ICRA 2019**　3∶1 皮带准直驱配合并联连杆，以电机反馈实现虚拟刚度与阻尼。作者同时给出台架扭矩控制带宽和整机跳跃实验，便于从执行器读到整机行为。[原论文](https://arxiv.org/pdf/1905.04254)

- **PAWS，Nature Machine Intelligence 2025**　把动物的运动协同落实为柔顺的跨关节机械耦合，让四个执行器驱动多种动作。实机受扰时的被动响应，可用于观察哪些调整由身体直接完成。[原论文](https://www.nature.com/articles/s42256-025-00988-x)

- **Chen 与 Aukes，IJRR 2025**　小型四足平台可换腿长、传动比和串并联刚度。以跨形态策略筛选分别适合快速直行、转弯和低运输成本的设计，再制造三种腿并用动捕和电流验证。不同任务偏好不同结构。[论文](https://doi.org/10.1177/02783649251337110) · [项目与数据](https://idealab.asu.edu/curating-legs-web/)

- **DyRET**（2021 年，Nature Machine Intelligence）— 四足实体根据感知的路面调整腿长，按地形选择能耗更低的机械形态。结果来自室内地面与户外试验，在线可调形态限于腿部尺寸。 [论文与代码入口](https://www.nature.com/articles/s42256-021-00320-3)

- **2006 · Bongard 等，连续自建模**　通过主动运动和传感读数推断自身结构，依据估计的结构重合成步态。四足实体在受损后重新生成可用步态。实验验证的是运行时形态识别和策略适应，硬件形态由人预先设定。[Science](https://doi.org/10.1126/science.1135929)

- **2023 · Bjelonic 等，ANYmal 并联弹性**　联合选取膝关节并联弹簧参数和学习式步态策略，通过形态条件控制评价弹性方案。实机在不同地形测试。可调范围集中在膝关节弹性，收益仍需结合步态任务与整机能耗边界解读。[ETH 论文库](https://www.research-collection.ethz.ch/items/4f25b4a9-9135-4da3-973a-09bc7eeb27d5)

- **2024 · Mini Cheetah 鲁棒弹性协同设计**　把地面性质作为随机变量，联合优化顺应性、标称轨迹和反馈策略。论文报告仿真平面 bounding 运输成本下降 58.3%，实机 trot 和 bounding 最高分别下降 17.4% 和 8.3%。任务与验证条件不同，三个数字宜分别引用。[IEEE/ASME](https://doi.org/10.1109/TMECH.2024.3382305)

- **2025 · Dong 等，清华传感化肌骨仿生腿**　用力学模型优化流体驱动人工肌肉的波纹腔壳，在柔性执行器上集成感知，并配套肌骨腿的运动控制。硬件证据集中于人工肌肉与腿部原型。适合作为结构、驱动和感知集成案例，全身地形泛化需要独立证据。[IEEE T-RO](https://doi.org/10.1109/TRO.2025.3567801) · [课题组实机演示](https://www.youtube.com/watch?v=7FFdYinwzSc)

- **2026 · Yu 等，模块化足式 metamachines**　以可独立感知、供电和驱动的单自由度模块作形态单元，优化模块构型并学习各形态运动，策略训练使用实体可获得的本体信号。米级实体在非结构化室外移动，部分设计展示故障后的移动能力。拓扑由模块与装配可行性限定，论文证据不涵盖自行装配所有候选形态。[PNAS 全文](https://pmc.ncbi.nlm.nih.gov/articles/PMC12974426/)

- **2026 · Liu 等，Argus**　依据动态各向同性选取球形放射足构型，分布式足与视觉感知支持不同姿态的移动。20 足实体展示无固定朝向的运动、越过杂乱地形、自稳与部分执行器失效后的运动。极端对称性的收益需与多执行器和多传感器的重量、能耗及维护成本一起评价。[Science Robotics 项目](https://generalroboticslab.com/Argus) · [论文](https://doi.org/10.1126/scirobotics.aec1725)

- **2026 · Lee 等，KAIST RAIBO2**　以续航为系统指标，整合硬件效率与步态控制设计。实机以单次充电完成 42.195 公里赛事。长程完成度属于系统级证据，不能直接归因于单个形态变量。[Nature](https://www.nature.com/articles/s41586-026-11102-5)

- **2026 · Dogger，11 月预印本**　训练形态条件策略后固定其权重，以贝叶斯优化选择三段腿长与两项并联膝弹簧参数。四次试验报告相对标称形态，巡检简化任务及负载运输实机运输成本分别下降 18.6%±1.7% 和 35.7%±3.1%。几何与弹性的单因素对照在仿真中完成，巡检简化成平地直线走停，且仿真巡检上 CPG+CMA-ES 的平均能耗更低。[arXiv](https://arxiv.org/abs/2611.02462)

- **ToddlerBot，CoRL 2025**　开源小型人形把可维修的打印件、柔顺掌部和仿真模型配套设计。实机用强化学习行走、用扩散策略抓握，并把一台机器上学出的操作策略迁移到另一台同款机器。热限制和跌倒后的维修时间也有实测。[项目与实机对照](https://toddlerbot.github.io/) · [论文](https://proceedings.mlr.press/v305/shi25a.html)

<a id="s7"></a>

## 空中运动与栖停

- **2018 在线 / 2019 卷期 · Falanga 等，Foldable Drone**　四臂构型可调整，控制器随形态更新；机载视觉惯性估计支撑形态变化时的闭环飞行。实体自主飞行验证适于狭小空间巡检和近壁观察的构型。形变收益依赖结构、感知和控制随构型变化的一致建模。[UZH 原论文](https://rpg.ifi.uzh.ch/docs/RAL18_Falanga.pdf)

- **2021 · Midair-Reconfigurable Quadcopter**　利用无源铰链与旋翼力完成形态转变，减少变形本身所需的独立执行器。原型演示飞行时变形。与有源变形相比，铰链状态与飞行推力直接耦合，构型可达性和稳定性须共同分析。[原论文](https://arxiv.org/abs/2103.16632)

- **2024 在线 / 2025 卷期 · Xu、Chirarattananon，香港城市大学**　通过被动变形实现常规四旋翼与旋转飞行两种模式，后者可相对独立地控制位置与滚转、俯仰姿态。实物实验验证双模式与姿态控制。适用于研究复用飞行驱动的机械变形，独立姿态控制的结论对应旋转飞行模式。[Advanced Intelligent Systems](https://doi.org/10.1002/aisy.202400464)

- **SNAG，Science Robotics 2021**　着枝冲击通过仿鸟腿传动变成抓力，欠驱动脚爪在 50 毫秒内包住不规则树枝，随后由闭环平衡控制稳定机身。作者改变着陆条件，考察哪些成功区域来自被动抓合、哪些需要主动平衡。[原论文](https://pubmed.ncbi.nlm.nih.gov/34851710/)

<a id="s8"></a>

## 软体与水下机器人

- **Scalable Sim-to-Real Transfer of Soft Robot Designs**（2019 年预印本，2020 年 IEEE RoboSoft）— 构建开放的体素软体设计与制造套件，制作了 108 种形态并对其中九种测量行为迁移。某些形态的性能排名相近，实物却会以不同方向和接触方式运动。 [会议论文](https://www.eng.yale.edu/faboratory/publications/conference/2020/Kriegman%20et%20al.%20-%202020%20-%20Scalable%20sim-to-real%20transfer%20of%20soft%20robot%20designs.pdf) · [全文](https://arxiv.org/abs/1911.10290)

- **A Soft Robot That Adapts to Environments Through Shape Change**（2021 年 1 月，Nature Machine Intelligence）— 在仿真中寻找适用于平地和斜坡的软体形状与步态，在同一实体中复现两种运动模式。实物证据来自两类对应测试环境。 [论文](https://www.eng.yale.edu/faboratory/publications/journal/2021/Shah%20et%20al.%20-%202021%20-%20A%20soft%20robot%20that%20adapts%20to%20environments%20through%20shape%20change.pdf)

- **2021 · Li 等，浙江大学团队深海软体鱼**　仿深海狮子鱼分散电子元件并嵌入柔性基体，材料、封装、驱动和能量系统共同适应高压。马里亚纳海沟 10,900 米在着陆器上验证鳍片驱动，南海 3,224 米验证自由游动。两个深度对应不同部署方式。[Nature](https://www.nature.com/articles/s41586-020-03153-z)

- **2025 · Pan 等，浙江大学 × 中国科学院深海所**　双稳态手性超材料和封管形状记忆合金结合，形态转换支撑游动、滑翔和爬行。在海马冷泉约 1,380 米及马里亚纳海沟约 10,600 米随载人潜器部署并取回。现场证明多模态可行，长期自主任务与续航需要另外验证。[Science Robotics](https://doi.org/10.1126/scirobotics.adp7821)

- **2025 · 可移动且可感知的磁驱动软体微机器人**　结构通过多足形态承载磁驱动运动，并利用结构与摩擦电机制产生感知信号。展示同一软体结构兼顾移动和感知，实验依赖外部驱动与所测条件。深圳北理莫斯科大学等中国团队参与。[npj Flexible Electronics](https://doi.org/10.1038/s41528-025-00437-0)

- **SoFi，Science Robotics 2018**　软尾用液压摆动推进，浮力控制支持下潜，潜水员用声学指令选择运动状态。在珊瑚礁的实地试游展示了这套组合怎样支持近距离水下观察，指令来自人。[MIT 项目与论文](https://www.csail.mit.edu/research/sofi-soft-robotic-fish)

- **RAD 折纸采样器，Science Robotics 2018**　连杆把一个旋转执行器的运动分到十二面体各面，遥控潜器只需一个开合指令就能围住脆弱生物。论文报告下潜至 700 米测试，机械联动减少了操作员要同时控制的自由度。[原论文与海试](https://pubmed.ncbi.nlm.nih.gov/33141728/)

<a id="s9"></a>

## 传感器布局与形态估计

- **2026 · 山东科技大学，软蛇形机器人的实时形态估计**　分布式微惯性传感器与连段坐标重建配合，通过补偿传感器安装偏差估计三维状态。不同尺寸比例柔性臂及蛇形实体的静动态试验证明估计可行。研究重点是感知和结构适配，任务驱动的传感器布局及控制全局优化留待独立验证。[Mechanical Sciences](https://ms.copernicus.org/articles/17/983/2026/ms-17-983-2026.html)

- **2021 · Spielberg、Amini 等，任务与传感位置共同学习**　用可微稀疏传感选择层同时优化传感位置与下游任务模型，覆盖触觉和本体感知。六种软体形态提供算法验证，并展示运动子空间与控制应用。形态在各实验中既定，对实体精度的外推还受候选传感位置和训练分布约束。[IEEE RA-L](https://ieeexplore.ieee.org/document/9345345)

- **2026 · Model-Free Co-Optimization of Manufacturable Sensor Layouts and Deformation Proprioception**　用变形数据联合选择长度传感器数量、长度、位置与形状预测网络，将可制造性纳入损失。报告优于未优化布局的预测精度。数据须覆盖部署后的变形方式，预测精度与闭环任务表现仍需分别评估。[IEEE](https://ieeexplore.ieee.org/abstract/document/11455383) · [预印本](https://arxiv.org/abs/2603.10059)

- **2026 · Observability-Informed Optimal Sensor Placement for Soft Robots**　用可观测 Gramian 指标表征动力学与布局耦合，通过凸优化选取传感配置。预印本报告用软体连续臂进行位置与应变传感实验。结论依赖动力学近似和实验激励所覆盖的工作域，尚需跨平台验证。[arXiv](https://arxiv.org/abs/2609.33681)

<a id="s10"></a>

## 形态搜索与可微设计

- **Embodied Intelligence via Learning and Evolution / DERL**（2021 年，Nature Communications）— 用外层形态演化和内层强化学习研究地形复杂度如何影响虚拟生物的结构与行为学习。证据来自大规模仿真与后续任务，覆盖的是 UNIMAL 形态空间。 [论文与代码入口](https://www.nature.com/articles/s41467-021-25874-z)

- **DiffHand**（2021 年 7 月，RSS）— 用形变参数化表示关节机构，以可微刚体接触仿真联合优化几何、动力学参数与控制。作者制作了代表性的 3D 打印操作器，证据覆盖论文中的接触操作任务。 [项目、论文与代码](https://people.csail.mit.edu/jiex/papers/DiffHand/)

- **Text2Robot**（2024 年 6 月预印本，2025 年 ICRA）— 文本生成网格作为初始结构，再用几何处理及身体与步态协同优化构建可制造四足机器人。作者展示了能走的实物，硬件与形态搜索限定在其四足平台。 [论文](https://ieeexplore.ieee.org/abstract/document/11128168) · [项目与硬件手册](https://generalroboticslab.com/Text2Robot/)

- **DASH 软体灵巧手协同优化**（2024 年 3 月预印本）— 遗传算法和策略迁移在仿真中评估了 396 种手形，随后打印两个优化设计。实物拾取与重定向使用遥操作，检验的是形态而非学习策略的直接部署。 [论文](https://arxiv.org/abs/2403.09933)

- **Lang2Morph**（2025 年 9 月首版预印本）— 把自然语言任务转成 Open Parametric Hand 的结构语法和可打印参数，再按语义匹配与尺寸筛选候选。更新版用三种实物手交叉测试抓卡片、操作螺丝刀和负重，证据覆盖少量代表性形态。 [论文](https://arxiv.org/abs/2509.18937)

- **HandCDO**（2026 年 4 月预印本）— 联合搜索手掌、指运动学、指尖曲率和抓取构型，局部接触曲面也参与优化。仿真按抓取稳定性评分。三种实物手安装在机械臂上执行搅拌、敲击和切割，测量工具相对手掌的滑转。 [论文](https://arxiv.org/abs/2604.27557) · [项目](https://www.aminmirzaee.com/HandCDO/)

- **Task2Hand / SAGE Hand**（2026 年 11 月 20 日预印本）— 从任务描述生成参数化手形，用接触与碰撞检查筛选设计，再打包 URDF、MJCF、强化学习评测和设计记录。论文在三种物体上开展对照，触觉和操作结果来自仿真。 [论文](https://arxiv.org/abs/2611.27967)

- **1994 · Sims，Evolving Virtual Creatures**　进化搜索同时编码刚体连接和神经控制，按游动、移动等任务评估。三维仿真出现多种运动策略。搜索受奖励定义和物理近似影响，作者还记录了利用仿真漏洞的解。[SIGGRAPH](https://doi.org/10.1145/192161.192167) · [作者演示](https://www.karlsims.com/evolved-virtual-creatures.html)

- **2000 · Lipson、Pollack，演化与自动制造**　在受限物理仿真中演化机械结构与控制网络，再将设计自动制造并安装执行部件。打印出的实体原型实现移动。零件库和任务均较简单，制造过程仍需装配执行部件。[Nature](https://www.nature.com/articles/35023115)

- **2019 · ChainQueen**　可微 MLS-MPM 仿真允许对软材料动力学及控制计算梯度，可用于设计和控制相关优化。报告前向与梯度精度和案例效率。材料辨识、实物制造误差和接触模型仍影响仿真最优解能否迁移。[论文](https://arxiv.org/abs/1810.01054)

- **2020 · RoboGrammar**　图文法把零件及装配约束写入候选空间，图启发式搜索筛选拓扑，以控制求解后的地形表现评价设计。多地形仿真出现不同足数和构型。结果说明预先定义的部件和连接约束如何引导搜索，尚需实物对照验证收益。[MIT 项目与论文](https://people.csail.mit.edu/jiex/papers/robogrammar/)

- **2021 · Evolution Gym**　体素材料和执行器位置形成形态空间，在统一任务环境内比较进化、搜索和控制学习方法。多个移动与操作任务提供可重复的仿真基线，高维空间的搜索仍是瓶颈。二维体素模型适合算法对照，制造与真实顺应特性须另验。[NeurIPS](https://papers.neurips.cc/paper_files/paper/2021/hash/118921efba23fc329e6560b27861f0c2-Abstract.html)

- **2023 · CuCo，清华深研院 × 腾讯 AI Lab**　逐级扩展体素设计空间，通过神经元胞自动机生长形态，通过自注意力控制策略共享不同构型的经验，每阶段同步更新设计和控制策略。仿真中相对从目标尺寸直接开始训练的基线，更高效地产出较大构型。结论适用于所测体素任务，尚无实物性能证据。[ICLR](https://openreview.net/pdf/13ac2fc1c4bb6b380af8507b9524a58b2144432e.pdf)

- **2021 · DiffAqua**　用 Wasserstein 重心插值参数化软体游动机器人的连续形状，通过可微仿真联合优化几何和控制。仿真中以较少仿真调用得到有竞争力的游动设计。几何空间由模板约束，仿真收益需做流体与材料实物校验。[MIT 项目及论文](https://diffaqua.csail.mit.edu/)

<a id="s11"></a>

## 人机协作与特殊作业环境

- **微重力壁虎抓手，Science Robotics 2017**　用切向载荷开关干黏附，均载机构将多个小黏附片连成大面积抓手，过载时手腕被动让位。作者在微重力下抓放平面及曲面物体，用材料和机构解决轻推就会漂走的难题。[原论文](https://pubmed.ncbi.nlm.nih.gov/33157899/)

- **个性化踝外骨骼，Nature 2022**　先用实验室模拟器确定助力需求，再据此选择便携设备的电机与绳传动。利用穿戴者自然行走时的运动数据调节助力。与穿普通鞋相比，作者报告自选步速增加 9±4%，单位距离耗能下降 17±5%；结果对应个性化优化后的整套设备。[原论文](https://pubmed.ncbi.nlm.nih.gov/36224415/)

- **腹腔镜机器人开放平台，2026**　远心运动约束要求器械绕穿刺点运动。作者在工业机械臂的笛卡尔速度控制器内解析地满足该约束，使遥操和策略执行共用接口；用组织模型及动物实验评估器械运动和肠组织牵拉。证据对应研究平台。[项目与验证条件](https://surgical-robot-testbed.github.io/iros_testbed_paper/) · [论文](https://arxiv.org/abs/2603.08490)

- **A Soft Neuroprosthetic Hand Providing Simultaneous Myoelectric Control and Tactile Feedback**（2021 年 8 月，Nature Biomedical Engineering）— 以肌电命令驱动 292 克柔性充气假手，并将指尖接触传给佩戴者。两名上肢截肢志愿者参加实验室任务，样本不足以支持长期临床结论。 [作者论文](https://softrobotics.sjtu.edu.cn/pdf/Guoying_NBE_2021.pdf) · [MIT 试验说明](https://news.mit.edu/2021/inflatable-robotic-hand-tactile-0816)

## 补充条目

欢迎通过 issue 或 pull request 推荐论文、技术报告或可复现的工程项目。请附一手链接，并注明改动了什么、在哪项实验中验证。
