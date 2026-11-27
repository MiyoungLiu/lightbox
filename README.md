# 灯箱 · LIGHTBOX

把结构照亮，再下判断。

灯箱是一个静态技术博客：AI 工程、模型训练，以及生活里值得拆开看的问题。
每篇文章是一个自包含的单文件 HTML——没有框架、构建步骤、统计脚本，也不加载任何
外部脚本、字体、图片或样式。页面里的推导、图表与交互演示都在本地计算；引用链接
只在点击时离开本站。断网也能阅读与运行演示（外部引用链接除外）。

## 目录结构

```text
<repo>/
├── index.html                                  # 首页
├── llm-pretraining-alignment.html              # 大模型是怎么造出来的
├── agent-production-engineering.html           # Agent 从 Demo 到生产
├── rag-production-engineering.html             # RAG 从 Demo 到生产
├── ai-product-fundamentals.html                # AI 产品基础认知
├── neural-network-overview.html                # 神经网络全景
├── neural-network-training-optimization.html   # 神经网络训练优化
├── scientific-cat-care.html                    # 科学养猫
├── appliance-safety.html                       # 家用电器安全
├── western-philosophy.html                     # 西方哲学两千六百年
├── chinese-philosophy.html                     # 中国哲学两千五百年
├── weather-lab.html                            # 天气实验室
├── lheure-bleue.html                           # 闻见黄昏：娇兰蓝调时光
├── README.md
├── LICENSE
├── .gitignore
└── .nojekyll
```

文件之间全部使用相对链接。放在仓库根目录即可被 GitHub Pages 直接托管；项目页
`https://miyoungliu.github.io/lightbox/` 下路径依然正确。

`.gitignore` 采用白名单：只放行首页、上面 12 篇文章和仓库元文件，其他本地稿件、
工具链与资料默认不进仓库。新增文章时需要把文件名加入白名单。

## 阅读路径

### AI 应用：认知 → 检索 → 行动

1. [AI 产品基础认知](ai-product-fundamentals.html)：能力边界、需求真伪与指标体系。
2. [RAG 从 Demo 到生产](rag-production-engineering.html)：知识治理、检索、重排、接地与评估闭环。
3. [Agent 从 Demo 到生产](agent-production-engineering.html)：工具契约、停机条件、权限边界与轨迹评估。

### 模型与训练

1. [大模型是怎么造出来的](llm-pretraining-alignment.html)：数据、预训练、SFT、偏好对齐与推理 RL 的工程约束。
2. [神经网络全景](neural-network-overview.html)：从神经元到 Transformer 的前向、反向与结构。
3. [神经网络训练优化](neural-network-training-optimization.html)：从学习率、优化器到混合精度与部署。

### 科普、互动与视觉

1. [科学养猫](scientific-cat-care.html)：能量、饮水、体况与环境。
2. [家用电器安全](appliance-safety.html)：回路、插座、延长线与使用场景。
3. [西方哲学两千六百年](western-philosophy.html)：问题接力与三台思想仪器。
4. [中国哲学两千五百年](chinese-philosophy.html)：经典与注疏，三教时间河与人性辩论台。
5. [天气实验室](weather-lab.html)：七种天象、二十四小时日光与一个会躲雨的行人。
6. [闻见黄昏：娇兰蓝调时光](lheure-bleue.html)：一朵生成的蓝花、一段蓝调时刻，与一瓶1912年的香水。

## 站点约定

- **单文件**：每页的样式、脚本、图标都内联或以 data URI 嵌入，不请求外部子资源。
- **可复核**：推导给出可逐步验算的数字；引用给到可回查的出处；演示现场计算，不用预录动画。
- **相对路径**：站内链接全部相对当前目录，仓库放到 GitHub Pages 子路径下也能正常工作。
- **本地记忆**：只用 `localStorage` 记住主题、侧栏与列表滚动位置；没有统计与追踪。
- **主题**：默认跟随系统，页眉按钮可手动切换深浅色并记忆选择。

## 本地预览

直接双击 `index.html` 即可阅读；更接近发布后的行为是起一个本地服务器。在仓库根目录执行：

```bash
python -m http.server 8000
```

然后打开 `http://localhost:8000/`。`index.html` 会由目录根自动提供。

## 发布到 GitHub Pages

仓库名为 `lightbox`，使用项目页即可，不需要自定义域名或构建流程。

先确认 `.gitignore` 仍在，再初始化仓库：

```bash
git init -b main
git config --local user.name "LIGHTBOX"
git config --local user.email "<GitHub noreply 地址>"
git add .
git status --short
git commit -m "init: LIGHTBOX static site"
git remote add origin https://github.com/MiyoungLiu/lightbox.git
git push -u origin main
```

`git status --short` 应只出现 17 个发布文件：`index.html`、12 篇文章、
`README.md`、`LICENSE`、`.gitignore` 与 `.nojekyll`。不要使用 `git add -f`
把本地工作目录强行加入仓库，也不要把整个目录打 zip 上传。提交身份用仓库级配置与
GitHub noreply 地址，不改全局 git 配置；remote 使用 SSH 或凭据管理器，不要把
访问令牌写进 URL。

在 GitHub 新建仓库 `lightbox` 后，进入 Settings → Pages → Source，选择
`main` 分支与 `/ (root)`，保存后约一分钟生效。`.nojekyll` 已包含在仓库里，
不需要 GitHub Actions。

发布后的地址形式：

- 首页：`https://miyoungliu.github.io/lightbox/`
- 文章：`https://miyoungliu.github.io/lightbox/<article>.html`

`index.html` 由目录根自动提供，文章保留 `.html` 后缀；站内相对链接在 `/lightbox/`
子路径下继续有效。

## 新增文章约定

1. 新建一个自包含 HTML 文件，文件名用英文短横线命名，例如 `my-new-post.html`。
2. 把文件名加入 `.gitignore` 的白名单，否则它不会进入仓库。
3. 在 `index.html` 的 `<div class="cards">` 里复制一张 `<a class="card">…</a>`，
   修改链接、标题、摘要、日期、时长与图标；色调三选一（`card cool` / `card warm` /
   `card paper`），并加上 `data-cat`（`survey` / `tutorial` / `life`）。
   分类筛选与搜索索引从 DOM 自动读取，但首页的硬编码总数与分类计数需要同步加一。
   卡数为偶数时，首卡可用 `card wide` 通栏特写，让 auto-fill 网格收尾完整；≤620px 会自动回落到普通卡。
4. 文章页顶部放回 `index.html` 的链接；页脚附「相关阅读」互链。
5. 不引入外部脚本、字体、图片、样式或统计；样式与脚本内联，图片用小尺寸 data URI。
6. 写作沿用站点约定：数字可验算、引用可回查、演示现场计算。

## 版权

© 2026 灯箱 · LIGHTBOX。本站文章、图表、交互演示与页面代码的版权归作者所有；
文中引用的论文、标准、专利、第三方图片与数据归原权利人所有。详见 [LICENSE](LICENSE)。
