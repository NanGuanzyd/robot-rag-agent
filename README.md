# 智扫通机器人智能客服

基于 **LangChain + LangGraph + Streamlit** 的扫地机器人智能客服系统，集成 RAG 检索增强生成与 ReAct Agent 自主推理能力。

## 技术栈

| 技术 | 用途 |
|------|------|
| Python 3.11 | 运行时 |
| Streamlit | Web UI |
| LangChain / LangGraph | Agent 框架 |
| 通义千问 qwen3-max | 推理模型 |
| DashScope text-embedding-v4 | 向量化引擎 |
| ChromaDB | 向量数据库 |

## 功能特性

- 🔍 **RAG 检索增强**：基于扫地机器人专业知识库（选购指南、故障排除、维护保养）进行精准回答
- 🤖 **ReAct Agent**：自主决策调用工具，支持天气查询、位置获取、外部数据检索等 7 个工具
- 📊 **个性化报告生成**：根据用户使用数据自动生成 Markdown 格式的使用报告与保养建议
- 🔄 **动态提示词切换**：通过中间件机制在不同场景间自动切换系统提示词

## 快速开始

### 1. 安装依赖

```bash
pip install -r requirements.txt
```

### 2. 设置 API Key

```bash
# Windows CMD
set DASHSCOPE_API_KEY=你的阿里云DashScope-API-Key

# Windows Git Bash / Linux / macOS
export DASHSCOPE_API_KEY=你的阿里云DashScope-API-Key
```

> 前往 [阿里云 DashScope 控制台](https://dashscope.console.aliyun.com/) 获取 API Key。

### 3. 启动应用

```bash
streamlit run app.py
```

浏览器访问 `http://localhost:8501` 即可使用。

## 项目结构

```
.
├── app.py                  # Streamlit 入口
├── agent/                  # Agent 核心
│   ├── react_agent.py      # ReAct Agent 主类
│   └── tools/
│       ├── agent_tools.py  # 7 个工具定义
│       └── middleware.py   # 中间件（日志、监控、提示词切换）
├── model/
│   └── factory.py          # 模型工厂（ChatTongyi + Embedding）
├── rag/
│   ├── rag_service.py      # RAG 总结服务
│   └── vector_store.py     # ChromaDB 向量存储
├── config/                 # YAML 配置文件
├── prompts/                # Prompt 模板文件
├── data/                   # 知识库文档 + 模拟数据
├── utils/                  # 工具类（日志、配置、文件处理）
└── logs/                   # 运行日志
```

## 应用截图

启动后界面包含：
- 对话输入框：输入扫地机器人相关问题
- 流式输出：实时显示客服回复内容
- 会话保持：自动保留对话历史
