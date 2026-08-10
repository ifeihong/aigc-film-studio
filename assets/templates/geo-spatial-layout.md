# GEO SPATIAL LAYOUT 模板（空间锁定）

> 用法：**每个场景写一次，逐镜粘贴不变**。只画地图——地标物、左右、摄影机位置与轴线；不含人物、不含动作。它治「人物瞬移 / 跳轴 / 摄影机站错边」。
> 地点的「长相」仍由地点资产（descriptor + 参考图）提供，GEO 只是地图。

```
GEO SPATIAL LAYOUT (locked across every shot — pure spatial map):
— <主地标> = <一句话定义，含位置基准，如 "raised circular stone disc at the edge of a cliff">.
— <次地标>: <相对主地标的位置，如 "at the cliff edge, MID-RIGHT relative to the platform">.
— <功能区>: <CENTER-LEFT, ~3 m from the altar>.
— 180° AXIS: camera ALWAYS stays on <某一侧> — it NEVER crosses the line.
— BACK-LIGHTING / KEY LIGHT: <主光源来自哪，如 "crimson horizon glow from BEHIND the platform, rim-lighting silhouettes">.
```

## 填写规则
- **方向只从摄影机说**：用 `frame-left` / `frame-right`，模型不懂「在英雄左边」。
- **位置用锚点 + 米数**：`at the altar`、`three meters away`。
- **写死摄影机一侧**与绝不越过的线，保住所有切镜在同一轴线。
- **每镜切后**重述「谁站哪、看向哪」——模型不记得上一镜。
- **静态对白给一个角落**，不给整个房间：给模型的空间越小，它乱放人物的余地越小。
- 首秒 wide 让模型「拍下」这个布局，之后每镜沿用。
- **GEO 与地点资产配合使用**：GEO 只管空间关系（谁在哪、地标在哪、轴线在哪），地点的视觉外观由地点资产的 descriptor + 参考图提供。两者并列进入提示词。

## 范例（仪式祭坛场景）
```
GEO SPATIAL LAYOUT (locked across every shot — pure spatial map):
— PLATFORM = raised circular ritual stone disc at the edge of a cliff.
— ALTAR-MONOLITH: at the cliff edge, MID-RIGHT position relative to the platform.
— RITUAL CENTER: CENTER-LEFT, ~3 m from the altar.
— 180° AXIS: camera ALWAYS stays on the corpse-field side — it NEVER crosses the line.
— BACK-LIGHTING: crimson horizon glow comes from BEHIND the platform, rim-lighting silhouettes from camera's perspective.
```
