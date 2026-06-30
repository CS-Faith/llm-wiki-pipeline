# LLM WIKI Pipeline — 知识工厂

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**Reasonix Skill** — 端到端知识库构建流水线。以 LLM 为引擎，将杂乱原始材料转化为 Obsidian 最佳范式知识库。

> 核心理念来自 Andrej Karpathy 的 LLM WIKI：「LLM 负责编写和维护知识库，人类负责阅读和提问。」

## 五阶段流水线

```
杂乱原始材料（任意格式）
  │
  ├─ Phase 1: 查重清理 ──── MD5→版本链→归一化→压缩包→目录重组
  ├─ Phase 2: 获取与转换 ── markitdown + defuddle → 统一 MD
  ├─ Phase 3: LLM 理解融合 ── 阅读→理解→融合多源→结构化文章
  ├─ Phase 4: Obsidian 化 ── Wikilinks/Callouts/Properties/Base/Canvas
  └─ Phase 5: 持续维护 ──── Query + Lint + 增量更新
```

| 阶段 | 做什么 | 用什么 |
|------|--------|--------|
| **Phase 1** 查重清理 | 五轮递进去重：MD5 完全重复 → 文件名版本链 → 激进归一化 → 压缩包清理 → 目录结构重组 | Python 脚本 |
| **Phase 2** 获取与转换 | 本地文件（PDF/DOCX/PPTX/XLSX/HTML/图片/音频 等 15+ 格式）→ Markdown；网页抓取 → 干净 Markdown | [markitdown](https://github.com/microsoft/markitdown) + [defuddle](https://github.com/kepano/defuddle) |
| **Phase 3** LLM 理解融合 | 阅读所有 MD → 理解内容 → 融合多源知识 → 重组为结构化文章 → 更新索引和日志 | LLM Agent |
| **Phase 4** Obsidian 化 | 标准 MD → Obsidian Flavored Markdown（wikilinks/callouts/tags）+ Base 数据库视图 + Canvas 知识图谱 | Obsidian 原生格式 |
| **Phase 5** 持续维护 | 语义查询、质量检查（自动修复 + 启发式报告）、增量更新 | LLM Agent |

## 快速开始

### 安装

```bash
# 安装 Skill 到 Reasonix
# 将 llm-wiki-pipeline.md 复制到 .reasonix/skills/ 目录

# 安装依赖工具
pip install "markitdown[pdf,docx,xlsx,pptx]>=0.1.5"
npm install -g defuddle
```

### 使用

在 Reasonix 对话中：

```
/ skill llm-wiki-pipeline
帮我把 ~/Documents/work-archive/ 整理成知识库
```

Skill 会引导你完成五个阶段，每轮生成报告并等待确认。

### 配置

首次使用前确认三个路径：

| 配置项 | 说明 |
|--------|------|
| `RAW_DIR` | 原始材料目录（只读，永不修改） |
| `WIKI_DIR` | 知识库输出目录 |
| `VAULT_DIR` | Obsidian Vault 路径（可选） |

## 目录结构（最终产出）

```
<WIKI_DIR>/
├── index.md                   ← 全局索引
├── log.md                     ← 操作日志
├── index.base                 ← Obsidian 多视图
├── knowledge-graph.canvas     ← 知识图谱
├── 01-主题A/
│   ├── 文章1.md              ← 融合文章（Obsidian 格式）
│   ├── 文章2.md
│   └── _原始提取/             ← 转换件归档
└── 02-主题B/
    └── ...
```

## 设计原则

1. **原始材料不可变** — 源目录只读，操作在副本中进行
2. **多轮递进，逐轮确认** — 每轮聚焦一种重复模式，等用户确认后才继续
3. **先移后备，不直接删除** — 所有清理操作移入 `_backup/`
4. **转换 ≠ 完成** — markitdown 输出是原始 dump，必须经过 LLM 理解融合
5. **Phase 3/4 分离** — 融合阶段用标准 MD，Obsidian 语法在 Phase 4 统一转换
6. **知识库是活的** — Phase 5 提供查询、质量检查和增量更新

## 包含的 Skill

本仓库包含完整工具链，共 9 个 Reasonix Skill：

| Skill 文件 | 用途 | 对应流水线阶段 |
|-----------|------|:---:|
| `llm-wiki-pipeline.md` | 🏭 **知识工厂总入口** — 五阶段端到端流水线 | 全部 |
| `skills/knowledge-cleanup.md` | 🔍 五轮递进查重清理 | Phase 1 |
| `skills/everything-markdown.md` | 📄 15+ 格式 → Markdown（markitdown） | Phase 2 |
| `skills/defuddle.md` | 🧹 网页内容清洗 → 干净 Markdown | Phase 2 |
| `skills/karpathy-llm-wiki.md` | 🧠 LLM 理解融合 + 索引/日志管理 | Phase 3, 5 |
| `skills/obsidian-markdown.md` | 📝 Obsidian Flavored Markdown 语法 | Phase 4 |
| `skills/obsidian-bases.md` | 🗃️ Obsidian Bases 数据库视图 | Phase 4 |
| `skills/json-canvas.md` | 🎨 JSON Canvas 知识图谱 | Phase 4 |
| `skills/obsidian-cli.md` | 🖥️ Obsidian CLI 批量操作 | Phase 4 |

每个 Skill 均可独立使用，也可通过 `llm-wiki-pipeline` 串联执行。

## 集成工具

本 Skill 整合了以下开源工具和方法论：

- [Microsoft MarkItDown](https://github.com/microsoft/markitdown) — 15+ 格式 → Markdown
- [Defuddle](https://github.com/kepano/defuddle) — 网页内容清洗
- [Obsidian Flavored Markdown](https://help.obsidian.md/obsidian-flavored-markdown) — wikilinks/callouts/tags
- [Obsidian Bases](https://help.obsidian.md/bases) — 数据库视图
- [JSON Canvas Spec](https://jsoncanvas.org/) — 知识图谱

## License

MIT
