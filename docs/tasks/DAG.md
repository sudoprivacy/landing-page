# SudoClaw Landing Page — 任务 DAG

## 依赖关系图

```
T0 (设计规范)
├──► T0.5 (视觉素材生成)
├──► T1 (Nav + Hero) ◄── T0.5
├──► T2 (Copilot + Worker) ◄── T0.5
├──► T3 (为什么选择) ◄── T0.5
├──► T4 (产品矩阵) ◄── T0.5
├──► T5 (场景案例) ◄── T0.5
├──► T6 (硅基产线 + 信任) ◄── T0.5
├──► T7 (资质背书)
└──► T8 (开源 + CTA + Footer)
      │
      ▼
T9 (页面集成) ◄── T1, T2, T3, T4, T5, T6, T7, T8
      │
      ▼
T10 (法律页面) ◄── T0
      │
      ▼
T11 (GitHub Pages 部署) ◄── T9, T10
```

## 任务清单

| ID | 任务名 | 依赖 | 可并行 | 优先级 | 预估复杂度 |
|---|---|---|---|---|---|
| T0 | 设计规范 & Tailwind Config | 无 | — | P0 | 低 |
| T0.5 | 视觉素材生成（SVG 图标/插画/Mockup） | T0 | T7,T8,T10 | P0 | 中 |
| T1 | Nav + Hero 区块 | T0, T0.5 | T2-T8 | P0 | 中 |
| T2 | Copilot + Worker 架构区块 | T0, T0.5 | T1,T3-T8 | P1 | 中 |
| T3 | "为什么选择" 差异化卡片 | T0, T0.5 | T1-T2,T4-T8 | P1 | 低 |
| T4 | 产品矩阵区块 | T0, T0.5 | T1-T3,T5-T8 | P1 | 低 |
| T5 | 场景案例区块（10分类34卡片） | T0, T0.5 | T1-T4,T6-T8 | P1 | 高 |
| T6 | 硅基产线 + 渐进信任 | T0, T0.5 | T1-T5,T7-T8 | P1 | 中 |
| T7 | 资质背书区块 | T0 | T1-T6,T8 | P1 | 低 |
| T8 | 开源 + CTA + Footer | T0 | T1-T7 | P1 | 中 |
| T9 | 页面集成 + 全局样式 + 响应式 | T1-T8 | — | P0 | 高 |
| T10 | 法律页面（terms + privacy） | T0 | T1-T8 | P2 | 低 |
| T11 | GitHub Pages 部署 | T9, T10 | — | P0 | 低 |

## 执行建议

**Wave 1（串行）：** T0
**Wave 2a（串行）：** T0.5（依赖 T0 的色板和品牌规范）
**Wave 2b（并行 ×8）：** T1-T8（T7/T8 不依赖 T0.5，可在 Wave 2a 同时启动）
**Wave 3（串行）：** T9（集成）+ T10（法律页面可并行）
**Wave 4（串行）：** T11（部署）

> **实际操作建议：** T0 和 T0.5 可以合并为一个 Worker 任务一起做。T7、T8、T10 不依赖图标素材，可以和 T0.5 并行启动。

## 品牌色

根据 Logo 原始 SVG（`#F59E0B`），品牌主色已更新：
- `--accent`: `#F59E0B` (amber-500)
- `--accent-hover`: `#D97706` (amber-600)
- `--accent-light`: `#FEF3C7` (amber-100)

## 文件结构（实际 repo 路径）

```
landing-page/                        ← repo 根目录
├── index.html                       ← T9 产出（待生成）
├── terms.html                       ← T10 产出（待生成）
├── privacy.html                     ← T10 产出（待生成）
├── assets/
│   ├── favicon.ico                  ← 浏览器标签图标 ✅
│   ├── logo/                        ← Logo 原始文件（多格式）✅
│   │   ├── sudowork.svg
│   │   ├── sudowork-clean.svg
│   │   ├── sudowork_logo_black_bg.svg
│   │   ├── sudowork-logo.png
│   │   ├── icon.png / white-icon.png
│   │   └── app.png / app_dev.png / app.ico / app.icns
│   └── images/                      ← 所有页面用图 ✅
│       ├── logo.svg                 ← amber 立方体 Logo（黑底）
│       ├── logo-black-bg.svg        ← 黑色立方体 Logo（黑底）
│       ├── hero-bg.jpg              ← 01 Hero 背景图
│       ├── hero-mockup.jpg          ← 02 Hero 产品界面 Mockup
│       ├── architecture-flow.jpg    ← 03 Copilot+Worker 架构流程图
│       ├── scenario-sales.jpg       ← 04 场景：销售与获客
│       ├── scenario-service.jpg     ← 05 场景：客户服务
│       ├── scenario-finance.jpg     ← 06 场景：金融与保险
│       ├── scenario-accounting.jpg  ← 07 场景：财务与合规
│       ├── scenario-supply-chain.jpg← 08 场景：运营与供应链
│       ├── scenario-delivery.jpg    ← 09 场景：专业服务与交付
│       ├── scenario-dev.jpg         ← 10 场景：研发与技术
│       ├── scenario-global.jpg      ← 11 场景：出海与国际业务
│       ├── scenario-knowledge.jpg   ← 12 场景：知识管理与决策支持
│       ├── scenario-hr.jpg          ← 13 场景：人力与行政
│       ├── production-line.jpg      ← 14 硅基员工产线概念图
│       ├── trust-timeline.jpg       ← 15 渐进信任四阶段图
│       ├── og-image.jpg             ← 16 OG 社交分享图
│       ├── product-nexus.jpg        ← 17 Nexus OS 架构图
│       ├── product-router.jpg       ← 18 SudoRouter 路由图
│       └── cta-bg.jpg               ← 19 底部 CTA 背景图
├── docs/
│   ├── SudoClaw-宣传资料.md          ← 品牌文案主文档
│   ├── image-prompts/               ← 图片生成 prompts（00-19）
│   └── tasks/                       ← 本目录，开发任务规格
└── README.md
```
