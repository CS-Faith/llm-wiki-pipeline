---
description: Build an Obsidian knowledge base from Wikipedia dumps
argument-hint: [source-path] [output-vault-path]
---

# LLM Wiki Pipeline

Build a complete Obsidian knowledge base from Wikipedia dump files.

## Arguments
- $ARGUMENTS: Source path (Wikipedia dump) and output vault path
  - Default source: ./wikipedia-dump
  - Default output: ./obsidian-vault

## Steps

1. Check if llm-wiki-pipeline is available
2. Run the pipeline:
   ```bash
   llm-wiki-pipeline --source $ARGUMENTS --output ./obsidian-vault
   ```
3. The pipeline will:
   - Clean and deduplicate source files
   - Convert to Markdown
   - Apply LLM summarization
   - Build knowledge graph links
   - Output as Obsidian vault
4. Show results summary (files created, links generated)
5. Suggest opening the vault in Obsidian

## Usage Example
```
/llm-wiki-pipeline ~/Downloads/zhwiki-dump ~/Documents/MyKnowledgeVault
```
