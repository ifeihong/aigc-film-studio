# 13 交付物系统 — Deliverable System

> 定位：本文件是 AIGC Film Studio skill 的交付物总纲。当 agent 需要知道「最终要产出什么文件、每个文件包含什么内容、如何组织、用哪种语言」时，读这里。
>
> 与其他 reference 的关系：
> - 资产生图提示词的写法规则 → `12-lira-image-prompt.md`（LIRA 4-D 方法论与模型路由）
> - 分镜视频提示词的 16-block 架构 → `10-cinedance-video-prompt.md`（CINEDANCE 导演系统）
> - 表演层写法 → `11-acting-performance.md`（ACTING 系统）
> - 质检关 → `20-qa-checklists.md`
> - 端到端阶段门禁 → `01-pipeline-runbook.md`
>
> 本文件新增的交付物类型：**分镜画面生图提示词（Shot Frame Image Prompts）** —— 此前 skill 不产此类，现补齐。

---

## 目录

1. [交付物总览（Deliverable Overview）](#1-交付物总览deliverable-overview)
2. [时长优化系统（Duration Optimization System）](#2-时长优化系统duration-optimization-system)
3. [交付物文件组织规范（File Organization）](#3-交付物文件组织规范file-organization)
4. [语言路由系统（Language Routing）](#4-语言路由系统language-routing)

---

## 1. 交付物总览（Deliverable Overview）

skill 产出五大类交付物。下表是全局速览，之后逐类详解。

| 类别 | 交付物名称 | 产出阶段 | 核心 reference | 文件去向 |
|---|---|---|---|---|
| A | 资产生图提示词（Asset Image Prompts） | 阶段 3 | `12-lira-image-prompt.md` | `01-assets/<type>/<tag>_image_prompt.md` |
| B | 分镜画面生图提示词（Shot Frame Image Prompts） | 阶段 6 | 本文件 + `12-lira` | `04-prompts/image/shot_<NNN>_frame.md` |
| C | 分镜视频提示词（Shot Video Prompts） | 阶段 6 | `10-cinedance-video-prompt.md` | `04-prompts/video/shot_<NNN>_v<N>.md` |
| D | 参考图清单（Reference Image Manifest） | 阶段 6 | 本文件 | `04-prompts/reference_manifest.md` |
| E | 交付物文件清单（Deliverable File Manifest） | 阶段 11 | 本文件 | `08-delivery/deliverable-manifest.md` |

---

### A. 资产生图提示词（Asset Image Prompts）

> **目标**：为每个角色、地点、道具产出一份完整的 LIRA 优化图像生成提示词，让用户在 Soul 2.0 / Soul Cinema / NBP / GPT Image 2 / Seedream 5.0 Pro 中生成参考图。
>
> **写法遵循**：`12-lira-image-prompt.md` 的 LIRA 4-D 方法论（DECONSTRUCT → DIAGNOSE → DEVELOP → DELIVER）。模型路由规则完全继承 LIRA 的固定路由表。

#### A.1 每份资产生图提示词的必含要素

每份资产生图提示词文件必须包含以下区块：

1. **Target Model Recommendation（目标模型推荐）**
   - 角色 → **Soul 2.0**（替代方案：Cinema Studio AI Cast，平台内置工具，参数在 UI 设）
   - 地点/环境 → **Soul Cinema**
   - 道具/产品式物体 → **NBP / GPT Image 2**（真实产品语境）
   - 帧编辑 → 永远先 NBP；纹理 pass → Seedream 5.0 Pro；最细局部 → GPT Image 2
   - 标注理由（为何选这个模型）

2. **Optimized Prompt Text（优化提示词文本）**
   - 按语言路由规则选择中文或英文（见本文件 §4）
   - 遵循 LIRA 防失败 10 条：自然散文、不堆关键词、正向 > 负向、画幅为 UI 参数、技术光照与材质、60/30/10 配色、Soul ID + 散文锚点、photoreal 防插画漂移、文字/纹身精确处理
   - 目标长度：≤1500–2000 字符，砍填充

3. **Reference Image Specifications（参考图规格说明）**
   - 要上传哪些参考图（如有参考输入）
   - 上传顺序（对 Seedance 等多参考图工具关键）
   - 每张参考图的用途说明（身份锚点 / 风格参考 / 配色参考）

4. **Negative Prompt / Quality Tags（负向提示词 / 质量标签）**
   - 无模型有负向提示词参数——所有「不要的东西」靠正向描述移除
   - 质量标签用英文技术标签收尾（如 `Photorealistic. NON-IP.`）
   - 如适用，标注防插画漂移措辞

5. **Multi-View Requirements（多视角要求）**

**角色（Soul 2.0）— 三视角：**
   - 正面全身（无头）—— 关键反直觉设计：删头使模型仅从特写取脸
   - 背面全身
   - 脸部特写（3/4 视角大肖像优先）
   - 一致性锚点：`the same real person in all three, consistent across panels`
   - 灰底平光、真实皮肤带可见毛孔、不磨皮
   - 无 `rule of thirds`（角色表豁免）、无 `painterly`、无 `character reference sheet`（插画触发）
   - 详见 `12-lira-image-prompt.md` 角色表模板

**地点（Soul Cinema）— 3/4 视角：**
   - 3/4 视角而非正面「美图」——给模型可读深度，覆盖近一整圈角度
   - 标注机位锚点（如 `high angle three-quarter wide shot, camera high above the room looking diagonally down at 45 degrees`）
   - 留一个锚点物（柱子/灯/沙发），调度绑上去
   - 单一光逻辑：一个主光源决定阴影方向；允许环境漫射底光但不产生第二阴影方向
   - 日/夜/雨为独立资产
   - 宽银幕板用 21:9（Soul Cinema 独有，Soul 2.0 无 21:9）

**道具（NBP / GPT Image 2）— 多版本：**
   - hero（完整版）/ bloodied（受损版）/ hidden（隐藏状态版）等，各独立资产
   - 中性背景、soft directional lighting、isolated subject
   - 无 logo：正向写 `plain unbranded wrapper, blank matte surface`
   - 触发词谨慎：器械道具用中性材质与功能描述

#### A.2 资产生图提示词文件范例（角色）

```markdown
# @mei — 角色生图提示词

## Target Model
**Soul 2.0**（角色生成专用；Soul ID 跨生成锁定同一张脸）
替代方案：Cinema Studio AI Cast（平台内置自动角色表，参数在 UI 设，无需提示词）

## Platform Parameters (UI 设，不进提示词)
- 画幅: 16:9
- 质量: 2k
- Soul ID: [如角色已有则填]

## Optimized Prompt

Three studio photographs of the same young woman arranged side by side on a
flat neutral mid-grey studio backdrop, a film character sheet: full-body front
photo on the left, full-body back photo in the middle, close-up portrait photo
on the right, the same real person in all three, consistent across panels. Soft
directional cinematic studio lighting from one side, gentle natural shadow
falloff, clean neutral cinematic look.

The young woman: slender build, East Asian features, heart-shaped face with
high cheekbones, straight black hair cut just below the jaw, small mole below
left eye, slight natural asymmetry in the brows. Pale skin with visible pores
and subtle capillary flush at the cheeks.

Consistent wardrobe in all panels: fitted charcoal turtleneck, dark olive
trousers, scuffed brown leather boots. A thin braided cord bracelet on the
left wrist.

On the left panel she stands straight facing the camera in a neutral pose, arms
relaxed at the sides, full figure head to feet — head removed, clean neutral
grey fill where the head was. In the middle panel the same standing pose is
seen from behind. On the right panel a close-up head-and-shoulders portrait at
3/4 angle, calm neutral expression, gaze slightly off-camera to the right.

Palette of 70% neutral grey, 20% charcoal and olive, 10% warm skin tone.
Photorealistic ARRI Alexa Mini LF with ARRI Signature Prime lens, clean modern
digital cinematic capture, crisp natural detail, minimal fine grain, soft
cinematic falloff, modern cinematic film still quality, hyperrealistic
photographic detail.

## Quality Tags
Photorealistic. NON-IP. Cinematic.

## Multi-View Requirements
- Panel 1 (left): 正面无头全身 — head removed, grey fill
- Panel 2 (middle): 背面全身
- Panel 3 (right): 3/4 角度脸部特写
- 一致性：`the same real person in all three, consistent across panels`
- 服装三栏一致：`consistent in all panels`

## Notes
- 无 `painterly`、无 `character reference sheet`（防插画漂移）
- 无 `rule of thirds`（角色表豁免）
- 灰底平光为角色表标准——电影感活在地点和视频提示词里
- 选最可信的版本，不是最美的——美但假的脸在视频里暴露
- 永远检查眼睛 catch-light
```

#### A.3 资产生图提示词文件范例（地点）

```markdown
# @loc_bookstore — 地点生图提示词

## Target Model
**Soul Cinema**（电影级质感、自然颗粒、电影美学；支持 21:9；Soul ID 角色可放进场景）

## Platform Parameters (UI 设，不进提示词)
- 画幅: 16:9 (宽银幕板用 21:9)
- 质量: 2k

## Optimized Prompt

High angle three-quarter wide shot, camera positioned in the far front-right
corner of the room looking diagonally across and down at approximately 35
degrees. A narrow independent bookstore interior, late afternoon. Tall wooden
shelves line both side walls, receding into warm amber depth. A central reading
table with a green banker's lamp sits at frame-center, slightly left. The front
counter with an old brass register is at frame-right foreground. A narrow
window with warm amber light streaming in from camera-left, casting long
diagonal shadows across the wooden floorboards.

Secondary elements: stacked books on the table, a ladder leaning against the
far shelves, a faded oriental rug under the table. Dust motes visible in the
window light beam.

Refined desaturated palette: 60% warm ochre and amber from the window light,
30% deep walnut brown of the shelves and floor, 10% muted sage green from the
lamp and rug. Soft cinematic falloff, natural room tone.

Photorealistic ARRI Alexa LF anamorphic Cooke S4 lens at T2.0, organic 35mm
Kodak Vision3 250D film grain, soft cinematic falloff, cinematic film still
aesthetic. Empty interior, still air, no people.

## Quality Tags
Photorealistic. NON-IP. Cinematic.

## Multi-View Requirements
- 主视角: 3/4 高角度宽景
- 反打视角: 如需生成反打，路由到 GPT Image 2，明确写出新物体排布
- 日/夜/雨为独立资产：@loc_bookstore / @loc_bookstore_night / @loc_bookstore_rain

## Notes
- 机位锚点用简单物理措辞，不用 CCTV/鱼眼行话
- 单一光源逻辑：窗光为主光源，环境漫射为底光
- Soul Cinema 原生带颗粒——技术块一行寄存器足够
- 地点空镜正向描述: `Empty interior, still air, no people`
```

#### A.4 资产生图提示词文件范例（道具）

```markdown
# @prop_letter — 道具生图提示词

## Target Model
**NBP**（真实产品语境 + 精确文字渲染；替代方案 GPT Image 2）

## Platform Parameters (UI 设，不进提示词)
- 画幅: 1:1 (高道具用 3:4)
- 分辨率: 2k–4k

## Optimized Prompt

Photorealistic top-down product shot of an aged handwritten letter on a
neutral grey concrete surface, soft directional lighting from upper-left,
isolated subject. Yellowed cream paper, folded once horizontally with a
visible crease line, edges slightly foxed and curling. Dense cursive handwriting
in faded blue-black ink covers most of the visible page. The paper has subtle
fiber texture and a small tear at the bottom-right corner. Plain unbranded,
blank matte surface beneath.

Photorealistic, crisp natural detail, minimal fine grain.

## Quality Tags
Photorealistic. NON-IP.

## Multi-View Requirements
- hero 版: 完整展开信纸（本提示词）
- bloodied 版: 信纸一角带血渍 → 独立资产 @prop_letter_bloodied
- hidden 版: 信纸折叠塞在书页间 → 独立资产 @prop_letter_hidden

## Notes
- 无 logo: 正向写 `plain unbranded, blank matte surface`
- 文字渲染: 引号给精确文案 + 字体/颜色（如需可读文字）
- 多状态 = 独立资产，不混进同一段描述
```

---

### B. 分镜画面生图提示词（Shot Frame Image Prompts）

> **这是本 skill 新增的交付物类型。**
>
> **目标**：为每个分镜产出一个「首帧」图像生成提示词。用户可以用这个提示词在图像模型中生成一张参考帧，然后：
> 1. 作为视频模型的视觉参考（visual reference for the video model）
> 2. 作为图生视频（image-to-video）的输入首帧（first frame for image-to-video generation）
>
> **为什么需要首帧图**：视频模型对「第一帧长什么样」极度敏感。用文字描述首帧，不如直接给一张图。尤其在图生视频模式下，首帧质量直接决定整段视频的质量。对于无多参考图锚点的工具（如 Kling、Veo），图生视频是最强的一致性手段（见 `01-pipeline-runbook.md` §5）。

#### B.1 每份分镜画面生图提示词的必含要素

| # | 要素 | 来源 | 说明 |
|---|---|---|---|
| 1 | Scene Context | 该镜 CINEDANCE 的 SCENE CONTEXT | 一两句简短描述本镜发生的事 |
| 2 | Character Descriptors in Position | 该镜 ACTIVE REFERENCES + spatial blocking | 每个在镜角色的关键锚点，按空间位置排列 |
| 3 | GEO Spatial Layout (simplified) | 该场景的 GEO | 简化为首帧需要的信息：地标位置、摄影机一侧、角色相对位置 |
| 4 | Lighting Setup | 该镜 LIGHTING | 主光源、方向、摄影机相对光的一侧 |
| 5 | Composition / Framing | 该镜 CAMERA + OPTICS | 画幅、机位高度、角度、主体大小、画面位置 |
| 6 | Style Prefix (appropriate variant) | `style-prefix.md` | 选合适的 Style Prefix 变体（电影感/竖屏/暗调等） |
| 7 | Reference Images to Upload | 本文件 §D | 上传哪些角色表/地点表/道具表参考图 |
| 8 | Target Model Recommendation | LIRA 路由 | 通常 Soul Cinema（含角色的场景帧）；纯环境帧也可 Soul Cinema |
| 9 | Quality Tags | 固定格式 | `Photorealistic. NON-IP.` + 画幅 |

#### B.2 分镜画面生图提示词的写法规则

首帧生图提示词与资产生图提示词的关键区别：

- **资产生图**：中性灰底、平光、孤立主体——目的是锁定身份，不含电影感
- **首帧生图**：完整场景、电影级光照、角色在位——目的是锁定「这一镜第一帧长什么样」

因此首帧生图提示词：
- 用 Soul Cinema（不是 Soul 2.0），因为需要电影级场景帧
- 角色 Soul ID 可放进 Soul Cinema 场景
- 光照从该镜的 LIGHTING block 直接取
- 构图从该镜的 CAMERA + OPTICS block 直接取
- 描述角色「已在」位置（状态非过渡——见 CINEDANCE §状态非过渡）
- 加 `rule of thirds`（非角色表场景）
- 画幅与该镜视频画幅一致

**防失败要点（继承 LIRA）：**
- 自然散文，不堆关键词
- 正向 > 负向
- 画幅为 UI 参数，不进提示词文本
- 60/30/10 配色
- 无 `painterly`（防插画漂移）；用 `cinematic film still`
- 画面内文字用引号精确文案 + 字体/颜色
- 无品牌 / IP / 真实人物名

#### B.3 分镜画面生图提示词文件范例

```markdown
# shot_003 — 首帧生图提示词

## Scene Context
A young woman discovers a hidden letter tucked between books on a shelf in a
warm independent bookstore at late afternoon. She has just pulled the letter
out and is reading the first lines, her back to the camera.

## Character Descriptors in Position
@mei: slender young woman, East Asian features, straight black jaw-length
hair, fitted charcoal turtleneck, dark olive trousers, thin braided cord
bracelet on left wrist. She stands at frame-center-left, facing the bookshelf
with her back 3/4 turned to camera, right hand holding the aged letter at chest
height, left hand resting on the shelf edge. 100% matches the reference.

## GEO Spatial Layout (simplified)
Camera is in the far front-right corner of the bookstore, looking diagonally
across and down. The central reading table with green banker's lamp is at
frame-right midground. Tall wooden shelves line the left wall. The front
counter with brass register is deep at frame-right background. The window with
warm amber light is behind the camera-left, casting long shadows across the
floor toward the shelves.

## Lighting Setup
Primary light source: warm amber window light from camera-left, low afternoon
angle. Camera is on the shadow side of the character — her back and the right
side of her face are rim-lit by the window glow, the camera-facing side falls
into soft warm shadow. The banker's lamp adds a small cool green accent on the
table. No flat front light, no beauty fill.

## Composition / Framing
Vertical 9:16 framing. Medium portrait — character occupies 60% of frame
height, head at upper-third line. Camera at eye level, approximately 2.5
meters from subject. 29° diagonal field of view, short telephoto portrait
character. Shallow depth of field: character and letter sharp, bookshelf
background dissolving into soft warm bokeh. Rule of thirds.

## Style Prefix
Style: Photorealistic — no 3D render, no game engine, no game-cutscene aesthetic.
Cinematography: tight vertical portrait framing; natural motivated light from
practical sources; subject fills 60% of frame vertically.
Lighting: Natural motivated light from in-scene practical sources — dominant
warm key from the window, soft ambient fill from room bounce, rim light on the
character's back; no flat front fill, no beauty light; shadows fall naturally
with visible depth.
Color: 60:30:10 — 60% warm amber and ochre, 30% walnut brown, 10% muted sage.
Camera: Physical lens. Natural motion blur.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush,
pore-shadow matching on-set light. Catch-lights from the window source only.
Acting: Hollywood — micro-pauses, precise eye-line, wet living eyes with
catch-lights, visible breath.
Physics: Gravity and inertia respected — correct contact shadows.
Composition: Vertical rule of thirds; subject at left-third; eyes at
upper-third line.
Continuity: Characters, props, environment identical across every cut. No
identity drift.
Technical: High detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.

## Reference Images to Upload
1. @mei face close-up (3/4 portrait) — Soul ID identity anchor
2. @mei front headless full body — body/clothing reference
3. @loc_bookstore main view — location geography and texture reference
4. @prop_letter hero version — prop reference

Upload order: face → body → location → prop

## Target Model
**Soul Cinema**（电影级场景帧；Soul ID 角色可放进场景）

## Platform Parameters (UI 设，不进提示词)
- 画幅: 9:16
- 质量: 2k
- Soul ID: [mei's Soul ID]

## Quality Tags
Photorealistic. NON-IP. 9:16.

## Notes
- 此帧用途: (1) 视频模型视觉参考, (2) 图生视频首帧输入
- 无 `painterly`; 用 `cinematic film still`
- 角色已在位置（状态非过渡）: `She has just pulled the letter out` — 不是 `reaching for the letter`
- 防文字乱码: 信上文字正向描述为 `dense cursive handwriting in faded blue-black ink` — 不要求可读
```

#### B.4 首帧生图与视频提示词的关系

```
分镜表 (shotlist)
    │
    ├──→ 视频提示词 (CINEDANCE 16-block) ──→ 视频模型生成
    │         │
    │         └── FIRST FRAME AND SPATIAL BLOCKING block
    │                    │
    │                    └──→ 首帧生图提示词 (LIRA + CINEDANCE 首帧) ──→ 图像模型生成首帧图
    │                                                                   │
    │                                                                   └──→ 图生视频输入
    │                                                                   └──→ 视觉参考
    │
    └──→ 参考图清单 (manifest) ──→ 上传参考图到视频/图像模型
```

**工作流**：
1. 写完该镜的 CINEDANCE 16-block 视频提示词
2. 从中提取 SCENE CONTEXT、ACTIVE REFERENCES、spatial blocking、LIGHTING、CAMERA、OPTICS
3. 组装成首帧生图提示词（本节格式）
4. 用图像模型生成首帧图
5. 将首帧图作为图生视频的输入，或作为文生视频的视觉参考

---

### C. 分镜视频提示词（Shot Video Prompts）

> **已有能力，不重复。** 每镜一份完整的 CINEDANCE 16-block 视频提示词。
>
> **完整规则见** `10-cinedance-video-prompt.md`。
>
> 此处仅列交付物规格与文件要求。

#### C.1 每份视频提示词文件的必含要素

| # | 要素 | 说明 |
|---|---|---|
| 1 | 16-block 完整架构 | SCENE CONTEXT → ACTIVE REFERENCES → LOCATION MAP → FIRST FRAME AND SPATIAL BLOCKING → FORMAT MODE → OPTICS → CAMERA → ACTION TIMING → PHYSICS → LIGHTING → AUDIO → CHARACTER ACTING → STYLE → QUALITY → POSITIVE CONSTRAINTS（+可选 OUTPUT SETTINGS / NEGATIVE CONSTRAINTS） |
| 2 | SCENE CONTEXT 计数头 | `EXACT N CHARACTERS — NO DUPLICATES` |
| 3 | 活跃 @tag 命名 | 每个参考都命名角色（`for character/location reference`）；地点参考带「不继承构图/角度/色调」禁令 |
| 4 | GEO SPATIAL LAYOUT | 本场景块的空间地图，逐字粘贴 |
| 5 | 首帧锁定 | 首秒为 wide（横屏）或 medium portrait（竖屏），人物立即可见 |
| 6 | ACTION TIMING | 按秒分拍，每拍 ≤3 句，状态非过渡 |
| 7 | AUDIO | 台词只在引号内；Voice 描述逐字粘贴；`SFX only. No music.` |
| 8 | CHARACTER ACTING | 参照 `11-acting-performance.md`——目标/障碍/战术/节拍/潜台词，眼生命 |
| 9 | STYLE | Style Prefix 逐字粘贴（选合适变体） |
| 10 | QUALITY | `8K detail, pore-level skin, no jitter, no flicker; faces stay exactly their references at every distance.` |
| 11 | POSITIVE CONSTRAINTS | 写成「画面里有什么」；计数与禁令明确 |
| 12 | 技术标签收尾 | `Photorealistic. NON-IP. [画幅]. [时长]s. SFX only. NO CGI. Cinematic.` |

#### C.2 文件命名与版本化

- 文件名：`shot_<NNN>_v<N>.md`（如 `shot_003_v2.md`）
- 每次 surgical 迭代（一次改一行）升一个版本号
- 版本号与 `iteration-log.md` 一一对应
- 摘要放单独文件 `04-prompts/video/shot_summaries.md`，格式：`- shot_003: <2-3句，用用户输入语言>`
- 绝不把摘要写进提示词 .md 正文（用户复制时会污染提示词）

#### C.3 语言规则

- 视频提示词正文语言 = 用户输入语言（见本文件 §4）。用户输入中文 → 中文提示词；输入英文 → 英文提示词；输入日文 → 日文提示词；依此类推。
- 16-block 骨架的 block 名称始终用英文（SCENE CONTEXT, ACTIVE REFERENCES 等）。
- block 内容用用户输入语言填写。
- 技术标签始终用英文。
- @tag 始终用英文。
- 镜头语言库始终用英文（`47° diagonal field of view` 等模型固定理解短语）。

---

### D. 参考图清单（Reference Image Manifest）

> **目标**：为每个分镜列清楚「要上传哪些参考图、按什么顺序上传、每张图起什么作用」。
>
> **为什么需要清单**：Seedance 等多参考图工具对上传顺序敏感；参考图用错（把地点参考当首帧、把构图参考当身份锚点）是最常见的一致性崩坏源。

#### D.1 参考图清单文件格式

清单文件统一放 `04-prompts/reference_manifest.md`，按镜号组织。

```markdown
# 参考图清单（Reference Image Manifest）

## shot_001 — <场景块名>

### 角色参考图
| 顺序 | @tag | 图片 | 用途 |
|---|---|---|---|
| 1 | @mei | face close-up (3/4 portrait) | Soul ID 身份锚点 — 脸的唯一取源 |
| 2 | @mei | front headless full body | 身体/服装/比例参考 |
| 3 | @mei | back view | 背面参考（本镜角色背对摄影机） |

### 地点参考图
| 顺序 | @tag | 图片 | 用途 |
|---|---|---|---|
| 4 | @loc_bookstore | main 3/4 view | 空间地理 + 材质 + 氛围参考；禁继构图/角度/色调 |

### 道具参考图
| 顺序 | @tag | 图片 | 用途 |
|---|---|---|---|
| 5 | @prop_letter | hero version | 道具形状/材质/状态参考 |

### 上传顺序（Seedance 关键）
1. @mei face → 2. @mei body → 3. @mei back → 4. @loc_bookstore → 5. @prop_letter

### @tag 角色
- @tag 1–3: 身份锚点（identity anchor）— 模型从这里取脸/身体/服装
- @tag 4: 地理参考（geography reference）— 只取空间与质感，不继承构图
- @tag 5: 道具参考（prop reference）— 100% matches the reference

### 首帧图（如使用图生视频）
- 首帧生图提示词: `04-prompts/image/shot_001_frame.md`
- 生成首帧后，作为图生视频的输入首帧
```

#### D.2 参考图上传规则

1. **角色参考图三张固定顺序**：face close-up → front headless full body → back view
   - face 是脸的唯一取源（正面无头全身使模型别无选择）
   - front headless 提供身体/服装/比例
   - back view 在角色背对摄影机时必需

2. **地点参考图带禁继指令**：在提示词的 ACTIVE REFERENCES 中写明
   ```
   @loc_bookstore for location reference — take only the space and the texture:
   raw wood, amber light, shelf geography. Do not use as a starting frame, do not
   inherit the composition, the angle or the grade.
   ```

3. **道具参考图格式**：
   ```
   @prop_letter for prop reference — aged cream paper, folded once, dense
   cursive in faded blue-black ink. 100% matches the reference.
   ```

4. **状态变体**：如本镜角色为特定状态（如 `@mei_wet`），上传该状态变体图而非基础角色图

5. **首帧图优先**：如使用图生视频模式，首帧图作为第一张上传，角色/地点/道具参考图作为后续补充

6. **无多参考图锚点工具的降级**：Kling、Veo 等工具无多参考图锚点机制。替代策略：descriptor 逐字进提示词 + 首帧图作图生视频输入

---

### E. 交付物文件清单（Deliverable File Manifest）

> **目标**：项目交付时，产出一份总清单，列出所有文件、路径与描述，确保项目可「复拍任何一镜」。

#### E.1 交付物清单文件格式

清单文件放 `08-delivery/deliverable-manifest.md`。

```markdown
# 交付物总清单（Deliverable File Manifest）

## 项目信息
- 项目名: <project_name>
- 体裁: <横屏电影 / 横屏短剧 / 漫剧 / 竖屏短视频>
- 总时长: <NNs>
- 画幅: <16:9 / 9:16>
- 生成渠道: <外部工具>
- 镜头数: <N>

## 交付物索引

### 00-brief/
| 文件 | 描述 |
|---|---|
| brief.md | 需求确认书：体裁/时长/画幅/渠道/风格/声音 |

### 01-assets/
| 文件 | 描述 |
|---|---|
| characters/mei.md | @mei descriptor + 行为主档 |
| characters/mei_image_prompt.md | @mei 生图提示词（LIRA 格式） |
| characters/mei_reference_guide.md | @mei 参考图规格说明 |
| characters/jax.md | @jax descriptor + 行为主档 |
| ... | ... |
| locations/loc_bookstore.md | @loc_bookstore descriptor |
| locations/loc_bookstore_image_prompt.md | @loc_bookstore 生图提示词 |
| locations/loc_bookstore_reference_guide.md | @loc_bookstore 参考图规格说明 |
| props/prop_letter.md | @prop_letter descriptor |
| props/prop_letter_image_prompt.md | @prop_letter 生图提示词 |

### 02-registry/
| 文件 | 描述 |
|---|---|
| asset-registry.md | 全项目唯一 @tag 命名词典 |

### 03-shotlists/
| 文件 | 描述 |
|---|---|
| block_01_bookstore.md | 场景块 1 分镜表 + GEO |
| block_02_letter.md | 场景块 2 分镜表 + GEO |

### 04-prompts/
| 文件 | 描述 |
|---|---|
| video/shot_001_v3.md | shot 001 视频提示词 v3（CINEDANCE 16-block） |
| video/shot_002_v1.md | shot 002 视频提示词 v1 |
| video/shot_summaries.md | 全部镜头中文摘要 |
| image/shot_001_frame.md | shot 001 首帧生图提示词 |
| image/shot_002_frame.md | shot 002 首帧生图提示词 |
| reference_manifest.md | 参考图清单（每镜用哪些参考图） |

### 05-generations/
| 文件 | 描述 |
|---|---|
| shot_001/ | shot 001 全部生成素材 |
| shot_002/ | shot 002 全部生成素材 |

### 06-logs/
| 文件 | 描述 |
|---|---|
| iteration-log.md | 迭代日志（哪版成了、改了什么、判定） |

### 07-post/
| 文件 | 描述 |
|---|---|
| post-production-notes.md | 调色/声音/清理指引 |

### 08-delivery/
| 文件 | 描述 |
|---|---|
| deliverable-manifest.md | 本文件（交付物总清单） |
| UI-PARAMS.md | UI 参数设置 + 参考图上传顺序 |

## 归档校验
- [ ] 每镜最终提示词（含版本号）与生成素材可对应
- [ ] asset-registry 与 01-assets 一一对应，@tag 无孤儿
- [ ] iteration-log 完整（哪一版成了、为什么）
- [ ] 清理记录：哪些镜做过点修/重生成
- [ ] 一句经验：本次翻车点 → 回写进 skill 对应 reference
```

#### E.2 UI-PARAMS.md 文件格式

```markdown
# UI 参数设置 + 参考图上传顺序

> 用法：本文件记录每镜在生成工具 UI 中需要设置的参数。这些参数绝不写进提示词文本。

## shot_001

### UI 参数
| 参数 | 值 |
|---|---|
| 模型 | Seedance 2.0 |
| 模式 | R2V (多参考图) |
| 画幅 | 9:16 |
| 时长 | 5s |
| 分辨率 | 2k |
| fps | 24 |

### 参考图上传顺序
1. @mei face close-up → 身份锚点
2. @mei front headless full body → 身体参考
3. @loc_bookstore main view → 地理参考
4. @prop_letter hero → 道具参考

### 首帧图（图生视频模式）
- 文件: 05-generations/shot_001/first_frame.png
- 来源: 用 04-prompts/image/shot_001_frame.md 在 Soul Cinema 生成
- 用途: 图生视频首帧输入
```

---

## 2. 时长优化系统（Duration Optimization System）

> **问题**：视频模型有单次最大时长限制，且不同模型差异巨大。镜头时长不能随意拍脑袋——要基于动作复杂度、情绪重量、对白长度、镜头运动和叙事节奏综合决策。
>
> **本节解决**：每镜分多少秒？总时长怎么分配？超了怎么压缩？不够怎么补？

### 视频模型能力感知表

> **重要说明**：
> - **视频模型选用前必须询问用户**（见下方「视频模型选用流程」）。

| 模型 | 厂商 | 单次最大时长 | 画幅支持 | 参考图锚点 | 核心优势 |
|---|---|---|---|---|---|
| **Seedance 2.5** | 字节跳动 | **30秒** | 16:9, 9:16, 1:1 | 多参考图 | 指令遵循、长叙事、真人感、声画质感大幅提升；适合复杂动作序列与长对白 |
| **Seedance 2.0** | 字节跳动 | **15秒** | 16:9, 9:16, 1:1 | 多参考图 | 多镜头叙事、角色一致性；性价比高 |
| **Kling 3.0** | 快手 | **15秒** | 16:9, 9:16 | 图生视频 | 物理精确（偏差<5%）、角色一致性（偏差<5%）；适合动作与物理交互场景 |
| **Kling 3.0 Omni** | 快手 | **15秒** | 16:9, 9:16 | 首尾帧控制 | 原生音画同步、唇形同步；适合需要同步音频的对白镜 |
| **Veo 3** | Google | **8秒** | 16:9, 9:16 | 文生视频 + 图生视频 | 原生音频生成（SFX/对白/环境声）、电影级画质；适合短而精的氛围镜 |

### 视频模型选用流程（Ask User First）

> **铁律：视频模型选用前，必须先询问用户。** 不同模型在时长上限、画幅、参考图机制、音频能力上差异巨大，agent 不可替用户决定。

#### 询问时机

在 **阶段 0（需求澄清）** 中，确定体裁/时长/画幅后，询问用户：

```
你计划用哪个视频生成模型？

可选模型及核心差异：
- Seedance 2.5：单次最长30秒，多参考图，长叙事最强（字节跳动）
- Seedance 2.0：单次最长15秒，多参考图，性价比高（字节跳动）
- Kling 3.0：单次最长15秒，物理精确，图生视频（快手）
- Kling 3.0 Omni：单次最长15秒，原生音画同步+唇形同步（快手）
- Veo 3：单次最长8秒，原生音频生成，电影级画质（Google）

如未指定，默认推荐 Seedance 2.5（时长上限最大，多参考图一致性最强）。
```

#### 选用决策树

```
用户已指定模型？
├── 是 → 按指定模型的能力约束设计分镜时长
└── 否 → 询问用户（上方话术）
         └── 用户仍未明确 → 默认 Seedance 2.5
              ├── 需要原生音频同步？ → 推荐 Kling 3.0 Omni 或 Veo 3
              ├── 需要极致物理精确？ → 推荐 Kling 3.0
              ├── 需要最长单镜时长？ → 推荐 Seedance 2.5（30s）
              └── 需要电影级短氛围镜？ → 推荐 Veo 3（8s，带原生音频）
```

#### 模型能力对分镜设计的影响

| 模型能力 | 对分镜设计的影响 |
|---|---|
| Seedance 2.5（30s） | 复杂动作序列可不拆镜；长对白单镜可完成 |
| Seedance 2.0 / Kling 3.0（15s） | 超过 15s 的动作必须拆镜硬切 |
| Veo 3（8s） | 单镜极短，适合快切风格；原生音频可省后期配音 |
| Kling 3.0 Omni | 对白镜可依赖原生唇形同步，减少后期 |
| 多参考图（Seedance 系列） | 角色/地点/道具参考图可分别上传，一致性最强 |
| 图生视频（Kling/Veo 3） | 首帧图质量决定整段视频质量；必须先生成高质量首帧 |

### 图像模型能力感知表

> 图像模型用于资产生图（角色/地点/道具）和分镜首帧生图。模型选用由 LIRA 路由规则自动决定（见 `12-lira-image-prompt.md`），但 agent 应了解各模型核心差异，在推荐时给用户清晰指引。

| 模型 | 厂商 | 分辨率 | 核心优势 | 最擅长 | 弱项 |
|---|---|---|---|---|---|
| **GPT Image 2** | OpenAI | 1k/2k/4k | 极致照片真实感、提示词遵循极强 | 照片级真实感、自然度、地点视角变更、最细局部微编辑 | 图层/区域编辑弱、整体帧偏「脏」 |
| **Nano Banana Pro (NBP)** | Google (Gemini 3 Pro Image) | 1k/2k/4k | 像素级细节控制、会话式编辑、多语言文字渲染 | 帧编辑（永远首选）、道具生成、文字渲染、复杂图表 | — |
| **Nano Banana 2** | Google | 1k/2k/4k | 清晰可读文字、角色跨场景一致性、自然语言编辑 | 文字渲染、角色一致性、信息图 | 区域编辑不如 Pro |
| **Seedream 5.0 Pro** | 字节跳动 | 2k/4k | 图层分离、精准区域编辑、结构化信息可视化、多语言文字 | 商业视觉、图层分离、信息图、与 Seedance 工作流配合 | 极端照片真实感略逊 GPT Image 2 |

#### 图像模型选用速查

| 任务 | 首选模型 | 理由 |
|---|---|---|
| 角色生成（选角表/肖像） | Soul 2.0 / Cinema Studio AI Cast | 角色生成专用，Soul ID 跨生成锁定 |
| 地点/环境/电影帧 | Soul Cinema | 电影级质感，支持 21:9 |
| 道具/产品式物体 | NBP / GPT Image 2 | 真实产品语境，精确文字渲染 |
| 帧编辑（任何改动） | **NBP 永远第一** | 原图的后期处理，最小改动 |
| 渣 AI 纹理修复 | Seedream 5.0 Pro | 纹理 pass（皮肤/布料/表面） |
| 最细局部微编辑 | GPT Image 2 | 最后手段，局部强但全局脏 |
| 商业视觉/信息图/海报 | Seedream 5.0 Pro | 图层分离+结构化输出最强 |
| 地点视角变更（反打） | GPT Image 2 | 表现好；NBP 需明确写出新物体排布 |
| 与 Seedance 配合的关键帧 | Seedream 5.0 Pro | 与 Seedance 工作流无缝衔接 |

**使用规则**：
- 单镜时长不超过所用视频模型的最大时长限制
- 如单镜动作需要超过模型最大时长，拆成两镜（硬切），不强行塞进一个 prompt
- Veo 3 只有 8 秒——适合短氛围镜和快切，不适合复杂动作序列
- Seedance 2.5 的 30 秒上限适用于复杂动作序列或长对白镜
- 图像模型路由由 LIRA 4-D 方法论自动决定（见 `12-lira-image-prompt.md`）

### 时长决策五因素

每镜时长由以下五个因素综合决定。取五者中要求最高的那个为基准，再按总时长约束微调。

#### 因素 1：动作复杂度（Action Complexity）

| 动作类型 | 建议时长 | 说明 |
|---|---|---|
| 简单动作（站立阅读、静坐、单手操作） | 3–5s | 够看清就够 |
| 中等动作（走路 + 互动、开门 + 转身） | 5–8s | 运动需要展开空间 |
| 复杂动作序列（打斗 + 多人、跑 + 跳 + 落地） | 8–15s | 需要时间让物理发生 |
| 超过 15s 的动作 | 拆镜 | 超过模型上限，拆成两镜硬切 |

**关键规则**：复杂动作放在提示词开头「已发生」（状态非过渡），不写到达过程。走到门口是另一镜。

#### 因素 2：情绪重量（Emotional Weight）

| 情绪类型 | 建议时长 | 说明 |
|---|---|---|
| 情绪铺垫镜（环境空镜、氛围建立） | 3–5s | 建立空间即可，不拖 |
| 情绪反应镜（特写、眼神变化、评估时刻） | 4–6s | 需要看到反应的展开 |
| 情绪高潮镜（核心戏剧时刻、崩溃/转折） | 6–10s | 情绪需要付出代价才可信 |

**关键规则**：评估时刻（assessment moment）是电影最值钱的帧——给它时间。但铺垫镜别拖，竖屏尤其要快。

#### 因素 3：对白长度（Dialogue Length）

| 对白类型 | 建议时长 | 计算方式 |
|---|---|---|
| 无对白 | 3–6s | 纯动作或环境 |
| 单句对白（1 句台词 + 反应） | 4–8s | 台词 2–3s + 反应 1s + 首尾静默各 1s |
| 多轮对白（2–3 轮） | 8–15s | 每句 2–3s + 反应 1s；首尾静默各 1s |

**关键规则**：
- 每句台词前后至少 1 秒静默（除非要求立刻说话）
- 台词在主镜前 0.3 秒内开始（如需立刻说话）
- 多轮对白如超过 15s，考虑拆镜
- 台词只在 AUDIO 段，动作段零台词

#### 因素 4：镜头运动（Camera Movement）

| 运动类型 | 建议时长 | 说明 |
|---|---|---|
| 固定机位（locked-off tripod） | 3–6s | 够看清就行 |
| 缓慢运动（推/拉/摇/微降） | 5–10s | 运动需要时间展开 |
| 复杂运动（跟拍 + 变焦、环绕） | 8–15s | 多段运动需要时间 |

**关键规则**：摄影机运动写为物理操作员行为。固定机位标准措辞：`Locked-off tripod, perfectly still — no handheld, no push, no zoom, no reframe, no pan, no tilt.`

#### 因素 5：叙事节奏（Narrative Pacing）

| 镜头功能 | 建议时长 | 说明 |
|---|---|---|
| 开场钩子镜（尤其竖屏） | 3–5s | 竖屏前 3 秒必须有钩子 |
| 过渡镜（场景间连接） | 2–4s | 越短越好 |
| 核心叙事镜（推进剧情的关键镜） | 5–10s | 给足时间讲清 |
| 收束镜（情绪尾声、定格） | 3–6s | 留余韵但不拖 |

**关键规则**：竖屏开场钩子镜必须快——3 秒内建立冲突/悬念。横屏可稍慢但也别超过 5 秒开场。

### 时长优化规则

#### 基本规则

1. **总时长 = 所有镜头时长之和**，必须在用户指定的总时长范围内
2. **优先给核心叙事镜和高潮镜分配更多时间**
3. **开场和过渡镜尽量短**（竖屏尤其要快）
4. **单镜不超过模型最大时长限制**（见上方模型能力感知表）
5. **如总时长超出**：优先压缩过渡镜和环境镜
6. **如总时长不足**：为高潮镜增加 1–2s（不要平均分配）

#### 镜头数建议

| 总时长 | 建议镜头数 | 平均单镜时长 |
|---|---|---|
| 30 秒（竖屏短视频） | 5–7 镜 | 4–6s |
| 60 秒（短剧/短视频） | 8–12 镜 | 5–7.5s |
| 120 秒（短剧/品牌片） | 15–20 镜 | 6–8s |
| 600 秒以上（长片场景块） | 按场景块 | 8–12s/镜 |

#### 时长分配优先级

当总时长紧张需要压缩时，按以下优先级从低到高保护：

1. **最低优先（先压）**：过渡镜、环境空镜、定场镜
2. **中优先**：情绪铺垫镜、反应镜（非高潮）
3. **高优先**：核心叙事镜、对白镜
4. **最高优先（最后压）**：情绪高潮镜、开场钩子镜、收束镜

当总时长有余量时，按相反顺序增加——先给高潮镜加，再给核心叙事镜加。

### 时长决策范例

> **案例**：「书店信件」30 秒竖屏短剧（9:16）
>
> 故事：女孩梅在旧书店发现一封藏在书页间的信，读信后情绪变化，最终将信放回原处。
>
> 生成渠道：Seedance 2.0（单次最大 15s，支持多参考图，9:16）

#### 分镜时长分析

| 镜号 | 场景描述 | 动作复杂度 | 情绪重量 | 对白 | 镜头运动 | 叙事节奏 | 决策时长 | 理由 |
|---|---|---|---|---|---|---|---|---|
| 001 | 梅走进书店，扫视书架 | 中等（走路 + 环顾） | 铺垫（3–5s） | 无（3–6s） | 缓慢跟拍（5–10s） | 开场钩子（3–5s） | **5s** | 开场必须快，竖屏前 3 秒建立场景与人物；走路 + 环顾属中等动作 5s 够；无对白省时间 |
| 002 | 梅在书架前抽出书，信件掉出 | 中等（手部动作 + 反应） | 反应（4–6s） | 无 | 固定中近景（3–6s） | 核心叙事（5–10s） | **5s** | 发现信件是第一个叙事钩子；手部动作 + 掉落 + 抬头反应需要完整节拍；固定机位省时间 |
| 003 | 梅捡起信，开始阅读 | 简单（站立阅读） | 反应→高潮过渡（4–6s） | 无 | 缓慢推近（5–10s） | 核心叙事（5–10s） | **6s** | 推近运动需要时间展开；阅读 + 表情变化是情绪转折点；这是内容最重的非高潮镜，给 6s |
| 004 | 梅脸部特写，读信反应 | 简单（微表情） | 高潮（6–10s） | 无 | 固定特写（3–6s） | 核心叙事高潮（5–10s） | **6s** | 评估时刻最值钱——给脸时间让情绪付出代价；特写固定机位不需要太长但情绪需要 6s；这是全片情绪顶点 |
| 005 | 梅将信折好放回书页间 | 中等（手部精细动作） | 收束（3–6s） | 无 | 固定中景（3–6s） | 收束（3–6s） | **4s** | 放回动作简单果断；收束镜不留太长；4s 够完成动作 + 留余韵 |
| 006 | 梅离开书店，回头看一眼书架 | 中等（转身 + 走） | 收束（3–6s） | 无 | 固定远景或缓慢拉远（5–10s） | 收束（3–6s） | **4s** | 离开 + 回头是情绪尾巴；拉远运动需要一点时间但不宜拖；竖屏结尾要干净 |

#### 总计

| 镜号 | 时长 | 累计 |
|---|---|---|
| 001 | 5s | 5s |
| 002 | 5s | 10s |
| 003 | 6s | 16s |
| 004 | 6s | 22s |
| 005 | 4s | 26s |
| 006 | 4s | 30s |

**总计 30s，6 镜，符合「30 秒竖屏建议 5–7 镜」。**

#### 决策说明

- **高潮镜（004）给了 6s**——全片情绪顶点，评估时刻最值钱，但不超过 Seedance 2.0 的 15s 上限
- **开场钩子镜（001）只给 5s**——竖屏前 3 秒必须有钩子，5s 够建立场景 + 人物 + 动态
- **过渡与收束镜（005/006）各 4s**——尽量短，留时间给核心叙事
- **核心叙事镜（002/003）各 5–6s**——发现信件 + 阅读转折需要完整节拍
- **无对白**——全片无台词，省下的时间全部分配给动作展开和情绪
- **镜头运动**：001 跟拍、003 推近是仅有的两处运动镜，各给了足够时间（5s/6s）让运动展开

#### 如需压缩到 25s

按优先级压缩：
- 005 从 4s → 3s（收束镜，先压）
- 006 从 4s → 3s（收束镜）
- 001 从 5s → 4s（开场镜，但竖屏钩子时间不能太短——保留 4s 底线）
- 002 从 5s → 4s（核心叙事但非高潮）
- 003/004 不动（高潮与核心转折，最后压）

结果：4+4+6+6+3+3 = 26s → 再压 001 到 3s = 25s。

#### 如需扩展到 45s

按优先级扩展：
- 004 从 6s → 8s（高潮镜，先加）
- 003 从 6s → 8s（核心转折镜）
- 001 从 5s → 6s（开场可稍展）
- 其余不动

结果：6+5+8+8+4+4 = 35s → 还差 10s → 可在 002 加 2s（7s）、005 加 3s（7s）、006 加 5s（9s，拉远运动给足时间）= 6+7+8+8+7+9 = 45s。

---

## 3. 交付物文件组织规范（File Organization）

> **目标**：统一所有项目的文件组织方式，确保项目可「复拍任何一镜」——任何人拿到项目文件夹，能找到任何一镜的提示词、参考图、生成素材与迭代记录。

### 输出目录结构

```
<output_directory>/<project_name>/
├── README.md                           # 项目概览（brief + 交付物索引）
├── 00-brief/
│   └── brief.md                        # 需求确认书
├── 01-assets/
│   ├── characters/
│   │   ├── <tag>.md                    # 角色 descriptor + 行为主档
│   │   ├── <tag>_image_prompt.md       # 角色生图提示词（LIRA 格式）
│   │   └── <tag>_reference_guide.md    # 参考图规格说明
│   ├── locations/
│   │   ├── <loc_tag>.md                # 地点 descriptor
│   │   ├── <loc_tag>_image_prompt.md   # 地点生图提示词
│   │   └── <loc_tag>_reference_guide.md
│   └── props/
│       ├── <prop_tag>.md               # 道具 descriptor
│       └── <prop_tag>_image_prompt.md  # 道具生图提示词
├── 02-registry/
│   └── asset-registry.md               # @tag 词典
├── 03-shotlists/
│   └── block_<NN>_<name>.md            # 分镜表 + GEO
├── 04-prompts/
│   ├── video/                          # 视频提示词
│   │   ├── shot_<NNN>_v<N>.md          # CINEDANCE 16-block 视频提示词
│   │   └── shot_summaries.md           # 中文摘要（单独文件）
│   ├── image/                          # 分镜画面生图提示词
│   │   └── shot_<NNN>_frame.md         # 首帧生图提示词
│   └── reference_manifest.md           # 参考图清单（每镜用哪些参考图）
├── 05-generations/                     # 用户生成的素材（按镜号归档）
│   └── shot_<NNN>/                     # 该镜全部生成素材
├── 06-logs/
│   └── iteration-log.md                # 迭代日志
├── 07-post/
│   └── post-production-notes.md        # 调色 / 声音指引
└── 08-delivery/
    ├── deliverable-manifest.md         # 交付物总清单
    └── UI-PARAMS.md                    # UI 参数设置 + 参考图上传顺序
```

### 与 pipeline runbook 目录结构的关系

本目录结构是 `01-pipeline-runbook.md` §0 项目目录脚手架的**扩展版**，新增以下内容：

| 新增 | 位置 | 说明 |
|---|---|---|
| 角色生图提示词 | `01-assets/characters/<tag>_image_prompt.md` | LIRA 格式资产生图提示词 |
| 角色参考图规格说明 | `01-assets/characters/<tag>_reference_guide.md` | 参考图规格与上传说明 |
| 地点生图提示词 | `01-assets/locations/<loc_tag>_image_prompt.md` | LIRA 格式地点生图 |
| 地点参考图规格说明 | `01-assets/locations/<loc_tag>_reference_guide.md` | |
| 道具生图提示词 | `01-assets/props/<prop_tag>_image_prompt.md` | LIRA 格式道具生图 |
| 视频提示词子目录 | `04-prompts/video/` | 视频提示词独立子目录 |
| 首帧生图提示词 | `04-prompts/image/shot_<NNN>_frame.md` | 新增交付物类型 |
| 参考图清单 | `04-prompts/reference_manifest.md` | 每镜参考图上传清单 |
| 交付目录 | `08-delivery/` | 交付物总清单 + UI 参数 |
| 后期指引 | `07-post/post-production-notes.md` | 调色 / 声音 / 清理指引 |

### 文件命名规范

1. **所有文件名用英文小写 + 下划线**
   - 正确：`shot_003_v2.md`、`loc_bookstore_image_prompt.md`
   - 错误：`Shot003.md`、`书店_地点_提示词.md`

2. **镜号三位数**：`shot_001`, `shot_002`, …, `shot_012`, …, `shot_128`
   - 三位数保证排序正确（`shot_012` 排在 `shot_003` 之后而非之前）

3. **版本号**：`v1`, `v2`, `v3`, …
   - 每次 surgical 迭代（一次改一行）升一个版本号
   - 版本号与 `iteration-log.md` 一一对应
   - 最终版标 `✅ 定稿`；迭代中标 `🔄 迭代中`

4. **中文项目名用拼音或英文翻译**
   - `bookstore_letter`（而非 `书店信件`）
   - 或 `shudian_xinjian`（拼音，仅当英文翻译不便时）

5. **@tag 命名**（继承 `01-pipeline-runbook.md` 规范）
   - 小写、下划线、唯一
   - 角色：`@mei`、`@jax`
   - 地点带前缀：`@loc_bookstore`、`@loc_bookstore_night`
   - 道具带前缀：`@prop_letter`、`@prop_letter_bloodied`
   - 状态变体在原 tag 后加状态：`@mei_wet`、`@mei_blood`
   - 同一 tag 处处一致：文件名、参考图文件夹、提示词内 ACTIVE REFERENCES、分镜表、日志

### README.md 格式

```markdown
# <project_name>

## 项目概览
- 体裁: <横屏电影 / 横屏短剧 / 漫剧 / 竖屏短视频>
- 总时长: <NNs>
- 画幅: <16:9 / 9:16>
- 生成渠道: <外部工具>
- 镜头数: <N>
- 风格: <写实电影感 / 亮调平台风>

## 交付物索引
- 需求确认书: 00-brief/brief.md
- 资产: 01-assets/
- @tag 词典: 02-registry/asset-registry.md
- 分镜表: 03-shotlists/
- 视频提示词: 04-prompts/video/
- 首帧生图提示词: 04-prompts/image/
- 参考图清单: 04-prompts/reference_manifest.md
- 生成素材: 05-generations/
- 迭代日志: 06-logs/iteration-log.md
- 后期指引: 07-post/post-production-notes.md
- 交付物总清单: 08-delivery/deliverable-manifest.md
- UI 参数: 08-delivery/UI-PARAMS.md

## 场景块列表
| 块号 | 名称 | 镜号范围 | GEO 文件 |
|---|---|---|---|
| 01 | 书店发现 | 001–006 | 03-shotlists/block_01_bookstore.md |
```

---

## 4. 语言路由系统（Language Routing）

> **目标**：根据用户在 agent 中输入的语言，决定提示词用什么语言写、说明文字用什么语言写。
>
> **核心原则**：**提示词语言 = 用户输入语言**（技术术语保持英文）。不因目标工具改变。

### 规则

- **提示词语言 = 用户输入语言**
  - 用户输入中文 → 中文提示词
  - 用户输入英文 → 英文提示词
  - 用户输入日文 → 日文提示词
  - 其他语言 → 对应语言提示词
- **始终用英文的部分**：block 名称、技术标签、@tag、镜头语言库
- **说明文字（给用户看的解释、注释、清单描述）** 与用户输入语言一致

### 语言路由表

| 用户输入语言 | 提示词语言 | 说明文字语言 |
|---|---|---|
| 中文 | **中文** | 中文 |
| 英文 | **英文** | 英文 |
| 日文 | **日文** | 日文 |
| 其他语言 | **对应语言** | 对应语言 |

### 多语言提示词规则

CINEDANCE 16-block 骨架与 LIRA 提示词在多语言环境下的处理规则：

| 组成部分 | 语言规则 | 说明 |
|---|---|---|
| 16-block 骨架的 block 名称 | **始终用英文** | `SCENE CONTEXT`, `ACTIVE REFERENCES`, `LOCATION MAP`, `FIRST FRAME AND SPATIAL BLOCKING`, `FORMAT MODE`, `OPTICS`, `CAMERA`, `ACTION TIMING`, `PHYSICS`, `LIGHTING`, `AUDIO`, `CHARACTER ACTING`, `STYLE`, `QUALITY`, `POSITIVE CONSTRAINTS` |
| block 内容 | **用用户输入语言填写** | 中文输入写中文内容，英文输入写英文内容，日文输入写日文内容 |
| Style Prefix 的根条款 | 可翻译但**保留英文技术术语** | 如 `Skin: 毛孔级真实` 可接受，但 `catch-lights`、`vellus hair` 等保留英文 |
| 技术标签 | **始终用英文** | `Photorealistic. NON-IP. 16:9. 5s. SFX only. NO CGI. Cinematic.` — 模型通用理解 |
| descriptor | **用用户输入语言写** | 中文输入 → 中文 descriptor；英文输入 → 英文 descriptor；依此类推 |
| @tag | **始终用英文** | `@mei`, `@loc_bookstore`, `@prop_letter` — 平台原生参考句柄 |
| 镜头语言库 | **始终用英文** | `47° diagonal field of view`, `29° short telephoto portrait` 等 — 模型对这些英文短语有固定理解 |
| GEO SPATIAL LAYOUT | block 名英文，内容用户输入语言 | `GEO SPATIAL LAYOUT (locked across every shot — pure spatial map):` 后跟用户输入语言内容 |
| 摘要 | **用用户输入语言** | `shot_summaries.md` 中的摘要用用户输入语言，2–3 句 |

### 语言路由实操指引

#### 判断流程

```
用户发来第一条消息
    │
    ├── 检测用户输入语言
    │   ├── 中文 → 提示词用中文，说明用中文
    │   ├── 英文 → 提示词用英文，说明用英文
    │   ├── 日文 → 提示词用日文，说明用日文
    │   └── 其他语言 → 提示词用对应语言，说明用对应语言
    │
    └── 无论哪种语言：
        - block 名称始终英文
        - 技术标签始终英文
        - @tag 始终英文
        - 镜头语言库始终英文
```

#### 中文提示词范例（block 名称英文，内容中文）

```text
SCENE CONTEXT
EXACT 2 CHARACTERS — NO DUPLICATES: 梅、杰克。独立旧书店内，傍晚。
梅在书架前发现一封藏在书页间的旧信，正低头阅读。杰克从门口走进来，手里端着两杯咖啡。
单镜连续拍，8秒，无切。

ACTIVE REFERENCES
@mei for character reference — 纤瘦年轻女性，东亚面孔，齐下巴黑直发，炭灰色高领毛衣，左腕细编绳手链。正在读信，信纸在胸前右手。
@jax for character reference — 高瘦年轻男性，浅棕卷发，卡其夹克，手里端着两杯外带咖啡。
@loc_bookstore for location reference — 取空间与质感：旧木书架、琥珀窗光、绿台灯。不作为起始帧，不继承构图、角度或色调。

LOCATION MAP
中央阅读桌在画面中央偏左，桌上绿色银行家台灯亮着。书架沿左右墙排列，向画面深处延伸。前柜台在画面右前景。窗户在画面左后方，琥珀色光线斜射进来，在地板上拉出长影。摄影机在房间右前角，朝左后方看，不越过这条轴线。

FIRST FRAME AND SPATIAL BLOCKING
首帧已为完整画面：梅在画面左中位置，面朝书架，背 3/4 对摄影机，右手持信在胸口高度。杰克在画面右远景门口，刚踏入一步。无空定场的，无延迟揭示。空间关系在首帧即可读出。

FORMAT MODE
单镜连续拍，8秒，实时，无切，无变速。

OPTICS
约 47° diagonal field of view，标准镜头，摄影机距梅约 3 米，景深足以同时保持梅和门口清晰。

CAMERA
平稳手持，保持构图——梅转头时有几度微调，无推拉无变焦。

ACTION TIMING
0.0–2.0s — 画面静止：梅低头读信，杰克在门口停住。
2.0–5.0s — 梅的眼角余光先到门口，然后头转过去；杰克举起一杯咖啡示意。
5.0–8.0s — 梅嘴角微微一松，把信折好塞回书页间。

PHYSICS
信纸有真实重量——折叠时纸面有阻力。咖啡杯液面随杰克停步微晃。

LIGHTING
主光源为画面左后方窗户的琥珀色光。摄影机在梅的阴影侧——她的背和右脸被窗光勾出轮廓，正脸落入柔和暖影。台灯在桌上投出小片冷绿光斑。无平正光，无补光。

AUDIO
现场声——书店环境嗡鸣，翻页声，脚步声。梅嗓音（逐字粘贴）：「二十多岁女声，轻而稳，普通话，读东西时语速放慢，习惯在句尾轻轻收气。」她的台词，只有这一句：「你来了。」杰克不说话。无音乐。

CHARACTER ACTING
梅 — 想独处读完这封信，被打断后收起情绪。主导节奏：慢、经济、内敛。可见习惯：读信时左手指无意识摩挲书脊；被打断时先眼到再头转。变化：门开的一刻她把信折好——不是藏，是收尾。
杰克 — 端着咖啡进来，看到她在读东西，举起杯子示意「不打扰」，在门口停住。grin 半拍后落——他读出了空气。

STYLE
[Style Prefix，逐字粘贴——竖屏暗调版或电影感原版，按场景选]

QUALITY
8K detail, pore-level skin, no jitter, no flicker; the two faces stay exactly their references at every distance.

POSITIVE CONSTRAINTS
Exactly two people in the bookstore, and no one else. Exactly ONE letter, in Mei's right hand, aged cream paper folded once — never unread, never duplicated. The camera stays on the front-right corner side for all eight seconds. Photorealistic. NON-IP. 9:16. 8s. SFX only. NO CGI. Cinematic.
```

> **注意**：上例中 block 名称（SCENE CONTEXT 等）和技术标签（`Photorealistic. NON-IP.`）始终用英文，block 内容用中文。镜头语言库（`47° diagonal field of view`）始终用英文。

### 语言路由与渠道的关系

| 渠道 | 提示词语言 | 说明 |
|---|---|---|
| 外部工具（任何模型） | 用户输入语言 | 提示词语言跟随用户输入，不因工具改变 |

### 多语言交付的特殊处理

当用户需要**双语交付**（如同时给中文和英文团队用）时：

1. 产出两份提示词文件：
   - `shot_<NNN>_v<N>_zh.md`（中文版）
   - `shot_<NNN>_v<N>_en.md`（英文版）
2. 两份内容完全对应，仅语言不同
3. block 名称两份都用英文
4. 技术标签两份都用英文
5. 摘要用各自语言分别产出

---

## 附录：交付物与 pipeline 阶段映射

| 阶段 | 交付物 | 本文件章节 | 模板 / reference |
|---|---|---|---|
| 0 需求澄清 | brief.md | §3 目录结构 | `01-pipeline-runbook.md` §2 |
| 1 剧本解析 | 场景块清单 | §3 目录结构 | `01-pipeline-runbook.md` §3 |
| 2 资产清单注册 | asset-registry.md | §3 目录结构 | `assets/templates/asset-registry.md` |
| 3 资产图生成 | 资产生图提示词（A 类） | §1.A | `12-lira-image-prompt.md` |
| 4 压力测试锁定 | 压力测试操作指引 | — | `00-overview-handbook.md` §3.5 |
| 5 分镜表 | shotlist + GEO | §3 目录结构 | `assets/templates/shotlist.md` + `geo-spatial-layout.md` |
| 6 逐镜提示词 | 视频提示词（C 类）+ 首帧生图提示词（B 类）+ 参考图清单（D 类） | §1.B / §1.C / §1.D | `10-cinedance` + `12-lira` + 本文件 |
| 7 生成 | 生成素材入库 | §3 目录结构 | `01-pipeline-runbook.md` §5 |
| 8 迭代 | iteration-log.md | §3 目录结构 | `assets/templates/iteration-log.md` |
| 9 清理 | 清理记录 | §3 目录结构 | `20-qa-checklists.md` Part C |
| 10 调色声音 | post-production-notes.md | §3 目录结构 | `00-overview-handbook.md` §7 |
| 11 交付归档 | 交付物总清单（E 类）+ UI-PARAMS.md | §1.E | 本文件 |
