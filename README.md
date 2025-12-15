# 🏆 DuoKui-LLM (夺魁)

> **专为高标准投标场景设计的私有化 LLM Agent 解决方案。**
>
> **口号：** 让 AI 深度理解公文和项目标书规范，只需上传模版及项目需求，即可一键撰写项目标书，解放广大研究牲通同胞，助力你的导师一举夺魁。

## 🚀 项目简介 (Introduction)

**DuoKui-LLM** 是一个基于 **RAG（检索增强生成）** 与 **轻量级微调** 技术构建的私有化投标 Agent。

传统的大模型在处理国企和大型项目标书时，常出现**格式错误、行文不规范（缺乏“官方腔”）、数据准确性差**等问题。本项目旨在通过定制化的数据工程和多 Agent 工作流，解决这些核心痛点，确保生成的标书**格式严谨、内容准确、风格契合**。

**核心解决的问题：**

1.  **高精度内容生成：** 将准确的业绩、资质数据与 AI 深度融合。
2.  **公文风格定制：** 通过微调，使模型具备严谨的“标书体”和“公文写作风格”。
3.  **数据安全保障：** 100% 私有化部署，确保敏感投标数据绝不外泄。

## ✨ 主要特性 (Features)

  * **RAG 驱动的准确性：** 内置**三层知识库**（业绩库、资质库、语料库），确保关键数据（如合同金额、人员资质）的准确引用。
  * **私有化 LoRA 微调：** 提供微调脚本，允许用户使用企业历史中标数据，定制专属的行文风格模型。
  * **多 Agent 协作流：** 实现从 **[Planner]**（招标文件解析）到 **[Writer]**（内容生成）再到 **[Reviewer]**（格式与关键词校验）的完整标书撰写流程。
  * **格式自动对齐：** 基于 `python-docx` 或其他工具，自动将生成的文本填充到预设的 Word 模板中，保持国企要求的排版标准。
  * **高安全性设计：** 全局支持容器化部署，数据不触碰任何公有云接口。

## 🧱 核心技术架构 (Architecture)

**DuoKui-LLM** 采用 RAG + Fine-tuning 的双核模式，确保内容质量与风格高度统一。

$$\text{DuoKui} = \text{高质量语料} \oplus \text{RAG（准确性）} \oplus \text{LoRA（风格性）}$$

### 技术栈

| 组件 | 推荐技术 | 作用 |
| :--- | :--- | :--- |
| **LLM 基座** | Qwen, DeepSeek 或其他国产开源模型 | 提供强大的中文理解和生成能力。 |
| **向量数据库** | Milvus / Chroma | 存储和检索历史标书、业绩数据。 |
| **后端框架** | Python (FastAPI / Flask) | 提供 API 服务和 Agent 调度。 |
| **Agent 框架** | LangChain / LlamaIndex | 管理 RAG 流程和多智能体交互。 |
| **文档处理** | Unstructured, python-docx | 复杂文档解析和最终 Word 输出。 |

## 🛠️ 快速上手 (Getting Started)

### 环境要求

  * Python 3.9+
  * 至少 XX GB 显存 (推荐配置：NVIDIA RTX 4090 或更高级别 GPU 用于微调和推理)

### 1\. 克隆项目

```bash
git clone https://github.com/lsysysu/DuoKui-LLM.git
cd DuoKui-LLM
```

### 2\. 环境配置

```bash
pip install -r requirements.txt
# 设置环境变量，指向您的本地模型路径
export LLM_MODEL_PATH="/path/to/your/qwen-local"
```

### 3\. 数据准备 (Data Prep)

将您的历史标书文件（.docx/.pdf）放置在 `./data/raw` 目录下，然后运行数据处理脚本：

```bash
python scripts/data_preprocessing.py
```

> *（该脚本会执行清洗、切片和向量化，并构建基础知识库。）*

### 4\. 运行 Agent 服务

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

访问 `http://localhost:8000/docs` 查看 API 文档。


## 🤝 贡献 (Contributing)

欢迎所有对 **LLM 应用、RAG、公文写作、私有化部署**等方向感兴趣的开发者贡献代码！


## 📄 许可证 (License)

本项目遵循 **MIT License** 或 **Apache 2.0 License**。

