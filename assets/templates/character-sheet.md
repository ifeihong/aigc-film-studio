# 角色表模板（character sheet）

> 用法：每个角色（含每个状态变体）建一个文件，文件名 = tag（`roco.md` → `@roco`）。descriptor 逐字进入每个视频/图像提示词，**绝不缩写**。

## @<tag>（如 @roco）

### 参考图（三张表图，规范不可省）
- [ ] **脸部特写**：3/4 视角（脸微侧、非正脸），选「最可信」不选「最美」；瞳孔必须有眼神光（catch-light）
- [ ] **正面全身图（无头）**：去掉头部，逼模型只从特写取脸，防小图取脸导致换脸
- [ ] **背面全身图**
- [ ] 纯灰背景、平光、真实皮肤带毛孔；不修图、不烤胶片颗粒/电影镜头（电影感留在地点与提示词，不进角色表）

### Descriptor（英文，逐字进提示词）
```
@<tag>: <role/body type (age implied by build/wardrobe)>, <hair>, <face>, <skin with visible pores / asymmetric moles>, <clothing>, <distinctive marks: scars/props on body>, <one-line physical manner>. 100% matches the reference.
```
> 规则：冒号格式（`@<tag>: ...`，非 em-dash），结尾必须写 `100% matches the reference.`；不写年龄数字（用体型/穿着/气质暗示）；含可见毛孔与不对称特征（防塑料脸）；描述可辨识的稳定特征，不随场景变。

### 状态变体（每个变体 = 独立资产 + 独立 tag）
- [ ] `@<tag>_wet`（湿身）/ `@<tag>_blood`（血）/ `@<tag>_<outfit>`（换装）……各配独立 descriptor
- [ ] 点修改铁律：改衣服/伤疤/血时，**绝不整张二次过模型**——在 Nano Banana Pro（Seedream 仅用于纹理清理 pass，不做 in-paint 编辑）做点修改后，用遮罩只把改动部分贴回原图，保住原皮肤纹理

### 声音锁定（有台词的角色必填，逐字进 AUDIO 段）
```
Voice: <register 音域>; <tempo 语速>; <accent 口音>; <manner 神态> — <一句性格化的声音描述>.
```
> 例：`Voice: deep, gravelly bass-baritone; slow, calculated pacing; London street accent; menacing calm — he never raises his voice.`
> 罕见名字给音标。同角色跨镜保持 3–4 个声音即可，但描述词逐字不变。
> 例：`Eilidh (AY-lee)`

### 行为主档（behavior profile，指向 behavior-profile 模板）
- 见 `behavior-profile.md`：移动方式 / 手的习惯 / 神经质 tic / 眼神 / 压力下如何崩溃。
- 核心是「来源真相」，各镜据此改编但不改核心；物理上不可能的动作用「转移」不用「删除」。

### 压力测试（通过才锁定）
- [ ] 10 次生成（不同姿势×不同光）10/10 可识别
- [ ] 与其他资产同框不崩；在实景光下不崩
- [ ] 失败 → 改 descriptor 文字，不改模型，重测