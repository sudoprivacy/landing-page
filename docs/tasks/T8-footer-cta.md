# T8 — 开源 + CTA + Footer

> **依赖：** T0（设计规范）
> **产出：** `<section id="opensource">` + `<section id="cta">` + `<footer>` 完整 HTML
> **内容来源：** `SudoClaw-宣传资料.md` 第 246-268 行 + sudoprivacy.com 法律信息

---

## 目标

页面收尾三连：开源展示（建立透明信任）→ 转化 CTA（推动预约）→ Footer（完整合规信息）。

---

## 第一块：开源区块

### 背景
米白 `bg-page`

### 区块标题
"开源透明，开箱即用" — `text-3xl md:text-4xl font-bold text-center`
副标题："核心组件全部开源，代码可审计、架构可验证。不需要签合同才能评估——先用起来，再谈合作。" — `text-secondary text-center mt-4 max-w-2xl mx-auto`

### 三个 GitHub 卡片
桌面 `grid grid-cols-3 gap-6`，移动堆叠。

每张卡片：
```html
<div class="bg-white rounded-2xl p-6 text-center shadow-sm hover:shadow-md transition">
  <div class="text-3xl mb-3">图标</div>
  <h3 class="text-lg font-bold mb-1">产品名</h3>
  <p class="text-sm text-secondary mb-4">一句话描述</p>
  <a href="URL" target="_blank"
     class="inline-block border-2 border-teal text-teal hover:bg-teal hover:text-white font-medium px-6 py-2 rounded-lg transition-colors text-sm">
    GitHub →
  </a>
</div>
```

| 图标 | 产品 | 描述 | 链接 |
|---|---|---|---|
| 🖥️ | SudoClaw | 企业级 AI 工作客户端 | https://github.com/sudoprivacy/sudowork |
| 🧠 | Nexus OS | 智能体操作系统 | https://github.com/nexi-lab/nexus |
| ⚡ | SudoRouter | 多模型智能路由 | https://sudorouter.ai |

---

## 第二块：底部 CTA

### 背景
深色 `bg-dark` (`#1a1a1a`)

### 布局
全宽深色区块，内容居中，`py-24 text-center`

### 内容
- **大标题：** "让 AI 从聊天工具，进化为企业的数字劳动力" — `text-3xl md:text-4xl font-bold text-white`
- **副文：** "我们的团队通常在一周内完成从需求对接到 POC 环境搭建。" — `text-white/70 mt-4`
- **主 CTA：** "预约演示" — amber-600 大号按钮 `px-10 py-4 text-lg rounded-lg mt-8`
- **次 CTA：** "或发送邮件至 business@sudoprivacy.com" — `text-white/50 text-sm mt-4`，邮箱用 `<a href="mailto:...">` 包裹，hover 变 accent 色

---

## 第三块：Footer

### 背景
`bg-[#111111]`

### 四栏布局（桌面），移动端堆叠

```html
<footer class="bg-[#111111] text-white/60 py-16">
  <div class="max-w-content mx-auto px-6 md:px-8">
    <div class="grid md:grid-cols-4 gap-12">
      <!-- 四栏 -->
    </div>
    <!-- 底部信息栏 -->
  </div>
</footer>
```

#### 栏 1：产品
- SudoClaw → #hero
- Nexus OS → https://github.com/nexi-lab/nexus
- SudoRouter → https://sudorouter.ai

#### 栏 2：场景
- 销售与获客 → #scenarios
- 客户服务 → #scenarios
- 金融与保险 → #scenarios
- 财务与合规 → #scenarios
- 更多场景… → #scenarios

#### 栏 3：资源
- GitHub → https://github.com/sudoprivacy
- 文档 → #（占位）
- API 参考 → #（占位）
- 博客 → #（占位）

#### 栏 4：公司
- 关于我们 → #about
- 联系我们 → mailto:business@sudoprivacy.com
- 加入我们 → #（占位）
- 法律声明 → terms.html
- 隐私政策 → privacy.html

每栏：
```html
<div>
  <h4 class="text-white font-bold text-sm mb-4">栏目名</h4>
  <ul class="space-y-2">
    <li><a href="#" class="text-sm hover:text-white transition-colors">链接</a></li>
  </ul>
</div>
```

### 底部信息栏

`border-t border-white/10 mt-12 pt-8`，三栏布局（flex justify-between）：

**左：** © 2019-2026 数牍科技 sudoprivacy.com

**中：**
- [京ICP备20011614号](https://beian.miit.gov.cn/) — `text-xs`
- [京公网安备 11010802035764号](https://www.beian.gov.cn/portal/registerSystemInfo?recordcode=11010802035764) — `text-xs`

**右：** 微信公众号二维码占位
```html
<div class="flex items-center gap-3">
  <div class="w-12 h-12 bg-white/10 rounded flex items-center justify-center text-xs text-white/30">
    二维码
  </div>
  <span class="text-xs">扫码关注公众号</span>
</div>
```

**最底部（可选）：** 地址一行
"北京市海淀区成府路28号优盛大厦A座18层" — `text-xs text-white/30 text-center mt-6`

## 产出要求

输出三个完整 section 的 HTML 代码：`<section id="opensource">` + `<section id="cta">` + `<footer>`。含所有 Tailwind 类名、链接和内容。
