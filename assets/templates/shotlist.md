# 分镜表模板（shotlist · 按场景块）

> 用法：每个场景块建一个文件（`block_<NN>_<name>.md`）。先定本块 GEO 与 Style，再逐镜登记。**一镜一动作**；首秒 wide 固定位置。

## Block <NN> — <场景块名>（如 block_03_tibet_heist）

- **GEO SPATIAL LAYOUT**（本块所有镜头共用，逐字粘贴）：见 `geo-spatial-layout.md`，粘贴于此。
- **Style Prefix**：本块统一（见 `style-prefix.md`）。
- **在场资产**：@roco / @roco_blood / @loc_xxx / @prop_xxx ……

| 镜号 | 时长 | 首帧（谁站哪/看向哪） | 动作一句话 | 对白 | @tags（本镜） | prompt 文件 | 状态 |
|---|---|---|---|---|---|---|---|
| 001 | 12s | Roco 在 mat 中心，门左开 | 训练中被撞见 | "You're late." | @roco @jax @rein @loc_training | shot_001_v3.md | ✅ 定稿 |
| 002 | 8s | … | … | — | … | shot_002_v1.md | 🔄 迭代中 |

## 填表纪律
- **首帧列**必填——模型靠它「拍下」布局，跨镜不丢位置。
- **一镜一动作**：一镜只发生一件事；复杂动作放开头「已发生」；要两个动作就拆两镜。
- **对白列**只记引号内那句；谁无台词标「—」表示完全静默。
- **@tags 列**只列本镜真用到的，与提示词 ACTIVE REFERENCES 逐字一致。
- **prompt 文件列**指向 `04-prompts/shot_<NNN>_v<N>.md`，与 iteration-log 对应。
- 每镜时长含首秒 wide；对白镜首秒可带上一镜台词尾音以缝合情绪。
