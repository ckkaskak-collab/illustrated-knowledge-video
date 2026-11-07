---
name: illustrated-knowledge-video
description: "将定稿文案或已有配音制作成插画知识视频：A-roll 用生成图片逐张定帧演绎铺垫、情绪与衔接，B-roll 用图形、图片和动效联动讲解干货。沿用已确认角色与简洁二维信息图风格，默认使用 Remotion，支持分镜、声学对齐、字幕、整片交付与续做。"
---

# 插画知识视频

本包内置角色原图、Ian 风格参考、B-roll 模板和执行脚本，基础能力可独立安装；B-roll 视觉参考 baoyu-infographic 方法，动效与音效分别按本机 video-shotcraft、sound 协作。缺少协作能力时明确报告，不声称已调用。安装与环境见 [README](README.md)，来源与许可边界见 [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)。

## 制作引擎

后续线条小人视频默认使用 Remotion 制作可编辑画面、整片时间轴和 MP4，执行 [Remotion 工作流](references/remotion-workflow.md)。ChatCut 仅用于用户明确指定的任务或明确保留的旧工程续做。包内原始提示词、模板、README 中的 ChatCut 流程属于可选旧分支，不能覆盖此默认选择；原始提示词保持不变，其工具接口按所选引擎适配。

## 开始本次任务

1. 先读取用户提供的文案、音频及已有 `project-state.json`，判断本次范围是方案、素材、整片、修改还是封面。按已授权范围连续执行；不为每镜重复提问。
2. 首次使用运行 `python3 scripts/doctor.py`。它检查本地包与可选 Python 依赖；图像生成、ChatCut 的登录/权限/费用仍由当前宿主工具核对。维护 Skill 不调用 TTS、生图或渲染。
3. 已有配音直接保留。需要新配音时按项目选择配置豆包；默认新合成 `speech_rate=15`，不再二次加速。没有音频可以做内容与动作方案，不能编造实测时长。
4. 优先沿用项目已选角色。延续彩色四人组（橙衣主角、紫衣女生、蓝衣男生、小猫）时读取 [角色绑定与三视图](references/character-binding.md)，按出场角色传入参考；未指定角色时使用 [包内原图](assets/character/reference.jpg)。若用户指定自己的角色，将其保存在项目并记录路径，替代角色参考和对应身份描述。每次生图都实际查看并传入选定参考。
5. 新项目使用 `python3 scripts/init_project.py --script <定稿.txt> --output <新项目目录>`，可加 `--audio <已有音频>`；它保存输入与续做结构，不自动触发外部付费操作。输入音频可由任意已获授权的来源提供。

## 画面分工与导演目标

视觉编排前读取 [A/B-roll 叙事与动作设计](references/visual-storytelling.md) 及其中的用户参考图。A/B 的分工用于区分内容层次、丰富表现方式：

- **A-roll 定帧图片负责场景演绎。** 铺垫、经历、情绪和衔接段落，用 Codex 图像生成工具直接输出的完整场景图逐张静止展示，以图片之间的状态变化组成小戏。执行 [A-roll 定帧展示规则](references/aroll-ian.md#已选动作方式关键状态图切换)，不添加 MG 或图片内部动画。
- **B-roll 视觉动效负责干货讲解。** 围绕当前知识关系，让图形、图片或真实素材与动作相互对应，呈现比较、筛选、拆解、因果或变化过程。

先明确这段文案的作用、观众要看懂什么及主体怎样变化，再选素材和模板。A-roll 检查动作与结果是否成立，B-roll 检查知识关系是否被画面解释出来；换姿势、逐项入场和配色通过只是局部检查。按语义选择 A/B，不设固定比例或轮换顺序。参考图用于校准分工，角色与配色沿用当前默认；更换画风以用户的明确选择为准。

B-roll 分镜与质量修订先读 [段落设计与具体范例](references/broll-sequence-design.md)：先组织连续讲解中的问题、案例与可见证据，再落到单镜。把设计写进已有九列表与素材清单，不增加逐段审批。给定文案和配音时在原内容内设计；缺少必要论据或案例时明确缺项，不为套参考片结构擅自改稿。

使用当前彩色角色组时，A-roll 按 [三人组场景设计](references/aroll-cast-design.md)组织橙衣主角、紫衣女生与蓝衣男生的意图、行动和反应；按本段需要选人，小猫作为可选搭档。造型绑定与人物搭戏分别检查，避免只把立绘放进画面。

## 已确定的默认风格

- A-roll：默认白底、黑线留白，项目已确认的角色与画风优先。用必要数量的独立完整图片表现处境、行动与结果，每张定帧停留，直接切换下一张。详见 [A-roll 接口](references/aroll-ian.md)。
- B-roll：采用 baoyu-infographic 方法组织讲解层；近白底、轻线条、清楚的文字层级与充分留白，强调色集中于当前重点。真实素材、成品演示、局部细节与图形解释按内容组合，保留主体必要的颜色、质感和可辨细节。制作前查看 [规范和确认图](references/broll-visual-style.md)，再用 video-shotcraft 适配动效、sound 选取音效。
- 当前 B-roll 信息图版不自动添加讲解头像；用户要求或旧工程明确保留时，读取[圆形讲解头像](references/broll-narrator.md)。A-roll 不显示。
- 平台识别优先用真实品牌标识；多服务连线分行、分落点；股价变化用逐步绘制的折线表达。素材来源、数据与示意边界见[视觉规范](references/broll-visual-style.md)。
- 布局修订沿用已确认的信息图风格：箭头尖端分开、目标文字对齐箭头、同组短句紧凑排列；画面默认不显示素材来源或制作说明。具体规则见视觉规范，出处保存在本地清单。
- 先确定知识关系和动作，再检查完整布局并制作动画。[包内模板](assets/broll/templates/index.json)按语义匹配，保留适用的骨架并按真实配音重设锚点；不适用时自行设计，记录实际来源。
- 逐项讲解时，框线、文字、数值、底条和相关连线作为整组，随对应口播依次出现；尚未讲到的组完整隐藏。执行[整组随口播出现](references/broll-editable.md#整组随口播出现)，并按[逐项出现检查](references/captions-and-delivery.md#逐项出现检查)核对合成及编码后的画面。用户指出一处同类问题时，检查全片相关镜头及共用组件。
- 画布默认 1920×1080、30 fps；已有工程沿用实际规格。新项目的字幕、字体、音色和片尾选择写入项目记录。没有指定片尾时不附加其他 IP 的片尾。
- 字幕默认以原稿标点和完整语义确定换屏，去除显示标点，每屏严格一行；短词和连续列举避免频繁闪切，短停顿保持到下一条，切镜不打断字幕。保留真实发声记录与独立显示区间，执行 [字幕规则](references/captions-and-delivery.md#字幕切分与显示)。
- 标题字体可先试 Ma Shan Zheng，字幕可先试 Noto Sans SC；每个目标工程查询实际可用字体并检查合成字形，名称相同也不能替代渲染检查。

## 原文与执行规则

X 的六段提示词和飞书 2.0 的两段提示词完整保存在 `references/original-prompts/`。来源、原版本和哈希见 [来源清单](references/source-manifest.json)。先运行 `python3 scripts/verify_sources.py`，不以重算基准掩盖原文变化。

执行某阶段时完整读取对应原文。具体输入、角色、配色、工具接口和本包补充规则放在原文外，不改写原文。默认视觉编排采用飞书 2.0，并按本包的 A/B 叙事分工填写画面设计与动态变化；X 02 留作可选原路线。A-roll 使用包内角色接口，X 03/04/05 作为角色三视图或原路线的可选参考，不同时强制注入。

A-roll 的“动态变化”填写图片状态变化、切图锚点与停留，不填写图片内部动画。原文、模板及旧流程中的运动或转场建议不得覆盖当前定帧展示规则；B-roll 继续按自身动效规范执行。

以下调度是本包补充：只请求分镜时到分镜结束；用户要求整片时，分镜完成后继续已授权的制作。单独请求挑动效时提供方案供选择；已授权整片时自行选合适模板并记录，不逐镜重问。外部费用按用户已有预算和授权执行，不能把原文“使用 Codex 额度”解释为第三方服务免费。

## 按阶段读取

| 阶段 | 读取 | 执行与交付 |
|---|---|---|
| 配音与对齐 | [X 01](references/original-prompts/x/01-voice-alignment.txt)、[时间和配音](references/timing-and-handoff.md)、[本地脚本](references/local-tools.md) | 整段合成或保留音频；保存原始 ASR、按定稿核对的短语表和连续编排表 |
| 视觉编排 | [叙事与动作设计](references/visual-storytelling.md)、[飞书编排 2.0](references/original-prompts/feishu/visual-storyboard-v2.txt) | 先确定段落问题、贯穿案例与可见证据；九列表中写明本镜作用、动作前后状态和承接对象；镜头结束节拍点、逗号数值、所缺素材；内部变化绑定真实短语/词锚点 |
| A-roll | [角色动作接口](references/aroll-ian.md)；彩色组同时读取 [三人组场景设计](references/aroll-cast-design.md) | 先选角并设计人物互动，再独立生成完整定帧图；保持身份、站位、视线与道具连续，核对行动、反应和结果 |
| B-roll | [段落设计与范例](references/broll-sequence-design.md)、[视觉规范](references/broll-visual-style.md)、[可编辑实现](references/broll-editable.md)、[X 06](references/original-prompts/x/06-broll-motion.txt) | 准备能支撑局部、变化与比较的素材；先完成代表性连续讲解段，核对解释证据与衔接，再扩展适用做法；按口播推进可编辑对象与整组出现；需要头像时另读其规范 |
| 整片剪辑 | 默认 [Remotion 工作流](references/remotion-workflow.md)；仅明确使用 ChatCut 时读取 [ChatCut 接口](references/chatcut-workflow.md) 和 [飞书剪辑 2.0](references/original-prompts/feishu/chatcut-editing-v2.txt) | 按选定引擎完成可编辑时间轴及两份制作清单；默认交付 Remotion 源工程 |
| 字幕与交付检查 | [字幕与成片](references/captions-and-delivery.md) | 核对最终 Card、渲染画面和 SRT；保存源码与实例参数；分别报告抽帧、播放、听审、导出 |
| 配乐与音效 | [声音后期](references/audio-postproduction.md) | 音效使用 sound 搜索 Freesound，配乐沿用项目选择；记录来源、混音和实际听审状态 |
| 封面 | [封面分支](references/covers.md) | 用户要求时制作独立比例的封面；标题与概念画面不改变正文事实 |

## 续做和真实交付

续做先看项目记录，再核对实时工程。静态资产、上轨、合成抽帧、连续观看、连续回听、编码导出是不同状态，各自记录证据。新配音或音频剪辑后重新对齐；只替换配乐时沿用已确认的人声、画面和字幕。

交付分别列出原生可编辑工程、本地源素材与代码、MP4、SRT、封面，以及确实取得的 NLE 包。云端链接、源码 ZIP、扁平 MP4 不能互相替代。缺少外部工具或材料时完成不受影响的部分，标明具体缺项，不把准备完毕写成视频已经完成。
