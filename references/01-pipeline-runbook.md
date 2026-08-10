# 01 Pipeline Runbook — 端到端制片操作规程

> 定位：从「一句想法」到「成片」的 12 阶段操作规程。
>
> 总原则：**每阶段有明确交付物，不达标不进下一阶段。资产未锁定（阶段 4 通过）之前，不生成任何镜头。**

---

## 0. 项目目录脚手架

接到新项目，先按模板 `assets/templates/project-structure.md` 建目录：

```
<project>/
├── 00-brief/            # 需求、剧本/文案、创意参考
├── 01-assets/           # 资产原文（descriptor + 参考图）
│   ├── characters/      # 每角色一个 .md + 3 张表图 + 状态变体
│   ├── locations/       # 每地点一个 .md + 表图（日/夜/雨为独立资产）
│   └── props/           # 每道具一个 .md + 表图（多版本）
├── 02-registry/         # asset-registry.md —— 全项目唯一 @tag 命名词典
├── 03-shotlists/        # 分镜表，按场景块一个文件
├── 04-prompts/          # 逐镜提示词，版本化命名（shot_012_v3.md）
├── 05-generations/      # 生成素材，按镜头号归档
├── 06-logs/             # iteration-log.md —— 迭代日志
└── 07-post/             # 清理、调色、声音、成片
```

---

## 1. 阶段总览（门禁表）

| # | 阶段 | 交付物（过了才放行） | 模板 / reference |
|---|---|---|---|
| 0 | 需求澄清 | 一页 brief：体裁/时长/画幅/渠道/风格/生成渠道 | 本文件 §2 |
| 0.5 | AI导演扩展 | L1标题→故事 / L2大纲→结构 / L3剧本→解析；产出分镜草案 | `references/14-ai-director.md` |
| 1 | 剧本解析 | 场景块清单（按地点×时间×人物状态切分） | 本文件 §3 |
| 2 | 资产清单与注册 | asset-registry.md：全部角色/地点/道具 + @tag | `assets/templates/asset-registry.md` |
| 3 | 资产图生成 | 每资产：descriptor + 参考图（角色表三图） | `assets/templates/character-sheet.md` 等 + `12-lira-image-prompt.md` |
| 4 | 压力测试与锁定 | 10/10 可识别；同框不崩；声音/行为主档锁定 | `00-overview-handbook.md` §3.5–3.7 |
| 5 | 分镜表 | 每场景块一份 shotlist（镜头号/时长+时长分析/首帧/@tags） | `assets/templates/shotlist.md` |
| 6 | 逐镜提示词 | 每镜 16-block 提示词，过生成前审查 | `assets/templates/shot-prompt-skeleton.md` + `assets/templates/shot-frame-prompt.md` + `references/13-deliverable-system.md` + `10-cinedance-video-prompt.md` + `20-qa-checklists.md` |
| 7 | 生成 | 镜头素材入库（外部工具包） | 本文件 §5 渠道路由 |
| 8 | 迭代 | 迭代日志；10–15 次不成则简化镜头 | `assets/templates/iteration-log.md` |
| 9 | 清理 | slop 图鉴对照清零；脸与手优先 | `20-qa-checklists.md` Part C |
| 10 | 调色 + 声音 | 统一 look；连续 ambience；音乐在后期 | `00-overview-handbook.md` §7 |
| 11 | 交付归档 | 成片 + 完整项目文件（可复拍任何一镜） | `assets/templates/deliverable-manifest.md` + `references/13-deliverable-system.md` §3 + 本文件 §6 |

---

## 2. 阶段 0：需求澄清（必问清单）

开工前向用户确认（缺失则合理假设并注明）：

1. **体裁**：横屏电影感叙事 / 横屏短剧 / 漫剧 / 竖屏短视频？→ 查 §4 体裁适配表
2. **时长与镜头规模**：总时长？大约多少镜？（短片 5–15 镜；短剧集 20–60 镜；长片按场景块）
3. **画幅**：16:9 / 9:16 / 其他（画幅是 UI 参数，不进提示词文本）
4. **生成渠道**：外部工具（Seedance / Kling / Veo 等）→ 查 §5 渠道路由
5. **风格参考**：写实电影感（默认 Style Prefix）还是平台化亮调？
6. **声音**：是否需要台词/配音？（需要 → 阶段 4 必须锁声音）

## 3. 阶段 1：剧本解析 → 场景块

- 把剧本/文案切成**场景块**：以「地点 × 时间（日/夜/雨）× 人物状态」为边界——因为地点的每种状态、角色的每种状态都是独立资产。
- 每个场景块命名（如 `block_03_tibet_heist`），后续 shotlist 按块建文件。
- 对白场景标注节奏点：谁先说话、反应落在谁脸上、有没有「打断活计」的重音时刻（见 `11-acting-performance.md`）。

## 4. 体裁适配表（电影 / 短剧 / 漫剧 / 短视频）

| 维度 | 横屏电影感叙事 | 横屏短剧 | 漫剧 | 竖屏短视频 |
|---|---|---|---|---|
| 画幅 | 16:9（UI 设） | 16:9 | 16:9 或 9:16 | 9:16（UI 设） |
| 单镜时长 | 8–12s 单镜或硬切 | 5–10s，切得更狠 | 4–8s | 3–8s，前 3 秒必须有钩子 |
| 节奏 | 生成偏慢，剪辑比感觉更狠地切 | 同左，且每镜裁掉头尾各半秒 | 分镜感强，panel 式构图 | 同左，且首镜即冲突/悬念 |
| Style Prefix | 原文逐字（8K IMAX 电影感） | 原文逐字 | 漫画风格变体，保留三条根（skin/acting/continuity） | 可用，但按需降格：去掉 IMAX/8K，保留 photoreal/skin/acting 条款；亮调平台风可换 Light 变体 |
| 首帧 | wide establishing | wide establishing | 场景全景或人物半身 | medium portrait（非传统 wide） |
| 字幕 | No subtitles（后期加） | No subtitles（后期加） | No subtitles（后期加） | No subtitles（后期加，竖屏字幕是安全区内的后期元素，绝不让模型生成文字） |
| 表演 | 全套 ACTING 系统 | 全套 | 全套，但动作幅度可风格化 | 收紧：反应前置、节拍更快，特写多→用「镜越紧动越少」条款 |
| 一致性纪律 | **不放松**（GEO/状态资产/逐字 descriptor 全保留） | 不放松 | 不放松 | 不放松——竖屏近距离脸部特写多，换脸更致命 |

**铁律：体裁只改节奏与风格参数，不改一致性纪律。**

> **竖屏首帧例外**：竖屏（9:16）不做传统 wide establishing shot，改用 medium portrait（中景肖像）：人物占画面60%垂直高度，眼睛在上三分线，环境在身后可见。详见 `00-overview-handbook.md` §4.7。

## 5. 阶段 7：生成渠道路由

### 外部工具（Nano Banana / GPT Image / Seedream / Seedance / Kling / Veo 等）

交付**提示词包**，用户自己进工具生成：

- 每镜一个文件（`04-prompts/shot_012_v3.md`）：完整 16-block 提示词（按用户输入语言生成），文末技术标签 `Photorealistic. NON-IP. [画幅]. [时长]s. SFX only. NO CGI. Cinematic.`（技术标签始终英文）
- 附一张 **UI 参数清单**（画幅/时长/分辨率/参考图上传顺序）——这些在工具 UI 里设，绝不写进提示词文本
- **每镜摘要**：放在单独文件 `04-prompts/shot_summaries.md` 中统一管理（不在提示词 .md 文件内），格式为"- 镜XXX：<2-3句，用用户输入语言>"。绝对不要把摘要写进提示词 .md 文件的正文（用户复制时会污染提示词）。如果需要在 .md 文件中加备注，用 HTML 注释包裹（`<!-- 备注 -->`），复制时不会带入。
- 资产图包：按 `01-assets/` 结构打包，文件名 = @tag，与提示词内 ACTIVE REFERENCES 一一对应

**阶段3-4交付形态**（用户在外部工具生成时）：
- 阶段3：为每个资产产出 LIRA 格式的图像提示词（按 `12-lira-image-prompt.md`），让用户可以在 GPT Image 2 / Nano Banana Pro / Seedream 5.0 Pro / Nano Banana 2 中生成参考图。提示词写入对应资产的 .md 文件中（在 Descriptor 段下方加"图像生成提示词"段）。
- 阶段4：产出"资产压力测试操作指引"文档（中文，给用户看的），包含：每资产测试用简单 prompt、参考图上传顺序、10/10 可识别判定标准、失败时 descriptor 修改建议。
- 仅有 Seedance 的用户降级方案：在 Seedance 中用图生视频模式，先用简单 descriptor 生成 3-5 张角色静态图，选最可信的一张作为后续视频的角色参考图。
- 无多参考图锚点的工具（如 Kling、Veo）：使用图生视频模式 + descriptor 逐字注入，是一致性降级下的最强策略。

## 6. 阶段 11：交付归档标准

成片之外，项目目录必须可支持「复拍任何一镜」：

- [ ] 每镜最终提示词（含版本号）与其生成素材可对应
- [ ] asset-registry 与 01-assets 一一对应，@tag 无孤儿
- [ ] iteration-log 完整（哪一版成了、为什么）
- [ ] 清理记录：哪些镜做过点修/重生成
- [ ] 一句经验：本次翻车点 → 回写进本 Skill 的对应 reference（Skill 迭代）

---

## 7. 交付物体系（详见 `13-deliverable-system.md`）

### 交付物五类
1. **资产生图提示词**：每个角色/地点/道具的 LIRA 优化图像提示词，让用户可在 GPT Image 2 / NBP / Seedream 5.0 Pro / Nano Banana 2 中生成参考图
2. **分镜首帧生图提示词**：每镜一张首帧参考图提示词，用于图生视频输入或视觉锚定
3. **分镜视频提示词**：每镜 CINEDANCE 16-block 提示词
4. **参考图清单**：每镜用哪些参考图、上传顺序
5. **交付物总清单**：文件索引 + 检查表

### 时长优化（阶段5集成）
每镜时长基于五因素决策：动作复杂度 / 情绪重量 / 对白长度 / 镜头运动 / 叙事节奏。同时感知模型能力上限（Seedance 2.5=30s, Seedance 2.0/Kling 3.0=15s, Veo 3=8s）。详见 `13-deliverable-system.md` §2。

### 语言路由
提示词语言 = 用户对话语言。中文对话默认中文提示词；英文对话用英文提示词；其他语言依此类推。技术标签始终英文。详见 `13-deliverable-system.md` §4。

---

## 8. 常见翻车点速查（详见 `20-qa-checklists.md`）

| 阶段 | 高频翻车 | 预防 |
|---|---|---|
| 3 | 脸选「最美」不选「最可信」；瞳孔无眼神光 | 视频阶段必露馅，选可信+查 catch-light |
| 4 | 只单独测，不同框测 | 同框+实景光下测 |
| 5 | 一镜塞多个动作 | 一镜一动作，复杂动作放开头已发生 |
| 6 | 提示词整段重写迭代 | 一次只改一行 |
| 7 | 无多参考图锚点工具一致性差 | 降级策略：图生视频+descriptor 逐字 |
| 9 | 边生成边修图 | 清理是 picture lock 后单独一遍 |