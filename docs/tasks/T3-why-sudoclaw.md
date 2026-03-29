# T3 — "为什么选择 SudoClaw" 差异化卡片区块

> **依赖：** T0（设计规范）
> **产出：** `<section id="why-sudoclaw">` 完整 HTML
> **内容来源：** `SudoClaw-宣传资料.md` 第 38-67 行

---

## 目标

6 张卡片快速展示核心差异化优势，让企业决策者在 10 秒内 get "你们和别人有什么不同"。

## 设计

### 背景
白色 `bg-white`（与米白页面底色微区分，制造层次）

### 区块标题
"为什么选择 SudoClaw？" — `text-3xl md:text-4xl font-bold text-center`

### 卡片网格
- 桌面：`grid grid-cols-3 gap-6`（3×2）
- 平板：`md:grid-cols-2`（2×3）
- 移动：`grid-cols-1`（1×6）

### 每张卡片结构
```html
<div class="bg-page rounded-2xl p-8 hover:-translate-y-1 hover:shadow-md transition-all">
  <div class="w-12 h-12 bg-accent-light rounded-xl flex items-center justify-center text-2xl mb-4">
    <!-- emoji 或 SVG 图标 -->
  </div>
  <h3 class="text-lg font-bold text-dark mb-2">标题</h3>
  <p class="text-sm text-secondary leading-relaxed">描述文字</p>
</div>
```

### 6 张卡片内容

| # | 图标 | 标题 | 描述 |
|---|---|---|---|
| 1 | 🤖 | Copilot + Worker 双引擎 | 不是对话框，是一支 AI 团队帮你从头干到尾。下一个意图，Copilot 拆解任务，Worker 并行执行，结果直接交付。 |
| 2 | 🔗 | 深入业务流 | 直接嵌入 ERP、数据库、审批流，实现高价值业务场景的端到端自动化，而非停留在"你问我答"。 |
| 3 | 📚 | 企业知识 + 专家技能 | 对接私有数据库、知识库和行业专家沉淀的 Skill 包，AI 懂你的业务、用你的数据、按你的规范执行。 |
| 4 | ⚡ | 多模型智能路由 | 内置 SudoRouter，20+ 模型按任务复杂度动态调度。模型降价一键切换，永不锁定供应商。 |
| 5 | 🔒 | 安全是基因，不是功能 | 全私有化部署，数据不出域。AI 沙箱物理隔离、PII 自动脱敏、细粒度访问控制，从第一行代码为企业安全而建。 |
| 6 | 🛡️ | 内置隐私计算 | 安全多方计算 + 联邦学习，跨机构数据协作"可用不可见"。不是第三方集成，是平台原生能力。 |

### 动效
卡片使用 `fade-up` class，通过全局 IntersectionObserver 触发。6 张卡片 stagger 入场（每张延迟 0.1s），通过 `transition-delay` 内联样式实现。

## 产出要求

输出完整的 `<section id="why-sudoclaw">` HTML 代码，含所有 Tailwind 类名和内容文字。
