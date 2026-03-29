# T2 — Copilot + Worker 架构说明区块

> **依赖：** T0（设计规范）
> **产出：** `<section id="architecture">` 完整 HTML
> **内容来源：** `SudoClaw-宣传资料.md` 第 19-35 行

---

## 目标

紧跟 Hero 下方，解释 SudoClaw 的核心架构差异——Copilot + Worker 双引擎。这是全站最重要的产品理解区块，让访客明白"你们跟 ChatGPT 类工具有什么本质不同"。

## 设计

### 背景
页面默认米白 `bg-page` (`#FAF9F0`)

### 区块标题
"核心架构：Copilot + Worker 双引擎" — `text-3xl md:text-4xl font-bold text-center`

### 双栏卡片（桌面并排，移动堆叠）

**左栏 — Copilot 卡片：**
```
┌─────────────────────────┐
│  🧠  (图标或占位 SVG)    │
│                          │
│  Copilot                 │
│  您的数字合伙人           │
│                          │
│  管理者唯一需要交互的     │
│  界面。理解战略意图，     │
│  将模糊指令转化为精准     │
│  的执行任务。不需要写     │
│  prompt，不需要懂技术。   │
└─────────────────────────┘
```

**右栏 — Worker 卡片：**
```
┌─────────────────────────┐
│  ⚙️  (图标或占位 SVG)    │
│                          │
│  Worker                  │
│  您的数字专员团队         │
│                          │
│  多个专业 Worker 各司     │
│  其职——代码编写、数据     │
│  处理、文档生成、ERP     │
│  对接，自动协同完成       │
│  完整闭环。               │
└─────────────────────────┘
```

卡片样式：`bg-white rounded-2xl p-8 shadow-sm hover:shadow-md transition`

### 对比流程（卡片下方）

用两行水平流程展示差异，箭头连接：

**传统 AI 工具：**
`人提问` → `AI 回答` → `人再操作` （灰色调，表示低效）

**SudoClaw：**
`人下达意图` → `Copilot 理解拆解` → `Worker 并行执行` → `结果直接交付` （accent 色调，表示高效）

实现方式：flex 横排，每个步骤是 pill 形状 `rounded-full px-4 py-2`，箭头用 `→` 字符或 SVG。移动端可换行。

### 真实案例引用

底部用引用样式（左侧 4px accent 色边条）：

> 售前顾问对 Copilot 说"帮我准备下周给客户的方案"。Copilot 将意图拆解为四个任务：行业数据采集、客户痛点提炼、方案架构设计、ROI 测算。四个 Worker 并行执行，当天交付一个带导航、带数据、带架构图的完整定制演示网页——不是 PPT，是一个可交互的网站。

### 动效
滚动进入视口时：
- 区块标题淡入
- 左卡片从左淡入，delay 0.15s
- 右卡片从右淡入，delay 0.3s
- 流程和引用从下淡入，delay 0.45s

用 `fade-up` class + IntersectionObserver（T0 定义的全局机制）

## 产出要求

输出完整的 `<section id="architecture">` HTML 代码，含所有 Tailwind 类名。不需要包含 JS（使用全局 IntersectionObserver）。
