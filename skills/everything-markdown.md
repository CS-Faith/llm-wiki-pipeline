---
name: everything-markdown
description: Convert any file to Markdown using Microsoft MarkItDown — PDF, DOCX, PPTX, XLSX, images, audio, ZIP, etc.
---

# everything-markdown：文件 → Markdown

把任意文件转成 Markdown，供读取、分析或进一步处理。

## 支持格式

| 类别 | 格式 |
|------|------|
| 文档 | PDF, DOCX, DOC, RTF, RST, EPUB |
| 表格 | XLSX, XLS, CSV |
| 演示 | PPTX, PPT |
| 网页/数据 | HTML, HTM, XML, JSON |
| 图片 | JPG, JPEG, PNG, GIF, BMP, TIFF, WEBP |
| 音频 | MP3, WAV, M4A, OGG, FLAC |
| 压缩包 | ZIP |

## 使用方式

### 方式一：命令行（单文件）

```bash
markitdown path/to/file.pdf
```

输出直接打印到 stdout，可重定向：

```bash
markitdown report.pptx > report.md
```

### 方式二：Python API（单文件）

```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("path/to/file.pdf")
print(result.text_content)
```

### 方式三：批量脚本（文件夹/多文件）

使用技能自带的 `convert.py`：

```bash
# 转换单个文件
python convert.py file.pdf

# 转换多个文件
python convert.py file1.pdf file2.pptx file3.xlsx

# 转换整个文件夹（递归）
python convert.py ~/Documents/reports/

# 转换文件夹，输出到指定目录
python convert.py ~/Documents/reports/ --output ~/Documents/markdown/

# 仅打印内容到 stdout（不写文件，适合 agent 读取）
python convert.py file.pdf --stdout
```

## 安装依赖

```bash
pip install "markitdown[pdf,docx,xlsx,pptx]>=0.1.5"
```

## 执行步骤

### 单文件读取分析

1. 用 `markitdown <path>` 或 Python API 获取文本
2. 将结果作为上下文进行分析

### 批量转换

1. 调用 `convert.py` 脚本，传入文件/文件夹路径
2. 脚本输出每个文件的转换结果和汇总（成功/失败数量）
3. 默认输出到源文件同目录（`同名.md`）；加 `--output` 可指定目录

## 注意事项

- 图片和音频需要 AI Vision / Whisper API，本地无密钥时会报错或返回空内容；其他格式完全离线
- 大文件（>50MB）建议加 `--stdout` 先预览，确认有内容再写文件
- ZIP 压缩包会尝试解析内部支持的文件
