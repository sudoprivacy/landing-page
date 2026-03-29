# T4 — 产品矩阵区块

> **依赖：** T0（设计规范）
> **产出：** `<section id="products">` 完整 HTML
> **内容来源：** `SudoClaw-宣传资料.md` 第 70-85 行

---

## 目标

展示 SudoClaw / Nexus OS / SudoRouter 三大产品的定位、特性和关系，让技术决策者理解整体架构。

## 设计

### 背景
米白 `bg-page`

### 区块标题
"产品矩阵" — `text-3xl md:text-4xl font-bold text-center`
副标题："SudoClaw 不是单点工具，而是由三大核心组件构成的完整 AI 工作平台" — `text-secondary text-center mt-4`

### 三栏布局
- 桌面：`grid grid-cols-3 gap-8`
- 平板/移动：`grid-cols-1`（堆叠）

### 每个产品卡片
```html
<div class="bg-white rounded-2xl p-8 shadow-sm hover:shadow-md hover:-translate-y-1 transition-all flex flex-col">
  <div class="text-4xl mb-4">图标</div>
  <h3 class="text-xl font-bold mb-1">产品名</h3>
  <p class="text-accent text-sm font-medium mb-4">一句话定位</p>
  <ul class="space-y-2 text-sm text-secondary flex-1">
    <li class="flex items-start gap-2">
      <span class="text-teal mt-0.5">●</span>
      <span>特性描述</span>
    </li>
    <!-- 更多特性 -->
  </ul>
  <a href="#" class="text-teal hover:text-teal-hover font-medium text-sm mt-6 inline-flex items-center gap-1">
    了解更多 →
  </a>
</div>
```

### 三个产品内容

**🖥️ SudoClaw — 终端客户端**
定位：用户与 AI 职场搭子交互的入口
特性：
- 企业微信、Web、Telegram、钉钉、飞书多端接入
- 对话、任务下发、进度追踪、结果查看完整工作流
- 跨平台支持 macOS、Windows、Linux
链接：github.com/sudoprivacy/sudowork

**🧠 Nexus OS — 智能体操作系统**
定位：承载所有 AI 员工的底层操作系统
特性：
- Plugin/Extension + Skill + Agent 三层架构
- 内置隐私计算引擎（安全多方计算、联邦学习）
- 不可变版本控制、语义搜索、多租户隔离
- 开源 Apache 2.0，兼容 Claude Agent SDK、OpenAI Agents 等主流框架
链接：github.com/nexi-lab/nexus

**⚡ SudoRouter — 多模型智能路由**
定位：按任务复杂度动态选择最优模型
特性：
- 支持 20+ 模型供应商（Claude、GPT、Gemini、Qwen、Kimi、GLM 等）
- 三层任务分级：轻量级、主力级、专家级
- 不绑定单一供应商，模型降价一键切换
链接：sudorouter.ai

### 动效
三张卡片 `fade-up`，stagger 0.15s。

## 产出要求

输出完整的 `<section id="products">` HTML 代码，含所有内容和 Tailwind 类名。
