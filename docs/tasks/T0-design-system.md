# T0 — 设计规范 & Tailwind Config

> **依赖：** 无
> **产出：** 一段可嵌入 `<head>` 的 `<style>` + Tailwind config 代码
> **上游消费者：** T1-T10 所有任务

---

## 目标

定义整个 Landing Page 的视觉规范，输出可直接复制粘贴的 CSS variables、Tailwind CDN 配置、字体引入，供所有后续区块任务使用。

## 设计基调

**Palantir 的信息架构 + Anthropic 的视觉质感。** 暖色系、大量留白、克制动效。不走蓝紫渐变 + 3D 球体的国内 AI 网站老路。

## 色板

| Token | 色值 | 用途 |
|---|---|---|
| `--bg-page` | `#FAF9F0` | 页面底色（Anthropic 式暖米白） |
| `--bg-card` | `#FFFFFF` | 卡片/区块背景 |
| `--bg-dark` | `#1a1a1a` | Hero、CTA 等深色强调区块 |
| `--bg-footer` | `#111111` | Footer 背景 |
| `--text-primary` | `#1a1a1a` | 主文字 |
| `--text-secondary` | `#6b7280` | 次要文字（gray-500） |
| `--text-on-dark` | `#FFFFFF` | 深色背景上的文字 |
| `--text-on-dark-muted` | `rgba(255,255,255,0.7)` | 深色背景上的次要文字 |
| `--accent` | `#F59E0B` | 品牌强调（amber-500，与 Logo 一致），CTA、重点标注 |
| `--accent-hover` | `#D97706` | 品牌强调 hover（amber-600） |
| `--accent-light` | `#FEF3C7` | 品牌强调浅色背景（amber-100） |
| `--teal` | `#0D9488` | 辅助强调（teal-600），产品/技术链接 |
| `--teal-hover` | `#0F766E` | 辅助 hover（teal-700） |
| `--border` | `#E5E7EB` | 边框/分割线（gray-200） |

## 字体

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;500;700;900&family=JetBrains+Mono:wght@400;500;700&display=swap');

:root {
  --font-heading: "Noto Sans SC", "PingFang SC", "Microsoft YaHei", sans-serif;
  --font-body: "Noto Sans SC", "PingFang SC", "Microsoft YaHei", sans-serif;
  --font-mono: "JetBrains Mono", "Fira Code", monospace;
}
```

- **标题（H1-H3）：** `--font-heading`，weight 700/900
- **正文：** `--font-body`，weight 400/500
- **数字/代码：** `--font-mono`，用于 Hero 数字、计数器、技术文本

## 间距 & 尺寸

| Token | 值 | 说明 |
|---|---|---|
| 最大内容宽度 | `1200px` | `max-w-[1200px] mx-auto` |
| 区块垂直间距 | `py-24`（桌面）`py-16`（移动） | section 间距 |
| 内容水平 padding | `px-6`（移动）`px-8`（桌面） | 防止贴边 |
| 卡片圆角 | `rounded-2xl` | 16px |
| 卡片阴影 | `shadow-sm` → hover `shadow-md` | 微交互 |
| 按钮圆角 | `rounded-lg` | 8px |
| 导航高度 | `64px` / `h-16` | 固定 |

## 响应式断点

| 名称 | 宽度 | 典型布局 |
|---|---|---|
| 移动 | < 768px | 单列，汉堡菜单 |
| 平板 | 768px - 1024px | 双列 |
| 桌面 | > 1024px | 多列（2-3） |

## 全局动效

```css
/* 滚动淡入 */
.fade-up {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}

/* 平滑滚动 */
html {
  scroll-behavior: smooth;
}

/* 减少动画偏好 */
@media (prefers-reduced-motion: reduce) {
  .fade-up { transition: none; opacity: 1; transform: none; }
  html { scroll-behavior: auto; }
}
```

## Tailwind CDN 配置

```html
<script src="https://cdn.tailwindcss.com"></script>
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          page: '#FAF9F0',
          dark: '#1a1a1a',
          'dark-footer': '#111111',
          accent: '#F59E0B',
          'accent-hover': '#D97706',
          'accent-light': '#FEF3C7',
          teal: '#0D9488',
          'teal-hover': '#0F766E',
        },
        fontFamily: {
          heading: ['"Noto Sans SC"', '"PingFang SC"', '"Microsoft YaHei"', 'sans-serif'],
          body: ['"Noto Sans SC"', '"PingFang SC"', '"Microsoft YaHei"', 'sans-serif'],
          mono: ['"JetBrains Mono"', '"Fira Code"', 'monospace'],
        },
        maxWidth: {
          'content': '1200px',
        }
      }
    }
  }
</script>
```

## 按钮规范

**主 CTA（实心）：**
```html
<a href="#" class="inline-block bg-accent hover:bg-accent-hover text-white font-medium px-8 py-3 rounded-lg transition-colors">
  预约演示
</a>
```

**次 CTA（描边）：**
```html
<a href="#" class="inline-block border-2 border-white text-white hover:bg-white hover:text-dark font-medium px-8 py-3 rounded-lg transition-colors">
  查看开源代码 →
</a>
```

**链接 CTA（文字）：**
```html
<a href="#" class="text-teal hover:text-teal-hover font-medium transition-colors">
  了解更多 →
</a>
```

## 卡片规范

```html
<div class="bg-white rounded-2xl p-8 shadow-sm hover:shadow-md transition-shadow">
  <!-- 内容 -->
</div>
```

## 产出要求

输出一个完整的 `<head>` 内代码片段，包含：
1. Meta charset + viewport
2. Google Fonts 引入
3. Tailwind CDN + config
4. `<style>` 标签内的 CSS variables + 全局样式 + 动效 keyframes
5. SEO meta tags

这段代码将被 T9 集成任务直接使用。
