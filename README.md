# LLM Wiki Pipeline - 知识工厂

[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![GitHub Stars](https://img.shields.io/github/stars/CS-Faith/llm-wiki-pipeline?style=social)](https://github.com/CS-Faith/llm-wiki-pipeline/stargazers)
[![GitHub Issues](https://img.shields.io/github/issues/CS-Faith/llm-wiki-pipeline)](https://github.com/CS-Faith/llm-wiki-pipeline/issues)

**端到端知识库构建流水线** - 从原始文件到结构化知识库的完整自动化解决方案

---
## 🏭 知识工厂 Skill 矩阵

### 核心 Skill 组件

| Skill | 类型 | 功能描述 | 输入 | 输出 | 依赖 |
|-------|------|----------|------|------|------|
| **knowledge-cleanup** | 📁 文件处理 | 五轮递进式文件去重与整理 | 原始文件目录 | 清理后文件目录 | Python 3.8+ |
| **everything-markdown** | 📄 格式转换 | 所有文档转Markdown格式 | 各种文档格式 | Markdown文件 | Python |
| **defuddle** | 🧹 内容清理 | 内容去重、去噪、标准化 | Markdown文件 | 标准化Markdown | Python |
| **karpathy-llm-wiki** | 🧠 LLM理解 | LLM驱动的内容理解与融合 | Markdown文件 | 语义增强文件 | LLM API |
| **obsidian-markdown** | ✍️ 格式优化 | Obsidian友好格式转换 | 标准Markdown | Obsidian格式 | Python |
| **json-canvas** | 🎨 可视化 | 知识图谱可视化生成 | 结构化数据 | JSON Canvas | Python |
| **obsidian-cli** | 💻 CLI工具 | Obsidian命令行管理 | Obsidian文件 | 管理操作 | Node.js |
| **obsidian-bases** | 📚 基础模板 | Obsidian知识库模板 | 空知识库 | 预配置知识库 | Obsidian |
### Skill 功能详解

#### 📁 knowledge-cleanup
**文件去重与整理**
- **R1**: MD5完全重复检测 - 字节级相同文件去重
- **R2**: 文件名相似度 - 版本链自动识别
- **R3**: 激进归一化 - 隐式版本发现
- **R4**: 压缩包检测 - 安全删除已解压文件
- **R5**: 目录重组 - 项目/管理二层结构
- **特点**: 安全备份，支持回滚，用户确认机制

#### 📄 everything-markdown
**全格式转Markdown**
- 支持Word、PDF、Excel、PPT等多种格式
- 保持原始内容结构和格式
- 自动处理表格、图片、公式
- 生成标准的Markdown文件

#### 🧹 defuddle
**内容清理与标准化**
- 去除重复内容
- 标准化文本格式
- 清理无用信息
- 统一编码和样式

#### 🧠 karpathy-llm-wiki
**LLM驱动的内容理解**
- 语义分析和理解
- 内容融合和关联
- 自动生成摘要和标签
- 智能分类和组织
#### ✍️ obsidian-markdown
**Obsidian格式优化**
- 添加Obsidian特有语法
- 优化文件命名和组织
- 生成YAML前置元数据
- 兼容Obsidian插件生态

#### 🎨 json-canvas
**知识图谱可视化**
- 生成交互式知识图谱
- 可视化文件间的关系
- 支持多种布局方式
- 导出为JSON Canvas格式

#### 💻 obsidian-cli
**Obsidian命令行工具**
- 批量处理Obsidian文件
- 自动化知识库管理
- 快速搜索和替换
- 与Git集成

#### 📚 obsidian-bases
**Obsidian知识库模板**
- 预配置的知识库结构
- 包含常用插件配置
- 示例笔记和模板
- 快速上手指南

---
## 🚀 流水线工作流程

### 端到端自动化流程

```
原始文件目录
       ↓
┌─────────────────┐
│ knowledge-cleanup │ ← 五轮清理：去重、版本链、归一化、压缩包、目录重组
└─────────────────┘
       ↓
清理后文件目录
       ↓
┌─────────────────────┐
│ everything-markdown │ ← 全格式转换：Word/PDF/Excel/PPT → Markdown
└─────────────────────┘
       ↓
Markdown文件集合
       ↓
┌─────────────────┐
│ defuddle        │ ← 内容清理：去重、去噪、标准化
└─────────────────┘
       ↓
标准化Markdown文件
       ↓
┌─────────────────────┐
│ karpathy-llm-wiki │ ← LLM理解：语义分析、内容融合、智能分类
└─────────────────────┘
       ↓
语义增强文件
       ↓
┌─────────────────────┐
│ obsidian-markdown │ ← 格式优化：Obsidian语法、YAML元数据
└─────────────────────┘
       ↓
Obsidian友好文件
       ↓
┌─────────────────┐
│ json-canvas     │ ← 可视化：生成知识图谱
└─────────────────┘
       ↓
知识图谱 + 结构化文件
       ↓
┌─────────────────┐
│ obsidian-bases  │ ← 模板应用：预配置知识库结构
└─────────────────┘
       ↓
📁 最终知识库 (Obsidian格式)
```
## 🎯 核心价值

### 为什么选择LLM Wiki Pipeline？

#### 📁 文件管理痛点
- **文件堆积**: 数千文件散落在嵌套目录中
- **版本混乱**: 同一文档存在多个版本（V1、V2、最终版...）
- **格式混乱**: Word、PDF、Excel、PPT等格式混杂
- **内容重复**: 大量重复和冗余内容
- **组织混乱**: 缺乏统一的组织结构

#### 🤖 AI驱动的解决方案
- **自动化**: 端到端自动化处理，无需人工干预
- **智能化**: LLM驱动的内容理解和融合
- **标准化**: 统一的Markdown和Obsidian格式
- **可视化**: 知识图谱可视化展示
- **可维护**: 持续维护和更新机制

---

## 🚀 快速开始

### 前置要求
- **Python 3.8+** - 推荐Python 3.10+
- **Node.js** - 用于obsidian-cli（可选）
- **Obsidian** - 用于最终知识库管理（可选）
- **LLM API** - 用于karpathy-llm-wiki（可选）

### 安装
```bash
git clone https://github.com/CS-Faith/llm-wiki-pipeline.git
cd llm-wiki-pipeline
pip install -r requirements.txt
```

---

## 📜 许可证
MIT License - 详见 [LICENSE](LICENSE) 文件。

## 📞 联系
- GitHub: [CS-Faith](https://github.com/CS-Faith)
- 仓库: [llm-wiki-pipeline](https://github.com/CS-Faith/llm-wiki-pipeline)
- Issues: [GitHub Issues](https://github.com/CS-Faith/llm-wiki-pipeline/issues)


---

## 🔗 相关项目

| 项目 | 描述 | 链接 |
|------|------|------|
| **reasonix-portakit** | 便携工具箱 | [CS-Faith/reasonix-portakit](https://github.com/CS-Faith/reasonix-portakit) |
| **reasonix-migration-assistant** | 配置迁移升级助手 | [CS-Faith/reasonix-migration-assistant](https://github.com/CS-Faith/reasonix-migration-assistant) |
| **knowledge-cleanup** | 知识库查重清理 | [CS-Faith/knowledge-cleanup](https://github.com/CS-Faith/knowledge-cleanup) |

