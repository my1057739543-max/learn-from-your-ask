# learn-from-your-ask

> 把 AI 对话变成你的长期知识体系。  
> Turn your AI conversations into a lasting personal knowledge graph.

[English](#english) | [中文](#中文)

---

## English

### What Is This?

**learn-from-your-ask** is a Claude Code skill that captures valuable technical Q&A from your AI conversations and turns them into a persistent, interactive, visual knowledge graph. You ask a technical question, get a great answer, run `/learn-from-your-ask` — and that knowledge point is saved forever.

### What It Does

- **Extracts** the latest meaningful technical Q&A from the current conversation
- **Filters** out casual chat, meta questions, duplicates, and low-value content
- **Infers** your profession and classifies the knowledge point by domain, subdomain, topic, and tags
- **Persists** structured knowledge into `knowledge/knowledge.json`
- **Visualizes** everything as an interactive dark-themed HTML graph (`knowledge/index.html`)

### Why HTML?

The knowledge graph is a single self-contained HTML file:

- **Offline-first** — no server, no dependencies. Open in any browser
- **3-layer navigation** — Domain overview → Subdomain → Knowledge cards → Full conversation replay
- **Smooth animations** — particle background, zoom transitions, glowing hover effects
- **Chat-style modals** — replay the original Q&A exactly as it happened

### Repository Structure

```text
learn-from-your-ask/
  SKILL.md               # Skill entrypoint (loaded by Claude Code)
  templates/
    graph.html           # HTML template with {{KNOWLEDGE_DATA}} placeholder
  knowledge/
    .gitkeep             # Keeps the output directory in source control
  README.md
  LICENSE
```

Generated at runtime (gitignored):

- `knowledge/knowledge.json` — structured knowledge base
- `knowledge/index.html` — interactive visualization

### Installation

Clone this repository into your Claude Code skills directory:

```bash
# macOS / Linux
git clone https://github.com/my1057739543-max/learn-from-your-ask.git \
  ~/.claude/skills/learn-from-your-ask
```

```powershell
# Windows (PowerShell)
git clone https://github.com/my1057739543-max/learn-from-your-ask.git `
  $env:USERPROFILE\.claude\skills\learn-from-your-ask
```

Or simply copy the entire folder:

```bash
cp -r learn-from-your-ask ~/.claude/skills/learn-from-your-ask
```

Then start Claude Code in any project and run `/learn-from-your-ask`.

### Usage

1. Ask Claude a technical question (e.g., *"How does FastAPI's dependency injection work?"*)
2. After receiving a useful answer, run `/learn-from-your-ask`
3. The skill saves one knowledge point and regenerates the HTML graph
4. Open `knowledge/index.html` in a browser to explore your growing knowledge graph

> **Tip:** Run the skill immediately after each valuable Q&A while the context is still fresh. Early conversation turns may be lost to context compaction if you wait too long.

### Knowledge Graph Layers

| Layer | What You See |
|-------|-------------|
| **1. Domain View** | Your profession at the center, domains orbiting around (Backend, Frontend, Database, DevOps…) |
| **2. Subdomain View** | Click a domain to drill into technologies (FastAPI, React, PostgreSQL…) |
| **3. Knowledge Cards** | Browse cards with date, topic, and tags. Click to open the full conversation |
| **Modal** | Chat-style replay of the original Q&A |

### What Gets Filtered Out

- Greetings, casual chat, weather talk
- Meta questions about Claude Code itself
- Questions too short with no technical terms
- AI refusals or "I don't know" answers
- Near-duplicates of already-saved knowledge points

### License

MIT

---

## 中文

### 这是什么？

**learn-from-your-ask** 是一个 Claude Code 技能，它能从你的 AI 对话中提取有价值的技术问答，转化为一个持久的、可交互的、可视化的知识图谱。问一个技术问题，得到好的答案，运行 `/learn-from-your-ask` —— 这个知识点就被永久保存了。

### 它做什么

- **提取** 当前对话中最新一轮有意义的技术问答
- **过滤** 掉闲聊、元问题、重复内容和低价值信息
- **推断** 你的职业领域，将知识点按领域、子领域、主题和标签分类
- **持久化** 结构化知识到 `knowledge/knowledge.json`
- **可视化** 生成暗色科技风的交互式 HTML 知识图谱

### 为什么用 HTML？

知识图谱是一个自包含的单文件 HTML：

- **离线可用** —— 无需服务器，无需依赖，浏览器直接打开
- **三层导航** —— 领域总览 → 子领域 → 知识点卡片 → 完整对话回放
- **流畅动画** —— 粒子背景、缩放切换、发光 hover 效果
- **聊天弹窗** —— 原汁原味重现当时问答场景

### 仓库结构

```text
learn-from-your-ask/
  SKILL.md               # 技能入口（Claude Code 自动加载）
  templates/
    graph.html           # HTML 模板，含 {{KNOWLEDGE_DATA}} 占位符
  knowledge/
    .gitkeep             # 保持输出目录在版本控制中
  README.md
  LICENSE
```

运行时生成（已 gitignore）：

- `knowledge/knowledge.json` —— 结构化知识库
- `knowledge/index.html` —— 交互式可视化

### 安装

将本仓库克隆到 Claude Code 的技能目录：

```bash
# macOS / Linux
git clone https://github.com/my1057739543-max/learn-from-your-ask.git \
  ~/.claude/skills/learn-from-your-ask
```

```powershell
# Windows (PowerShell)
git clone https://github.com/my1057739543-max/learn-from-your-ask.git `
  $env:USERPROFILE\.claude\skills\learn-from-your-ask
```

或者直接复制整个文件夹：

```bash
cp -r learn-from-your-ask ~/.claude/skills/learn-from-your-ask
```

然后在任意项目中启动 Claude Code，运行 `/learn-from-your-ask` 即可。

### 使用方法

1. 问 Claude 一个技术问题（比如 *"FastAPI 的依赖注入是怎么实现的？"*）
2. 收到有价值的回答后，运行 `/learn-from-your-ask`
3. 技能自动保存知识点并重新生成 HTML 图谱
4. 用浏览器打开 `knowledge/index.html`，探索你不断增长的知识图谱

> **提示：** 每次有价值的问答结束后立刻运行 skill，趁上下文还热乎就存下来。等对话太长了，早期的问答可能被上下文压缩丢弃。

### 知识图谱层级

| 层级 | 展示内容 |
|------|---------|
| **第一层：领域大图** | 中心显示职业标签，周围环绕领域节点（后端、前端、数据库、DevOps…） |
| **第二层：子领域** | 点击领域查看具体技术（FastAPI、React、PostgreSQL…） |
| **第三层：知识点卡片** | 浏览带日期、主题和标签的卡片，点击进入完整对话 |
| **弹窗** | 聊天风格回放原始问答 |

### 哪些内容会被过滤

- 问候、闲聊、天气话题
- 关于 Claude Code 本身的元问题
- 过短且无技术术语的提问
- AI 拒绝回答或"不知道"的回复
- 与已有知识点高度重复的内容

### 开源协议

MIT