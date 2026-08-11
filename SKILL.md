---
name: aigc-film-studio
description: "This skill should be used when producing AI-generated films, short dramas (短剧), comic dramas (漫剧), short videos (短视频), or video clips — for models like Nano Banana, GPT Image, Seedream, Seedance, Kling, Veo. It is an end-to-end AIGC production system: it takes a script or idea and produces character/location/prop asset sheets, shotlists, structured video & image prompts (CINEDANCE / LIRA), living performance writing (ACTING), the Style Prefix, GEO spatial locking, the SCALE LAW, and QA. Trigger on requests to: make an AI film / short-drama / comic-drama / short-video, write video/image prompts, turn a script into a shotlist, keep a character consistent across shots, parse 人物/场景/道具, generate 画面/视频, or fix consistency / teleport / drift / dead-face problems."
description_zh: "AIGC 电影/短剧/漫剧/短视频全流程制片系统：从剧本或想法出发，解析人物/场景/道具，生成资产表、分镜表与视频/图像提示词（CINEDANCE/LIRA/ACTING），支持外部工具（Seedance/Kling/Veo 等），含一致性锁定（GEO/Style Prefix/SCALE LAW）与质检。触发于：AI 拍电影/短剧/漫剧/短视频、写视频/图像提示词、脚本转分镜、角色一致性、生成画面/视频、修复换脸/瞬移/死脸/漂移。"
version: 3.2.0
tags: [AIGC, AI电影, AI短剧, 漫剧, 短视频, 竖屏视频, 视频生成, 图像生成, 提示词工程, 角色一致性, 分镜, 脚本转视频, Seedance, 文生视频, 图生视频, AI-filmmaking, short-drama, prompt-engineering, character-consistency, shotlist]
keywords: [AI电影制作, AI短剧制作, 短视频生成, 抖音视频, 视频号视频, 视频提示词, 图像提示词, 角色一致性, 人物场景道具解析, 脚本转分镜, AIGC制片, video prompt, image prompt, character consistency, AI film pipeline]
agent_created: true
---

# AIGC Film Studio — AIGC 电影 / 短剧 / 漫剧 / 短视频制片系统

一套从一部戛纳 2026 展映的 95 分钟全 AI 生成院线长片的制作实战中提炼、可直接复用的 AIGC 视频生产体系。**加载本 Skill，agent 能从一句想法或一段剧本，一路走到可交付的成片**：解析人物/场景/道具 → 锁定资产 → 出分镜 → 写提示词 → 生成 → 质检 → 后期。核心解决视频模型最致命的问题：**一致性（consistency）**。

## 核心心智模型

> **视频模型没有记忆。** 它不记得上一镜谁站在哪、穿什么。每一镜都必须把「完整描述 + 参考图」逐字喂进去，否则角色换脸、场景崩坏、人物瞬移。本 Skill 的全部规则都因「某一帧失败」而生。

## 三种使用模式（入口即分流）

| 模式 | 用户说什么 | agent 怎么做 |
|---|---|---|
| **A. 全套制片** | 「帮我做个短剧/短片/电影」「把这段剧本做成视频」 | 走 §端到端主工作流（12 阶段，含需求澄清阶段 0），从建项目目录开始 |
| **B. 单点支援** | 「帮我写这条视频提示词」「这个角色总换脸」「审一下这段表演」 | 直接路由到对应 reference / 清单，不建项目 |
| **C. 提示词包交付** | 「给我提示词，我自己去 Seedance 生成」 | 只产出标准化提示词包 + 资产图包 + UI 参数清单 |

判断不清时，问一句用户的**体裁、生成渠道、时长规模**（见 `01-pipeline-runbook.md` §2），再分流。

**单点支援路由表**：

| 用户说什么 | 加载哪个 reference |
|---|---|
| 写视频提示词 / Seedance 提示词 / 视频 prompt | `references/10-cinedance-video-prompt.md` |
| 写图像提示词 / 画图 prompt / NBP/Seedream 提示词 | `references/12-lira-image-prompt.md` |
| 角色表演 / 演技 / 人物太僵 / 死脸 | `references/11-acting-performance.md` |
| 角色换脸 / 一致性 / 瞬移 / 跳轴 | `references/20-qa-checklists.md` + `assets/templates/geo-spatial-layout.md` |
| 全流程 / 制片怎么做 | `references/00-overview-handbook.md` + `references/01-pipeline-runbook.md` |

## AI 导演（从任何输入到分镜）

用户给一句标题、一段大纲、或完整剧本，都能转为 AIGC 可拍的分镜结构：

| 输入级别 | 用户给什么 | AI导演做什么 |
|---|---|---|
| L1 标题/主题 | 一句话（如"雨天旧书店发现旧信"） | 创意扩展→完整故事→分镜 |
| L2 简要大纲 | 3-5句故事大纲 | 结构补全→场景细化→分镜 |
| L3 详细剧本 | 完整剧本/小说片段 | 直接解析→场景块切分→分镜 |

详见 `references/14-ai-director.md`。在12阶段管线中位于阶段0.5（需求澄清后、剧本解析前）。

## 端到端主工作流（模式 A · 12 阶段，含需求澄清阶段 0）

详细操作规程、每阶段交付物门禁、项目目录脚手架见 `references/01-pipeline-runbook.md`。压缩版：

| # | 阶段 | 关键动作 | 用哪个模板 / reference |
|---|---|---|---|
| 0 | 需求澄清 | 定体裁/时长/画幅/渠道/风格 | runbook §2 |
| 1 | 剧本解析 | 切场景块（地点×时间×状态） | runbook §3 |
| 2 | 资产清单注册 | 穷举角色/地点/道具 + @tag 词典 | `assets/templates/asset-registry.md` |
| 3 | 资产图生成 | 角色表三图/地点 3/4 视角/道具多版本 | `assets/templates/character-sheet.md` 等 + `12-lira` |
| 4 | 压力测试锁定 | 10/10 可识别、同框不崩、锁声音+行为主档 | handbook §3.5–3.7 |
| 5 | 分镜表 | 按块出 shotlist，一镜一动作 | `assets/templates/shotlist.md` |
| 6 | 逐镜提示词 | 16-block + GEO + Style Prefix，过生成前审查 | `assets/templates/shot-prompt-skeleton.md` + `10-cinedance` + `20-qa` |
| 7 | 生成 | 外部工具路由（见下） | runbook §5 |
| 8 | 迭代 | surgical 一次一行，10–15 次不成则简化镜头 | `assets/templates/iteration-log.md` |
| 9 | 清理 | slop 图鉴对照清零，脸手优先 | `20-qa-checklists.md` Part C |
| 10 | 调色声音 | 统一 look、连续 ambience、音乐后期加 | handbook §7 |
| 11 | 交付归档 | 成片 + 可复拍任何一镜的项目文件 | runbook §6 |

## 生成渠道路由（阶段 7）

- **外部工具（Nano Banana / GPT Image / Seedream / Seedance / Kling / Veo 等）**：交付提示词包。每镜一个 16-block 提示词文件（按用户输入语言生成） + 资产图包（文件名=@tag）+ UI 参数清单（画幅/时长/分辨率，绝不写进提示词文本）+ 每镜 2–3 行摘要（用户语言，只给人看，不进提示词）。
- 详见 `references/01-pipeline-runbook.md` §5。

## 交付物体系

本 Skill 产出五类交付物，统一组织到项目目录：

| 交付物 | 内容 | 文件位置 |
|---|---|---|
| 资产生图提示词 | 每个角色/地点/道具的 LIRA 优化图像提示词 | 01-assets/*/`<tag>_image_prompt.md` |
| 分镜首帧生图提示词 | 每镜一张首帧参考图提示词（图生视频输入） | 04-prompts/image/`shot_<NNN>_frame.md` |
| 分镜视频提示词 | 每镜 CINEDANCE 16-block 视频提示词 | 04-prompts/video/`shot_<NNN>_v<N>.md` |
| 参考图清单 | 每镜用哪些参考图、上传顺序 | 04-prompts/reference_manifest.md |
| 交付物总清单 | 文件索引 + 检查表 | 08-delivery/deliverable-manifest.md |

详见 `references/13-deliverable-system.md`。

## 体裁适配（电影 / 短剧 / 漫剧 / 短视频）

| 维度 | 横屏电影感 | 横屏短剧 | 漫剧 | 竖屏短视频 |
|---|---|---|---|---|
| 画幅（UI 设） | 16:9 | 16:9 | 16:9 或 9:16 | 9:16 |
| 单镜时长 | 8–12s | 5–10s 切更狠 | 4–8s | 3–8s，前 3 秒必钩子 |
| Style Prefix | 原版逐字 | 原版逐字 | 漫画风格变体，保留三条根 | 可降格，但保留 skin/acting/continuity 三条根 |
| 首帧 | wide establishing | wide establishing | 场景全景或人物半身 | medium portrait（非传统 wide） |
| 节奏 | 沉稳，给情绪时间 | 快切，推进叙事 | 分镜感强，panel 式构图 | 极快，前 3 秒钩子生死线 |
| 字幕 | 后期加 | 后期加 | 后期加 | 后期加（绝不生成文字） |

**时长优化**：单镜时长不按体裁固定，而是根据动作复杂度、情绪重量、对白长度、镜头运动、叙事节奏五因素综合决策。同时感知模型能力（Seedance 2.5=30s / Seedance 2.0=15s / Kling 3.0=15s / Veo 3=8s）。视频模型选用前必须询问用户。详见 `references/13-deliverable-system.md` §2。

**铁律：体裁只改节奏与风格参数，不改一致性纪律。** 详表见 runbook §4。

## 语言路由（提示词语言 = 用户输入语言）

> **核心原则**：提示词语言始终跟随用户在 agent 中输入的语言——不因目标工具改变。

| 用户输入语言 | 提示词语言 | 说明文字语言 |
|---|---|---|
| 中文 | **中文** | 中文 |
| 英文 | **英文** | 英文 |
| 日文 | **日文** | 日文 |
| 其他语言 | **对应语言** | 对应语言 |

- 16-block 骨架的 block 名称始终用英文（SCENE CONTEXT, ACTIVE REFERENCES 等）
- block 内容用用户输入语言填写
- 技术标签（Photorealistic. NON-IP. 等）始终用英文
- @tag 始终用英文（`@mei`, `@loc_bookstore` 等平台原生句柄）
- 镜头语言库始终用英文（`47° diagonal field of view` 等模型固定理解短语）
- 详见 `references/13-deliverable-system.md` §4

## 视频模型选用（Ask User First）

> **铁律：视频模型选用前，必须先询问用户。**

当前主流视频生成模型及核心差异：

| 模型 | 厂商 | 单次最大时长 | 核心优势 |
|---|---|---|---|
| Seedance 2.5 | 字节跳动 | 30秒 | 长叙事、多参考图、真人感 |
| Seedance 2.0 | 字节跳动 | 15秒 | 多镜头叙事、角色一致性 |
| Kling 3.0 | 快手 | 15秒 | 物理精确、角色一致性 |
| Kling 3.0 Omni | 快手 | 15秒 | 原生音画同步、唇形同步 |
| Veo 3 | Google | 8秒 | 原生音频生成、电影级画质 |

- 用户未指定时，默认推荐 Seedance 2.5（时长上限最大，多参考图一致性最强）
- 详见 `references/13-deliverable-system.md` §2 视频模型选用流程

## 图像模型推荐

当前主流图像生成模型：

| 模型 | 厂商 | 最擅长 |
|---|---|---|
| GPT Image 2 | OpenAI | 极致照片真实感、提示词遵循 |
| Nano Banana Pro (NBP) | Google | 帧编辑（永远首选）、文字渲染、道具 |
| Nano Banana 2 | Google | 文字渲染、角色一致性、信息图 |
| Seedream 5.0 Pro | 字节跳动 | 图层分离、商业视觉、与 Seedance 配合 |

- 图像模型路由由 LIRA 4-D 方法论自动决定（详见 `references/12-lira-image-prompt.md`）
- 角色生成 → GPT Image 2 / Nano Banana 2；地点 → GPT Image 2 / Seedream 5.0 Pro
- 详见 `references/13-deliverable-system.md` §2 图像模型能力感知表

## 失败现象对照表（出问题先查这里）

| 失败现象 | 错误码 | 根因 | 解法所在 |
|---|---|---|---|
| 角色换脸 / 换衣 | `F-ID-DRIFT` / `F-STATE-DRIFT` | 描述不完整、参考被误用、正面图未去头 | handbook §3 + `20-qa` Part C#5 |
| 人物瞬移 / 跳轴 | `F-AXIS` / `F-SPATIAL-RESET` | 缺 GEO / 缺首秒 wide / 切后未重述位置 | `templates/geo-spatial-layout.md` + `20-qa` C#6 |
| 表演像死人 / 假 | `F-PERFORMANCE` | 写感受非行为、脸无眼神光 | `11-acting` + `20-qa` C#4/#13 |
| 图像崩坏 / 多指 / 文字乱码 | `F-MATERIAL` / `F-AUDIO-POLLUTION` | 模型弱点未规避 | `12-lira` + `20-qa` C#1–3 |
| 巨人越画越矮 | — （SCALE LAW） | 缺尺度锚点 | SKILL §SCALE LAW + `20-qa` C#8 |
| 多人 / 克隆家具 / 自带配乐 / 自创台词 | `F-DUP-SUBJECT` / `F-PROP-DUP` / `F-AUDIO-POLLUTION` / `F-DIALOGUE-TEXT` | 约束缺失 | `20-qa` C#10–12 |
| 塑料皮 / 对称脸 | `F-MATERIAL` | 图像整张二次过模型 | `20-qa` C#7（点修改铁律） |

完整质检关：`references/20-qa-checklists.md`（生成前 Part A/B，生成后 Part C，修复路由 Part D）+ `references/31-failure-codes.md`（33 错误码 + 责任层决策树 + 复测纪律）。

## SCALE LAW（尺度锁定法）

> **问题**：视频模型没有尺寸记忆。一镜里巨人是 30 米，下一镜悄悄缩回 2 米——因为没有参照物，模型默认把一切拉回人高。

**规则：凡出现超大 / 超小 / 非标尺度角色或物体，每镜提示词的 POSITIVE CONSTRAINTS 段必带「尺寸对比 + 人形参照物」双锚。**

模板（填入实际数值）：
```
POSITIVE CONSTRAINTS
THE SCALE LAW — VISIBLE PROOF IN THE PICTURE: <对象> stands <实际高度> tall —
<一个可感知的尺寸类比，如 his palm is as wide as a family car>,
and <参照人> at his foot reaches just above the ankle.
In every frame <对象>'s silhouette is at least <N> TIMES the height of the human figure beside him,
and the frame cannot hold both his feet and his head at once.
A <对象> that reads as a large man, or fits comfortably in frame next to a standing human = failed shot.
```

**要点**：
- 尺寸类比用日常物体（车 / 门 / 树），不写数字外的抽象描述。
- 人形参照物必须在画面里，不能只写文字说「旁边有人」。
- 范例见 `00-overview-handbook.md` §6 Hack #4。

## 即抄即用模板（assets/templates/）

| 模板 | 用途 |
|---|---|
| `project-structure.md` | 项目目录结构 + 命名规范（开工先建） |
| `asset-registry.md` | 资产注册表 + @tag 命名词典 |
| `character-sheet.md` | 角色表：三图规范 + descriptor + 状态变体 + 声音锁 |
| `location-sheet.md` | 地点表：3/4 视角 + 锚点 + 单光源 + 状态变体 |
| `prop-sheet.md` | 道具表：hero/bloodied/hidden 多版本 + 尺度锚点 |
| `behavior-profile.md` | 行为主档：移动/手/tic/眼神/崩溃阶梯 |
| `shot-prompt-skeleton.md` | 逐镜 16-block 空白骨架（填空即出提示词，按用户语言生成） |
| `geo-spatial-layout.md` | GEO 空间锁定模板（每场景写一次逐镜粘贴） |
| `style-prefix.md` | Style Prefix 逐字 + 技术标签 + 体裁变体 |
| `shotlist.md` | 分镜表（按场景块） |
| `iteration-log.md` | 迭代日志 |
| `shot-frame-prompt.md` | 分镜首帧生图提示词（每镜一张参考图） |
| `deliverable-manifest.md` | 交付物总清单（文件索引+参考图清单+检查表） |

## references 索引

- `00-overview-handbook.md` — 全流程手册：心智模型、工具链、资产规范、提示词骨架范例、表演要点、实战 hack、后期、五条黄金规则、速查表。**先读这个建立全局。**
- `01-pipeline-runbook.md` — 端到端 11 阶段操作规程 + 项目脚手架 + 体裁适配 + 渠道路由。**做完整项目读这个。**
- `10-cinedance-video-prompt.md` — 视频提示词导演系统：4-D 方法论、16-block 详解、镜头决策树、光学/防漂移、物理与光照锁定、无声 QA。
- `11-acting-performance.md` — 角色表演系统：核心公理「表演=压力下的行为」、五支柱、眼生命、主档模板、实战范例、坏表演图鉴与 0–5 量表。
- `12-lira-image-prompt.md` — 图像提示词优化：模型路由（GPT Image 2/NBP/Seedream 5.0 Pro/Nano Banana 2）、防失败 10 条、手术式编辑模板、各类型骨架。
- `20-qa-checklists.md` — 生成前提示词审查（A 视频 / B 图像）+ 生成后 slop 图鉴 + 修复路由。
- `13-deliverable-system.md` — 交付物系统：资产生图提示词规范、分镜首帧生图提示词、参考图清单、视频/图像模型能力感知表（Seedance/Kling/Veo 3 + GPT Image 2/NBP/Seedream 5.0 Pro）、视频模型选用流程（Ask User First）、时长优化系统（五因素决策）、文件组织规范、语言路由系统。
- `14-ai-director.md` — AI导演方法论：三级输入处理（标题→故事 / 大纲→结构 / 剧本→分镜）、扩展五步法、钩子设计模板、与12阶段管线集成。
- `31-failure-codes.md` — 失败诊断错误码体系：6 类 33 码（资产/空间/动作/摄影/对白/光色）+ 责任层决策树（6 层先定位再修复）+ 复测纪律（最小化修复 + 迭代记录格式）+ Part C slop 映射表。

## 五条黄金规则（每条都因某帧失败而生）

1. **资产优先。** 锁定并压力测试所有角色/地点/道具前，不生成任何镜头。
2. **逐字描述一切。** 模型无记忆，descriptor 每镜逐字进提示词，绝不缩写。
3. **一次只改一处。** 提示词是工作机；整段重写会丢掉已生效的部分。每行迭代进日志。
4. **给模型更少自由。** 用角落不用房间、用锚点不用空场、用地图不用猜、一镜一动作。
5. **镜头不行就简化镜头，不简化文字。** 拆成两镜、删动作、换角度。

## 注意

- 提示词语言遵循语言路由规则（见上）：用户输入什么语言，提示词就用什么语言。reference 与模板内的 prompt 范例保持英文原样（作为技术参考）；实际交付给用户的提示词按用户输入语言生成。技术标签（Photorealistic. NON-IP. 等）、block 名称、@tag、镜头语言库始终用英文。
- 本 Skill 为自包含单元：全部规则、模板与清单均在包内，无外部依赖。