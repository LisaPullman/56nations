# Vercel 手动部署指南

> 目标:把 `LisaPullman/56nations` 仓库里的 `site/` 目录部署到 Vercel,获得一个公开的访问 URL。

## 一、准备工作 (5 分钟)

### 1.1 你需要的东西

- ✅ 一个 Vercel 账号 (用 GitHub 登录最快):[vercel.com/signup](https://vercel.com/signup)
- ✅ 代码已经推到了 GitHub:`https://github.com/LisaPullman/56nations` (已包含 `site/` 目录)
- ✅ `site/` 目录里已经有了:
  - `index.html` (主页面)
  - `ethnic-groups.js` (数据)
  - `vercel.json` (Vercel 配置)
  - `README.md` (说明文档)

### 1.2 项目结构

仓库根目录长这样:

```
56nations/
├── .gitignore
├── README.md (在site/目录里)
└── site/
    ├── index.html
    ├── ethnic-groups.js
    ├── vercel.json
    └── README.md
```

⚠️ **重要**:Vercel 部署时需要把 "根目录" 设为 `site/`,这样它只会部署静态页面,不会把根目录的 `.gitignore` 等一起打包。

---

## 二、开始部署 (3 分钟)

### 方式 A: 网页界面 (推荐新手)

#### Step 1: 打开 Vercel 控制台
访问 **[vercel.com/new](https://vercel.com/new)**,用 GitHub 账号登录。

#### Step 2: 导入仓库
- 在 "Import Git Repository" 列表中找到 **`LisaPullman/56nations`**
- 如果看不到,点击 "Adjust GitHub App Permissions" 给 Vercel 授权访问
- 找到仓库后,点右边的 **"Import"** 按钮

#### Step 3: 配置项目
进入项目配置页,按下面填写:

| 字段 | 填写 |
|------|------|
| **Project Name** | `56nations` (也可以改成 `lisa-56nations`、`ethnic-atlas` 等,会作为子域名) |
| **Framework Preset** | 选择 **`Other`** (不是 Next.js,不是 Vite) |
| **Root Directory** | 点 "Edit" 按钮,改成 **`site`** ⚠️ 这一步很关键 |
| **Build and Output Settings** | 保持默认 (Output Directory 留空) |

#### Step 4: 点击 Deploy
- 点击页面底部蓝色 **"Deploy"** 按钮
- 等待 30-60 秒,会看到 "Building..." 动画
- 完成后会显示 "🎉 Congratulations!" 和一个预览 URL

#### Step 5: 拿到 URL
- Vercel 会自动分配一个 URL,格式:`https://56nations-xxx.vercel.app`
- 你也可以在 Project Settings → Domains 里绑定自己的域名

---

### 方式 B: Vercel CLI (推荐有经验的用户)

#### Step 1: 安装 CLI
```bash
npm install -g vercel
```

#### Step 2: 登录
```bash
vercel login
```
按提示在浏览器里授权。

#### Step 3: 进入项目目录
```bash
cd /Users/foxai/Desktop/56/site
```

#### Step 4: 部署
```bash
vercel --prod
```

第一次会问几个问题:
- `Set up and deploy?` → **Y**
- `Which scope?` → 选你的账号
- `Link to existing project?` → **N** (新建)
- `What's your project's name?` → `56nations`
- `In which directory is your code located?` → `./` (已经在 site/ 目录里了)

部署完成后会输出:
```
✅ Production: https://56nations-xxx.vercel.app [copied to clipboard]
```

---

## 三、部署后验证 (2 分钟)

打开你的 Vercel URL,检查这些都正常:

- [ ] 页面顶部有 `foxai` logo + "五十六族" 标题
- [ ] 56 张民族卡片全部显示
- [ ] 点开任意一张卡片,弹出详情
- [ ] 搜索 "苗族" 能过滤出苗族卡片
- [ ] 切换到 "游戏模式" 看到 4 个游戏入口
- [ ] 进入 "记忆翻翻乐" 能翻牌
- [ ] 移动设备访问 (手机扫码),布局正常
- [ ] 暗色模式 (系统设置深色) 颜色适配

---

## 四、常见问题 FAQ

### Q1: 部署后页面空白 / 加载不出来
**原因**:根目录没设为 `site`,Vercel 找不到 `index.html`。
**解决**:
1. 打开 Vercel Dashboard → Project → Settings → General
2. 找到 "Root Directory" → Edit → 改成 `site`
3. Deployments → 找到最新部署 → 点 "..." → Redeploy

### Q2: 民族卡片不显示,只剩标题
**原因**:`ethnic-groups.js` 没被加载 (路径错误)。
**检查**:
- 浏览器按 F12 → Console 标签
- 看到类似 `Failed to load resource: 404` 的报错
- 解决:确认 `site/index.html` 里 `<script src="./ethnic-groups.js">` 路径是相对路径,且 `ethnic-groups.js` 在 `site/` 目录下

### Q3: 部署到一半失败
**原因**:`vercel.json` 里的某个配置不识别。
**解决**:
- 暂时把 `site/vercel.json` 改名成 `vercel.json.bak`,再 Redeploy
- 部署成功后改回来

### Q4: 想换域名
**步骤**:
1. 去你的域名服务商 (阿里云 / Cloudflare / Namecheap 等) 把 DNS 改成 Vercel 提供的 CNAME
2. 在 Vercel Project → Settings → Domains 添加 `yourdomain.com`
3. 等待 DNS 生效 (几分钟到 24 小时)

### Q5: 怎么改完代码重新部署?
1. 在本地改文件
2. `git add .` → `git commit -m "..."` → `git push`
3. Vercel 会自动检测 GitHub 仓库变更,30 秒后自动部署完成
4. 也可以手动:打开 Vercel Dashboard → Deployments → Redeploy

### Q6: 部署是免费的吗?
是的。Vercel 的 Hobby (免费) 计划包含:
- ✅ 无限次部署
- ✅ 100 GB 带宽 / 月
- ✅ 自动 HTTPS
- ✅ 全球 CDN
- 静态网站完全够用。

### Q7: 想加个自己的后端 API?
Vercel 不适合在静态 site 加后端。如需 API,可考虑:
- 改用 Cloudflare Pages (同样支持静态 + Workers)
- 把数据迁移到 Supabase / Firebase

---

## 五、部署后的目录速查

部署成功后,你的 Vercel 项目大致长这样:

```
Project: 56nations
├── Production URL:  https://56nations.vercel.app
├── Git:             https://github.com/LisaPullman/56nations
├── Root Directory:  site/
├── Framework:       Other
└── Build:           (no build step, serves static files)
```

Dashboard: [vercel.com/dashboard](https://vercel.com/dashboard)

---

## 六、下一步建议

部署成功之后可以:

1. **分享给朋友** — 把 Vercel URL 发到群里,让他们试用
2. **二维码** — 用 [qr-code-generator.com](https://www.qr-code-generator.com/) 把 URL 转成二维码,方便手机扫码
3. **性能监控** — 在 Vercel Project → Analytics 开启 Web Analytics (免费)
4. **自定义 404** — 创建 `site/404.html`,处理访问不存在页面
5. **SEO 优化** — 在 `index.html` 已有 `<meta name="description">`,可以再加 Open Graph 标签方便分享

---

## 七、命令速查

```bash
# 本地预览
cd /Users/foxai/Desktop/56/site
python3 -m http.server 8080
# 打开 http://127.0.0.1:8080

# 改完代码后
cd /Users/foxai/Desktop/56
git add .
git commit -m "描述你改了什么"
git push

# Vercel CLI 部署
cd /Users/foxai/Desktop/56/site
vercel --prod

# 重新部署
vercel --prod --force
```

---

有部署相关问题随时问我!🚀
