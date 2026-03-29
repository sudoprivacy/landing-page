# T11 — GitHub Pages 部署

> **依赖：** T9（完整 index.html）、T10（法律页面）
> **产出：** 一个可通过 `https://<org>.github.io/<repo>/` 访问的线上网站
> **优先级：** P0（端到端完成的最后一步）

---

## 目标

将 T9 产出的 `index.html` 和 T10 产出的 `terms.html` / `privacy.html` 部署到 GitHub Pages，使网站可公开访问。

## 方案

使用 GitHub Pages 的 **Static HTML** 部署方式（不需要 Jekyll），从 `main` 分支的根目录或 `/docs` 目录部署。

## 执行步骤

### Step 1：准备仓库

确认或创建 GitHub 仓库。建议选项之一：

**选项 A：使用现有仓库**
如果 `sudoprivacy/sudowork` 已存在，可以在该仓库中创建 `docs/` 目录放置静态文件。

**选项 B：创建专用仓库**
```bash
# 创建新仓库（公开）
gh repo create sudoprivacy/sudoclaw-landing --public --description "SudoClaw Landing Page" --confirm

# 克隆到本地
git clone https://github.com/sudoprivacy/sudoclaw-landing.git
cd sudoclaw-landing
```

### Step 2：组织文件结构

```
sudoclaw-landing/
├── index.html          ← T9 产出的完整页面
├── terms.html          ← T10 服务条款
├── privacy.html        ← T10 隐私政策
├── .nojekyll           ← 告诉 GitHub 不用 Jekyll 处理
├── CNAME               ← 自定义域名（可选，如 sudoclaw.com）
├── assets/             ← 静态资源目录
│   ├── images/
│   │   ├── logo.svg          ← Logo（待提供）
│   │   ├── hero-screenshot.png  ← Copilot 截图（待提供）
│   │   ├── wechat-qr.png       ← 微信二维码（待提供）
│   │   └── og-image.png        ← Open Graph 分享图
│   └── favicon.svg
└── README.md           ← 仓库说明
```

### Step 3：创建 .nojekyll

```bash
touch .nojekyll
```

这个空文件告诉 GitHub Pages 不要用 Jekyll 处理，直接 serve 静态文件。

### Step 4：提交并推送

```bash
git add .
git commit -m "feat: SudoClaw landing page v1.0"
git push origin main
```

### Step 5：启用 GitHub Pages

```bash
# 使用 GitHub CLI 启用 Pages
gh api repos/sudoprivacy/sudoclaw-landing/pages \
  --method POST \
  --field source='{"branch":"main","path":"/"}' \
  --field build_type="legacy"
```

或者手动操作：
1. 进入仓库 Settings → Pages
2. Source 选择 `main` 分支，目录选 `/ (root)`
3. 点击 Save

### Step 6：验证部署

```bash
# 等待部署完成（通常 1-3 分钟）
# 检查部署状态
gh api repos/sudoprivacy/sudoclaw-landing/pages

# 访问网站
open https://sudoprivacy.github.io/sudoclaw-landing/
```

### Step 7：（可选）配置自定义域名

如果要用自定义域名（如 `www.sudoclaw.com`）：

1. 创建 CNAME 文件：
```bash
echo "www.sudoclaw.com" > CNAME
git add CNAME && git commit -m "add custom domain" && git push
```

2. 在域名注册商配置 DNS：
   - 添加 CNAME 记录：`www` → `sudoprivacy.github.io`
   - 或 A 记录指向 GitHub Pages IP

3. 在 GitHub Pages 设置中启用 HTTPS

## 验收清单

- [ ] `https://sudoprivacy.github.io/sudoclaw-landing/` 可正常访问
- [ ] 页面加载时间 < 3s（纯静态 HTML，应该很快）
- [ ] 移动端访问正常（用手机浏览器测试）
- [ ] `terms.html` 和 `privacy.html` 链接正常
- [ ] Open Graph 标签正确（在 https://www.opengraph.xyz/ 测试）
- [ ] Footer 的 ICP 备案链接可点击跳转到工信部网站
- [ ] 微信分享预览正常（标题 + 描述 + 图片）

## 后续优化（非本次范围）

- CDN 加速（如接入 Cloudflare）
- Google Analytics / 百度统计
- 表单后端（预约演示的实际提交处理）
- 图片压缩 + WebP 格式
- 自定义域名 + SSL
- 百度收录提交

## 产出要求

执行上述步骤，最终提供可访问的线上 URL。如果没有仓库写入权限，则输出完整的文件目录结构和所有文件内容，以及部署指令，供手动执行。
