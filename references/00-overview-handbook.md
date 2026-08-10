# AIGC 长片制作手册

> AIGC 长片制作手册——核心方法论与可操作清单。
> 一句话心智模型：**视频模型没有记忆**——所以角色、地点、道具、声音、动作，每一次都要原样重述。所有规则都因「某一帧失败过」而生。

---

## 目录

1. [一页速览：核心心智模型](#1-一页速览核心心智模型)
2. [项目背景与工具链](#2-项目背景与工具链)
3. [前期筹备 A：资产（Assets）](#3-前期筹备-a资产assets)
4. [前期筹备 B：视频提示词](#4-前期筹备-b视频提示词)
5. [表演系统：写行为，不写感受](#5-表演系统写行为不写感受)
6. [截止压力下的实战 Hack](#6-截止压力下的实战-hack)
7. [后期：清理 · 调色 · 声音](#7-后期清理--调色--声音)
8. [五条黄金规则（结论）](#8-五条黄金规则结论)
9. [可照搬的速查表](#9-可照搬的速查表)

---

## 1. 一页速览：核心心智模型

整个流程围绕一个事实展开：**视频模型没有记忆**。

| 失败现象 | 根因 | 解法 |
|---|---|---|
| 同一角色隔镜变脸、换夹克 | 描述不完整，模型自行补全 | 资产 = 文本描述 + 参考图，每次原样复用 |
| 空间一转镜头就崩 | 地点只有「正面美图」，边缘靠模型瞎编 | 3/4 视角地点表 + 锚点 + 单一光逻辑 |
| 声音漂移 | 未提前锁定嗓音参数 | 前期锁声，音频字段逐字粘贴 |
| 场景失去地理关系（人瞬移、换边） | 模型不记得上一镜谁在哪 | **GEO SPATIAL LAYOUT** 每镜粘贴 |
| 同一提示反复改不出好镜 | 一次改太多，好的部分也丢了 | **一次只改一行**，全进日志 |

**三个支柱**：
- **资产优先**（Assets）：开拍前锁死一切角色/地点/道具。
- **结构化提示词**（Prompt skeleton）：刚性骨架，每镜复用同一套 block。
- **后期兜底**（Post）：清理、统一调色、声音缝合。

**规模可降维**：这套管线不需要 15 个人——它需要的是「规则被遵守」。可缩小到 1 人团队。

---

## 2. 项目背景与工具链

### 2.1 工具链（按用途）
| 用途 | 工具 |
|---|---|
| 视频 + 语音 | Seedance 2.0 |
| 脸 + 地点 | Soul Cinema |
| 图像编辑 | Nano Banana Pro、Seedream 5.0 Pro |
| 画面内文字 / 道具 / 地点反打 | GPT Image 2 |
| 提示词协作（项目上下文） | AI 助手持有整包：剧本、资产表、登记表、带 @ 标签的镜头表） |

> 团队构成：导演组 + 提示词工程师，每人负责自己的一块场景。

---

## 3. 前期筹备 A：资产（Assets）

> **资产 = 文本 + 图像 的简单配对。**
> - **文本（descriptor）**：角色/地点的完整描述，**逐字**进入每个提示词。
> - **图像（reference）**：参考图，作为模型的「锚」。
> 二者共同保证角色跨镜不变。

### 3.1 角色表：三张图
1. **脸部特写**
2. **正面全身（无头）** ← 关键反直觉设计
3. **背面全身**

**为什么正面全身要「无头」**：
- 远景时，模型会去角色表上那张小小的全身图里「借脸」——而那张脸又小又糊。
- 把头删掉，模型就**只剩一个取脸来源：特写**。这一类坏镜一次性解决。

### 3.2 脸在 Soul Cinema 里生成
- 它皮肤质感最好，但它是「创意模型」：一条 prompt 返回多个不同版本。
- **选最可信的，不是最美的**。一张「美但假」的脸会在后期的视频里暴露虚假——那时已无法挽回。
- **永远检查眼睛**：哪怕深色瞳孔，也要有细微光反射（catch-light / 眼神光）。没有它，脸像死的，没有任何视频模型能对着死脸演戏。

### 3.3 故意把角色表做「无聊」
- 中性灰背景、平光、真实皮肤带可见毛孔、不磨皮。
- **电影感不活在角色表里，而活在地点和视频提示词里。**
- 把胶片颗粒/电影镜头感「烤进」角色表 → 角色会把这层 look 带进每个场景，并停止对新光线做出反应。
- 经验：**模型最懂的表，是带一张 3/4 视角大肖像**（脸微侧，非正脸）。

### 3.4 衣服 / 伤疤 / 血：用「点修改」
工作流（保质量的一种可行做法）：
1. 在 **Nano Banana Pro** 对原始角色表做点修改（Seedream 5.0 Pro 仅用于纹理 pass，不做 in-paint 编辑）；
2. 在任何支持蒙版的图形编辑器里，**手动**把改动部分叠回原图。
3. 蒙版只放改动部分（夹克、伤疤、血），其余原样保留 → 原皮肤质感存活。

**铁律：`an image never runs through a model twice in full`（图像绝不整张二次过模型）。**
- 每多过一次模型就毁一次质感、漂一次色。
- 两次之后脸变对称、塑料、无生命；这层死质感之后会毁掉视频里的表演。

### 3.5 资产上线前必过压力测试
- **十次生成**：不同姿态、不同光线，10/10 都要认得出。
- 不只单独测：要**和其他资产同框**、在真实场景的光里测。
- 单独稳的角色，一旦与他人同框常崩。
- **测试不过 = 你的描述有问题，不是模型问题。重写文字，再测。**

### 3.6 声音不是资产，但必须提前锁
- Seedance 在一个音色内可容纳 3–4 种声线，够一部长片——**前提是你管理它**。
- 在写对白前（前期）就锁死每个主角的嗓音：音区、节奏、口音、习惯。
- 嗓音提示**逐字粘贴进音频字段**，每次角色开口都用，**永不改变**。
  > 范例：`Voice: deep, gravelly bass-baritone; slow, calculated pacing; London street accent; menacing calm — he never raises his voice.`
- 像测长相一样测嗓音跨生成是否稳定；漂移就回去把措辞锁更死。

### 3.7 行为档案（behavior profile）——和长相、嗓音同样方式锁定
- 每个主角一段段落，**在任何拍摄前写好**：怎么走、手做什么、紧张小动作、眼神怎么动、压力下具体如何崩。
- 这段是「唯一真相源」：每场戏把它适配到当下的姿态与动作，但**核心不变**。
- 物理上不可能的行为要「转移」而非删除：一个爱踱步的人坐到沙发上，仍保留同样的能量——摇晃、敲指、断裂式手势。

### 3.8 每个「状态」都是独立资产
- 湿身、带伤、换衣 = `@roco`、`@roco_wet`、`@roco_blood`，各自独立描述。
- 把状态混进同一段文字 → 模型开始跨镜混淆。
- **地点同理**：白天、夜晚、雨天是三个不同资产。
- **道具同理**：关键神器做了三个版本——近景完整版、掌心一闪的血迹小版、攥拳版（提示词禁止显示晶体、只许指缝漏蓝光）。
- 拆分状态，比跟模型死磕便宜。

**跨镜状态过渡**：当角色在连续镜头间切换状态变体（如 @girl_wet → @girl），在前一镜末尾和后一镜开头都保留过渡痕迹：前一镜末可见状态正在变化（如"hair damp but drying, water droplets fewer"），后一镜首帧仍带残留痕迹（如"hair slightly wavy from being wet, shoulders dry"）。不要在切镜时瞬间完全切换状态——那会让模型认为是换了一个人。状态变化是渐进的，跨至少2-3镜完成。

### 3.9 地点资产
- **为未来的机位生成地点**：用 **3/4 视角**而非正面拍地点表。
  - 正面「美图」在远景里变成平面壁纸，越过边缘模型每次都瞎编新环境。
  - 3/4 给模型可读的深度 → 把主角放对位置，覆盖近一整圈角度。
- **每处留一个锚点**：柱子、灯、沙发，并把调度绑上去。
  - ✅「英雄在灯旁，面朝门」；❌「英雄在房间里」（纯抽奖）。
- **光源逻辑**：一个主光源决定阴影方向；允许环境漫射光（窗光/天光）作为底光，但底光不产生第二个阴影方向。绝不让两个强光源各投各的阴影（**"两个太阳"**）——否则每个新角度重造光。
- **反打镜头两种做法**：
  - 方法一（早期）：在 GPT Image 2 / Nano Banana 生成同室一角，匹配原图柔焦。
  - 方法二（后期发现）：生成空地点视频，镜头缓缓穿行——Seedance 会把其他几面画得和你的表一致；截图所需角度 → Seedream/Nano Banana Pro 提升质感与光。一张图出整套地点表。

### 3.10 把资产喂给 Seedance 时，给每个参考**命名角色**
- 参考只含资产（角色 + 地点）。在提示词里**直接写明每个的角色**，否则模型自己决定、且往往错：它抄构图而非脸，或抄脸而非配色。
  ```
  @roco for character reference
  @jaxx for character reference
  @loc_cave_front for location reference
  ```
- **地点参考加直接禁继指令**：「不作为起始帧、不继承构图/角度/配色——只取空间与质感」。
- 所有资产用统一标签（`@roco`、`@loc_cave_front`），**文档、提示词、界面通用同一本命名词典**。

---

## 4. 前期筹备 B：视频提示词

### 4.1 三大系统（都做成了 AI 助手可自载的 skill）
- **CINEDANCE**：写视频提示词。
- **Lira**：写图像提示词，等同 CINEDANCE 但针对图像；懂每个图像模型的弱点。
- **表演系统（acting system）**：活人表演——如何写行为而非情绪、脸+身提示 hack、角色表演主格式。

> 提示词用 AI 助手协作写，它持有整包上下文。标准封进 skill，AI 助手自载后照做。

### 4.2 提示词是刚性骨架（16 个 block）
```
SCENE CONTEXT         — 带 "EXACT N CHARACTERS — NO DUPLICATES" 头：发生什么、谁在镜内、时长
ACTIVE REFERENCES     — 角色/地点标签 + 各自角色命名
LOCATION MAP          — 用文字描述地点地理
FIRST FRAME & SPATIAL BLOCKING — 第一帧谁站哪
FORMAT MODE           — 单镜 or 硬切、时长、真实时间
OPTICS                — 镜头 + 对焦计划
CAMERA                — 摄影机怎么动、绝不做什么
ACTION TIMING         — 动作逐拍、按秒
PHYSICS               — 重量、接触、一切运动的惯性
LIGHTING              — 单一光源逻辑、来自哪
AUDIO                 — 嗓音描述 + 原句；仅 SFX
CHARACTER ACTING      — 状态、欲望、隐藏、身体节奏、变化
STYLE                 — Style Prefix，逐字粘贴
QUALITY               — 细节与稳定要求
POSITIVE CONSTRAINTS  — 每个计数与禁令，写成「画面里有什么」
```

**角色计数头不是形式**：模型爱加多余的人和克隆家具。只有提示词里带参考的才存在于画面；家具直接禁：「exactly ONE mannequin, NEVER render a second one.」

### 4.3 一个真实填好的范例（crew 撞见 Roco 独自训练）

```
SCENE CONTEXT
EXACT 3 CHARACTERS — NO DUPLICATES: ROCO, JAX, REIN. Underground base, training hall, day.
ROCO has been drilling alone for hours; JAX and REIN come in late with food and find the room
wrecked. One continuous 12-second shot, no cuts.

ACTIVE REFERENCES
@roco for character reference — bare-chested, the crystal sheathing his right arm from wrist to
shoulder, blood dried under his nose.
@jax for character reference — carrying two food trays.
@rein for character reference — tablet in her left hand, screen alive.
@loc_training_room for location reference — take only the space and the texture: raw concrete,
black rock walls, the round mat, the hard light above it. Do not use as a starting frame, do not
inherit the composition, the angle or the grade.

LOCATION MAP
The round training mat sits at the center of the hall under one hard overhead light. The door is
in the far wall at frame-LEFT, about eight metres from the mat. Five smashed mannequins lie
scattered at CENTER-RIGHT, one still rocking on its base. A bench with two trays stands at
frame-RIGHT, two metres off the mat. The camera lives on the door side of the room and never
crosses that line.

FIRST FRAME AND SPATIAL BLOCKING
First frame is already the full room: ROCO planted at the center of the mat, torso angled to
frame-LEFT, gaze down on the broken mannequins; the open door at frame-LEFT with JAX and REIN just
inside it, trays in hand, two metres apart. No empty establishing beat, no camera move on frame one.

FORMAT MODE
Single continuous take, 12 seconds, real time, no cuts, no speed ramps.

OPTICS
≈40° wide, camera low at chest height, six metres from the mat, deep enough focus to hold the door
and the mannequins in one read; the crystal arm stays sharp.

CAMERA
Calm breathing handheld that holds its framing — a slow reframe of a few degrees when ROCO turns
his head, nothing more. No push, no zoom, no whip.

ACTION TIMING
0.0–1.0s  — the room holds: positions fixed, one mannequin still rocking.
1.0–4.0s  — the door swings; JAX and REIN step in and stop at the edge of the mat, trays held.
4.0–8.0s  — ROCO's eyes find them before his head turns; chest pumping in short pulls, the blood
            untouched, the jaw setting once.
8.0–12.0s — he speaks; the smile cracks on all three at once; nobody steps toward anybody.

PHYSICS
The crystal arm has real weight — it drags the right shoulder low and swings a beat behind the
body. The rocking mannequin loses momentum and settles. Trays carry liquid: the cups tilt and
steady when JAX stops. Breath is audible work, not decoration.

LIGHTING
One hard overhead source above the mat: ROCO lit from above, eye sockets in shadow, the crystal
catching a cold edge; the door area falls two stops darker; no fill from the camera side.

AUDIO
Diegetic only — the hum of the hall, one mannequin creaking to a stop, footsteps and trays. ROCO
voice (verbatim): "A worn-out voice in his twenties, dry and low, humour used as armour." His line,
and nothing else: "You're late." Nobody else speaks. No music.

CHARACTER ACTING
ROCO — burnt out and still going; wants one more clean hit before anyone sees him fail; hides that
the arm is winning; heavy planted rhythm, slow recovery; re-arms his face when the door opens.
JAX  — carries the reaction: the grin holds a half-beat too long, then drops as he reads the room.
REIN — reads the damage before the person: eyes sweep the broken mannequins, then the arm, then his
face; the tablet lowers without her noticing.

STYLE
[Style Prefix, pasted word for word]

QUALITY
8K detail, pore-level skin, no jitter, no flicker; the three faces stay exactly their references at
every distance.

POSITIVE CONSTRAINTS
Exactly three people in the hall, and no one else. Exactly ONE crystal arm, on ROCO's right arm,
wrist to shoulder — never on the left, never spreading past the shoulder. FIVE smashed mannequins,
never re-rendered as intact, never multiplied. Two trays, never more. The camera stays on the door
side of the room for all twelve seconds. Photorealistic. NON-IP. 16:9. 12s. SFX only. NO CGI. Cinematic.
```

### 4.4 写作规则（骨架之内的纪律）
- **用现在时、短句。**
- **摄影机写在动作里。**
- 每拍要轻：**每拍最多三句**——一拍过载，模型就糊。
- 提示词本身可以长（他们跑到 3000–4000 词）。**长度不是敌人，过载的拍才是。**
- **四条例外措辞规则**：
  1. 动作只用**肯定式**——模型忽略「does NOT fall on his back」，甚至反着做；写「falls on his stomach」。
  2. 角色从**第一帧就在画面里**；除非要求，绝不看镜头。
  3. **绝不写年龄**（任何语言都别写）——内容过滤器一读「未成年人」就骤严。用角色、衣服、动作代替年龄。
  4. 维护**禁用词词典**（模型会惩罚的词）：`dark` → `low key`；`jolting` → `rapid motion`。

### 4.5 Style Prefix（逐字粘到每个提示词末尾）

```
Style: 8K IMAX. Photorealistic — no 3D render, no game engine, no game-cutscene aesthetic.
Cinematography: floating immersive camera that lives with the actors; natural motivated light;
painterly composed frames, strong silhouettes against the light.
Lighting: Natural light only — contre-jour backlight, camera on shadow side, atmospheric haze
throughout. Key light from sky and windows only.
Color: 60:30:10 — dominant / secondary / accent.
Camera: Physical cine lens. 180° shutter motion blur.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush, pore-shadow matching
on-set light.
Acting: Hollywood — micro-pauses before reactions, precise eye-line, wet living eyes with
catch-lights, visible breath and chest rise.
Physics: Gravity and inertia respected — mass has real weight, correct contact shadows. No
floating props.
Composition: Rule of thirds + golden ratio. Every person moving from frame one.
Continuity: Characters, props, environment identical across every cut. No identity drift.
Technical: 24fps smooth motion. 8K detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.
```

**`SFX only. No music.` 是强制的**：音乐属于后期，生成版配乐只会碍剪辑。

**技术标签收尾**（固定格式）：`Photorealistic. NON-IP. [画幅]. [时长]s. SFX only. NO CGI. Cinematic.`

### 4.6 GEO SPATIAL LAYOUT（最贵教训的解药）
**问题**：角色瞬移、换位、镜头跳到错边——因为模型不记得上一镜谁站哪。
**解药**：写一个地点的「楼层平面」几行：地标物、右边是什么、左边是什么、摄影机站哪。**无角色、无动作——只有地点本身。** 每场戏写一次，原样粘进该场每一镜。

```
GEO SPATIAL LAYOUT (locked across every shot — pure spatial map):
— PLATFORM = raised circular ritual stone disc at the edge of a cliff.
— ALTAR-MONOLITH: at the cliff edge, MID-RIGHT position relative to the platform.
— RITUAL CENTER: CENTER-LEFT, ~3 m from the altar.
— 180° AXIS: camera ALWAYS stays on the corpse-field side — it NEVER crosses the line.
— BACK-LIGHTING: crimson horizon glow comes from BEHIND the platform, rim-lighting silhouettes
  from camera's perspective.
```

**读取地图的规则**：
- 侧面**只从摄影机视角**定义：`frame-left` / `frame-right`（模型不懂「英雄左边」）。
- 位置从**地标物 + 米数**定：「在祭坛旁」「三米外」。
- 直接写明摄影机站哪侧、绝不越哪条线 → 所有切都锁在同一条轴。
- 两个连带动作：① 每次切后**重报谁站哪、看向哪**（模型不记得上一镜）；② 给静态对白**一个房间角落而非整间**——空间越小，模型乱放主角的余地越小。
- **GEO 只是地图**：地点长相仍来自地点资产（其 descriptor + reference 与地图并列进提示词）。

### 4.7 第一秒永远是全景
- 场景开头 **1 秒、无台词无动作**：模型「拍下」排布——谁站哪、什么躺哪、光从哪来——并在后续每镜守住它。删掉这秒，角色就开始换位。
- 小 hack：让某人那秒说一个短字（如「hm」），Seedance 更易把全景当独立镜处理。
- 全景不必静音：若本镜回应上一镜，把上一镜台词**尾巴喂进第一秒**——演员用对的语气答对的词，两镜在接缝处黏住。

```
FIRST FRAME AND SPATIAL BLOCKING
SHOT 1 (~1.0s) — a wide that FIXES THE POSITIONS and does nothing else: ROCO planted at the center
of the mat, five smashed mannequins at CENTER-RIGHT, the door open at frame-LEFT with JAX and REIN
one step inside it, trays in hand. No camera move, no action beat.

AUDIO
Over that first second, the tail of the previous clip's line arrives on REIN's lips as she walks in:
"...I've got the coordinates." ROCO's eyes find her before his head turns.

ACTION TIMING
1.0s onward — ROCO answers into the same rhythm, dry and worn: "You're late."
```

**代价是 1 秒 runtime，省下的是数小时重拍。**

**竖屏例外（9:16）**：竖屏不做传统 wide（会拍到大量天花板/地板，人脸太小浪费前3秒钩子时间）。竖屏首帧改用 medium portrait（中景肖像）：人物占画面60%垂直高度，眼睛在画面上三分线，环境在人物身后可见而非独立空镜。空间锁定通过 GEO + 首帧人物位置+朝向实现，不依赖 wide establishing shot。

---

## 5. 表演系统：写行为，不写感受

### 5.1 主规则：写行为，不写感受
- 活场景 = 一个**想要某物**、**有东西挡路**、并**为得到它而行动**的主角。情绪自己从这场斗争里长出来。
- 给模型目标和障碍，并让「他为得到它而战的方式」随场景变：开玩笑→失败→推进→失败→乞求。每次变化都是可见事件：停顿、姿态变、节奏变。
- 一路做同一件事的主角，戏是平的。

### 5.2 写物理，不写形容词
- 情绪词（sad/angry/shocked）让模型开始即兴，给浅结果。
- 更深的情绪：**描述肌肉与身体的工作**——颤抖、愤怒咬紧又绷紧的下颌、颧骨收紧、鼻腔轻呼。
- 叠**意图**：每段动作配一行内心独白（所想所愿），标 `INNER`（未说出）。
- **分阶段眨眼**：「一次慵懒眨 → 快速双眨 → 一次硬重置眨」——最便宜的活脸信号。
- 除眨眼外写清**视线方向**或**游移眼神**：持续工作的微表情给脸更多生命。
- 静态镜里反「冻脸」：**微生命规则**——每 1–2 秒一个可见微事件（呼吸顶起胸、鼻孔动、眉一紧一松）。把静止写成「绷住张力」，绝不写成「冻结」：`nobody moves` 这类安抚句会自己冻帧。

**真实段落（ROCO 独自训练后）——「exhausted/angry」二字没出现，状态由肌肉的 timing + 意图的 acting block 搭出来：**

```
ACTION TIMING
0.0–2.0s — ROCO holds the center of the mat, feet planted wide, chest pumping in short shallow
pulls; the crystal arm hangs heavy at his side and drags his right shoulder a finger lower than
the left.
2.0–4.5s — the jaw sets and releases twice; a thread of blood runs from his nose to his upper lip
and he lets it run; one lazy blink, a quick DOUBLE-BLINK, one HARD reset-blink.
4.5–6.0s — the gaze drops to the smashed mannequins at CENTER-RIGHT, holds one beat, then lifts to
the door as it opens — the eyes reach the door before the head turns.

CHARACTER ACTING
ROCO — emotional state: burnt out and still going. What he wants in this moment: one more clean hit
before anyone walks in on him failing. What he is hiding: that the arm is winning, and that it
frightens him. Dominant body rhythm: heavy, planted, slow recovery between bursts. Visible habits in
this beat: the jaw set-and-release, the right shoulder pulled low by the crystal, the blood he does
not wipe, the gaze that finds the broken mannequins first and people second. What changes across the
shot: the second the door opens he re-arms his face — the exhaustion folds back behind a dry
half-smile before he says a word.
```

### 5.3 区分活镜与死镜的三件事
1. **反应在对方台词结束前就开始**：听者半句就懂，脸已答；重要事件后给主角一瞬「接住」再开口。
2. **情绪不会瞬间关掉**：重场之后呼吸仍不均、手仍不稳——这尾巴带进下一镜，把切缝缝起来。
3. **让主角手别闲着**：他不是在「对话」，是在修理、数数、倒酒、边干边说；戏最强的重音，是他因刚听到的话**停下手头活**的那一刻。

### 5.4 对白线在提示词里永远同构
> 嗓音+情绪 → 引号内台词 → 身体动作 → 面部反应。
- **台词只活在 AUDIO 段**，动作段里一个字都不许有。
- Seedance 爱自己加「uhm/嗤笑/整句闲话」，所以提示词带硬块：每人**只说引号里的词**；没词的人**完全静默**；动作里写的「半笑」是面部表情，**不出声**。
- 写混音：人声干净贴麦、环境在其下、有人说话时环境沉一沉。
- 生僻名给音标，否则模型读崩。
- **接缝两 trick**：① 对白全景把上一句尾巴喂进提示词（帮对口型与节奏）；② 每次新生成用「上一镜收尾那句」开场——情绪连同文字跨缝。

**真实两行对白（动作在 timing、言语在 audio，绝不混）：**

```
ACTION TIMING
0.0–3.0s — JAX and REIN walk the corridor toward the lens, in step. JAX talks with his eyes up on
the ceiling lights, one hand patting his stomach; REIN's thumb keeps scrolling the tablet, her pace
unchanged, she never looks up at him.
3.0–4.0s — the distant THUD from the training room lands: REIN's thumb STOPS on the glass, and only
then her head turns to the door — the interrupted work is the accent of the beat. JAX's grin drops
half a second later.

AUDIO
Diegetic only — corridor air, two sets of footsteps on concrete, soft taps on the tablet, the
distant THUD and a hiss of crystal behind the door. JAX voice (verbatim): "A London street voice in
his twenties, loose and hungry, always half-joking, sentences thrown out mid-stride." His line, and
nothing else: "Man, some cereal and a milkshake would hit the spot right now." REIN voice (verbatim):
"A technical voice in her twenties — flat, fast, precise, no wasted air." Her line, and nothing
else: "I think I've got the coordinates." Nobody else speaks; JAX's amused breath is a facial
expression, with no sound. No music.
```

### 5.5 工作组织：按场景块
- 顺序：彩绘序章 → 地狱冷开场 → 孤儿院闪回 → 基地与西藏劫案 → 日本终章。
- 每块独立镜头表文件；每个镜头有编号、时长、完整提示词。
- descriptor 与 Style Prefix 作**常量**：一处改，全镜同步。
- **批量生成、逐场推进**；每次迭代是「手术」：只改一行，其余逐字不动。
- **全进日志**：提示词版本、改了什么、判定。无日志则无法复现好镜。
- **10–15 次法则**：一镜这么多次还不成 → 问题不在措辞。简化镜头：拆两镜、删动作、换角度。

---

## 6. 截止压力下的实战 Hack

1. **复杂动作绝不放在 timing 中间**：门总破不了——英雄挪到门边就冻住。改为动作在提示词开头就发生——「他已在挥击途中、门已在裂」；走到门是另一镜。
2. **人群是一个「角色」资产**：给定身高与衣服范围；1–2 个领演单独建资产做近景。中景直接写数字「20+」，否则模型这镜给 3 人、下镜给 100 人。
3. **两空间转场停在阈值**：一个提示词里放两个地点资产，接缝是「带光差的门洞」——「暖琥珀房间，拱门外冷蓝走廊」。光差解释配色变化，原谅小几何错。
4. **巨人活在尺度锚点**：每镜都要尺寸对比 + 画面里放个人当尺。缺任一，模型会悄悄把巨人缩回人身高。
   ```
   POSITIVE CONSTRAINTS
   THE SCALE LAW — VISIBLE PROOF IN THE PICTURE: the stone guardian stands THIRTY METRES tall — his
   head is lost in the darkness of the dome, his open palm is as wide as a family car, and ROCO at
   his foot reaches just above the ankle. In every frame the guardian's silhouette is at least FIVE
   TIMES the height of the human figure beside him, and the frame cannot hold both his feet and his
   head at once. A guardian that reads as a large man, or fits comfortably in frame next to a
   standing human = failed shot.
   ```

---

## 7. 后期：清理 · 调色 · 声音

### 7.1 剪辑与生成并行
- 剪辑师边收边组，主动下需求：「需要切到手的特写」「需要更宽的」。
- 重拍只花几分钟，所以剪辑**主动塑造制作**，而非等它。
- 生成素材节奏常偏慢：**比感觉对的剪更狠**；计划**每条首尾各裁半秒**（边缘会漂）。

### 7.2 清理（picture lock 后单独一遍）
- AI 素材几乎都带工作时看不见、大屏才见的缺陷：多指、沸腾纹理、假字。
- 小缺陷逐帧修；全崩的镜用保存的终版提示词重生成，**只改一行**。
- **优先顺序：脸与手的特写第一**。全部严格在调色前做。

### 7.3 调色
- 先**统一**：每次生成自带内置调色，调色师先把同场相邻镜拉到一个 look。
- 这个 look 早在前期就**烤进地点资产**——所以调色师是 refining，不是 inventing。

### 7.4 声音
- **没重录嗓音**：直接用生成里的对口型台词清理——去噪、跨镜音色匀、把人声放进空间。
- 仅当某镜完全无可用人声时才进棚录。
- 声音设计与音乐在后期建于**连续环境底**之上：一个共享氛围把生成的镜缝成一-space，哪怕画面略有漂。

---

## 8. 五条黄金规则（结论）

> 若把整部电影压成五条规则：

1. **资产优先（Assets first）**。在锁死并压力测试完每个角色/地点/道具前，一镜都别生成。这一条省的钱比其余所有加起来都多。
2. **每次都描述一切（Describe everything, every time）**。模型没有记忆。descriptor 逐字进每个提示词，永不缩写。
3. **一次只改一件事（Change one thing at a time）**。提示词是台工作机器：整段重写 = 丢掉好用的部分。每次迭代一行，全进日志。
4. **给模型更少自由（Give the model less freedom）**。要角落不要房间，要锚点不要空场，要地图不要猜，一镜一动作。
5. **一镜做不出就简化镜头，不是简化文字（If a shot won't come together — simplify the shot, not the words）**。拆两镜、删动作、换角度。

> 每条规则都因「没有它就有镜失败」而生。从一场戏开始：一个锁死的角色、一张地点表、一套提示词骨架。管线不需要十五人——它需要规则被遵守。可降维到一人团队。

---

## 9. 可照搬的速查表

**开拍前 checklist**
- [ ] 每个角色：3 图角色表（脸特写 / 正面无头全身 / 背面全身）
- [ ] 脸选「最可信非最美」、有 catch-light
- [ ] 角色表灰底平光、真实皮肤、3/4 大肖像
- [ ] 衣/伤/血走点修改（图像绝不整张二次过模型）
- [ ] 每个角色 + 每个状态（`_wet`/`_blood`）独立资产
- [ ] 地点 3/4 视角 + 锚点 + 单一光逻辑
- [ ] 反打镜头两种方法备好
- [ ] 全部资产 10/10 压力测试通过
- [ ] 每个主角锁嗓音（逐字粘音频字段）
- [ ] 每个主角写行为档案段落

**每镜提示词 checklist**
- [ ] 带 `EXACT N CHARACTERS — NO DUPLICATES` 头
- [ ] 参考全命名角色（`@x for character reference` 等）
- [ ] 地点参考加「禁继」指令
- [ ] GEO SPATIAL LAYOUT 每场写一次、每镜粘
- [ ] 第一秒全景固定位置（可喂上一镜台词尾）
- [ ] 动作只肯定式、现在时、短句、每拍 ≤3 句
- [ ] 不写年龄；用禁用词词典
- [ ] 台词只在 AUDIO；动作段零台词
- [ ] Style Prefix 逐字粘；尾部技术标签 `Photorealistic. NON-IP. [画幅]. [时长]s. SFX only. NO CGI. Cinematic.`
- [ ] 一次只改一行，进日志

**尺度/人群/转场速记**
- 巨人：每镜带尺寸对比 + 人形尺 + SCALE LAW 硬约束
- 人群：单资产 + 范围；中景直接写「20+」
- 转场：双地点资产 + 门洞光差
- 复杂动作：开头就发生，走到是另一镜