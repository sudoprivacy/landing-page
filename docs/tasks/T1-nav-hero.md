# T1 — Nav + Hero 区块

> **依赖：** T0（设计规范）
> **产出：** `<header>` + `<section id="hero">` 的完整 HTML（含 Tailwind class + JS）
> **上下文：** 这是用户看到的第一个画面，必须在 3 秒内传达"这不是聊天工具，是企业级 AI 劳动力平台"

---

## 参考风格

- **Palantir：** 深色 Hero，一句话主张 + 产品截图 + 双 CTA
- **Anthropic：** 克制动效，高级留白感

## Nav

### 布局
```
[SudoClaw Logo]    产品  场景  开源  关于我们    [预约演示]
```

### 规格
- 高度 `64px`，固定在顶部 `fixed top-0 w-full z-50`
- 初始状态：背景透明（Hero 是深色的，Nav 文字白色）
- 滚动 > 50px 后：背景 `rgba(250,249,240,0.9)` + `backdrop-blur-md` + 底部 `border-b border-gray-200`，文字变深色
- Logo："SudoClaw" 文字，font-heading weight-900，左侧。"Sudo" 用白色（滚动后深色），"Claw" 用 accent 色
- 导航项：字号 text-sm，font-medium，间距 gap-8。点击后 smooth scroll 到对应 section `#products` `#scenarios` `#opensource` `#about`
- CTA 按钮："预约演示"，amber-600 实心，rounded-lg，px-5 py-2 text-sm
- 移动端（< 768px）：隐藏导航项 + CTA，显示汉堡按钮（三横线），点击展开全屏菜单覆盖层

### JS 行为
1. **滚动变色：** `window.addEventListener('scroll', ...)` 检测 scrollY
2. **汉堡菜单：** toggle class 控制展开/收起
3. **当前 section 高亮：** IntersectionObserver 监测各 section，给对应 nav 项加 `text-accent` 下划线

## Hero

### 布局（桌面）
```
┌──────────────────────────────────────────────────┐
│  (深色背景 #1a1a1a)                               │
│                                                    │
│   9 个岗位 · 8 套系统 · 6 周上线     ┌──────────┐ │
│                                       │  Copilot │ │
│   不是聊天工具，是企业的              │  界面    │ │
│   硅基员工产线。                      │  截图    │ │
│                                       │  占位    │ │
│   [预约演示]  [查看开源代码 →]        └──────────┘ │
│                                                    │
└──────────────────────────────────────────────────┘
```

### 布局（移动端）
标题居中 → 副标题 → 双 CTA 堆叠 → 截图占位区（宽度 100%）

### 规格
- 背景 `bg-dark` (`#1a1a1a`)
- 最小高度 `min-h-[90vh]`，flex 居中
- 主标题：`text-5xl md:text-6xl lg:text-7xl font-black text-white`
  - 数字（9、8、6）用 `font-mono text-accent` 突出
  - 中间分隔符 `·` 用 `text-white/50`
- 副标题：`text-xl md:text-2xl text-white/70 mt-6`
- 双 CTA 区：`mt-10 flex gap-4`
  - 主 CTA："预约演示" — accent 实心按钮，px-8 py-4 text-lg
  - 次 CTA："查看开源代码 →" — 白色描边按钮
- 产品截图占位：`w-full max-w-lg rounded-2xl bg-white/10 border border-white/20 aspect-video flex items-center justify-center`
  - 内部文字 "Copilot 界面截图" text-white/30
  - 后续替换为真实截图 `<img>`

### 入场动效
```js
// 标题：从下淡入，delay 0
// 副标题：从下淡入，delay 0.2s
// CTA：从下淡入，delay 0.4s
// 截图：从右淡入，delay 0.6s
```
用 CSS animation（不依赖 IntersectionObserver，Hero 一加载就播放）：
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
.hero-animate {
  animation: fadeInUp 0.8s ease forwards;
  opacity: 0;
}
```

### 内容（直接使用）

**主标题：** `9 个岗位 · 8 套系统 · 6 周上线`

**副标题：** `不是聊天工具，是企业的硅基员工产线。`

**主 CTA：** `预约演示` → href="#cta"

**次 CTA：** `查看开源代码 →` → href="https://github.com/sudoprivacy/sudowork" target="_blank"

## 产出要求

输出完整的 `<header>` + `<section id="hero">` HTML 代码，包含：
- 所有 Tailwind 类名
- 内联 `<style>` 中的 hero 动画 keyframes
- 内联 `<script>` 中的 Nav 滚动变色 + 汉堡菜单 + section 高亮 JS
- 移动端完全可用
