# build-your-own-x · Code Wiki

> 面向对象：`codecrafters-io/build-your-own-x` 仓库（本地路径 `/workspace`）
> 文档定位：结构化解析该仓库的组织方式、内容架构、数据模型、协作流程与使用方式。

---

## ⚠️ 重要前提：这是一个「文档型仓库」，不是代码工程

在阅读任何"架构 / 模块 / 类 / 函数 / 运行方式"相关章节前，必须先明确本仓库的根本性质：

- 本仓库**不含任何源代码**（没有 `src/`、没有 `.py`/`.js`/`.go`/`.rs` 等源文件）。
- 本仓库**没有构建系统**（没有 `package.json` / `requirements.txt` / `Makefile` / `Dockerfile` / `gradle` / `Cargo.toml`）。
- 本仓库**没有 CI/CD 配置**（没有 `.github/workflows`）。
- 本仓库**没有运行时、没有依赖安装、没有编译步骤**——它唯一的产物就是一个 Markdown 文件。

因此，传统 Code Wiki 中的「模块职责、关键类与函数、依赖关系、运行方式」在本仓库中需要**换一种映射**：

| 传统 Code Wiki 概念 | 本仓库的对应物 |
| --- | --- |
| 架构 | 内容分层结构（导航目录 → 分类章节 → 条目列表） |
| 模块 | 内容分区（TOC、各技术分类章节、贡献/许可章节）与元数据文件 |
| 类 / 函数 | 不存在；对应的是**条目的书写格式（数据模式）**与**章节/锚点命名规则** |
| 依赖关系 | 外部教程链接依赖（359 条外链）+ 渲染器依赖 + Linguist 元数据依赖 |
| 运行方式 | 「阅读/消费」方式（克隆仓库或用 GitHub 网页阅读），而非「启动服务」 |

> 若你的目标其实是分析某个**含源代码**的项目，请确认仓库指向是否正确。本文档严格基于当前仓库的真实内容撰写。

---

## 1. 项目概览

| 项目 | 内容 |
| --- | --- |
| 仓库名 | `build-your-own-x` |
| 一句话定义 | 一个精选的「从零构建各种技术」编程教程索引集合（curated list / awesome-list 风格） |
| 仓库性质 | **纯文档型仓库（Documentation-only）**，无源代码、无可执行程序 |
| 核心内容 | 一份 `README.md`，内含 359 条指向外部教程的链接，按技术领域分类 |
| 创始者 | Daniel Stefanovic |
| 维护方 | [CodeCrafters, Inc.](https://codecrafters.io) |
| 开源许可 | CC0 1.0（公共领域贡献，放弃全部版权及相关权利） |
| 核心信条 | "What I cannot create, I do not understand — Richard Feynman." |
| 数据规模 | 受版本控制的文件：4 个；`README.md` 46683 字节 / 507 行；359 条教程条目；31 个内容章节 |

### 1.1 仓库的核心价值

它本身不提供教程内容，而是提供一个**索引**：把互联网上"从零手搓某技术"的优质分步教程按技术领域归类，降低学习者的检索成本。教程的实际内容托管在第三方站点（GitHub、个人博客、YouTube、aosabook.org、build-your-own.org 等）。

---

## 2. 技术栈与仓库性质

| 维度 | 实际情况 |
| --- | --- |
| 主要语言 | Markdown（100%） |
| 编程语言源码 | 无 |
| 包管理 / 依赖清单 | 无 |
| 构建 / 编译 | 无 |
| 测试 | 无 |
| 运行时 | 无（若把"运行"理解为"渲染文档"，则运行时是任意 Markdown 渲染器） |
| 版本控制 | Git |
| 平台增强配置 | `.gitattributes`（针对 GitHub Linguist） |

**结论**：本仓库属于"内容即产品"型仓库。它的"技术栈"实质上只有 **Markdown + Git + GitHub 渲染**。

---

## 3. 文件结构（完整清单）

仓库根目录下受 Git 跟踪的全部文件仅 4 个：

```
/workspace
├── .gitattributes            # GitHub Linguist 语言识别配置
├── ISSUE_TEMPLATE.md         # 教程投稿 / 贡献模板
├── README.md                 # 主内容：教程索引（唯一的实质内容载体）
└── codecrafters-banner.png   # 品牌横幅图片
```

### 3.1 各文件职责

| 文件 | 类型 | 职责 | 关键点 |
| --- | --- | --- | --- |
| [README.md](file:///workspace/README.md) | 内容主体 | 承载全部教程索引与项目说明 | 507 行；结构见第 4、5 章 |
| [ISSUE_TEMPLATE.md](file:///workspace/ISSUE_TEMPLATE.md) | 元数据 / 流程 | 定义投稿时需要填写的字段与收录标准 | 内含 HTML 注释形式的规则说明 |
| [.gitattributes](file:///workspace/.gitattributes) | 元数据 / 配置 | 指示 GitHub 如何对 `.md` 做语言统计 | 仅 2 行规则 |
| [codecrafters-banner.png](file:///workspace/codecrafters-banner.png) | 静态资源 | README 顶部横幅 + 许可章节 CC0 徽标 | 25061 字节；被 README 引用 2 次 |

> 备注：仓库还包含 `README.md` 顶部引用的一个**外部**横幅图片（`https://codecrafters.io/images/new-ccgithub-banner.png`）与一个**外部** CC0 徽标（`mirrors.creativecommons.org`），这两个不在仓库内。

---

## 4. 整体架构

### 4.1 架构本质：单源发布（Single Source of Truth）

整个项目以 **`README.md` 为唯一内容源**，其余 3 个文件都是围绕它的"外围元数据"。没有多模块拆分，没有生成流程，没有构建产物。

```
        ┌──────────────────────────────────────────────┐
        │                README.md                      │
        │  （唯一内容源 / 唯一交付物）                    │
        └──────────────────────────────────────────────┘
             ▲                          │
   （辅助/约束）│                          │（GitHub 渲染）
   ┌──────────┴──────────┐              ▼
   │ .gitattributes      │      GitHub 网页 / 任意 MD 渲染器
   │ ISSUE_TEMPLATE.md   │              │
   │ banner.png          │              ▼
   └─────────────────────┘        终端用户阅读 → 跳转外部教程
```

### 4.2 README 内部的三层内容结构

`README.md` 自身按"导航 → 分类 → 条目"三层组织：

```
第 1 层：顶部横幅 + 项目简介 + Feynman 信条
        │
第 2 层：导航目录（TOC）—— 30 个锚点链接，快速跳转
        │  （## Tutorials 之下）
第 3 层：31 个分类章节（#### 级标题）
        │     每个章节下是若干条目（* 列表项）
        │
        尾部：## Contribute（贡献指引） + ## Origins & License（来源与许可）
```

### 4.3 内容流转架构（从投稿到发布）

```
投稿者
  │  1) 提 PR，或 2) 开 Issue（按 ISSUE_TEMPLATE.md 填写）
  ▼
维护者审核（依据收录标准）
  │  ← 标准：必须是"从零构建"的编程教程，有循序渐进的学习路径
  ▼
合并进 README.md（在对应分类下追加一条 entry）
  │
  ▼
GitHub 渲染 README → 对外发布（这就是"上线"）
```

**没有**自动化流水线参与；人工审阅 + Git 合并即发布机制。

---

## 5. 主要「模块」职责

由于没有代码模块，这里把 README 的内容分区 + 元数据文件定义为"逻辑模块"。

| 逻辑模块 | 位置 | 职责 |
| --- | --- | --- |
| 品牌与简介区 | `README.md` 第 1–9 行 | 展示横幅、项目名、"从零构建"定位、Feynman 信条 |
| 导航目录（TOC） | `README.md` 第 11–40 行 | 30 个分类锚点，提供快速跳转；**注意它不含 Distributed Systems 分类** |
| 教程分类区（主体） | `README.md` `## Tutorials` 之下 | 31 个 `####` 章节，按技术领域聚合 359 条条目 |
| 贡献指引区 | `README.md` `## Contribute` | 说明投稿方式（PR / Issue）、复审入口 |
| 来源与许可区 | `README.md` `## Origins & License` | 声明来源、维护方、CC0 许可 |
| 投稿模板 | `ISSUE_TEMPLATE.md` | 定义投稿字段与收录标准 |
| 语言统计配置 | `.gitattributes` | 控制 GitHub Linguist 对 Markdown 的处理方式 |

---

## 6. 关键「数据结构」与命名规则

本节是传统文中"关键类与函数说明"的替代物——本仓库真正的"数据结构"是**文本条目的书写模式**。

### 6.1 教程条目（Tutorial Entry）—— 主数据单元

标准模式：

```markdown
* [**{主语言}**: _{教程原始标题}_]({URL}){可选标签}
```

字段说明：

| 字段 | 语法 | 含义 | 是否必填 |
| --- | --- | --- | --- |
| 主语言 | `**...**`（加粗） | 教程使用的主要编程语言，如 `C++`、`Python`、`Go` | 是 |
| 标题 | `_..._`（斜体） | 教程的**原始标题** | 是 |
| URL | `](...)` | 教程地址（外链） | 是 |
| 标签 | `[video]` / `[pdf]` | 资源形态标记 | 否 |

**真实变体**（均来自 README 实际内容）：

- 常规条目：`* [**C++**: _Ray Tracing in One Weekend_](https://raytracing.github.io/...)`
- 带视频标签：`* [**C#**: _How To: Augmented Reality App Tutorial..._](...) [video]`
- 带 PDF 标签：`* [**Python**: _Making Games with Python & Pygame_](...) [pdf]`
- 任意语言：`* [**(any)**: _mal - Make a Lisp_](...)`
- 简化写法（省略斜体）：`* [**C**: Write a shell in C](...)`
- 换行续写（标签被折到下一行）：如 Game 分类中某条把 `[video]` 单独置于下一行并缩进两个空格

### 6.2 分类章节标题（Category Heading）—— 分组单元

模式：

```markdown
#### Build your own `{技术名}`
```

- 使用 4 级标题（`####`）。
- 技术名置于反引号内。
- 全部 30 个命名分类都以 `Build your own ...` 开头，加上 1 个特殊章节 `#### Uncategorized`，共 **31 个章节**。

### 6.3 导航锚点（Anchor）—— 导航单元

模式：

```markdown
* [{技术名}](#build-your-own-{技术名-slug})
```

- 由 GitHub 依据标题自动生成的小写、连字符化 slug。
- TOC 共 **30** 条，但**未包含** `Distributed Systems`，因此导航与正文存在 1 处不一致（详见附录 A）。

---

## 7. 内容清单（分类目录与条目数）

以下为 `README.md` 实际统计（各章节下 `* [...]` 条目数，总计 **359**）：

| # | 分类章节 | 条目数 | 代表性条目示例 |
| --- | --- | --- | --- |
| 1 | Distributed Systems | 1 | Building Your Own Kafka-like System（Java） |
| 2 | 3D Renderer | 11 | Ray Tracing in One Weekend；tinyrenderer |
| 3 | AI Model | 3 | LLMs-from-scratch；RAG for Document Search |
| 4 | Augmented Reality | 6 | Unity ARCore；AR with Python + OpenCV |
| 5 | BitTorrent Client | 5 | Building a BitTorrent client in Go / C# / Python |
| 6 | Blockchain / Cryptocurrency | 21 | Building Blockchain in Go；Naivecoin |
| 7 | Bot | 15 | Discord bot；Telegram bot；Starcraft bot in Rust |
| 8 | Command-Line Tool | 9 | lolcat；cowsay；fortune（Go） |
| 9 | Database | 13 | Let's Build a Simple Database；Build Your Own Redis |
| 10 | Docker | 6 | Linux containers in 500 lines；bocker |
| 11 | Emulator / Virtual Machine | 13 | Write Your Own Virtual Machine；CHIP-8；Game Boy |
| 12 | Front-end Framework / Library | 14 | Build your own React；Build Yourself a Redux |
| 13 | Game | 34 | Handmade Hero；Chess Engine in C；Tetris；Snake |
| 14 | Git | 7 | Write yourself a Git!；ugit；Rebuilding Git in Ruby |
| 15 | Memory Allocator | 1 | Malloc is not magic |
| 16 | Network Stack | 4 | Let's code a TCP/IP stack；Beej's Guide |
| 17 | Neural Network | 17 | Neural Networks: Zero to Hero；A Neural Network in 11 lines |
| 18 | Operating System | 19 | Writing an OS in Rust；os-tutorial；Linux from scratch |
| 19 | Physics Engine | 7 | How Physics Engines Work；Custom Physics Engine |
| 20 | Processor | 1 | From Blinker to RISC-V（Verilog） |
| 21 | Programming Language | 41 | mal - Make a Lisp；Crafting Interpreters；Build Your Own Lisp |
| 22 | Regex Engine | 9 | Regular Expression Matching Can Be Simple And Fast |
| 23 | Search Engine | 6 | Building a search engine using Redis；TF-IDF |
| 24 | Shell | 7 | Write a Shell in C；Build Your Own Shell |
| 25 | Template Engine | 5 | Template engine in just 20 lines；A Template Engine |
| 26 | Text Editor | 6 | Build Your Own Text Editor（kilo）；Hecto（Rust） |
| 27 | Visual Recognition System | 2 | License Plate Recognition；Facial Recognition Pipeline |
| 28 | Voxel Engine | 1 | Let's Make a Voxel Engine（C++） |
| 29 | Web Browser | 2 | Let's build a browser engine；Browser Engineering |
| 30 | Web Server | 11 | Build Your Own Web Server（Node.js）；lets-build-express |
| 31 | Uncategorized | 62 | From NAND to Tetris；Minipack；Building a spell-checker |
| | **合计** | **359** | — |

> 观察：**Programming Language（41）**、**Game（34）**、**Blockchain（21）**、**Uncategorized（62）** 是内容最密集的区域；而 **Distributed Systems / Memory Allocator / Processor / Voxel Engine** 各仅 1 条，属于长尾分类。

---

## 8. 依赖关系

本仓库无代码级依赖，其"依赖"体现在内容与外部环境上：

### 8.1 外部资源依赖（强依赖）

- README 中的 **359 条条目全部指向第三方外部 URL**。
- 常见域名来源（基于实际内容）：`github.com`、`youtube.com`、`aosabook.org`、`build-your-own.org`、`raytracing.github.io`、`craftinginterpreters.com`、各作者个人博客等。
- **风险**：任一外部链接失效（404 / 域名过期），对应条目的价值即归零；仓库本身不缓存任何教程内容。

### 8.2 渲染 / 平台依赖

- 内容以 Markdown 呈现，依赖 **GitHub 的 Markdown 渲染器**或任意第三方渲染器来生成锚点、排版。
- 锚点跳转（TOC）依赖 GitHub 自动 slug 生成规则；更换渲染器可能导致锚点失效。

### 8.3 元数据依赖

- `.gitattributes` 中的规则依赖 **GitHub Linguist** 生效；离开 GitHub，这两行无实际作用。

### 8.4 品牌依赖

- 顶部横幅与 CC0 徽标依赖外部图片服务；`codecrafters-banner.png` 为仓库内自备资源。

---

## 9. 协作 / 贡献流程

### 9.1 投稿方式

README 的 `## Contribute` 章节声明：

- 欢迎直接发 PR；
- 或通过 [提交 Issue](https://github.com/codecrafters-io/build-your-own-x/issues/new) 投稿；
- 维护者通过审阅 [pending submissions](https://github.com/codecrafters-io/build-your-own-x/issues) 并点赞/评论进行复审。

### 9.2 投稿模板字段（来自 `ISSUE_TEMPLATE.md`）

| 字段 | 说明 |
| --- | --- |
| Main programming language | 主要编程语言，最多 1 个 |
| Tutorial title | 教程原始标题（取自文章 / 仓库） |
| Tutorial URL | 教程地址 |
| Category | 分类勾选清单 |

### 9.3 收录标准（模板内嵌的规则注释）

模板顶部以 HTML 注释形式声明了收录门槛：

1. 教程必须提供**循序渐进的学习路径**（分步文章，或把代码拆解为易跟读的部分）。
2. 仅收录**"从零构建"**某事物的编程教程。
3. **拒绝**：框架 / 库的教程、框架库的使用指南、以及仅把现成库"粘合"起来的教程。

### 9.4 分类勾选清单

`ISSUE_TEMPLATE.md` 提供了一个 25 项的复选清单（3D Renderer、Augmented Reality、BitTorrent Client、Blockchain / Cryptocurrency、Bot、Command-Line Tool、Database、Docker、Emulator / Virtual Machine、Front-end Framework / Library、Game、Git、Network Stack、Neural Network、Operating System、Physics Engine、Programming Language、Regex Engine、Search Engine、Shell、Template Engine、Visual Recognition System、Voxel Engine、Web Search Engine、Web Server、Uncategorized）。

> ⚠️ 该模板清单与 README 实际分类**存在漂移**（模板已落后于正文），差异见附录 A。这是仓库需要维护的元数据一致性问题。

---

## 10. 运行方式 / 使用方式

本仓库**无构建、无启动、无部署**。所谓"运行"即"阅读"。

### 10.1 获取仓库（克隆）

```bash
git clone https://github.com/codecrafters-io/build-your-own-x.git
cd build-your-own-x
```

### 10.2 阅读入口

- **在线（推荐）**：直接访问 GitHub 仓库页面读取 `README.md`，利用顶部 TOC 跳转分类。
- **本地**：使用任意 Markdown 阅读器 / 编辑器（如 VS Code Markdown 预览）打开 `README.md`。

### 10.3 使用路径

1. 从顶部 TOC 或直接滚动定位到目标技术分类；
2. 按"语言 + 标题"挑选条目；
3. 点击链接跳转到外部教程站点开始学习。

### 10.4 参与贡献（如需）

1. 先阅读 `ISSUE_TEMPLATE.md` 确认符合收录标准；
2. 按要求在对应分类下追加一条符合第 6.1 节格式的条目；
3. 提交 PR，或开 Issue 由维护者处理。

---

## 11. `.gitattributes` 解析

文件内容仅两行：

```gitattributes
*.md linguist-detectable=true
*.md linguist-documentation=false
```

含义说明（针对 GitHub Linguist 语言统计系统）：

| 规则 | 作用 |
| --- | --- |
| `*.md linguist-detectable=true` | 允许把 `README.md` 中的代码块按语言进行识别统计 |
| `*.md linguist-documentation=false` | 不把 `.md` 归类为"文档"，从而避免被 Linguist 排除出语言统计 |

目的：由于本仓库唯一的实质文件是 Markdown，这两行配置用于**影响 GitHub 上该仓库的语言统计呈现**（否则纯 Markdown 仓库通常会被标记为文档而影响展示）。

---

## 12. 维护要点与风险清单

| 类别 | 风险 / 待办 |
| --- | --- |
| 链接失效 | 359 条外链缺乏自动检查机制，需人工巡检 |
| 元数据漂移 | `ISSUE_TEMPLATE.md` 的分类清单与 README 实际分类不一致（缺 AI Model、Distributed Systems、Memory Allocator、Processor、Text Editor、Web Browser；多出 Web Search Engine） |
| 导航遗漏 | 顶部 TOC 未包含 `Distributed Systems`，导航与正文不完整对应 |
| 格式一致性 | 条目写法存在多种变体（斜体有无、标签换行等），无 lint 约束 |
| 无自动化 | 无 CI、无链接检查、无格式校验，全部依赖人工 PR 审核 |

---

## 附录 A：分类差异对照

### A.1 顶部 TOC（30 项） vs 正文 `## Tutorials`（31 章节）

| 差异 | 说明 |
| --- | --- |
| `Distributed Systems` | 存在于正文（第 1 个分类），**缺失**于顶部 TOC |

### A.2 `ISSUE_TEMPLATE.md` 分类清单 vs README 正文分类

| 状态 | 分类 |
| --- | --- |
| 模板**缺少**（正文有） | `AI Model`、`Distributed Systems`、`Memory Allocator`、`Processor`、`Text Editor`、`Web Browser` |
| 模板**多出**（正文无同名分类） | `Web Search Engine`（正文对应为 `Search Engine`；`Web Browser` 为独立分类） |

---

## 附录 B：关键事实一览（元数据）

| 指标 | 值 |
| --- | --- |
| 受版本控制文件数 | 4 |
| `README.md` 大小 | 46683 字节 |
| `README.md` 行数 | 507 |
| 教程条目总数 | 359 |
| 顶部导航条目数 | 30 |
| 内容章节数（`####`） | 31（30 命名分类 + Uncategorized） |
| 条目数最多的分类 | `Uncategorized`（62）、`Programming Language`（41）、`Game`（34） |
| 条目数最少的分类 | `Distributed Systems`、`Memory Allocator`、`Processor`、`Voxel Engine`（各 1） |
| 许可协议 | CC0 1.0（公共领域） |
| 维护方 | CodeCrafters, Inc. |
| 有无源代码 | **无** |
| 有无构建 / 运行步骤 | **无** |
