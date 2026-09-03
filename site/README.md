# 五十六个民族图鉴 · 56 Ethnic Atlas

一份以东方纸本质感 + 现代编辑美学设计的中国 56 民族图鉴。融合图文、服饰特征与文化脉络,致敬中华大地的多元与共美。

![Ember Brand](https://img.shields.io/badge/brand-Ember-E2571F?style=flat-square)
![Made with](https://img.shields.io/badge/made_with-pure_HTML%2BCSS%2BJS-1A1714?style=flat-square)

## ✨ 功能

- **学习模式**:56 个民族卡片网格,按地域筛选、关键词搜索;点开任意一张卡片查看服饰照片、服饰特征、文化概览与关键词。
- **语音朗读**:卡片详情内可朗读民族名字、介绍与趣味小知识(Web Speech API,儿童友好语速)。
- **学习进度**:在详情里点「我认识它啦」打卡,进度条实时统计,集齐 56 个有庆祝动画(进度存在浏览器本地)。
- **明暗主题**:默认暗色,一键切换宣纸米亮色,跟随记忆。
- **游戏模式**:4 款适合小朋友记忆的小游戏 —
  - **民族找一找**:看节日/服饰/小知识/家乡线索,从 4 个选项中挑出对应民族(8 题,干扰项已避免与线索撞车)
  - **翻牌配一配**:翻开两张卡,把民族与代表节日配对(6 对)
  - **连连看**:把民族名与它的聚居地区连成一对(6 对,选项文本去重)
  - **记忆翻翻乐**:20 张卡里藏着 10 对「民族 + 节日」,翻牌配对(计时)

## 🎨 设计

- **主色**:Ember `#E2571F` (foxai 品牌色)
- **副色**:宣纸米 `#F8F3E7`
- **字体**:Noto Serif SC (中文衬线) + PingFang SC (无衬线)
- **响应式**:从 iPhone (≥320px) 到 iPad Pro 12.9 (1024-1366px) 全部覆盖

## 📁 文件

```
site/
├── index.html         # 单页应用 (HTML + CSS + JS)
├── ethnic-groups.js   # 56 个民族数据
├── images/            # 民族服饰照片
│   └── 汉族.jpg        # 当前占位图
├── vercel.json        # Vercel 部署配置
└── README.md          # 本文件
```

### 🖼 如何替换民族照片

卡片详情弹窗按 `images/<民族名>.jpg` 加载服饰照片(如 `images/傣族.jpg`),缺图时自动回退到 `images/汉族.jpg` 占位。**放入对应命名的 jpg 即自动生效,无需改代码**;建议长边 900px 左右、200KB 以内。

## 🚀 本地预览

```bash
cd site
python3 -m http.server 8080
# 打开 http://127.0.0.1:8080
```

## ☁️ 部署到 Vercel

最简单的两种方式:

### 方式 A:CLI 部署
```bash
npm i -g vercel
cd site
vercel --prod
```

### 方式 B:连接 GitHub
1. 把本仓库推到 GitHub
2. 打开 [vercel.com/new](https://vercel.com/new)
3. 选仓库 → Framework Preset 选择「Other」→ 根目录选 `site`
4. 点击 Deploy,30 秒后拿到一个 `https://xxx.vercel.app` 的 URL

## 📊 数据来源

民族人口、分布、服饰特征、文化概览综合自官方公开资料整理。数据可能与最新统计略有出入,仅供文化学习参考。

## 🪪 License

数据与文字按综合资料整理,代码 MIT。
