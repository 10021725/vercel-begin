# 部署到 Vercel — 详细操作计划

> 本项目是一个纯静态单页网站，将通过 Vercel 平台完成部署。下方列出了**所有需要你手动参与**的关键步骤。

---

## 第一阶段：准备工作（你来操作）

### 步骤 1：注册 / 登录 Vercel 账号

**目的**：获得 Vercel 控制台访问权限

**操作**：
1. 访问 [https://vercel.com](https://vercel.com)
2. 点击 **Sign Up**，使用以下方式之一注册：
   - **GitHub 账号授权**（推荐，一站式体验）
   - GitLab / Bitbucket
   - 邮箱注册
3. 完成验证后进入控制台

> **⚠️ 重要**：建议直接使用 **GitHub 授权登录**，因为后续步骤与 GitHub 深度集成会更顺畅。

---

### 步骤 2：创建 GitHub 仓库

**目的**：将项目代码托管到 GitHub，Vercel 会从这个仓库拉取代码进行部署

**操作**（两种方式任选其一）：

#### 方式 A：网页端创建（适合不熟悉 Git 命令的同学）
1. 访问 [https://github.com/new](https://github.com/new)
2. Repository name 填 `my-vercel-site`（或其他你喜欢的名字）
3. 选择 **Public**（公开仓库，免费版需要）
4. 点击 **Create repository**
5. 页面会显示空仓库，此时**先跳过**，我们稍后把代码推送上去

#### 方式 B：GitHub CLI 命令（适合习惯命令行的同学）
```bash
# 安装 gh（如果没有）
# Windows: 下载 https://github.com/cli/cli/releases

# 登录
gh auth login

# 创建仓库
gh repo create my-vercel-site --public --clone=false
```

---

### 步骤 3：安装 Git（如果还没有）

**目的**：将本地代码推送到 GitHub

**检查是否已安装**：
```bash
git --version
```

如果没有安装，下载安装：[https://git-scm.com/download/win](https://git-scm.com/download/win)

---

## 第二阶段：推送代码（你来操作）

### 步骤 4：初始化 Git 并推送代码

在项目根目录下执行以下命令（Windows 推荐用 PowerShell 或 Git Bash）：

```bash
# 1. 进入项目目录
cd C:\Users\xiatian\WorkBuddy\2026-05-19-task-8

# 2. 初始化 Git 仓库（如果尚未初始化）
git init

# 3. 添加所有文件
git add index.html

# 4. 提交
git commit -m "feat: initial project"

# 5. 添加远程仓库（把下面的 YOUR_USERNAME 换成你的 GitHub 用户名）
git remote add origin https://github.com/YOUR_USERNAME/my-vercel-site.git

# 6. 推送到 GitHub
git branch -M main
git push -u origin main
```

> **⚠️ 注意**：`YOUR_USERNAME` 和仓库名需要替换为你实际创建的值。

---

## 第三阶段：连接 Vercel（你来操作）

### 步骤 5：在 Vercel 上导入项目

**目的**：让 Vercel 读取 GitHub 仓库并开始部署

**操作**：
1. 登录 [https://vercel.com](https://vercel.com) 控制台
2. 点击右上角 **Add New...** → **Project**
3. Vercel 会列出你的 GitHub 仓库，找到 `my-vercel-site`
4. 点击 **Import** 导入

### 步骤 6：配置构建选项

**目的**：告诉 Vercel 这是一个静态网站

此时 Vercel 会自动检测框架，由于我们是纯 HTML，配置如下：

| 配置项 | 值 | 说明 |
|---|---|---|
| **Framework Preset** | `Other` | 纯静态网站，选 Other |
| **Root Directory** | `./`（默认） | 项目根目录 |
| **Build Command** | （留空） | 静态网站无需构建 |
| **Output Directory** | `./`（默认） | 直接托管根目录 |
| **Environment Variables** | （无需设置） | 本项目不需要 |

确认无误后，点击 **Deploy**。

### 步骤 7：等待部署完成

- Vercel 会显示部署进度（通常 30 秒～1 分钟）
- 完成后会生成一个 `.vercel.app` 子域名的在线链接
- 点击链接即可查看网站！

---

## 第四阶段：自定义域名（可选）

### 步骤 8：绑定你自己的域名（可选）

**目的**：用你自己的域名（如 `yoursite.com`）替代 Vercel 分配的免费子域名

**操作**：
1. 在 Vercel 项目控制台点击 **Settings** → **Domains**
2. 输入你的域名，点击 **Add**
3. 按提示在域名服务商处添加 DNS 记录（Vercel 会给出具体配置）
4. 等待 DNS 生效（约几分钟到48小时）

---

## 后续：感受 Vercel 的核心优势

部署完成后，你可以体验以下功能：

| 功能 | 操作入口 | 说明 |
|---|---|---|
| **自动部署** | 修改代码 → `git push` | Vercel 自动检测到代码变更并重新部署 |
| **预览部署** | 创建 Pull Request | 自动生成预览链接供团队查看 |
| **Analytics** | 项目控制台 → Analytics | 查看访问量、性能数据（需开启） |
| **Speed Insights** | 同上 | 查看 Core Web Vitals 等性能指标 |

---

## 流程图

```
┌─────────────────────────────────────────────────────────┐
│  你的工作（手动）                                         │
│                                                         │
│  ① 注册 Vercel 账号（GitHub 授权登录）                   │
│  ② 创建 GitHub 仓库                                      │
│  ③ 本地 Git init + push 代码到 GitHub                    │
│  ④ Vercel 导入仓库 → 点击 Deploy                         │
│  ⑤ 获得 .vercel.app 在线链接 ✅                          │
│                                                         │
│  ─────────────────────────────────────────────────────  │
│  Vercel 自动完成的工作                                    │
│  ⑥ 从 GitHub 拉取代码 → 构建 → 部署到全球边缘节点          │
│  ⑦ 配置 SSL 证书 / CDN / 域名解析                        │
└─────────────────────────────────────────────────────────┘
```

---

## 常见问题

**Q: 需要信用卡吗？**
> 免费版（Hobby）无需信用卡，零成本体验。

**Q: 部署失败了怎么办？**
> Vercel 控制台会显示构建日志，可以查看具体报错信息。如果遇到问题，把错误信息复制给我，我来帮你排查。

**Q: 想删除项目怎么办？**
> Vercel 控制台 → 项目 Settings → 底部有 Delete 按钮。

---

## 下一步

准备好后，直接告诉我你进行到哪一步，遇到任何问题都可以问！
