# 交付物清单模板（deliverable manifest）

> 用法：项目完成后，生成本清单作为交付物总索引。列出所有产出文件、路径、用途和状态。用户通过此文件可快速找到任何需要的提示词或参考图。

---

## 项目信息
- **项目名**：<project_name>
- **体裁**：<竖屏短视频 / 横屏短剧 / 漫剧 / 横屏电影>
- **总时长**：<N>秒
- **画幅**：<9:16 / 16:9>
- **生成渠道**：<外部工具>
- **提示词语言**：<中文 / 英文>（按语言路由规则）
- **目标视频模型**：<Seedance 2.5 / Seedance 2.0 / Kling 3.0 / Kling 3.0 Omni / Veo 3>

---

## 一、资产生图提示词

### 角色资产
| @tag | 资产文件 | 生图提示词 | 参考图规格 | 状态 |
|---|---|---|---|---|
| @<tag> | 01-assets/characters/<tag>.md | 01-assets/characters/<tag>_image_prompt.md | 3图（脸/无头全身/背面） | 待生成 / 已生成 |
| @<tag2> | ... | ... | ... | ... |

### 地点资产
| @tag | 资产文件 | 生图提示词 | 参考图规格 | 状态 |
|---|---|---|---|---|
| @<loc_tag> | 01-assets/locations/<tag>.md | 01-assets/locations/<tag>_image_prompt.md | 3/4视角 | 待生成 / 已生成 |

### 道具资产
| @tag | 资产文件 | 生图提示词 | 参考图规格 | 状态 |
|---|---|---|---|---|
| @<prop_tag> | 01-assets/props/<tag>.md | 01-assets/props/<tag>_image_prompt.md | hero/多版本 | 待生成 / 已生成 |

---

## 二、分镜画面生图提示词（首帧参考图）
| 镜号 | 时长 | 视频提示词 | 首帧生图提示词 | 参考图清单 | 状态 |
|---|---|---|---|---|---|
| shot_001 | <N>s | 04-prompts/video/shot_001_v1.md | 04-prompts/image/shot_001_frame.md | 见 reference_manifest.md | 待生成 / 已生成 |
| shot_002 | ... | ... | ... | ... | ... |

---

## 三、分镜视频提示词
| 镜号 | 时长 | 提示词文件 | 中文摘要 | 时长分析 | 状态 |
|---|---|---|---|---|---|
| shot_001 | <N>s | 04-prompts/video/shot_001_v1.md | shot_summaries.md | <时长决策理由> | 待生成 / 已生成 |
| shot_002 | ... | ... | ... | ... | ... |

---

## 四、参考图总清单（reference manifest）

### 每镜参考图搭配
| 镜号 | 角色参考图 | 地点参考图 | 道具参考图 | 上传顺序 |
|---|---|---|---|---|
| shot_001 | @<tag>脸+无头+背面 | @<loc_tag> 3/4 | — | 1.脸 2.无头 3.背面 4.地点 |
| shot_002 | @<tag>脸+无头 | @<loc_tag> 3/4 | @<prop_tag> | 1.脸 2.无头 3.地点 4.道具 |
| ... | ... | ... | ... | ... |

---

## 五、UI 参数设置
| 参数 | 设置值 |
|---|---|
| 画幅 | <9:16 / 16:9> |
| 分辨率 | 1080p 或更高 |
| 模式 | 多参考图 / 图生视频 |
| 单次最大时长 | <按模型能力：30s / 15s / 10s> |

---

## 六、交付文件总目录
```
<output_directory>/<project_name>/
├── README.md                           # 项目概览
├── 00-brief/brief.md                   # 需求确认书
├── 01-assets/                          # 资产（descriptor + 生图提示词 + 参考图规格）
│   ├── characters/
│   ├── locations/
│   └── props/
├── 02-registry/asset-registry.md       # @tag 词典
├── 03-shotlists/block_<NN>_<name>.md   # 分镜表 + GEO
├── 04-prompts/
│   ├── video/shot_<NNN>_v<N>.md        # 视频提示词
│   ├── image/shot_<NNN>_frame.md       # 首帧生图提示词
│   ├── shot_summaries.md               # 中文摘要
│   └── reference_manifest.md           # 参考图清单
├── 05-generations/                     # 用户生成的素材
├── 06-logs/iteration-log.md            # 迭代日志
├── 07-post/post-production-notes.md    # 后期指引
└── 08-delivery/
    ├── deliverable-manifest.md         # 本文件
    └── UI-PARAMS.md                    # UI参数设置
```

---

## 七、交付检查清单
- [ ] 所有角色/地点/道具都有生图提示词
- [ ] 所有镜头都有视频提示词（16-block 格式）
- [ ] 所有镜头都有首帧生图提示词
- [ ] 参考图清单完整（每镜列出所有需要的参考图及上传顺序）
- [ ] 时长分析完成（每镜时长有决策理由）
- [ ] 总时长在用户指定范围内
- [ ] 中文摘要在独立文件中（不污染提示词正文）
- [ ] UI 参数清单完整
- [ ] asset-registry 与 01-assets 一一对应
- [ ] iteration-log 模板就绪