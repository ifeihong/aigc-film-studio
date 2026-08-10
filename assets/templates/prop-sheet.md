# 道具表模板（prop sheet）

> 用法：每个关键道具建一个文件，文件名 = tag（`prop_crystal.md` → `@prop_crystal`）。道具按用途分**多版本**，比跟模型硬扛更便宜。

## @<prop_tag>（如 @prop_crystal）

### 多版本（按需建，各配独立 descriptor）
- [ ] **hero 特写版**：用于近景/特写，细节最全
- [ ] **bloodied / damaged 版**：用于「掌中一闪」等短暂Reveal
- [ ] **hidden 版**：用于握拳镜头——提示词**禁止**显示本体，只允许「指缝漏蓝光」之类

### Descriptor（英文，逐字进提示词）
```
@<prop_tag> — <object>, <material + surface finish>, <size reference（用熟悉物比大小）>,
<distinctive detail>, <glow/wear/state>. 
```

### 尺度锚点（ oversized / 巨型道具必带）
- 若道具超大或是巨型物：每个相关提示词带 **SCALE LAW**——「尺寸对比 + 人形参照物」双锚，防模型悄悄缩回人高。
- 范例见 SKILL.md「SCALE LAW」模板或 `00-overview-handbook.md` §6。

### 硬规则
- 哪个版本上哪个镜，在分镜表里写死对应 tag（如 `@prop_crystal_hidden`）。
- 关键道具同样过压力测试：在不同手、不同光下能被认出。
- 改道具外观（加血/破损）用点修改 + 遮罩贴回，不整张二次过模型。
