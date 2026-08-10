# Style Prefix 模板（逐字粘贴到每个提示词末尾）

> 用法：复制下方原文，逐字粘到每个视频提示词的 STYLE 块。`SFX only. No music.` 是强制的——音乐属于后期。

## 电影感原版（横屏电影 / 短剧默认）
```
Style: 8K IMAX. Photorealistic — no 3D render, no game engine, no game-cutscene aesthetic.
Cinematography: floating immersive camera that lives with the actors; natural motivated light; painterly composed frames, strong silhouettes against the light.
Lighting: Natural light only — contre-jour backlight, camera on shadow side, atmospheric haze throughout. Key light from sky and windows only.
Color: 60:30:10 — dominant / secondary / accent.
Camera: Physical cine lens. 180° shutter motion blur.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush, pore-shadow matching on-set light.
Acting: Hollywood — micro-pauses before reactions, precise eye-line, wet living eyes with catch-lights, visible breath and chest rise.
Physics: Gravity and inertia respected — mass has real weight, correct contact shadows. No floating props.
Composition: Rule of thirds + golden ratio. Every person moving from frame one.
Continuity: Characters, props, environment identical across every cut. No identity drift.
Technical: 24fps smooth motion. 8K detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.
```

## 技术标签（收尾必写，填画幅与时长）
```
Photorealistic. NON-IP. [画幅]. [时长]s. SFX only. NO CGI. Cinematic.
```

## 体裁变体（按需替换，一致性条款永远保留）
- **横屏电影 / 短剧**：用上面原版逐字。
- **漫剧**：用下方漫画风格变体——切换为漫画/分镜式渲染风格，但 **保留** `Skin` / `Acting` / `Continuity` 三条根条款，确保跨镜头角色一致性。
- **竖屏短视频（9:16）**：可降格——去掉 `8K IMAX`，保留 `Photorealistic` / `Skin` / `Acting` / `Continuity` 条款；`Composition` 适配竖构图；`No subtitles` 保留（竖屏字幕在后期安全区内加，绝不让模型生成文字）。
- **亮调平台风**（若不要电影感）：把 `Lighting` 换成明亮高调描述，但 **保留** `Skin`（毛孔级真实）与 `Acting`（眼神光/微停顿）与 `Continuity`（无身份漂移）——这三条是活人感与一致性的根。
```
Style: Photorealistic — no 3D render, no game engine, no game-cutscene aesthetic.
Cinematography: clean contemporary framing; bright motivated key light; natural vibrant colors.
Lighting: Bright high-key lighting — soft diffused key from front-above, gentle fill from camera side, even exposure across faces and environment. No deep shadows.
Color: 60:30:10 — dominant / secondary / accent.
Camera: Physical lens. Natural motion blur.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush, pore-shadow matching on-set light.
Acting: Hollywood — micro-pauses before reactions, precise eye-line, wet living eyes with catch-lights, visible breath and chest rise.
Physics: Gravity and inertia respected — mass has real weight, correct contact shadows. No floating props.
Composition: Rule of thirds + golden ratio. Every person moving from frame one.
Continuity: Characters, props, environment identical across every cut. No identity drift.
Technical: 24fps smooth motion. High detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.
```

## 漫剧风格变体（漫画/分镜式渲染，保留三条根）
```
Style: Cinematic comic drama — high-fidelity manga-inspired live-action with stylized rendering. No pure 2D animation, no flat cartoon. Photorealistic base with comic-grade contrast and panel composition.
Cinematography: strong graphic framing; bold compositional lines; dynamic panel-style blocking; dramatic angle shifts between shots. Characters framed with comic-book intensity.
Lighting: High-contrast motivated light — strong key with deep shadows, rim light for separation. Chiaroscuro with comic-book edge lighting. Atmospheric haze for depth.
Color: 60:30:10 — dominant / secondary / accent. Saturated but controlled palette, graphic color blocking.
Camera: Physical lens with stylized depth. Slight exaggeration in focal length for dramatic effect.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush, pore-shadow matching on-set light.
Acting: Hollywood — micro-pauses before reactions, precise eye-line, wet living eyes with catch-lights, visible breath and chest rise.
Physics: Gravity and inertia respected — mass has real weight, correct contact shadows. No floating props.
Composition: Bold graphic composition; strong diagonals; panel-style framing. Every person moving from frame one.
Continuity: Characters, props, environment identical across every cut. No identity drift.
Technical: 24fps smooth motion. High detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.
```

## 竖屏短视频（9:16 降格版）
```
Style: Photorealistic — no 3D render, no game engine, no game-cutscene aesthetic.
Cinematography: tight vertical framing; bright natural light; subject fills 60% of frame vertically.
Lighting: Natural motivated light — soft key from front, gentle fill, even exposure on faces.
Color: 60:30:10 — dominant / secondary / accent.
Camera: Physical lens. Natural motion blur.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush, pore-shadow matching on-set light.
Acting: Hollywood — micro-pauses before reactions, precise eye-line, wet living eyes with catch-lights, visible breath and chest rise.
Physics: Gravity and inertia respected — mass has real weight, correct contact shadows. No floating props.
Composition: Vertical rule of thirds; subject centered vertically with headroom. Every person moving from frame one.
Continuity: Characters, props, environment identical across every cut. No identity drift.
Technical: 24fps smooth motion. High detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.
```

## 竖屏电影感暗调版（9:16 · 夜景/雨天/情绪场景）
```
Style: Photorealistic — no 3D render, no game engine, no game-cutscene aesthetic.
Cinematography: tight vertical portrait framing; natural motivated light from practical sources; subject fills 60% of frame vertically.
Lighting: Natural motivated light from in-scene practical sources (lamps, windows, candles) — dominant key from one practical source, soft ambient fill from environment, rim light from back sources when present; no flat front fill, no beauty light; shadows fall naturally with visible depth.
Color: 60:30:10 — dominant / secondary / accent.
Camera: Physical lens. Natural motion blur.
Skin: Pore-level realism — vellus hair, asymmetric moles, capillary flush, pore-shadow matching on-set light. Catch-lights from the practical source only.
Acting: Hollywood — micro-pauses before reactions, precise eye-line, wet living eyes with catch-lights, visible breath and chest rise.
Physics: Gravity and inertia respected — mass has real weight, correct contact shadows. No floating props.
Composition: Vertical rule of thirds; subject centered vertically with headroom; eyes at upper-third line. Every person moving from frame one.
Continuity: Characters, props, environment identical across every cut. No identity drift.
Technical: 24fps smooth motion. High detail. No jitter.
Audio: Environmental SFX only. No music. No subtitles.
```

## 不可删的根条款（任何体裁都保留）
- `Skin: Pore-level realism` —— 防塑料脸
- `Acting: ... wet living eyes with catch-lights` —— 防死脸
- `Continuity: ... No identity drift` —— 防换脸
- `Audio: Environmental SFX only. No music.` —— 防自带配乐