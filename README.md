# AIGC Film Studio — AI 影视制片系统 | 视频提示词工程 · 角色一致性 · AI 电影/短剧/漫剧/短视频

[![Version](https://img.shields.io/badge/version-3.2.0-blue)]()
[![Skill Type](https://img.shields.io/badge/type-AIGC%20Film%20Production-purple)]()
[![Languages](https://img.shields.io/badge/languages-Multi%20%2F%20ZH%20%2F%20EN%20%2F%20JA-brightgreen)]()
[![Models](https://img.shields.io/badge/models-Seedance%202.5%20%7C%20Kling%203.0%20%7C%20Veo%203%20%7C%20GPT%20Image%202-orange)]()

> **AI 视频生成全流程制片 Skill** — 从一句话标题到完整剧本，任何输入级别都能转为 AIGC 可拍分镜。自动解析人物/场景/道具，生成电影级视频与图像提示词，锁定跨镜头一致性，智能优化每镜时长，按用户语言交付提示词。支持外部工具（Nano Banana / GPT Image / Seedream / Seedance / Kling / Veo），覆盖 AI 电影、短剧、漫剧、短视频。核心解决 AI 视频最致命的问题：**一致性崩坏**（角色换脸、场景瞬移、死脸、身份漂移）。

---

## 目录

- [概述](#概述)
- [解决的核心痛点](#解决的核心痛点)
- [核心功能](#核心功能)
- [五条黄金规则](#五条黄金规则)
- [适用人群](#适用人群)
- [三种使用模式](#三种使用模式)
- [端到端工作流（12 阶段）](#端到端工作流12-阶段)
- [一致性锁定体系](#一致性锁定体系)
- [交付物体系](#交付物体系)
- [支持的工具与模型](#支持的工具与模型)
- [失败现象对照表](#失败现象对照表)
- [目录结构](#目录结构)
- [快速开始](#快速开始)
- [使用示例](#使用示例)
- [常见问题 FAQ](#常见问题-faq)
- [兼容性说明](#兼容性说明)
- [关键词索引](#关键词索引)
- [许可协议](#许可协议)
- [版权声明](#版权声明)

---

## 概述

**AIGC Film Studio** 是一套从全 AI 生成院线长片制作实战中提炼、可直接复用的 AIGC 视频生产体系。它不是「丢给大模型写一段提示词」——而是把一套经过实战验证的 AI 影视制作方法论，封装成「触发 → 路由 → 模板 → 质检」的可执行工作流。

本 Skill 部分核心模块依托 Higgsfield 95 分钟全 AI 实拍长片《Hell Grind》全套工业化制作文档搭建，集成六大核心标准模块：CINEDANCE 提示词自动化批量渲染工具、分层式 Lira 图像提示词系统、适配长片连贯叙事的 ACTING 数字人表演写作规范、影片原生 11 阶闭环制作流水线、标准化分镜清单模板、全流程问题踩坑校验图集。

加载本 Skill 后，AI 助手能从**任何级别的输入**出发，完成完整的 AI 视频制片链路：

```
标题/大纲/剧本 → AI导演扩展 → 解析人物·场景·道具 → 锁定资产 → 出分镜
→ 写提示词(视频+图像) → 生成 → 质检 → 后期 → 交付
```

**核心理念**：视频模型没有记忆。它不记得上一镜谁站在哪、穿什么。每一镜都必须把「完整描述 + 参考图」逐字喂进去，否则角色换脸、场景崩坏、人物瞬移。本 Skill 的全部规则都因「某一帧失败」而生。

**与直接让大模型写提示词的区别**：大模型只给「一段文字」；本 Skill 给「一套体系」——AI 导演、资产注册、分镜表、16-block 骨架、GEO 空间锁定、Style Prefix、SCALE LAW、时长优化、质检清单、迭代日志、五类交付物。大模型写的提示词往往第二镜就换脸，本 Skill 的体系保证可复拍任何一镜，角色 100 镜始终一致。

---

## 解决的核心痛点

| 痛点 | 典型表现 | 本 Skill 的解法 |
|---|---|---|
| **一致性崩坏** | 角色换脸、场景瞬移、跳轴、死脸、塑料皮、身份漂移 | descriptor 逐字注入 + GEO 空间锁定 + Style Prefix + SCALE LAW |
| **提示词写不全** | 英文 prompt 漏 block、被内容过滤误杀、模型自由发挥 | CINEDANCE 16-block 刚性骨架 + LIRA 4-D 图像路由 + 13 个即抄模板 |
| **表演僵硬** | 人物像念稿、无生命感、情绪切换生硬 | ACTING「表演 = 压力下的行为」五支柱 + 行为主档 |
| **流程缺失** | 有剧本但不知怎么变成片 | 12 阶段端到端管线 + 每阶段交付物门禁 + 项目脚手架 |
| **输入太粗** | 只有一句话标题或简单大纲，不知道怎么变分镜 | AI 导演三级输入处理（L1 标题→故事 / L2 大纲→结构 / L3 剧本→分镜） |
| **时长乱分配** | 每镜都拍满模型上限，节奏全乱 | 五因素时长决策（动作/情绪/对白/运动/叙事）+ 模型能力感知 |
| **不知道用哪个模型** | 模型选错导致时长不够、一致性差 | 视频模型选用流程（Ask User First）+ 图像模型 LIRA 自动路由 |

---

## 核心功能

### AI 导演：从任何输入到分镜

用户给一句标题、一段大纲、或完整剧本，都能转为 AIGC 可拍的分镜结构。AI 导演是**结构化翻译器**——把任意级别的创意输入翻译成可执行的制片前置文件。

| 输入级别 | 用户给什么 | AI 导演做什么 | 产出什么 |
|---|---|---|---|
| **L1 标题/主题** | 一句话（如"雨天旧书店发现旧信"） | 创意扩展（五步法：情绪提取→角色最小化→空间锁定→故事弧→钩子设计）→ 完整故事 → 分镜 | 分镜草案 + 角色/场景/道具清单 + 故事弧文档 |
| **L2 简要大纲** | 3-5 句故事大纲 | 结构补全（场景块识别→情感节拍→视觉叙事）→ 分镜 | 同上 |
| **L3 详细剧本** | 完整剧本/小说片段 | 直接解析（场景块切分→对白节奏→动作密度→视觉重点）→ 分镜 | 同上 |

**5 种钩子设计模板**（竖屏前 3 秒生死线）：悬念钩子、情绪钩子、视觉钩子、动作钩子、声音钩子——可组合使用。

AI 导演在 12 阶段管线中位于阶段 0.5（需求澄清后、剧本解析前），产出直接喂入后续阶段。详见 `references/14-ai-director.md`。

### 资产解析与锁定

- **人物 / 场景 / 道具解析**：角色表三图规范（正面无头防换脸 + 背面全身 + 脸部 3/4 特写）、地点 3/4 视角表（含机位锚点 + 单光源逻辑）、道具多版本表（hero / bloodied / hidden）
- **@tag 命名词典**：每个状态（湿身 / 血 / 日 / 夜 / 雨）都是独立资产，统一管理。角色 `@mei`、地点 `@loc_bookstore`、道具 `@prop_letter`，状态变体 `@mei_wet`、`@loc_bookstore_night`
- **压力测试**：10/10 可识别、同框不崩、锁声音 + 行为主档，达标才进下一阶段

### 跨镜头一致性系统

本 Skill 的核心价值：**让 AI 视频角色在跨镜头间保持一致**。

| 锁定机制 | 治什么病 | 怎么用 |
|---|---|---|
| **descriptor 逐字注入** | 角色换脸 / 换衣 | 每镜把角色完整描述逐字写进提示词，绝不缩写 |
| **GEO 空间锁定** | 人物瞬移 / 跳轴 | 每场景写一次空间地图，逐镜粘贴 |
| **Style Prefix** | 死脸 / 塑料皮 / 身份漂移 | 逐字粘贴到每个提示词末尾，含 Skin / Acting / Continuity 三条不可删根条款 |
| **SCALE LAW** | 巨人缩水 / 尺度漂移 | 超大物体每镜带尺寸对比 + 人形参照物双锚 |

### 提示词工程三体系

- **CINEDANCE 视频提示词系统**：16-block 刚性骨架（SCENE CONTEXT → ACTIVE REFERENCES → LOCATION MAP → FIRST FRAME → FORMAT → OPTICS → CAMERA → ACTION TIMING → PHYSICS → LIGHTING → AUDIO → CHARACTER ACTING → STYLE → QUALITY → POSITIVE CONSTRAINTS）+ 镜头决策树 + 光学/物理/光照锁定 + 无声 QA，直出可投产的 Seedance / Kling / Veo 提示词
- **LIRA 图像提示词优化**：4-D 方法论（DECONSTRUCT → DIAGNOSE → DEVELOP → DELIVER）+ 模型路由（NBP / Seedream 5.0 Pro / GPT Image 2）+ 防失败 10 条 + 手术式编辑模板
- **ACTING 表演写作**：核心公理「表演 = 压力下的行为」+ 五支柱（目标/障碍/战术/节拍/潜台词）+ 眼生命 + 行为主档 + 坏表演图鉴与 0-5 量表

### 交付物体系

本 Skill 产出五类标准化交付物，统一组织到项目目录，确保项目可「复拍任何一镜」：

| 交付物 | 内容 | 文件位置 |
|---|---|---|
| **资产生图提示词** | 每个角色/地点/道具的 LIRA 优化图像提示词 + 目标模型推荐 + 参考图规格 | `01-assets/<type>/<tag>_image_prompt.md` |
| **分镜首帧生图提示词** | 每镜一张首帧参考图提示词（用于图生视频输入或视觉参考） | `04-prompts/image/shot_<NNN>_frame.md` |
| **分镜视频提示词** | 每镜 CINEDANCE 16-block 视频提示词（含版本化迭代） | `04-prompts/video/shot_<NNN>_v<N>.md` |
| **参考图清单** | 每镜用哪些参考图、上传顺序、每张图的用途 | `04-prompts/reference_manifest.md` |
| **交付物总清单** | 文件索引 + 参考图清单 + 归档校验表 + UI 参数设置 | `08-delivery/deliverable-manifest.md` |

详见 `references/13-deliverable-system.md`。

### 时长优化

单镜时长不按体裁固定，而是基于五因素综合决策，同时感知模型能力上限：

| 决策因素 | 影响范围 | 示例 |
|---|---|---|
| 动作复杂度 | 简单 3-5s / 中等 5-8s / 复杂 8-15s | 站立阅读 vs 打斗+多人 |
| 情绪重量 | 铺垫 3-5s / 反应 4-6s / 高潮 6-10s | 评估时刻最值钱 |
| 对白长度 | 无对白 3-6s / 单句 4-8s / 多轮 8-15s | 每句前后至少 1s 静默 |
| 镜头运动 | 固定 3-6s / 缓慢 5-10s / 复杂 8-15s | 运动需要时间展开 |
| 叙事节奏 | 钩子 3-5s / 过渡 2-4s / 核心 5-10s / 收束 3-6s | 竖屏前 3 秒必钩子 |

**压缩优先级**：过渡镜 > 铺垫镜 > 核心叙事镜 > 高潮镜（最后压）。视频模型选用前自动询问用户，按模型能力约束设计分镜时长。详见 `references/13-deliverable-system.md` §2。

### 生成渠道

- **外部工具**：交付标准化提示词包（16-block 提示词 + 资产图包 + UI 参数清单 + 摘要），用户自行在 Nano Banana / GPT Image / Seedream / Seedance / Kling / Veo 等工具中生成

### 视频模型选用（Ask User First）

> **铁律：视频模型选用前，必须先询问用户。**

不同模型在时长上限、画幅、参考图机制、音频能力上差异巨大，AI 助手不可替用户决定。选用决策树按需求路由：需要原生音频同步 → Kling 3.0 Omni / Veo 3；需要极致物理精确 → Kling 3.0；需要最长单镜时长 → Seedance 2.5（30s）；需要电影级短氛围镜 → Veo 3（8s，带原生音频）。用户未指定时默认推荐 Seedance 2.5。

### 多语言路由

提示词语言始终跟随用户在 agent 中输入的语言——不因目标工具改变：

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

### 统一质检与诊断

- **生成前审查**：提示词审查清单（视频 Part A / 图像 Part B），过审才生成
- **生成后清理**：14 种典型 AI 缺陷 slop 图鉴（多指 / 沸腾纹理 / 假文字 / 死脸 / 瞬移……），脸手优先清零
- **修复路由**：问题 → 根因 → 修复路径（详见下方[失败现象对照表](#失败现象对照表)）
- **迭代纪律**：surgical 一次改一行，进日志；10-15 次不成则简化镜头（拆镜/删动作/换角度）

---

## 五条黄金规则

每条规则都因某一帧失败而生：

1. **资产优先。** 锁定并压力测试所有角色/地点/道具前，不生成任何镜头。
2. **逐字描述一切。** 模型无记忆，descriptor 每镜逐字进提示词，绝不缩写。
3. **一次只改一处。** 提示词是工作机；整段重写会丢掉已生效的部分。每行迭代进日志。
4. **给模型更少自由。** 用角落不用房间、用锚点不用空场、用地图不用猜、一镜一动作。
5. **镜头不行就简化镜头，不简化文字。** 拆成两镜、删动作、换角度。

---

## 适用人群

- 想用 AI 做**电影 / 短剧 / 漫剧 / 短视频**的个人创作者与团队
- 使用 **Seedance、Kling、Veo** 等视频生成工具的用户
- 被**角色一致性、换脸、瞬移、死脸**折磨过的提示词工程师
- 需要把**剧本 / 小说 / 文案批量转成视频分镜**的内容项目
- 只有**一句话想法或简单大纲**，需要 AI 帮忙扩展成完整故事的创作者
- 研究 **AI 视频提示词工程**的开发者与研究者

---

## 三种使用模式

对 AI 助手说出需求即可自动触发：

| 模式 | 你可以这样说 | AI 助手怎么做 |
|---|---|---|
| **A. 全套制片** | 「用 aigc-film-studio 把这段剧本做成一个竖屏短剧」「帮我做一支 60 秒 AI 短片」 | 走完整 12 阶段管线，从建项目目录开始 |
| **B. 单点支援** | 「帮我写这条 Seedance 视频提示词」「这个角色总换脸怎么办」「审一下这段表演」 | 按路由表加载对应 reference / 清单 |
| **C. 提示词包交付** | 「给我全套提示词，我自己去 Seedance 生成」 | 只产出标准化提示词包 + 资产图包 + UI 参数清单 |

**单点支援路由表**（模式 B 自动匹配）：

| 需求关键词 | 加载文档 |
|---|---|
| 视频提示词 / Seedance 提示词 / 视频 prompt | `references/10-cinedance-video-prompt.md` |
| 图像提示词 / 画图 prompt / NBP 提示词 | `references/12-lira-image-prompt.md` |
| 表演 / 演技 / 人物僵硬 / 死脸 | `references/11-acting-performance.md` |
| 换脸 / 一致性 / 瞬移 / 跳轴 | `references/20-qa-checklists.md` + `assets/templates/geo-spatial-layout.md` |
| 全流程 / 制片流程 / 怎么做 | `references/00-overview-handbook.md` + `references/01-pipeline-runbook.md` |

---

## 端到端工作流（12 阶段）

```
0 接需求 → 0.5 AI导演扩展 → 1 剧本解析 → 2 资产清单+注册 → 3 资产图提示词 → 4 压力测试
  5 分镜表 → 6 逐镜提示词(视频+首帧) → 7 生成(渠道路由) → 8 迭代 → 9 清理
  10 调色声音 → 11 交付归档
```

| 阶段 | 关键动作 | 交付物门禁 |
|---|---|---|
| 0 需求澄清 | 定体裁/时长/画幅/渠道/风格 + 询问视频模型 | 需求确认书 |
| 0.5 AI导演 | L1→故事 / L2→结构 / L3→解析 | 分镜草案 + 清单 + 故事弧 |
| 1 剧本解析 | 切场景块（地点×时间×状态） | 场景块清单 |
| 2 资产注册 | 穷举角色/地点/道具 + @tag 词典 | 资产注册表 |
| 3 资产图生成 | 角色三图/地点 3/4 视角/道具多版本 | 资产生图提示词 + 资产图包 |
| 4 压力测试 | 10/10 可识别、同框不崩 | 压力测试通过 |
| 5 分镜表 | 按块出 shotlist，一镜一动作 | 分镜表 |
| 6 逐镜提示词 | 16-block + GEO + Style Prefix + 首帧生图 + 参考图清单 | 过生成前审查 |
| 7 生成 | 外部工具路由 | 原始素材 |
| 8 迭代 | surgical 一次一行，进日志 | 终版提示词 |
| 9 清理 | slop 图鉴对照清零 | picture lock |
| 10 调色声音 | 统一 look + 连续 ambience | 成片 |
| 11 交付归档 | 成片 + 可复拍项目文件 + 交付物总清单 | 交付包 |

---

## 一致性锁定体系

本 Skill 的核心价值：**让 AI 视频角色在跨镜头间保持一致**。

```
                    ┌──────────────────────────────────┐
                    │        一致性锁定体系              │
                    └──────────┬───────────────────────┘
           ┌──────────────┬────┴────┬──────────────┐
           ▼              ▼         ▼              ▼
    ┌─────────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
    │ descriptor  │ │   GEO    │ │  Style   │ │  SCALE   │
    │  逐字注入   │ │ 空间锁定 │ │  Prefix  │ │   LAW    │
    ├─────────────┤ ├──────────┤ ├──────────┤ ├──────────┤
    │ 治:换脸/换衣│ │治:瞬移   │ │治:死脸   │ │治:巨人   │
    │             │ │     /跳轴│ │ /塑料皮  │ │   缩水   │
    └─────────────┘ └──────────┘ └──────────┘ └──────────┘
```

**Style Prefix 三条不可删根条款**：(1) `Skin: Pore-level realism` 防塑料脸；(2) `Acting: ...wet living eyes with catch-lights` 防死脸；(3) `Continuity: ...No identity drift` 防换脸。任何体裁变体都必须保留。

详见 `references/` 下的对应文档与 `assets/templates/` 下的即抄模板。

---

## 交付物体系

本 Skill 产出五类标准化交付物，统一组织到项目目录，确保任何人拿到项目文件夹，能找到任何一镜的提示词、参考图、生成素材与迭代记录。

### 项目目录结构

```
<project_name>/
├── README.md                           # 项目概览（brief + 交付物索引）
├── 00-brief/brief.md                   # 需求确认书
├── 01-assets/
│   ├── characters/                     # 角色 descriptor + 生图提示词 + 参考图规格
│   ├── locations/                      # 地点 descriptor + 生图提示词
│   └── props/                          # 道具 descriptor + 生图提示词
├── 02-registry/asset-registry.md       # @tag 词典
├── 03-shotlists/                       # 分镜表 + GEO（按场景块）
├── 04-prompts/
│   ├── video/                          # CINEDANCE 16-block 视频提示词 + 中文摘要
│   ├── image/                          # 首帧生图提示词
│   └── reference_manifest.md           # 参考图清单（每镜用哪些参考图）
├── 05-generations/                     # 用户生成的素材（按镜号归档）
├── 06-logs/iteration-log.md            # 迭代日志
├── 07-post/post-production-notes.md    # 调色/声音指引
└── 08-delivery/
    ├── deliverable-manifest.md         # 交付物总清单
    └── UI-PARAMS.md                    # UI 参数设置 + 参考图上传顺序
```

### 参考图上传规则

- **角色参考图三张固定顺序**：face close-up → front headless full body → back view
- **地点参考图带禁继指令**：只取空间与质感，不继承构图/角度/色调
- **道具参考图**：标注 `100% matches the reference`
- **首帧图优先**：图生视频模式下，首帧图作为第一张上传

详见 `references/13-deliverable-system.md`。

---

## 支持的工具与模型

### 视频生成模型

| 模型 | 厂商 | 单次最大时长 | 画幅支持 | 参考图锚点 | 核心优势 |
|---|---|---|---|---|---|
| **Seedance 2.5** | 字节跳动 | **30秒** | 16:9, 9:16, 1:1 | 多参考图 | 长叙事、多参考图、真人感；适合复杂动作与长对白 |
| **Seedance 2.0** | 字节跳动 | **15秒** | 16:9, 9:16, 1:1 | 多参考图 | 多镜头叙事、角色一致性；性价比高 |
| **Kling 3.0** | 快手 | **15秒** | 16:9, 9:16 | 图生视频 | 物理精确、角色一致性；适合动作与物理交互 |
| **Kling 3.0 Omni** | 快手 | **15秒** | 16:9, 9:16 | 首尾帧控制 | 原生音画同步、唇形同步；适合对白镜 |
| **Veo 3** | Google | **8秒** | 16:9, 9:16 | 文生+图生 | 原生音频生成、电影级画质；适合短氛围镜 |

### 图像生成模型

| 模型 | 厂商 | 最擅长 | 典型用途 |
|---|---|---|---|
| **GPT Image 2** | OpenAI | 极致照片真实感、提示词遵循、最细局部微编辑 | 地点视角变更、局部手术 |
| **Nano Banana Pro (NBP)** | Google | 帧编辑（永远首选）、文字渲染、道具 | 帧编辑、道具生成、文字渲染 |
| **Nano Banana 2** | Google | 文字渲染、角色一致性、信息图 | 信息图、文字密集图 |
| **Seedream 5.0 Pro** | 字节跳动 | 图层分离、商业视觉、纹理修复 | 纹理 pass、商业视觉、与 Seedance 配合 |

> 图像模型路由由 LIRA 4-D 方法论自动决定。帧编辑固定顺序：NBP 永远第一 → Seedream 纹理 pass → GPT Image 2 最后手段。

### 体裁适配

| 维度 | 电影 | 短剧 | 漫剧 | 短视频 |
|---|---|---|---|---|
| 画幅 | 16:9 | 16:9 或 9:16 | 16:9 或 9:16 | 9:16 |
| 单镜时长 | 8-12s | 5-10s | 4-8s | 3-8s，前 3 秒必钩子 |
| Style Prefix | 原版逐字 | 原版逐字 | 漫画风格变体，保留三条根 | 可降格，保留三条根 |
| 首帧 | wide establishing | wide establishing | 场景全景或人物半身 | medium portrait（非传统 wide） |
| 节奏 | 沉稳，给情绪时间 | 快切，推进叙事 | 分镜感强， panel 式构图 | 极快，前 3 秒钩子生死线 |

**铁律：体裁只改节奏与风格参数，不改一致性纪律。**

---

## 失败现象对照表

出问题先查这里：

| 失败现象 | 根因 | 解法所在 |
|---|---|---|
| 角色换脸 / 换衣 | 描述不完整、参考被误用、正面图未去头 | handbook §3 + `20-qa` Part C#5 |
| 人物瞬移 / 跳轴 | 缺 GEO / 缺首秒 wide / 切后未重述位置 | `geo-spatial-layout.md` + `20-qa` C#6 |
| 表演像死人 / 假 | 写感受非行为、脸无眼神光 | `11-acting` + `20-qa` C#4/#13 |
| 图像崩坏 / 多指 / 文字乱码 | 模型弱点未规避 | `12-lira` + `20-qa` C#1-3 |
| 巨人越画越矮 | 缺尺度锚点 | SKILL §SCALE LAW + `20-qa` C#8 |
| 多人 / 克隆家具 / 自带配乐 / 自创台词 | 约束缺失 | `20-qa` C#10-12 |
| 塑料皮 / 对称脸 | 图像整张二次过模型 | `20-qa` C#7（点修改铁律） |

完整质检关：`references/20-qa-checklists.md`（生成前 Part A/B，生成后 Part C，修复路由 Part D）。

---

## 目录结构

```
aigc-film-studio/
├── SKILL.md                         # 入口：触发条件、三种模式、工作流路由、SCALE LAW、黄金规则
├── README.md                        # 本文件
├── references/                      # 按需加载的详文
│   ├── 00-overview-handbook.md      # 全流程手册（先读，建立全局）
│   ├── 01-pipeline-runbook.md       # 12 阶段端到端操作规程 + 项目脚手架 + 体裁适配 + 渠道路由
│   ├── 10-cinedance-video-prompt.md # 视频提示词导演系统（16-block 骨架）
│   ├── 11-acting-performance.md     # 角色表演系统（活人表演写作）
│   ├── 12-lira-image-prompt.md      # 图像提示词优化（4-D 方法论 + 模型路由 + 防失败）
│   ├── 13-deliverable-system.md     # 交付物系统 + 时长优化 + 文件组织 + 语言路由 + 模型能力表
│   ├── 14-ai-director.md            # AI导演方法论 + 三级输入处理 + 钩子设计
│   └── 20-qa-checklists.md          # 生成前审查 + 生成后 slop 图鉴 + 修复路由
└── assets/templates/                # 13 个可复制模板
    ├── project-structure.md         # 项目目录结构 + 命名规范
    ├── asset-registry.md            # 资产注册表 + @tag 命名词典
    ├── character-sheet.md           # 角色表（三图规范 + descriptor + 状态变体 + 声音锁）
    ├── location-sheet.md            # 地点表（3/4 视角 + 锚点 + 单光源）
    ├── prop-sheet.md                # 道具表（hero/bloodied/hidden 多版本）
    ├── behavior-profile.md          # 行为主档（移动/手/tic/眼神/崩溃阶梯）
    ├── shot-prompt-skeleton.md      # 16-block 提示词空白骨架
    ├── geo-spatial-layout.md        # GEO 空间锁定模板
    ├── style-prefix.md              # Style Prefix 逐字 + 体裁变体（电影感/亮调/竖屏）
    ├── shotlist.md                  # 分镜表（按场景块）
    ├── iteration-log.md             # 迭代日志
    ├── shot-frame-prompt.md         # 分镜首帧生图提示词（每镜一张参考图）
    └── deliverable-manifest.md      # 交付物总清单（文件索引+参考图清单+检查表）
```

---

## 快速开始

### 安装

本 Skill 兼容支持自定义 Skill 加载的 AI 助手平台。安装方式：

1. 下载或克隆本仓库到本地
2. 将 `aigc-film-studio` 文件夹放入你的 AI 助手 Skill 目录
3. 重启或刷新 AI 助手，Skill 将自动加载

支持 Codex、Claude Code、Cursor、Trae、WorkBuddy 等 Agent 加载。

> 具体 Skill 目录路径因平台而异，请参考对应平台的文档。

### 触发方式

无需手动调用。AI 助手会根据你的自然语言需求自动识别并加载本 Skill。你也可以显式指定：

- 「用 aigc-film-studio 帮我做个短剧」
- 「用 aigc-film-studio 写视频提示词」
- 「用 aigc-film-studio 把这段剧本转成分镜」

### 第一个项目（3 分钟上手）

最简单的起步方式是模式 B（单点支援）——先让 AI 助手帮你写一条视频提示词，感受 CINEDANCE 16-block 骨架的输出质量：

```
你：帮我写一条 Seedance 视频提示词，场景是一个穿风衣的女人在雨夜街头撑伞等车
```

AI 助手会加载 CINEDANCE 系统，输出完整的 16-block 提示词 + 中文摘要。你可以直接复制到 Seedance 生成。

当你准备好了，可以尝试模式 A（全套制片）：

```
你：用 aigc-film-studio 帮我做一个 30 秒的竖屏短剧，剧本是：[粘贴你的剧本]
```

甚至只有一句话：

```
你：用 aigc-film-studio 帮我做一个关于深夜便利店的短视频
```

AI 导演会从这一句话扩展出完整故事、分镜草案和角色/场景/道具清单。

---

## 使用示例

### 示例 1：从一句话到全套制片（模式 A + AI 导演）

```
用户：帮我做一个关于深夜便利店的短视频

AI 助手：
→ 阶段 0：确认需求（体裁：竖屏短视频 / 画幅：9:16 / 时长：30s / 渠道：Seedance / 风格：写实）
→ 阶段 0.5 AI导演（L1 标题扩展）：
   - 核心情绪：孤独 + 意外联结
   - 角色：店员 + 深夜来客（2人）
   - 空间：便利店内部·凌晨·雨天
   - 故事弧：日常→发现→变化（3拍6镜）
   - 钩子：情绪钩子 + 声音钩子
→ 阶段 1-2：解析剧本为场景块，注册资产（@clerk 店员 / @visitor 来客 / @loc_store 便利店 / @prop_cat 流浪猫）
→ 阶段 3：生成资产图提示词（角色三图、地点 3/4 视角、道具多版本）
→ 阶段 4：压力测试（10/10 可识别，同框测试通过）
→ 阶段 5：出分镜表（6 个镜头，总时长 30s）
→ 阶段 6：逐镜写 16-block 视频提示词 + 首帧生图提示词 + 参考图清单，过 QA 审查
→ 阶段 7：交付提示词包
```

### 示例 2：修复一致性问题（模式 B）

```
用户：我生成的视频里角色每一镜脸都不一样，怎么办？

AI 助手：
→ 诊断：角色换脸，通常是 descriptor 不完整或缺少参考图锚定
→ 加载 20-qa-checklists.md Part C#5
→ 提供修复方案：检查角色表是否有正面无头参考图、descriptor 是否逐镜完整、Style Prefix 是否粘贴
→ 如果需要，帮你重写角色 descriptor
```

### 示例 3：提示词包交付（模式 C）

```
用户：给我全套提示词，我自己去 Seedance 生成

AI 助手：
→ 按已确认的分镜表逐镜输出
→ 每镜一个 16-block 提示词文件（按用户语言生成）
→ 每镜一张首帧生图提示词（用于图生视频输入）
→ 附资产图包（文件名 = @tag）
→ 附参考图清单（每镜用哪些参考图、上传顺序）
→ 附 UI 参数清单（画幅/时长/分辨率/参考图绑定方式）
→ 附交付物总清单（文件索引 + 归档校验表）
```

---

## 常见问题 FAQ

<details>
<summary><b>提示词是什么语言？中文用户看不懂英文怎么办？</b></summary>

提示词语言始终跟随用户在 agent 中输入的语言。用户输入中文 → 中文提示词；输入英文 → 英文提示词；输入日文 → 日文提示词；依此类推。技术标签（Photorealistic. NON-IP. 等）、16-block 骨架的 block 名称、@tag、镜头语言库始终用英文（模型对这些有固定理解）。交付的提示词包每镜附 2-3 行摘要（用用户输入语言）。

</details>

<details>
<summary><b>能做竖屏短视频吗？</b></summary>

能。提供四种 Style Prefix 变体：电影感原版（横屏电影/短剧）、漫画风格变体（漫剧）、亮调平台风（广告/品牌片）、竖屏降格版（9:16 短视频）。体裁只改节奏与风格参数，一致性纪律不放松。所有变体保留 Skin / Acting / Continuity 三条根条款。竖屏首帧用 medium portrait（非传统 wide），前 3 秒必须有钩子。漫剧变体保留三条根，仅切换为漫画风格渲染。

</details>

<details>
<summary><b>我用 Kling / Veo 等工具，没有 Seedance 的多参考图锚点，一致性怎么办？</b></summary>

降级策略：descriptor 逐字进提示词 + 图生视频（用角色表图或上一镜末帧作输入图），这是无多参考图锚点下最强的一致性手段。本 Skill 的 16-block 骨架在任何工具中都保留核心一致性条款（descriptor 逐字注入 + GEO 空间锁定 + Style Prefix 三条根），确保跨工具可用。

</details>

<details>
<summary><b>只有一句话想法，能做成视频吗？</b></summary>

能。AI 导演系统支持 L1 标题/主题输入。从一句话出发，通过五步法（核心情绪提取→角色最小化→空间锁定→故事弧设计→钩子设计）扩展出完整故事、分镜草案和角色/场景/道具清单。详见 `references/14-ai-director.md`。

</details>

<details>
<summary><b>视频模型怎么选？不同模型有什么区别？</b></summary>

视频模型选用前 AI 助手会先询问你。当前主流模型：Seedance 2.5（30s，长叙事最强）、Seedance 2.0（15s，性价比高）、Kling 3.0（15s，物理精确）、Kling 3.0 Omni（15s，原生音画同步）、Veo 3（8s，原生音频+电影级画质）。未指定时默认推荐 Seedance 2.5。详见 `references/13-deliverable-system.md` §2。

</details>

<details>
<summary><b>每镜时长怎么决定？都拍满模型上限吗？</b></summary>

不是。每镜时长基于五因素综合决策：动作复杂度、情绪重量、对白长度、镜头运动、叙事节奏。高潮镜和核心叙事镜给更多时间，过渡镜和铺垫镜尽量短。总时长紧张时按优先级压缩（过渡镜先压，高潮镜最后压）。详见 `references/13-deliverable-system.md` §2。

</details>

<details>
<summary><b>提示词能直接用在哪些模型？</b></summary>

视频——Seedance 2.5/2.0、Kling 3.0/Omni、Veo 3；图像——Nano Banana Pro/2、GPT Image 2、Seedream 5.0 Pro。不同模型的路由规则见 `references/12-lira-image-prompt.md` 和 `references/13-deliverable-system.md`。

</details>

<details>
<summary><b>为什么提示词里不写年龄数字？</b></summary>

年龄数字（如 20yo / 25yo）可能触发内容过滤（涉及未成年人保护机制），且会导致模型对特定年龄特征过度拟合。正确做法是通过体型、穿着、气质自然暗示年龄（如 "young adult male"、"broad-shouldered man in his prime"）。

</details>

<details>
<summary><b>Style Prefix 里的三条根条款是什么？为什么不能删？</b></summary>

三条不可删根条款：(1) `Skin: Pore-level realism` 防塑料脸；(2) `Acting: ...wet living eyes with catch-lights` 防死脸；(3) `Continuity: ...No identity drift` 防换脸。这三条是活人感与跨镜头一致性的底线，任何体裁变体都必须保留。

</details>

<details>
<summary><b>一镜生成 10-15 次还不满意怎么办？</b></summary>

根据「10-15 次法则」：一镜这么多次迭代还不成，问题不在措辞，在镜头设计。简化镜头：拆成两镜、删动作、换角度、减少同框人数。不要继续在提示词上做微调——那是在错误的方向上优化。

</details>

<details>
<summary><b>最终交付物有哪些？</b></summary>

五类标准化交付物：(1) 资产生图提示词（每个角色/地点/道具）；(2) 分镜首帧生图提示词（每镜一张，用于图生视频输入）；(3) 分镜视频提示词（每镜 CINEDANCE 16-block）；(4) 参考图清单（每镜用哪些参考图、上传顺序）；(5) 交付物总清单（文件索引 + UI 参数 + 归档校验）。所有文件统一组织到项目目录，确保可复拍任何一镜。

</details>

---

## 兼容性说明

### 提示词语言（语言路由系统）

提示词语言始终跟随用户在 agent 中输入的语言——不因目标工具改变：

| 用户输入语言 | 提示词语言 | 说明文字语言 |
|---|---|---|
| 中文 | **中文** | 中文 |
| 英文 | **英文** | 英文 |
| 日文 | **日文** | 日文 |
| 其他语言 | **对应语言** | 对应语言 |

- 16-block 骨架的 block 名称始终用英文
- block 内容用用户输入语言填写
- 技术标签（Photorealistic. NON-IP. 等）始终用英文
- @tag 始终用英文
- 镜头语言库始终用英文
- 详见 `references/13-deliverable-system.md` §4

### 平台/工具兼容性

本 Skill 产出的提示词包为标准化格式，兼容主流外部视频/图像生成工具：

| 工具类型 | 兼容工具 | @tag 参考图锚定 | 16-block 骨架 | 一致性等级 |
|---|---|---|---|---|
| **视频生成** | Seedance 2.5/2.0 | 原生支持（多参考图） | 直接使用 | 最高 |
| | Kling 3.0/Omni | 图生视频支持 | 直接使用 | 高 |
| | Veo 3 | 文生+图生支持 | 直接使用 | 高 |
| **图像生成** | Nano Banana Pro/2 | 帧编辑支持 | 直接使用 | 高 |
| | GPT Image 2 | 支持 | 直接使用 | 高 |
| | Seedream 5.0 Pro | 支持 | 直接使用 | 高 |

> 无多参考图锚点的工具（如 Kling、Veo）：使用图生视频模式 + descriptor 逐字注入，是一致性降级下的最强策略。本 Skill 的 16-block 骨架在任何工具中都保留核心一致性条款。

### 注意事项

- reference 与模板内的 prompt 范例保持英文原样（作为技术参考）；实际交付给用户的提示词按用户输入语言生成
- 本 Skill 为自包含单元：全部规则、模板与清单均在包内，无外部依赖

---

## 关键词索引

### 中文关键词

AI 电影制作 · AI 短剧制作 · 漫剧制作 · 竖屏短视频 · 抖音视频生成 · 视频号视频 · 文生视频 · 图生视频 · 视频提示词 · 图像提示词 · 角色一致性 · 人物场景道具解析 · 脚本转分镜 · AIGC 制片流程 · 换脸修复 · 镜头一致性 · AI 分镜表 · Seedance 提示词 · 提示词工程 · AI 视频生成 · AI 影视制作 · 短剧制作工具 · 视频提示词模板 · AI 视频质检 · 角色锁定 · 场景一致性 · 跨镜头一致性 · AI 制片系统 · Seedance · Kling 提示词 · Veo 提示词 · 视频生成工作流 · AI 导演 · 分镜脚本 · 一句话转视频 · 标题扩展 · 时长优化 · 视频模型选用 · Nano Banana Pro · Seedream 5.0 Pro · GPT Image 2 · Veo 3

### English Keywords

AI filmmaking · AI short drama · text-to-video · image-to-video · video prompt engineering · image prompt optimization · character consistency · shotlist generation · AIGC film pipeline · Seedance · Kling · Veo 3 · Nano Banana Pro · Seedream 5.0 Pro · GPT Image 2 · AI video production · prompt engineering · cross-shot consistency · character drift fix · AI film studio · short video generation · vertical video · AI drama production · video prompt template · AIGC production system · AI director · storyboard generation · video generation workflow · prompt language routing · duration optimization · model selection · SCALE LAW · GEO spatial locking · Style Prefix · CINEDANCE · LIRA · ACTING

---

## 许可协议

本项目采用 [MIT License](LICENSE) 开源协议。

## 版权声明

© 2026 Feihong. 保留所有权利。

AIGC Film Studio 由 [Feihong](https://github.com/ifeihong) 开发与维护。部分核心模块依托 Higgsfield 95 分钟全 AI 实拍长片《Hell Grind》全套工业化制作文档搭建。

本项目仅供学习和创作使用，不保证适用于商业场景。使用本 Skill 生成的任何内容，其版权归属由使用者自行判断和承担。
