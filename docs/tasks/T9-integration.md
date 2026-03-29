# T9 — 页面集成 + 全局样式 + 响应式

> **依赖：** T0, T1, T2, T3, T4, T5, T6, T7, T8（全部区块完成后执行）
> **产出：** 完整的 `index.html`，可直接在浏览器打开运行
> **这是最关键的集成任务**

---

## 目标

将 T1-T8 产出的所有 HTML 区块组装为一个完整的单文件 Landing Page，补充全局样式、JS 交互、SEO meta、响应式适配。

## 页面结构（从上到下）

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <!-- T0 的产出：meta + fonts + tailwind + global css -->
</head>
<body class="bg-page font-body text-dark">
  <header>              <!-- T1: Nav -->
  <section id="hero">   <!-- T1: Hero -->
  <section id="architecture">  <!-- T2: Copilot + Worker -->
  <section id="why-sudoclaw">  <!-- T3: 差异化卡片 -->
  <section id="products">      <!-- T4: 产品矩阵 -->
  <section id="scenarios">     <!-- T5: 场景案例 -->
  <section id="production-line"> <!-- T6: 产线 + 信任 -->
  <section id="about">         <!-- T7: 资质背书 -->
  <section id="opensource">    <!-- T8: 开源 -->
  <section id="cta">           <!-- T8: 底部 CTA -->
  <footer>                     <!-- T8: Footer -->

  <!-- 返回顶部按钮 -->
  <!-- 全局 JS -->
</body>
</html>
```

## `<head>` 内容

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SudoClaw — 企业硅基劳动力平台</title>
<meta name="description" content="SudoClaw 是企业级 AI 工作平台，Copilot + Worker 双引擎架构，深入业务流程实现端到端自动化。支持私有化部署，内置隐私计算，20+ 模型智能路由。">
<meta name="keywords" content="SudoClaw,企业AI,智能体,Agent,Copilot,隐私计算,私有化部署,数牍科技,SudoPrivacy">
<meta property="og:title" content="SudoClaw — 企业硅基劳动力平台">
<meta property="og:description" content="不是聊天工具，是企业的硅基员工产线。9 个岗位 · 8 套系统 · 6 周上线。">
<meta property="og:type" content="website">
<meta property="og:url" content="https://sudoprivacy.github.io/sudoclaw-landing/">
<link rel="icon" type="image/svg+xml" href="data:image/svg+xml,..."> <!-- 简单 SVG favicon -->

<!-- Google Fonts -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;500;700;900&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">

<!-- Tailwind CDN + Config (来自 T0) -->
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = { /* T0 的配置 */ }
</script>

<style>
  /* T0 的全局样式 + 各区块的自定义 CSS */
</style>
```

## 全局 JS（页面底部 `<script>`）

需要整合以下功能：

### 1. IntersectionObserver — 滚动淡入
```javascript
// 监测所有 .fade-up 元素，进入视口时加 .visible
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target); // 只触发一次
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
```

### 2. 数字计数器（T7）
```javascript
// 监测 #about 区块，进入视口时启动计数
function animateCounter(el) {
  const target = parseInt(el.dataset.count);
  const suffix = el.dataset.suffix || '';
  const duration = 2000;
  const start = performance.now();

  function update(now) {
    const progress = Math.min((now - start) / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3); // ease-out
    el.textContent = Math.floor(target * eased) + suffix;
    if (progress < 1) requestAnimationFrame(update);
  }
  requestAnimationFrame(update);
}
```

### 3. Nav 滚动行为（T1）
- scrollY > 50：添加毛玻璃背景 + 深色文字
- IntersectionObserver 监测各 section，高亮对应 nav 项

### 4. 场景 Tab 切换（T5）
- Tab 点击切换对应 panel
- 默认选中第一个 tab

### 5. 汉堡菜单（T1）
- 移动端展开/收起

### 6. 返回顶部按钮
```html
<button id="back-to-top"
  class="fixed bottom-8 right-8 w-12 h-12 bg-accent text-white rounded-full shadow-lg
         flex items-center justify-center opacity-0 pointer-events-none transition-opacity z-40"
  onclick="window.scrollTo({top:0})">
  ↑
</button>
```
scrollY > 500 时显示。

## 响应式检查清单

集成完成后逐项确认：
- [ ] 移动端 Nav 汉堡菜单正常展开/收起
- [ ] Hero 文字在 375px 宽度上不溢出
- [ ] Copilot/Worker 双栏在移动端正确堆叠
- [ ] 差异化卡片在移动端单列
- [ ] 产品矩阵在移动端堆叠
- [ ] 场景 Tab 栏在移动端可横向滑动
- [ ] 案例卡片在移动端单列堆叠
- [ ] 时间轴在移动端切换为垂直
- [ ] 数字计数器在小屏上 2 列 or 3+2 排列
- [ ] Footer 四栏在移动端堆叠
- [ ] 返回顶部按钮不遮挡内容
- [ ] 所有 anchor 链接 smooth scroll 正确

## 产出要求

一个完整的 `index.html` 文件（单文件，所有 CSS/JS 内联），可直接用浏览器打开。文件保存到项目根目录。
