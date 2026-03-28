# MarkItDown 中文指南

> 📄 **微软出品的文档转 Markdown 工具**
> 
> 📦 原版项目：[microsoft/markitdown](https://github.com/microsoft/markitdown) (92,718⭐)
> 
> 🤖 AutoGen Team 构建
> 
> 📝 中文维护者：[@toyball860721](https://github.com/toyball860721)
> 
> ☕ 支持本项目：[爱发电](https://afdian.com/a/toyball) | [GitHub Sponsors](https://github.com/sponsors/toyball860721)

---

## 🚀 项目简介

MarkItDown 是一个轻量级 Python 工具，用于将各种文件转换为 Markdown，供 LLM 和相关文本分析管道使用。

**支持转换的格式：**
- PDF
- PowerPoint (PPTX)
- Word (DOCX)
- Excel (XLSX)
- 图片（EXIF 元数据和 OCR）
- 音频（EXIF 元数据和语音转录）
- HTML
- 文本格式（CSV、JSON、XML）
- ZIP 文件（遍历内容）
- YouTube 链接
- EPUB
- ... 等等！

---

## 🎯 为什么选择 Markdown？

Markdown 非常接近纯文本，格式标记最少，但仍能表示重要的文档结构。主流 LLM（如 GPT-4o）原生"说"Markdown，这表示它们在大量 Markdown 格式文本上训练过，理解得很好。

---

## 🛠️ 安装

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
| `[xls]` | 旧版 Excel 文件 |
| `[pdf]` | PDF 文件 |
| `[outlook]` | Outlook 邮件 |
| `[az-doc-intel]` | Azure 文档智能 |
| `[audio-transcription]` | 音频转录（wav、mp3） |
| `[youtube-transcription]` | YouTube 视频转录 |

---

## 💡 使用方式

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

## 🔌 插件支持

MarkItDown 支持第三方插件。插件默认禁用。

**列出已安装插件：**
```bash
markitdown --list-plugins
```

**启用插件：**
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

## 📊 MCP 服务器集成

MarkItDown 现在提供 MCP（Model Context Protocol）服务器，用于与 Claude Desktop 等 LLM 应用集成。

**安装：**
```bash
pip install markitdown-mcp
```

**配置：**
在 Claude Desktop 的 MCP 配置中添加：
```json
{
  "mcpServers": {
    "markitdown": {
      "command": "npx",
      "args": ["markitdown-mcp"]
    }
  }
}
```

---

## 📚 使用场景

| 场景 | 说明 |
|------|------|
| **LLM 文档分析** | 将 PDF、Word 等转换为 Markdown 供 LLM 处理 |
| **知识库构建** | 批量转换文档为 Markdown 建立知识库 |
| **RAG 系统** | 为检索增强生成系统准备文档 |
| **内容提取** | 从 PPT、Excel 中提取结构化内容 |
| **YouTube 转录** | 获取 YouTube 视频字幕文本 |

---

## ❓ 常见问题

### Q: 支持中文文档吗？

A: 支持。MarkItDown 处理 Unicode 文本，中文文档可以正常转换。

### Q: 转换质量如何？

A: 对于结构化文档（Word、PPT）效果很好，能保留标题、列表、表格等。复杂布局可能丢失部分格式。

### Q: 需要付费吗？

A: 完全免费，MIT 许可证。

### Q: 可以本地运行吗？

A: 可以，所有转换都在本地完成（除 YouTube 转录等在线功能）。

---

## 📖 更多资源

- [英文原版项目](https://github.com/microsoft/markitdown)
- [MCP 服务器文档](https://github.com/microsoft/markitdown/tree/main/packages/markitdown-mcp)
- [AutoGen 项目](https://github.com/microsoft/autogen)

---

## 🤝 参与贡献

欢迎提交 Issue 和 Pull Request 改进中文文档！

---

## 📄 许可证

本项目遵循 MIT 许可证。

---

## ☕ 支持作者

如果你觉得这个中文文档对你有帮助，欢迎支持：

- [爱发电](https://afdian.com/a/toyball)
- [GitHub Sponsors](https://github.com/sponsors/toyball860721)

**中文维护者持续更新中...** 🦞

*最后更新：2026-03-28*
