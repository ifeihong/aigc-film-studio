# 资产注册表（asset-registry）

> 用法：全项目唯一的 @tag 命名词典。每新增一个角色/地点/道具（含每个状态变体），在此登记一行。提示词、分镜表、日志里的 tag 必须与此表逐字一致。

| @tag | 类型 | 状态/版本 | descriptor 文件 | 参考图 | 压力测试 | 声音锁定 | 行为主档 | 备注 |
|---|---|---|---|---|---|---|---|---|
| @roco | 角色 | 常服 | 01-assets/characters/roco.md | ✅ 3图 | 10/10 ✅ | ✅ v1 | ✅ | 主角 |
| @roco_wet | 角色 | 湿身 | 01-assets/characters/roco_wet.md | ✅ | 10/10 ✅ | 同 @roco | 同 @roco | 雨戏 |
| @roco_blood | 角色 | 血 | 01-assets/characters/roco_blood.md | ✅ | 10/10 ✅ | 同 @roco | 同 @roco | 战后 |
| @loc_cave_front | 地点 | 日 | 01-assets/locations/loc_cave_front.md | ✅ 3/4 | 同框✅ | — | — | 锚点：石柱 |
| @loc_cave_night | 地点 | 夜 | 01-assets/locations/loc_cave_night.md | ✅ | 同框✅ | — | — | 独立资产 |
| @prop_crystal | 道具 | hero特写 | 01-assets/props/prop_crystal.md | ✅ | — | — | — | 另有 bloodied/hidden 版 |

## 填写规则

- **每个状态 = 独立行**：湿/伤/换装、日/夜/雨，都是独立资产，绝不混在一个 tag 里。
- **压力测试** 填 10 次生成中可识别的次数（10/10 才算过），并注明是否做过「同框 + 实景光」测试。
- **声音锁定 / 行为主档** 只适用于角色；状态变体继承原角色，标「同 @xxx」。
- **道具多版本**：hero（特写）/ bloodied / hidden（握拳只露光缝）各占一行或合一行多版本列。
- 本表与 `01-assets/` 目录一一对应；**不允许出现表外 tag（孤儿），也不允许表内 tag 缺文件**。
