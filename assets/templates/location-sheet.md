# 地点表模板（location sheet）

> 用法：每个地点（含日/夜/雨等状态）建一个文件，文件名 = tag（`loc_cave_front.md` → `@loc_cave_front`）。地点的每种状态都是**独立资产**。

## @<loc_tag>（如 @loc_cave_front）

### 参考图（表图规范）
- [ ] **3/4 视角**拍摄/生成，**不要正面「美图」**——正面图在远景变平墙纸，边缘外模型每次乱编
- [ ] 3/4 视角给模型足够纵深，覆盖近一圈角度
- [ ] 反打角度两法：① 用 GPT Image 2 / Nano Banana 生成同房间另一角（匹配原图柔焦）；② 生成一段空镜视频让镜头慢走空间，截图目标角度再到 Seedream/NBP 提升纹理光照

### Descriptor（英文，逐字进提示词）
```
@<loc_tag> — <space type>, <key architecture/material>, <the one anchor object>, <light source & direction>,
<atmosphere/haze>, <color mood 60:30:10>. 3/4 view.
```

### 锚点与轴线（必填）
- [ ] **锚点物**：一个地标物（柱子 / 灯 / 沙发 / 祭坛），场面调度都绑它——「the hero at the lamp, facing the door」
- [ ] **光源逻辑**：一个主光源决定阴影方向；允许环境漫射光（窗光/天光）作为底光，但底光不产生第二个阴影方向。绝不让两个强光源各投各的阴影（"两个太阳"）。
- [ ] **GEO SPATIAL LAYOUT**：本地点的空间地图（见 `geo-spatial-layout.md` 模板），每场景写一次、逐镜粘贴不变
- [ ] **180° 轴线**：摄影机站哪一侧、绝不越过哪条线，写死

### 状态变体（独立资产）
- [ ] `@<loc_tag>_day` / `@<loc_tag>_night` / `@<loc_tag>_rain` ……各占一行注册表、各配 descriptor

### 喂模型时的硬规则
- 提示词里给地点参考**命名角色**：`@loc_cave_front for location reference`
- 并加禁令：`take only the space and the texture — do not use as a starting frame, do not inherit the composition, the angle or the grade.`
