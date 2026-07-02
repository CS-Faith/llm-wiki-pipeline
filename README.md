# LLM Wiki Pipeline - 知识工厂

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/CS-Faith/llm-wiki-pipeline?style=social)](https://github.com/CS-Faith/llm-wiki-pipeline/stargazers)

**端到端知识库构建流水线** — 从原始文件到结构化知识库的完整解决方案。核心理念来自 Karpathy LLM WIKI：**LLM 负责编写和维护知识库，人类负责阅读和提问。**

---

## 流水线架构

```
杂乱原始材料（任意格式）
  │
  ├─ Phase 1: 查重清理 —— 五轮递进：MD5→版本链→归一化→压缩包→目录重组
  ├─ Phase 2: 获取与转换 —— 本地文件(markitdown) + 网页(defuddle) → 统一 MD
  ├─ Phase 3A: 初步融合 —— 快速覆盖 → 项目概述（15-40%密度，建立全局索引）
  ├─ Phase 3B: 深度知识 ⭐—— 圆桌讨论 → 逐子系统深度文章（70%密度，2-3万字/系统）
  ├─ Phase 4: Obsidian 化 —— Frontmatter + Wikilinks + Callouts + Base + Canvas
  └─ Phase 5: 持续维护 —— Query(查询) + Lint(质量检查) + 增量更新
```

---

## Phase 3B: 深度知识层（核心创新）

### 什么是 70% 知识密度

| 密度级别 | 表现 | 示例 |
|---------|------|------|
| 15-20%（命名层） | 列出文件名和一句话概述 | "某项目有 3 个 PDF" |
| 40-50%（结构层） | 列出模块名称和功能描述 | "某系统有 5 个模块" |
| **70%（知识层）** | 包含设计决策因果、数值参数、端到端流程、接口契约 | "为什么用 X 模型而不是 Y" |

### S/A/B/C 四级质量标准

| 级别 | 适用对象 | 硬指标 |
|------|---------|--------|
| **S 级**（核心技术系统） | 用户直接负责的核心业务系统 | >=3 设计决策因果 + >=5 数值参数 + >=1 端到端流程 + >=2 接口契约 + >=3000字 |
| **A 级**（项目/业务系统） | 重要项目或业务系统 | 前 4 项硬指标 |
| **B 级**（产品/方案类） | 产品原型、数据网关等 | >=2 设计决策 + >=1 业务流程 + >=1500字 |
| **C 级**（小型/支撑项目） | 小型方案、外围支撑项目 | >=1 设计决策 + >=1500字 |

### 关键原则

- **粒度原则**：一个子系统 ≠ 一篇文章。S 级系统（50-70 源文件）→ 5-6 篇深度文章 → 2-3 万字
- **双层结构**：深度文章是"理解层"（LLM 融合），原始文档是"参考层"（保留不替换）
- **多 Agent 圆桌讨论**：写作前通过知识架构师+领域专家+执行专家+质量门神四方讨论确定方案

---

## Skill 矩阵

| Skill | 类型 | 功能 |
|-------|------|------|
| **knowledge-cleanup** | 查重清理 | 五轮递进式文件去重（MD5→版本链→归一化→压缩包→目录重组） |
| **everything-markdown** | 格式转换 | 15+ 格式→Markdown（PDF/DOCX/PPTX/XLSX/图片/音频/XMind） |
| **defuddle** | 网页清洗 | 网页→干净 Markdown，去导航/广告/侧栏 |
| **karpathy-llm-wiki** | LLM 理解 | 语义分析、内容融合、智能分类 |
| **multi-agent-discuss** | 圆桌讨论 | 深度知识写作前的方案设计（Phase 3B 前置步骤） |
| **obsidian-markdown** | Obsidian 格式 | Wikilinks/Callouts/Frontmatter 增强 |
| **obsidian-bases** | 数据库视图 | 多视图浏览（表格/卡片/列表） |
| **json-canvas** | 知识图谱 | 交互式知识关系可视化 |
| **obsidian-cli** | CLI 工具 | Obsidian 批量管理 |

---

## 快速开始

### 前置要求
- Python 3.8+ / Node.js / Obsidian（可选）/ LLM API（用于 Phase 3B）

### 安装
```bash
git clone https://github.com/CS-Faith/llm-wiki-pipeline.git
cd llm-wiki-pipeline
pip install "markitdown[pdf,docx,xlsx,pptx]>=0.1.5"
npm install -g defuddle
```

---

## 许可证
MIT License

## 相关项目

| 项目 | 描述 | 链接 |
|------|------|------|
| **reasonix-portakit** | 便携工具箱 | [CS-Faith/reasonix-portakit](https://github.com/CS-Faith/reasonix-portakit) |
| **knowledge-cleanup** | 知识库查重清理 | [CS-Faith/knowledge-cleanup](https://github.com/CS-Faith/knowledge-cleanup) |
