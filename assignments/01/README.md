# 作业 02 — 概念学习资料生成（Agent × 上下文 × Skill）

> 大数据与人工智能 · 课程作业
> 学号 / GitHub：lishiyi69
> 提交日期：2026-09-04

## 仓库用途

本作业是"大数据与人工智能"课程的第 2 次作业：用 AI 协助学习 Agent、大模型的上下文、Skill 三个概念，并产出一个**可复用的项目级 Skill**。

作业目标不是"用 AI 帮我读完三个词条"，而是：
1. 自己设计一个能针对任意新概念生成结构化学习包的 Skill（不是一次性提示词）。
2. 用这个 Skill 真的去生成三份概念资料 + 一份关系图。
3. 在 AI 产出之上做**人工核查**：术语准确性、引用真实性、边界与适用条件是否讲清。

## 目录结构

```
agent-skills/                      # 本次作业根目录
├── .workbuddy/
│   └── skills/
│       └── concept-study-pack/    # 项目级 Skill（可在 WorkBuddy 中调用）
│           └── SKILL.md
├── learning-materials/            # 生成的 4 份学习资料
│   ├── agent.html
│   ├── llm-context.html
│   ├── skill.html
│   └── concept-relationship.html
├── README.md                      # 本文件
└── .gitignore
```

## 项目级 Skill：`concept-study-pack`

- **位置**：`.workbuddy/skills/concept-study-pack/SKILL.md`
- **作用**：接收任意一个概念名（中文或英文），按八个固定板块（学习目标 / 核心问题 / 个人解释 / 核心机制 / 应用场景 / 概念辨析 / 自测题 / 参考来源 + 核查记录）生成自包含、可离线打开的 HTML 学习包。
- **设计要点**：
  - **通用性**：不绑定本次三个概念，可用于任意新概念。
  - **可核查**：每个关键论断要求附真实可达的 URL，禁用编造。
  - **结构化输出**：HTML 内联 CSS、不依赖外部 CDN，可直接 `open *.html` 查看。
  - **自我约束**：Skill 末尾列出"自检要求"10 条与"限制与边界"4 条，AI 必须先通过自检再交付。

### 在 WorkBuddy 中如何调用

1. **作为项目级 Skill 加载**：本仓库的 `.workbuddy/skills/concept-study-pack/SKILL.md` 会被 WorkBuddy 在打开本项目时自动识别。
2. **手动调用方式**：
   - 在 WorkBuddy 对话中提出："用 concept-study-pack 生成 X 概念的学习资料"。
   - 或者："请按 `.workbuddy/skills/concept-study-pack/SKILL.md` 的规范，为我整理 Transformer 的学习包"。
3. **预期输出**：一份命名为 `<概念英文或拼音>.html` 的文件，包含 8 个固定板块 + 核查记录。

## 已生成的学习资料

| 文件 | 概念 | 主要参考来源 |
|------|------|-------------|
| `learning-materials/agent.html` | AI Agent | Anthropic - Building Effective Agents；OpenAI - A Practical Guide to Building Agents；Lilian Weng 经典博客 |
| `learning-materials/llm-context.html` | 大模型的上下文 | IBM - What is a context window；C# Corner - Context Window；Lost in the Middle 论文 |
| `learning-materials/skill.html` | Skill | Anthropic - Introducing Agent Skills；Anthropic - Skills explained；Zapier / Developer Playground 实战解读 |
| `learning-materials/concept-relationship.html` | 三者关系（含 SVG 关系图） | 综合上述三份资料，重点在"上下文如何影响 Agent"和"Skill 如何沉淀可复用知识" |

每份 HTML 的"9. 核查记录"小节都列出了本次的检索关键词、来源数量、待核实推断和人工核查时间，可直接追溯。

## 我在 AI 输出之上做了哪些人工核查与修改

> 作业要求"必须阅读、理解并核查 AI 生成的内容；资料来源不得伪造，概念解释不得整段照搬 AI 对话结果"。以下是我实际做的核查清单：

1. **Skill 设计层**
   - 我**没有**直接复用 WorkBuddy 自带的 `concept-learning-material` Skill，而是基于作业要求（项目级、HTML 输出、八板块、含自测）重新设计了一个 `concept-study-pack`，并明确写入了"必须可复用、不得编造 URL"等约束。
   - 删除了初稿中"AI 腔"的表述（如"非常重要"、"至关重要"），改为具体可核查的事实描述。

2. **资料来源核查**
   - 每一份资料末尾的"参考来源"链接均来自本次实际检索（WebSearch 输出可回溯），未凭记忆拼凑 URL。
   - 对时效性较强的数字（如"上下文窗口从 4K 扩到 1M"），已在结尾标注"以官方最新文档为准"。
   - 引用的论文 / 文档均加 `<b>` 强调或脚注式说明，方便老师/助教点击验证。

3. **概念解释核查**
   - Agent 部分：核对"Agent = LLM + Memory + Planning + Tool Use"公式源自 Lilian Weng 2023 年博客；"Workflow vs Agent"区分源自 Anthropic 2024-12 报告，均已加引用。
   - 上下文部分：核对 O(N²) 复杂度、KV-Cache、Lost in the middle 三大机制均有 ≥1 条独立来源；表格中的具体数字（如 1000 token 对应 100 万次运算）来自 C# Corner 详细计算过程。
   - Skill 部分：核对了 YAML 元数据结构、四大属性（Composable/Portable/Efficient/Powerful）的措辞与 Anthropic 官方公告一致；五概念辨析（Prompt/Project/Subagent/MCP/Skill）参照 Anthropic 的 "Skills explained" 博客整理。

4. **边界与适用条件核查**
   - 三份资料都明确写了"适用前提 / 失效条件"小节，避免把概念讲成"万能"。
   - 自测题中专门设计了一题"应用判断"和一题"边界辨析"（如"长上下文是否能替代 RAG"），强迫学习者面对工程取舍。

5. **结构与可读性核查**
   - 所有 HTML 均为**单文件、纯内联 CSS、无外部 CDN/字体/图片依赖**，双击即可在浏览器打开。
   - 4 个文件都通过 8 个板块的结构一致性检查；关系图用纯 SVG，不依赖 Mermaid JS。
   - "核查记录"小节是每份资料都有的硬性要求，方便老师快速验证"是否做了人工核查"。

6. **安全与隐私核查**
   - `.gitignore` 排除了 macOS 系统文件、IDE 配置、API Key、`.env` 等敏感文件。
   - HTML 内未出现任何凭据、个人隐私信息或内部网络地址。

## 如何在本地复现 / 验证

```bash
# 克隆仓库
git clone https://github.com/lishiyi69/bigdata-ai-homework.git
cd bigdata-ai-homework/assignments/01

# 打开任意一份学习资料（macOS）
open learning-materials/agent.html

# 查看 Skill 源文件
cat .workbuddy/skills/concept-study-pack/SKILL.md
```

## 版本

- v1.0 · 2026-09-04 · 首版提交（4 份 HTML + 1 份 Skill + README + .gitignore）
