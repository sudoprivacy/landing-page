# T7 — 资质背书区块

> **依赖：** T0（设计规范）
> **产出：** `<section id="about">` 完整 HTML
> **内容来源：** `SudoClaw-宣传资料.md` 第 258-264 行

---

## 目标

用硬数据和权威认证建立信任。参考国内企业网站常见的"数字墙 + 荣誉标签"模式，但用更克制、更 Anthropic 风格的设计。

## 设计

### 背景
米白 `bg-page`

### 区块标题
"关于我们" — `text-3xl md:text-4xl font-bold text-center`
副标题："数牍科技——从隐私计算到企业 AI 劳动力平台" — `text-secondary text-center mt-4`

---

### 公司介绍段落

居中，最大宽度 `max-w-3xl mx-auto`，`text-secondary leading-relaxed`：

"数牍科技（SudoPrivacy）是国内最早一批将隐私计算技术落地商用的企业，国家级专精特新"小巨人"。核心团队来自 Google DeepMind、Meta、Microsoft、Amazon、清华大学、UCLA、剑桥大学等机构，在数据安全、AI 基础设施和企业级系统架构领域深耕多年。"

---

### 数字计数器

5 个关键数字横向排列：
- 桌面：`grid grid-cols-5 gap-8`
- 平板：`grid-cols-3`
- 移动：`grid-cols-2`（最后一个居中）

每个数字：
```html
<div class="text-center">
  <div class="text-4xl md:text-5xl font-mono font-bold text-dark" data-count="3" data-suffix="亿+">
    0
  </div>
  <div class="text-sm text-secondary mt-2">A 轮融资</div>
</div>
```

| 数字 | 后缀 | 标签 |
|---|---|---|
| 3 | 亿+ | A 轮融资 |
| 107 | + | 参与标准建设 |
| 100 | + | 知识产权 |
| 60 | + | 权威测评认证 |
| 40 | + | 行业荣誉 |

**计数器 JS 逻辑：**
- IntersectionObserver 监测此区块
- 进入视口后，每个数字从 0 动画滚动到目标值
- 持续时间 2s，easing `ease-out`
- 用 `requestAnimationFrame` 实现平滑计数
- 只触发一次

---

### 荣誉标签

水平排列，`flex flex-wrap justify-center gap-3 mt-12`：

每个标签：
```html
<span class="inline-block px-4 py-2 bg-accent-light text-accent text-sm font-medium rounded-full">
  标签文字
</span>
```

标签内容（8 个）：
1. 国家级专精特新"小巨人"
2. IDC 中国 FinTech 50（连续三年）
3. 金融密码杯三项一等奖（首家）
4. 信通院双项测评
5. 多地数据交易所首批数商
6. 红杉中国投资
7. 招商局创投投资
8. 纪源资本投资

---

### 标准贡献

居中一行文字，`text-sm text-secondary mt-8`：
"主导或参与制定 7 项国际标准、7 项国家标准、6 项行业标准，拥有 100+ 项知识产权含 30+ 项美国专利"

---

### 动效
- 数字计数器：IntersectionObserver 触发滚动计数（2s ease-out）
- 荣誉标签：`fade-up` stagger 入场

## 产出要求

输出完整的 `<section id="about">` HTML 代码，含：
1. 所有 Tailwind 类名和内容文字
2. 计数器动画 JS（内联 `<script>`）
3. 响应式布局
