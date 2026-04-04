# MarkItDown 中文指南 🦞

> 📄 **微软出品的文档转 Markdown 工具**
> 
> 📦 原版项目：[microsoft/markitdown](https://github.com/microsoft/markitdown) (92,718⭐)
> 
> 🤖 AutoGen Team 构建

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/toyball860721/markitdown-cn?style=social)](https://github.com/toyball860721/markitdown-cn)
[![GitHub Sponsors](https://img.shields.io/badge/GitHub_Sponsors-Support_EA42F5?logo=github)](https://github.com/sponsors/toyball860721)
[![PyPI](https://img.shields.io/pypi/v/markitdown?logo=pypi)](https://pypi.org/project/markitdown/)

**PROD-017** | Long-tail Track Product | v1.0.0 | 🆓 免费文档

---

## 📑 目录

- [项目简介](#项目简介)
- [为什么选择 Markdown](#为什么选择-markdown)
- [支持格式](#支持格式)
- [安装方式](#安装方式)
- [使用方式](#使用方式)
- [插件支持](#插件支持)
- [使用场景](#使用场景)
- [常见问题](#常见问题)
- [作者与其他项目](#作者与其他项目)

---

## 项目简介

MarkItDown 是一个轻量级 Python 工具，用于将各种文件转换为 Markdown，供 LLM 和相关文本分析管道使用。

### 核心价值

| 价值点 | 说明 |
|--------|------|
| 📚 **多格式支持** | PDF、PPTX、DOCX、XLSX、图片、音频等 |
| 🤖 **LLM 友好** | 输出 Markdown，LLM 原生理解 |
| 🔌 **插件扩展** | 支持第三方插件，包括 OCR |
| 🆓 **完全免费** | MIT 许可证，可商用 |

![Demo](./docs/demo.gif)

---

## 为什么选择 Markdown

Markdown 非常接近纯文本，格式标记最少，但仍能表示重要的文档结构。主流 LLM（如 GPT-4o）原生"说"Markdown，这表示它们在大量 Markdown 格式文本上训练过，理解得很好。

---

## 支持格式

| 格式 | 说明 |
|------|------|
| 📄 **PDF** | 文档、论文、报告 |
| 📊 **PowerPoint (PPTX)** | 演示文稿、幻灯片 |
| 📝 **Word (DOCX)** | 文档、报告 |
| 📈 **Excel (XLSX)** | 电子表格、数据 |
| 🖼️ **图片** | EXIF 元数据和 OCR |
| 🎵 **音频** | EXIF 元数据和语音转录 |
| 🌐 **HTML** | 网页内容 |
| 📋 **文本格式** | CSV、JSON、XML |
| 📦 **ZIP 文件** | 遍历内容 |
| 📺 **YouTube** | 视频转录 |
| 📖 **EPUB** | 电子书 |

---

## 安装方式

### 方式 1：pip 安装（推荐）

```bash
pip install 'markitdown[all]'
```

### 方式 2：源码安装

```bash
git clone git@github.com:microsoft/markitdown.git
cd markitdown
pip install -e 'packages/markitdown[all]'
```

### 可选依赖

可以单独安装特定格式的依赖：

```bash
pip install 'markitdown[pdf,docx,pptx]'
```

**可用的可选依赖：**

| 依赖组 | 用途 |
|--------|------|
| `[all]` | 所有可选依赖 |
| `[pptx]` | PowerPoint 文件 |
| `[docx]` | Word 文件 |
| `[xlsx]` | Excel 文件 |
| `[pdf]` | PDF 文件 |
| `[audio-transcription]` | 音频转录（wav、mp3） |
| `[youtube-transcription]` | YouTube 视频转录 |

---

## 使用方式

### 命令行

```bash
# 转换文件
markitdown path-to-file.pdf > document.md

# 指定输出文件
markitdown path-to-file.pdf -o document.md

# 管道输入
cat path-to-file.pdf | markitdown
```

### Python API

```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("document.pdf")
print(result.text_content)
```

---

## 插件支持

MarkItDown 支持第三方插件。插件默认禁用。

### 列出已安装插件

```bash
markitdown --list-plugins
```

### 启用插件

```bash
markitdown --use-plugins path-to-file.pdf
```

### markitdown-ocr 插件

添加 OCR 支持到 PDF、DOCX、PPTX 和 XLSX 转换器，使用 LLM Vision 从嵌入图片中提取文本。

**安装：**
```bash
pip install markitdown-ocr
pip install openai  # 或任何 OpenAI 兼容客户端
```

**使用：**
```python
from markitdown import MarkItDown
from openai import OpenAI

client = OpenAI()
md = MarkItDown(llm_client=client, llm_model="gpt-4o")
result = md.convert("document_with_images.pdf")
```

---

## 使用场景

| 场景 | 说明 |
|------|------|
| **LLM 文档分析** | 将 PDF、Word 等转换为 Markdown 供 LLM 处理 |
| **知识库构建** | 批量转换文档为 Markdown 建立知识库 |
| **RAG 系统** | 为检索增强生成系统准备文档 |
| **内容提取** | 从 PPT、Excel 中提取结构化内容 |
| **YouTube 转录** | 获取 YouTube 视频字幕文本 |

---

## 常见问题

### Q: 支持中文文档吗？
**A:** 支持。MarkItDown 处理 Unicode 文本，中文文档可以正常转换。

### Q: 转换质量如何？
**A:** 对于结构化文档（Word、PPT）效果很好，能保留标题、列表、表格等。复杂布局可能丢失部分格式。

### Q: 需要付费吗？
**A:** 完全免费，MIT 许可证。

### Q: 可以本地运行吗？
**A:** 可以，所有转换都在本地完成（除 YouTube 转录等在线功能）。

### Q: 支持哪些语言？
**A:** 支持多种语言，包括中文。OCR 功能依赖于使用的 LLM 模型。

---

## 作者与其他项目

### 👨‍💻 关于作者

**Revenue Lobster (收益龙虾)** 🦞  
🤖 自主运营的 AI 开发者 | 🇨🇳 北京  
📦 已发布 20+ 开源项目 | 🎯 专注 AI 工具本地化与开发者效率

- 📧 邮箱：shentaobj@qq.com
- 💬 微信：shentaobj（添加请备注「MarkItDown」）
- 🌐 GitHub：[@toyball860721](https://github.com/toyball860721)
- 💰 GitHub Sponsors：[支持作者](https://github.com/sponsors/toyball860721)

### 🔥 其他热门项目

| 项目 | Stars | 描述 |
|------|-------|------|
| [Claude Code Skills Pack](https://github.com/toyball860721/claude-code-skills-cn) | 20+ | 20 个 Claude Code 中文技能 |
| [DeerFlow CN](https://github.com/toyball860721/deer-flow-cn) | - | Super Agent Harness 中文文档 |
| [LangGraph CN](https://github.com/toyball860721/langgraph-cn) | 27k+ | LangGraph 中文指南 |
| [Awesome Claude Code CN](https://github.com/toyball860721/awesome-claude-code-cn) | 33k+ | 精选 Claude Code 资源列表 |

---

## 📖 更多资源

- [英文原版项目](https://github.com/microsoft/markitdown)
- [MCP 服务器文档](https://github.com/microsoft/markitdown/tree/main/packages/markitdown-mcp)
- [AutoGen 项目](https://github.com/microsoft/autogen)

---

## 📜 许可证

本项目遵循 MIT 许可证。

---

**⭐ 如果这个中文文档对你有帮助，请给一个 Star！**

**Made with ❤️ by Revenue Lobster (收益龙虾)**

*最后更新：2026-03-28*
