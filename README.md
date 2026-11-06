# 吴宇歌 · 个人作品集 2026

> 把复杂业务，拆成可运行的算法系统。

大模型算法 / 多智能体工程 / 数据与知识系统。五类、十个项目，每个项目按「背景 — 介绍 — 亮点 — 原理与架构 — 可视化 — 可公开的技术细节」展开。

- 网页版（GitHub Pages）：`index.html`
- PDF 版：`吴宇歌_个人作品集_2026.pdf`（A4，14 页）

## 内容结构

| 类别 | 项目 | 性质 |
| --- | --- | --- |
| 算法类 | 01 AI 远程异地评审专家异常行为识别 | 实战交付 |
| 算法类 | 02 大模型全链路工程手册 | 课程实战复现 |
| 开发类 | 03 彩翼 · 公共采购智能体协同管理平台 | 实战交付 |
| 开发类 | 04 EchoMind · 多 Agent 客服运行时 | 自研 |
| 产品类 | 05 问对 · 访谈实时辅导 | 开源二次开发 |
| 产品类 | 06 知栈 · 企业知识库问答 | 课程实战复现 |
| 数据类 | 07 政务采购数据治理 | 实战交付 |
| 数据类 | 08 47,950 条文本的 LLM 辅助编码 | 实战交付 |
| 行业类 | 09 AI 量化交易系统 | 课程实战复现 |
| 行业类 | 10 金融风控算法模型 | 课程实战复现 |

### 性质标注口径

- **实战交付**：在职期间的真实项目，有真实用户与上线记录，涉敏内容已脱敏。
- **自研**：独立完成设计与实现的系统，可现场演示并讲解实现细节。
- **课程实战复现 / 开源二次开发**：基于公开课程或开源项目的实现与改造，标注基线来源，不冒充原创。

## 目录

```
00_作品集/
├── index.html                      # 网页版（单文件，无外部依赖）
├── portfolio_pdf.html              # PDF 排版专用页
├── 吴宇歌_个人作品集_2026.pdf        # PDF 成品
├── build.py                        # 渲染器（网页版 / PDF 版共用一套数据）
├── build_parts/
│   ├── theme.py                    # 视觉系统 + 内联 SVG 图表组件
│   ├── projects_1.py               # 项目 01–05 数据与图表
│   ├── projects_2.py               # 项目 06–10 数据与图表
│   └── build_all.py                # 一键构建（HTML → PDF → 逐页预览）
└── README.md
```

## 本地构建

```bash
python build.py            # 生成 index.html
python build.py --pdf      # 生成 portfolio_pdf.html
python build_parts/build_all.py   # 全量：网页版 + PDF + 逐页预览
```

PDF 由 Chrome headless 打印 `portfolio_pdf.html` 得到，需带独立 `--user-data-dir`。

## 技术说明

- 纯 Python 生成静态 HTML，无外部依赖、无 CDN，离线可看，GitHub Pages 直接托管。
- 所有图表为内联 SVG（`viewBox` 自适应），文字可选中、可打印，不依赖图片资源。
- 视觉系统：墨黑 `#101827` / 深海军蓝 `#12324E` / 青 `#0E7C86` / 琥珀 `#D98A1F` / 米白纸底 `#FBFAF7`。

## 相关仓库

- [bid-evaluation-behavior-recognition](https://github.com/Sheroisshero/bid-evaluation-behavior-recognition) — 项目 01
- [Caiyi-Agent-Platform](https://github.com/Sheroisshero/Caiyi-Agent-Platform) — 项目 03
- [resume-wuyuge](https://github.com/Sheroisshero/resume-wuyuge) — 个人简历
- [ai-assisted-content-analysis](https://github.com/Sheroisshero/ai-assisted-content-analysis) — 文本编码与分析

---

吴宇歌 · 新加坡国立大学 科学人工智能硕士 · github.com/Sheroisshero

## 项目说明文档

三个未单独建库的项目，说明文档归档在本仓库 `projects/` 下：

- [EchoMind · 多 Agent 客服运行时](projects/echomind-agent-runtime/README.md)
- [问对 · 访谈实时辅导](projects/wendui-interview-coach/README.md)
- [知栈 · 企业知识库问答](projects/zhizhan-rag-knowledge-base/README.md)
