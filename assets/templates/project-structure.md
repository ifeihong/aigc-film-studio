# 项目目录结构模板

> 用法：新 AIGC 视频项目开工时，复制本结构到项目根目录。所有产物归位，项目可「复拍任何一镜」。

```
<project>/
├── README.md                # 项目 brief：体裁/时长/画幅/渠道/风格（阶段 0 产物）
├── 00-brief/
│   └── script.md            # 剧本/文案原文
├── 01-assets/
│   ├── characters/
│   │   ├── <tag>.md         # 角色 descriptor + 三图规范 + 状态变体（如 roco.md → @roco）
│   │   └── <tag>/           # 该角色参考图：face.jpg / front_headless.jpg / back.jpg / 状态变体
│   ├── locations/
│   │   ├── <tag>.md         # 地点 descriptor（如 loc_cave_front.md → @loc_cave_front）
│   │   └── <tag>/           # 3/4 视角表图；日/夜/雨为独立资产
│   └── props/
│       ├── <tag>.md         # 道具 descriptor + 多版本（hero/bloodied/hidden）
│       └── <tag>/
├── 02-registry/
│   └── asset-registry.md    # 全项目唯一 @tag 命名词典（见 asset-registry 模板）
├── 03-shotlists/
│   └── block_<NN>_<name>.md # 按场景块一份分镜表（如 block_03_tibet_heist.md）
├── 04-prompts/
│   └── shot_<NNN>_v<N>.md   # 逐镜提示词，版本化（shot_012_v3.md）
├── 05-generations/
│   └── shot_<NNN>/          # 该镜全部生成素材
├── 06-logs/
│   └── iteration-log.md     # 迭代日志（见 iteration-log 模板）
└── 07-post/
    ├── cleanup/             # 点修/重生成记录
    ├── color/               # 调色
    ├── sound/               # 声音/音乐（后期才加）
    └── final/               # 成片
```

## 命名规范（全项目统一，一个词典管到底）

- **@tag**：小写、下划线、唯一。角色 `@roco`；地点带前缀 `@loc_cave_front`；道具 `@prop_crystal`。状态变体在原 tag 后加状态：`@roco_wet` / `@roco_blood` / `@loc_cave_night`。
- **同一 tag 处处一致**：descriptor 文件名、参考图文件夹、提示词内 ACTIVE REFERENCES、分镜表、日志——全部用同一个 tag，绝不改写法。
- **提示词版本**：`shot_<NNN>_v<N>.md`，每次 surgical 迭代升一个版本，与 iteration-log 一一对应。
- **场景块**：`block_<NN>_<name>`，以「地点 × 时间 × 人物状态」为边界切分。
