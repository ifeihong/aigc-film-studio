# 逐镜提示词骨架（shot-prompt skeleton）

> 用法：每个镜头复制本骨架填空，输出提示词（按用户输入语言生成）。块名保持英文，技术标签保持英文，填写内容用用户输入语言。范例见 `10-cinedance-video-prompt.md` 与 `00-overview-handbook.md` §4.3。
> 发出前必过 `20-qa-checklists.md` Part A。

```
SCENE CONTEXT
EXACT <N> CHARACTERS — NO DUPLICATES: <角色A>, <角色B>. <地点>, <时间/光>. <发生了什么，一句>. One continuous <时长>-second shot, no cuts.

ACTIVE REFERENCES
@<tag> for character reference — <此刻状态：服装/伤/手持物，逐字引 descriptor>. 100% matches the reference.
@<loc_tag> for location reference — take only the space and the texture: <材质/锚点/光>. Do not use as a starting frame, do not inherit the composition, the angle or the grade.
@<prop_tag> for prop reference — <1-2句物理描述>. 100% matches the reference.

LOCATION MAP
<此段粘贴 GEO SPATIAL LAYOUT 模板内容（以 GEO SPATIAL LAYOUT 开头）。block 标题是 LOCATION MAP，内容是 GEO：纯空间地图——地标物、左/右有什么、距地标几米、摄影机站哪侧、绝不越过的轴线。逐字粘贴本场景 GEO。>

FIRST FRAME AND SPATIAL BLOCKING
<第一帧即完整空间：谁站哪、朝向哪、看向哪；首秒为 wide、无台词无动作，固定位置。竖屏（9:16）例外：不做传统 wide，改用 medium portrait——人物占画面60%垂直高度，眼睛在上三分线，环境在身后可见（详见 handbook §4.7）。>

FORMAT MODE
Single continuous take, <时长> seconds, real time, no cuts, no speed ramps.

OPTICS
≈<角度>° <镜头性格>, camera <高度>, <距离> from <锚点>, <对焦计划>; <必须保持锐利的主体>.

CAMERA
<摄影机行为：如 calm breathing handheld, slow reframe of a few degrees. No push, no zoom, no whip.>

ACTION TIMING
0.0–<t>s — <拍1：每拍≤3句；复杂动作放开头「已发生」；写物理不写形容词>.
<t>–<t>s — <拍2：反应先于台词；含 phased blinking 与 gaze>.
<t>–<t>s — <拍3：节拍变化在行为上可见>.

PHYSICS
<重量/接触/惯性：谁有真实重量、什么在动、呼吸是可听见的工作>.

LIGHTING
One <性质> source <方向>: <谁被怎样照亮、眼窝阴影、冷边>; <暗部几档>; no fill from the camera side.

AUDIO
<!-- 有对白模板 -->
Diegetic only — <环境声/脚步/道具声>. <角色> voice (verbatim): "<逐字 Voice 描述>". His line, and nothing else: "<台词>". Nobody else speaks; <半笑等是面部动作，无声音>. No music.
<!-- 无对白模板：Diegetic SFX only — <环境声描述>. No dialogue. No music. Nobody speaks. -->

CHARACTER ACTING
<每个可见角色一段流畅英文散文：用角色名字大写开头（如 MEI —），不用 @tag。@tag 只用在 ACTIVE REFERENCES 段。写他想要什么（目标动词）、压力下的身体节律、可见的微动作/习惯/眼神、跨镜变化。无项目符号、无字段标签、无"emotional state:"等dial行。详见 11-acting-performance.md。>

STYLE
<逐字粘贴 Style Prefix（见 style-prefix.md）>

QUALITY
8K detail, pore-level skin, no jitter, no flicker; the faces stay exactly their references at every distance.

POSITIVE CONSTRAINTS
Exactly <N> people, no one else.
Exactly ONE <关键物>, on <位置> — never <错误位置>.
<计数/禁令，全写成「画面里有什么」>.
The camera stays on <一侧> for all <时长> seconds.
Photorealistic. NON-IP. <画幅>. <时长>s. SFX only. NO CGI. Cinematic.
```

## 填写纪律
- 全部**现在时、短句**；动作只用**正向**（写 falls on his stomach，不写 does NOT fall on his back）。
- 角色**第一帧就在画面里**；除非要求，绝不看镜头。
- 不写年龄数字；敏感词换安全表述（dark→low key）。
- 台词只进 AUDIO 段；动作只进 ACTION 段；二者不混。
- 对白镜：首秒 wide 可带上一镜台词尾音；新镜以「上一镜收尾那句」开场，情绪随文本过缝。