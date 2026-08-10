# 分镜首帧生图提示词模板（shot frame image prompt）

> 用法：为每个镜头生成一张"首帧参考图"的图像提示词。这张图用于：(1) 给视频模型提供视觉参考（图生视频模式）；(2) 锁定镜头的画面构图、人物位置、光照状态。从对应的 CINEDANCE 视频提示词中提取关键信息，转化为图像提示词格式。
> 提示词语言遵循语言路由规则（见 `13-deliverable-system.md` §4）。
> 目标模型选择见 `12-lira-image-prompt.md` 模型路由。

---

## 镜号：shot_<NNN>

### 基本信息
- **对应视频镜号**：shot_<NNN>
- **目标模型**：GPT Image 2 / Nano Banana Pro / Nano Banana 2 / Seedream 5.0 Pro（按 LIRA 路由）
- **画幅**：<9:16 / 16:9 / 1:1>（与视频镜一致）
- **用途**：首帧参考图（图生视频输入 / 视觉参考锚定）

### 参考图上传清单
| 序号 | 参考图 | 角色 | 来源 |
|---|---|---|---|
| 1 | <角色A> 脸部特写（3/4视角） | 身份锚点 | 01-assets/characters/<tag>/ |
| 2 | <角色A> 正面无头全身图 | 体型/服装锚点 | 01-assets/characters/<tag>/ |
| 3 | <角色A> 背面全身图 | 背部细节锚点 | 01-assets/characters/<tag>/ |
| 4 | <地点> 3/4视角参考图 | 空间/材质参考 | 01-assets/locations/<tag>/ |
| 5 | <道具> 特写参考图 | 道具锚点 | 01-assets/props/<tag>/ |

> 注：只列本镜实际用到的参考图。道具参考图仅在道具可见时上传。

### 首帧图像提示词

```
SHOT FIRST FRAME — shot_<NNN>

SCENE
<从 CINEDANCE SCENE CONTEXT 提取：地点、时间、天气/光照状态。一句话。>

CHARACTERS IN FRAME
<从 CINEDANCE ACTIVE REFERENCES 提取每个可见角色的 descriptor（逐字）。>
<角色名> — <descriptor 全文>. 100% matches the reference.
（每个可见角色一段，用名字大写开头。）

LOCATION
<从 CINEDANCE LOCATION MAP 提取 GEO 空间布局的简化版——只保留可见的地标物和空间关系，不含轴线/摄影机位等技术信息。>

SPATIAL BLOCKING
<从 CINEDANCE FIRST FRAME AND SPATIAL BLOCKING 提取：谁站哪、朝向哪、看向哪、与地标物的距离关系。这是首帧的构图核心。>

LIGHTING
<从 CINEDANCE LIGHTING 提取：主光源方向和性质、阴影方向、色温、面部光照状态。>

COMPOSITION
<从 CINEDANCE OPTICS 提取：焦段感觉、构图法则（三分法/黄金比例）、主体在画面中的位置和占比。>
<竖屏（9:16）：人物占画面60%垂直高度，眼睛在上三分线。>
<横屏（16:9）：按镜头设计构图。>

STYLE
<逐字粘贴对应体裁的 Style Prefix 变体。>

MOOD
<一句话画面情绪描述——不是角色情绪，是画面的情绪（如"静谧的暖光中一个孤独的身影"、"冷调雨幕中的等待"。>）

TECHNICAL TAGS
Photorealistic. NON-IP. <画幅>. No text. No watermark. No logo.
```

### 填写纪律
- 首帧图必须与视频提示词的 FIRST FRAME AND SPATIAL BLOCKING 完全一致
- 角色descriptor 逐字复制，绝不缩写
- GEO 简化版只保留**画面中可见的**空间元素，删去轴线/摄影机位等技术信息
- Style Prefix 与视频提示词使用同一变体
- 首帧图不包含任何动作——这是一个静止的画面
- 不生成任何文字、水印、logo（技术标签中明确禁止）
- 如果该镜有道具特写，确保道具在画面中的位置与视频提示词一致