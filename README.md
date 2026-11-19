# ai-mv

两个横屏 AI 概念 MV 的实验项目：AI 插画 + 程序化剪辑，各自独立渲染。

| 项目 | 时长 | 规格 | 主题 |
| --- | --- | --- | --- |
| `ainight/` | 14.96s | 1920×1080 / 30fps | AI 焦虑、夜晚、屏幕与代码 |
| `jianghu/` | 91s | 1920×1080 / 30fps | 一笑江湖·天上白玉京，古风歌词叙事 |

## 环境

- Python 3（Pillow、numpy、scipy）
- `ffmpeg` / `ffprobe`
- 中文字体（Noto Serif / Sans CJK）

```bash
python3 -m pip install pillow numpy scipy
```

## 目录

```
ai-mv/
├── ainight/
│   ├── config/timeline.json   # 镜头顺序、时长、转场
│   ├── config/lyrics.json     # 歌词与逐字时间
│   ├── assets/                # AI 插画（原始素材入库）
│   └── build/encode.sh        # 渲染 + 编码入口
└── jianghu/
    ├── config/                # 同上
    ├── assets/
    ├── docs/
    └── build/encode.sh
```

中间帧、混音、成片不入库（见 `.gitignore`）。

## 运行

```bash
cd ainight && bash build/encode.sh
cd jianghu && bash build/encode.sh
```

产出默认落在各自 `build/` 或 `out/` 目录，具体路径看脚本头部注释。

## 改一支片子的顺序

1. 改 `config/timeline.json`：镜头顺序、每镜时长、转场类型
2. 改 `config/lyrics.json`：句子与逐字高亮时间（要跟音轨对齐）
3. 换 `assets/` 里的插画（保持同名可免改配置）
4. 重跑 `encode.sh`；只想看单帧可用脚本里的预览分支

## 已知限制

- 每个项目自带 `encode.sh`，重复度高；后续可以收口到 codecut 统一时间线
- 歌詞/字幕是脚本烧录，没有独立的字幕轨，改文案要重渲染
- `jianghu` 使用的参考曲目仅作技术演示，公开传播前必须换成已授权音乐
- 成片体积大，走 Release 分发，不入 Git

## 相关仓库

- [codecut](https://github.com/xcsweb/codecut)：通用剪辑 CLI，可承接这两个项目的终剪
- [travel](https://github.com/xcsweb/travel)：竖屏情绪片
- [motion-video](https://github.com/xcsweb/motion-video)：横屏高能混剪与网页特效
