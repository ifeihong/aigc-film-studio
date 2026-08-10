# ACTING SYSTEM
## 面向 AI 视频生成的角色表演（Seedance 2.0）

你正在读这篇文档，是因为你的用户在做电影级 AI 视频，需要你在提示词里写出**角色表演**。研读本文，然后每次你为视频生成提示词撰写、审阅或修正「表演层」时，都应用它。本文件格式与模型无关：无论用户用哪种提示词模板，你产出的表演内容都进入提示词的 motion / character-behavior / performance 部分。

**整个系统的核心公理：表演是「压力下的行为」，而不是情绪的展示。** 一个角色想要某物，有东西挡路，于是他行动去争取。情绪是这场斗争的副产品——绝不该由你直接写。下文全是这条规则的拆解。

## 独角戏 / 无对白场景特别指引
- AUDIO 段格式（无对白）：`Diegetic SFX only — <环境声描述>. No dialogue. No music. Nobody speaks.`
- Voice 字段：无对白角色省略 Voice 描述段，不写"No voice"或占位符。
- 独角戏的"障碍"不是人，是情境/物体/记忆/自我：如"她想看清信上的字但光线不足"、"他想保持冷静但手在抖"。
- 独角戏的"战术"是身体对障碍的物理应对：凑近、眯眼、深呼吸、手指加压。
- 给手活计：独角戏角色必须在做某件物理的事（翻书、擦拭、写信、整理），反应通过"停下活计"的时刻传递。
- 无对白场景的反应全部是物理的：吞咽、眨眼、呼吸变化、手指动作、目光转移。绝不用情绪形容词。

---

# 第一部分 — 工艺：好表演是什么

## 1. 定义

表演是在想象情境中真实可信的行为（Meisner 方法）。不是描绘情绪，不是背诵台词，不是「表情丰富」。画面里的人**想要**某物，**受阻**，并**行动**去得到它。

| 坏表演 | 好表演 |
|---|---|
| 展示情绪（「我很愤怒」） | 追求目标（「我要让你还钱」）——愤怒自己长出来 |
| 等自己的cue | 每秒都在听搭档、对搭档反应 |
| 身体图解词语（手势=词义） | 身体有自己的生命，有时与词语矛盾 |
| 所有台词同节奏同语气 | 节奏随战术每次变化 |
| 情绪在台词处开、台词后关 | 状态是连续的——台词有「之前的生活」和「之后的生活」 |
| 脸在「表演」——挑眉、做怪相 | 脸在「思考」——想法先于词语在眼里可读 |

## 2. 每个场景的五大支柱

每个场景里的每个角色都拆成五个元素。缺一个，表演就垮。

**2.1 目标（Objective）。** 角色在此场景、此刻、对某个具体的人想要什么。永远是瞄准搭档的动词：「让他招供」「求一周宽限」「说服她我不怕」。绝不是一个状态（「愤怒」「愧疚」）——状态无法被直接演出。场景目标背后坐着「超级目标」——角色贯穿整故事想要的东西；每个场景目标都是通向它的一个台阶。

**2.2 障碍与赌注（Obstacle & stakes）。** 是什么阻止他得到——外部（另一个角色想要相反；屋里有证人；离死线还有两小时）或内部（骄傲不让他求人；他不信自己说的话）。赌注：失败代价越高，场景越绷紧。始终回答「如果我得不到想要的会怎样？」——答案必须让角色害怕。

**2.3 战术（Tactics）。** 此刻追求目标的具体方法。战术是动作动词：施压、魅惑、羞辱、恳求、激将、讨价、威胁、拖延。战术失败，活人会**换**战术。死表演是整场一个战术。

**2.4 节拍（Beats）。** 节拍是最小的行动单位：角色想要一件事、用一种方式追求它的一段时间。节拍在以下时刻结束：目标达成、战术失败、新信息到来、或力量平衡改变。**每个节拍变化必须在行为上「可见」**：停顿、姿态改变、语速改变、视线转移。好场景有 2–4 次节拍变化；若整段行为不变，戏就演平了。

**2.5 潜台词（Subtext）。** 角色真正所想所愿，与他说出口的相反。潜台词**不是演出来的**——当角色演着真实目标、却说着虚假台词时，它自己漏出来。可写进场景的标记：不是问题的提问；重复（问同一件事——不信回答）；突兀转话题；错时机的玩笑（对脆弱的盾）；过短的回答（「挺好。」「行。」——一扇关上的门）。

## 3. 聆听与反应——质量的主要试金石

表演不在台词里，而在台词**之间**。应写进场景的真实聆听标记：

1. **反应在搭档台词结束前就开始。** 人在半句话里就抓住了点——脸和身体已经回答。直到搭档台词结束才「开机」的中性脸，是死表演。
2. **思在言前。** 回答难题前有一瞬微停顿——人 visibly 决定说什么。匀速即时回答=背稿，无生命。
3. **评估时刻（assessment moment）。** 重要事情发生（消息、威胁、侮辱），角色需要时间消化——从一瞬到长时间停顿。电影活在这些评估的特写里：一张脸、失焦的眼神、世界在游。
4. **来自搭档的传染。** 节奏、音量、能量随搭档反应而变：一声吼要么换来反吼，要么换来刻意压低——但一定「接住」，而非盖过。

## 4. 身体：角色的物理生命

**4.1 身体状态先于心理。** 身体在第一句台词前就讲了故事。为每个角色设这些参数：

- **重心（Center of gravity）：** 高（胸、下巴——自信、攻击性、地位）或低（肩、塌腰——疲惫、恐惧、顺从）。
- **节奏（Tempo）：** 快/凌乱（紧张、兴奋剂能量）或慢/经济（控制、威胁——最危险的人动得最少）。
- **开放度（Openness）：** 双肩方正、掌心摊开 vs 抱臂、低头、封闭姿态。
- **呼吸（Breath）：** 高而急（恐慌）vs 低而缓（控制）。呼吸是最诚实的状态指标；屏住的呼吸=屏住的表演。声音与物理必须匹配：刚跑完的人不可能用平稳嗓音说话。

**4.2 活计（Business）——物理任务。** 角色几乎总需要一件「在做的事」：他们不是「在对话」，而是在修引擎、数钱、做饭、擦杯子——边干边说。活计杀死虚假的舞台腔（手忙着真相），制造场景节奏（停顿被动作填满），并生出潜台词（一个人怎么数钱比台词说得更多）。**中断动作规则：** 最强的重音是角色**停**下活计。他在切片面包，因一句话停住——那句话就成了事件。把停当作标点用。

**4.3 空间关系（Proxemics）——距离即戏剧。** 角色间距离是关系可见的图：亲密区（0.5 米内）——爱或暴力，未经允许进入是攻击，10 厘米脸前低语的威胁比隔屋吼更吓人；个人区（0.5–1.2 米）——信任；社交区（1.2–3.5 米）——公事、戒备；公共区（3.5+ 米）——疏离、等级。场景戏剧常只是距离的故事：谁拉近、谁打破、谁冻结。**距离改变=节拍改变。**

**4.4 地位（Status）——看不见的层级。** 地位是你**做**什么，不是你**是**谁。高地位：头不动、动作慢、凝视长、回答前停顿、占空间、碰别人的东西。低地位：忙乱、频繁自触（脸、头发）、说话破碎、填充式假笑、用眼神求许可。表演里最有趣的是**地位崩塌（status breaks）**：老板有一秒露怯；下属突然不笑了。有力的场景形状：高位进场却崩塌，或低位进场却翻转全场。

## 5. 言语：好表演听起来如何

- 节奏写在文本里——精确交付；快≠含糊。
- 重叠正常（台词踩着彼此尾巴），但关键词保持干净。
- **音量对比：最可怕的东西说得最轻。** 吼是弱者的货币；掌控场景的人压低音量，所有人凑近听。
- 停顿是事件，不是洞：停顿只在里面有事发生（评估、决定、拒绝回答）时才合法。
- 真实言语有碎屑：打断、半听清的词、重复、未完的句子。完美造句的句子杀死街头真实。

---

# 第二部分 — 写表演：提示词架构

## 6. 角色表演主档案（character acting master profile）

每个常驻角色有一条主档案——关于他怎么演的永久真相源。写一次，再按场景改编（见第 8 节）。目标长度：**150–220 词，一段流畅散文**，全英文，完全可观察、可拍。

**模板（block 顺序固定）：**

```
Character acting as [NAME]. [Age, build, physique, posture — the body as a
document of their biography]. [The psychological engine in one clause — the
inner drive that explains the physicality]. Vocal profile: [pitch/timbre,
accent/origin, pace and delivery manner, and how the voice breaks or shifts
under emotion]. Key physical habits and tics: [signature tic with its
trigger; stress tic with its trigger; concealment behavior — what they do
to hide what they feel; the facial mask and the exact condition under which
it cracks]. Walking style: [the gait as characterization — named and
specific, with weight, rhythm and foot placement]. However, when [emotional
trigger], [the transformation — how the posture, gait and face change].
[Optional: the softening target — the one person or thing that makes the
face genuinely soften].
```

**写每个 block 的规则：**

1. **只写可观察行为。** 每个内在状态都要有身体标记。绝写「他紧张」——写发抖的下唇、沉重的吞咽、张口长吸与噘唇急呼。
2. **每个 tic 都有触发（trigger）。** 不是「他掰指节」，而是「他在闲聊时为假装有自信而掰指节」。格式：[tic] + [何时/为何]。无触发的 tic 是装饰；有触发的 tic 是剧作。
3. **给步态起名。** 一个被引用的独创名锚定生物力学：「power-walk」「peacock strut」「gallery walk」「battering-ram stride」「dreadnought pace」。然后拆解：重量、步幅、躯干与手臂做什么、头做什么。
4. **造面具 AND 裂缝。** 档案里最电影化的装置是「条件性转变」： facade 与精确使它崩塌的触发。被拒就垮成孩童式塌腰的霸气swagger；一提家人就闪过惊慌无能的喧哗大嘴；在某具体人面前融成灿烂微笑的严厉纪律。**每个档案至少带一条「However, when X — …」从句。** 同时演两种真相，是木偶与人的区别。
5. **一个软化对象（softening target）。** 合适时给脸一个、且仅一个让它真正软下来的人/动物/物。一个——不是两个。这让人性化而不稀释。
6. **无服装。** 衣装永远在提示词的场景/外观 block，绝不在表演档案。档案必须扛得住任何换装。
7. **无摄影机、无颜色。** 表演只驱动表演、脸、嗓音、动作。摄影机、调色、光在提示词别处。
8. **体格承载传记。** 年龄、体格、姿态被选中来讲后台故事：被过往斗争「风化的」体格、永远紧绷的肩、「为显权威而过度矫正」的姿态。身体是文献——职业、旧伤、自我形象必须可读于其中。

## 7. 眼生命（Eye life）——每个档案、每个场景强制

死眼是 AI 生成表演的头号破绽。给每个角色连续、自然的眼部生命：

- **微扫视与视线定位（Micro-saccades and gaze targeting）** 朝向他注意的人/物；视线持续移动——眼神飘走、思考中闪开、扫到一个细节再落回。绝不冻结锁定一点。
- **真实的眨眼频率与质量**，随状态变：压力下快速眨眼爆发；控制中缓慢沉稳的眼皮；抽离时刻一次眨眼+呆滞。
- **鲜活的眼神光（catchlights）**——眼睛必须读起来湿润、有光、活着。
- **受控的静止是被选择的，不是死的。** 若角色寄存器是近乎不眨的掠食者式冷静，保持眨眼稀少、缓慢、刻意——是决策，不是冻结——且让视线仍随意图缓慢移动。
- **眼睛引领思想。** 眼睛比头转略早到达目标。思想在词语到来前于眼中可读。
- **眼生命随节拍反应**，如其他行为：眨眼频率、视线稳定度、眼神光温度都随节拍变而变。

## 8. 场景改编——主档案是「重写」，不是「粘贴」

主档案是角色「是谁」。每个场景，把它**重写**进当下时刻：

1. **只写在场角色。** 只为实际在镜中的角色写表演段。镜中无角色→无段落。
2. **保留恒定核心。** 身份、嗓音档案、标志性 tic、眼生命、情绪主线在每个场景相同——这是跨切保持角色一致的东西。绝不矛盾主档案。
3. **为本场重表达。** 选取、强调、修改或删去具体行为，以贴合场景姿态（坐/站/跑/藏）、动作与节拍、情绪状态、时段。
4. **转变，不删除。** 本场物理无法发生的行为被转化，而非移除：瘫在沙发上的不安踱步者，保留同样的紧张引擎，移进不安的微晃、甩腕、撕纸。能量恒定；出口变。
5. **一段流畅散文。** 把改编折进角色寄存器里的散文——无项目符号、无标题、无提示词内「dial」行。
6. **用角色参考 tag 起头**（若你的管线用资产参考），让模型把表演绑对的人。

## 9. 嗓音：锁定身份，绝不改编

表演按场景重写；**嗓音锁定**。每个角色一条 Voice 提示词——永久嗓音身份。角色有台词时，把 Voice 提示词**逐字**粘进提示词的音频/嗓音字段。绝不按场景改。若角色出现但不说话，省略。

**Voice 提示词公式（1–2 句，引号）：**

```
"A [age]-year-old [origin / accent descriptor]. [Timbre and register];
[pace and delivery manner]; [emotional character — and how it shifts under
pressure]."
```

表演段**内**的嗓音档案描述言语如何戏剧化表现（节奏变、破音、低语）；音频字段的 Voice 提示词锁定声音本身。两者必须一致。

## 10. 状态，不是过渡（States, not transitions）

视频生成模型搞砸过渡、搞定状态。描述角色**已在**动作状态——mid-throw、mid-punch、mid-pace、mid-argument——而非到达的过程（「reaches into the bag, pulls out, winds up」会塌；「mid-throw, arm extended」能成）。用状态逐拍串联，而非叙述连续过程。

## 11. 群像与空间（Ensemble and space）

- **群体反应如波传导，绝不整齐。** 一个人先笑到点，第二人半拍后，第三人根本没懂。同步一致的反应读起来假（除非刻意的编排式喜剧同步是重点）。
- **反应比动作更值钱。** 每个事件后，最值钱的帧是「看到它的人」的脸。
- **威胁前冻结（Freeze at the threat）。** 持续的群像微动——重心移、比划、前倾——到关键威胁一切**停**。喧嚣→静止的对比是标点。
- **移动=动机。** 没人横穿房间没有内在冲动：朝向某物或逃离某物。有力的动机化事件：逼近（升级）、背过身（ Dismissal 或藏脸）、他人坐时你站着（抢支配）、冲突中坐下（悖论式权力）、停在门道（门槛=决策点）、开始收拾（用身体下最后通牒）。
- **强者静止安静；弱者焦躁大吼。** 危险不是由危险者演出，而是由周围所有人的张力演出。无预兆的威胁：无威胁式停顿、无慢镜转身——真实世界里暴力不宣而至。
- **损耗累积（Degradation accumulates）。** 若角色在故事里被磨损，在身体上累积携带——更灰、更沉、反应更慢——绝不场景间重置。

---

# 第三部分 — 质量控制

## 12. 坏表演图鉴——在提示词里识别并修正

| # | 症状 | 长相 | 提示词级修正 |
|---|---|---|---|
| 1 | 指示式（mugging） | 脸「描绘」情绪：挑眉、怪相 | 把脸移出任务；写目标并给手活计 |
| 2 | 演结果 | 角色从第二秒就演场景结局 | 只写角色此刻知道的 |
| 3 | 等 cue | 搭档说话时空脸 | 写反应始于搭档台词半句 |
| 4 | 单战术 | 整场一色（全吼/全哀） | 标节拍；每个新战术动词 |
| 5 | 手势图解 | 手势复制词（「大」——张臂） | 手势要么先于思想、要么与词矛盾、要么 absent |
| 6 | 自由情绪 | 无铺垫无触发的泪/怒 | 搭梯子：克制→崩；情绪必须付出代价 |
| 7 | 身体不符传记 | 暴徒舞者姿态；瘾君子鲜亮塑料感 | 设身体档案：重心、节奏、磨损 |
| 8 | 言语过净不符阶层 | 街头角色用文学句 | 碎屑化言语：打断、掉尾、重复 |
| 9 | 威胁信号 | 暴力前「威胁」停顿、眯眼、慢转 | 威胁是平凡的；暴力无预兆 |
| 10 | 同步群像 | 所有人同刻同反应 | 波状错开反应，强度各异 |
| 11 | 死停顿 | 无事发生的静默 | 用评估或活计填满——或删 |
| 12 | 情绪重置 | 强事件后角色瞬间「恢复」 | 状态有惯性；尾巴带进下一拍 |
| 13 | 评论角色 | 表演对观众眨眼（「都知道这好笑」） | 对情境全信；喜剧也死认真演 |
| 14 | 特写过载 | 特写上活跃模仿 | 镜越紧动越少：只有眼与思想 |
| 15 | 死眼 | 冻结瞪视、无眨、无扫视、玻璃眼神光 | 完整套用第 7 节——眼生命从不可选 |

## 13. 表演量表（自我核查）

- **0 — 人偶（Mannequin）。** 台词到了，行为缺席。
- **1 — 朗诵者（Declamer）。** 「有表现力」的台词、指示式情绪、图解身体。
- **2 — 勤勉（Diligent）。** 能猜出目标，但单一战术、反应迟、空停顿。
- **3 — 工匠（Craftsman）。** 目标与节拍在、听搭档、身体合理。缺：潜台词、惊喜战术、状态惯性。
- **4 — 活着（Alive）。** 连续行为、对比战术、潜台词背离文本、地位在身体、反应先于台词、至少一个意外却真实的抉择。
- **5 — 磁石（Magnet）。** 全部「4」加悖论：角色结合不兼容——有趣又可怕、残忍又迷人、说谎又触碰。**两真相规则：5 级时角色总在同时演两种真相**（帮——且恨它；道歉——且防御；爱——且已离开）。特写上单一无矛盾的情绪读起来像合成。

每个主角镜头瞄准 4+；自核查在 2 或以下的段落，发前重写。

## 14. 发送前清单（Pre-send checklist）

- [ ] 目标作为瞄准搭档的动词——每个镜中角色都有
- [ ] 障碍与赌注存在；失败代价真实
- [ ] 2–4 次节拍变化，每次在行为上可见（停顿/姿态/节奏/视线）
- [ ] 反应始于搭档台词结束前；有评估时刻
- [ ] 每个角色有活计；中断动作重音被刻意使用
- [ ] 距离变化且变化有动机；地位在身体而非仅词
- [ ] 所有 tic 带触发；面具带裂缝（「However, when X...」）
- [ ] 眼生命被明确写出：扫视、眨眼质量、眼神光、眼领思想
- [ ] 角色说话则 Voice 提示词逐字粘；静默则省略
- [ ] 状态非过渡；表演内无服装、摄影机或颜色
- [ ] 群像反应错开；强者静、弱者躁
- [ ] 量表核查：这段能打 4+ 吗

---

# 第四部分 — 实战范例（虚构角色，作模式用）

## 15. 主档案（Master profile）

```
Character acting as VIKTOR. Early 60s male, a retired night-shift taxi
driver and former amateur boxer; heavy, thick-necked build gone soft at the
middle, with a flat-nosed face and old scar tissue over both eyebrows; sits
and stands with a low, grounded center of gravity, weight always on the
whole foot. Runs on a single engine: decades of waiting — for fares, for
rounds, for trouble — have made patience his weapon. Vocal profile: low,
hoarse, unhurried baritone with a working-class rasp, short sentences
delivered flat and economical, dropping to a slower, quieter register the
more serious things get — he never speeds up. Key physical habits and tics:
rolls an old coin across his knuckles when sizing a situation up; a slow,
audible nose-breath before he says no; when lying is happening in front of
him, he goes completely still and lets a long silence do the pressing; his
default face is a heavy-lidded, bored mask that conceals total attention.
Eye life: sleepy, hooded eyes with slow deliberate blinks and constant
quiet scanning — mirrors, hands, exits — the gaze settling on a speaker a
beat before his head turns; catchlights low but alive. Walking style: a
heavy, rolling "old boxer's walk," short economical steps, shoulders level,
hands loose and ready, never hurrying. However, when someone raises a hand
near him, the sleepy mask vanishes in a half-second: the chin drops, the
hands rise halfway, the feet find their old stance — then he catches
himself and folds it away, embarrassed. His face only truly softens for
stray dogs, which he feeds from his coat pocket.
```

**Voice（VIKTOR 说话时逐字粘）：** "A 60-year-old ex-boxer and night-cab driver, working-class city accent. Low, hoarse, unhurried baritone; short flat economical sentences with long comfortable pauses; calm and faintly amused, going quieter — never louder — as things get serious."

## 16. 场景改编范例（Scene adaptation example）

场景：VIKTOR 夜里坐在停着的出租车里；后座一个紧张年轻乘客在谎称有钱付车费。

```
VIKTOR sits motionless in the driver's seat, heavy and grounded, watching
the passenger in the rear-view mirror instead of turning around — his
hooded eyes flick between the mirror, the passenger's hands and the door
lock in slow, quiet scans, blinks rare and deliberate, the gaze settling
on the mirror a beat before his head ever moves. The old coin walks across
his knuckles on the seat-rest, unhurried; as the passenger's story falls
apart, the coin stops mid-roll — he lets the silence sit, takes one slow,
audible breath through the nose, and answers in his low, hoarse baritone,
flatter and quieter than before, never speeding up. Only when the kid's
voice cracks does the sleepy mask ease a fraction: a long exhale, a slow
blink, the coin resuming its roll — patience choosing, for now, to be
kind.
```

此处发生：步行无关（坐着）所以能量移进静止与硬币；标志性 tic 保留触发（硬币=评估、停币=中断动作作标点、鼻息=拒绝、静止+沉默=对说谎者的压力）；眼生命服从主档案但重新瞄准镜、手、锁；节拍变化可见（币停→沉默→更轻的嗓音→软化）；嗓音未动——它将逐字粘进音频字段。

---

# 最终公理（FINAL AXIOMS）

1. 表演是压力下的行为，不是感受的展示。
2. 聆听比说话重要；反应比朗诵重要。
3. 情绪是赢或输的斗争的后果，且它昂贵。
4. 身体比词语聪明：当文本与身体冲突，观众信身体。
5. 强者静止安静；弱者忙乱大吼。例外是事件。
6. 每个 tic 需要触发；每个面具需要裂缝。
7. 每个场景都是某人的失败。若无人输，便无场景。
8. 潜台词不是「演出来」——是「没藏住」。
9. 状态，不是过渡；模型拍「是何」，不拍「成为何」。
10. 拿不准时——剪。更少的表演=更多的真实。
