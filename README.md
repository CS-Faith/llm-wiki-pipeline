# LLM Wiki Pipeline - 知识工厂

> 你有文件堆，它造知识网：一条流水线，把杂乱档案炼成结构化的知识图谱。
> LLM Wiki Pipeline 把 50GB 原始材料变成 70% 密度的 Obsidian 知识图谱。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Reasonix](https://img.shields.io/badge/Reasonix-Ecosystem-58a6ff)](https://github.com/CS-Faith/reasonix-ecosystem)

---

## 一句话定位

| 输入 | 输出 |
|------|------|
| 50GB 杂乱原始文件（PDF/MD/网页） | 70% 密度的 Obsidian Wikilinks 知识图谱 |

---

## 为什么不是 Dataview + Obsidian 原生？

| 能力 | Obsidian + Dataview | LLM Wiki Pipeline |
|------|---------------------|-------------------|
| 查询已有笔记 | ✅ | ✅ |
| 从 0 写一篇深度文章 | ❌ | ✅（2-3 万字/系统） |
| 理解「为什么用 X 不用 Y」 | ❌ | ✅（70% 密度） |
| 多文档圆桌讨论 | ❌ | ✅（4 Agent 讨论） |
| 持续增量更新 | 手动 | ✅ 自动检测变更 |

---

## 密度对比

| 密度 | 表现 | 你现在的位置 |
|------|------|-------------|
| 15-20%（命名层） | 只列文件名和一句话描述 | ← 大多数人在这里 |
| 40-50%（结构层） | 列模块名称和功能描述 | ← 少数认真的人 |
| **70%（知识层）** | 设计决策因果、数值参数、接口契约、替代方案对比 | ← Pipeline 目标 |

> **示例**：一篇 70% 密度的笔记会写「为什么选 Transformer 而不是 RNN：长序列任务中梯度消失问题在 200 token 后显著，实测 PPL 从 45 上升到 127」。

---

## 流水线架构

```
杂乱原始材料（任意格式）
  │
  ├─ Phase 1: 查重清理 —— 五轮递进：MD5→版本链→归一化→压缩包→目录重组
  ├─ Phase 2: 获取与转换 —— 本地文件(markitdown) + 网页(defuddle) → 统一 MD
  ├─ Phase 3A: 初步融合 —— 快速覆盖 → 项目概述（15-40%密度，建立全局索引）
  ├─ Phase 3B: 深度知识 —— 圆桌讨论 → 逐子系统深度文章（70%密度，2-3万字/系统）
  ├─ Phase 4: Obsidian 化 —— Frontmatter + Wikilinks + Callouts + Base + Canvas
  └─ Phase 5: 持续维护 —— 智能检测新文件 + 仅处理变化部分（增量更新）
```

---

## 关键原则

- **粒度原则**：一个子系统 ≠ 一篇文章。S 级系统（50-70 源文件）→ 5-6 篇深度文章 → 2-3 万字
- **双层结构**：深度文章是「理解层」（LLM 融合），原始文档是「参考层」（保留不替换）
- **增量更新**：智能检测新文件，仅处理变化部分，避免重复运行

---

## Next Step

原始材料太多重复？先清理 → [**knowledge-cleanup**](https://github.com/CS-Faith/knowledge-cleanup) 五轮递进去重后再上流水线

想让历史 AI 会话也参与知识创造？ → [**Conversation Council**](https://github.com/CS-Faith/conversation-council) 多视角讨论加入知识融合

---

## License
MIT © 2026 [CS-Faith](https://cs-faith.github.io)

<details>
<summary>English Version</summary>

**LLM Wiki Pipeline** — You have a file pile. Pipeline builds a knowledge web — one assembly line, from raw chaos to structured insight.

Raw documents don't become knowledge on their own. Dataview queries notes — it doesn't write them. Wiki Pipeline writes deep articles (20k-30k chars per system) with design rationale, parameter tradeoffs, and contract specifications.

### Architecture
- Phase 1: Dedup (5 progressive rounds)
- Phase 2: Ingestion + format unification
- Phase 3A: Quick coverage overview
- Phase 3B: Deep knowledge via multi-agent roundtable
- Phase 4: Obsidian enhancement
- Phase 5: Continuous incremental maintenance
</details>