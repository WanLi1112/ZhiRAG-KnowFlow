# 知汇 · ZhiRAG

> 面向多源课程资料的 RAG 智能学习助手

## 📖 项目简介

**知汇（ZhiRAG）** 是一个基于 RAG（检索增强生成）技术的智能学习助手，旨在帮助大学生整合教材、PPT、试题等多源课程资料，实现精准问答与自动复习卡片生成，提升复习效率。

项目针对当前大学生学习资料分散、通用AI工具缺乏课程针对性的痛点，设计并实现一套**多源异构资料混合检索 + 重排序 + 复习卡片生成**的系统方案。

## 🎯 核心功能

-   **多源资料整合**：支持上传教材（PDF）、PPT、试题等资料，自动提取文字内容构建知识库
    
-   **混合检索**：融合语义检索（向量）与关键词检索（BM25），结合重排序（Rerank）优化检索结果
    
-   **智能问答**：基于自有知识库精准回答课程相关问题，答案可追溯来源
    
-   **复习卡片生成**：自动将知识点扩展为结构化复习卡片（定义、例题、出处、常见错误）
    

## 🧑‍💻 团队成员

| 成员 | 角色 | 职责 |
| --- | --- | --- |
| 李婉尔 | 项目负责人 | 统筹协调、系统设计文档、测试、路演答辩 |
| 刘源宜 | 技术负责人 | 后端核心开发（检索、重排序、卡片生成、API） |
| 刘嘉雯 | 前端负责人 | Gradio 界面开发、用户体验测试 |
| 赵清睿 | 路演主理人 | 路演展示、PPT、演讲稿、演示视频 |

## 🛠️ 技术栈

-   **后端**：Python 3.10+
    
-   **前端**：Gradio
    
-   **向量数据库**：ChromaDB
    
-   **检索框架**：LangChain
    
-   **PDF解析**：MinerU
    
-   **大模型API**：智谱AI / DeepSeek
    
-   **重排序模型**：bge-reranker-v2-m3
    
-   **版本控制**：Git / GitHub
    

## 📁 项目结构

```
ZhiRAG/
├── src/
│   ├── api.py              # 主接口（问答、卡片生成）
│   ├── retriever.py        # 混合检索 + 重排序
│   ├── reranker.py         # 重排序模块
│   ├── card_generator.py   # 复习卡片生成
│   ├── chunking.py         # 文档切片
│   └── embedder.py         # 向量化
├── app.py                  # Gradio 前端入口
├── data/                   # 测试数据集
├── docs/                   # 设计文档
├── requirements.txt        # Python 依赖
├── README.md               # 本文件
└── .gitignore
```

## 🚀 快速开始

### 1\. 克隆仓库

```
git clone git@github.com:your-username/ZhiRAG.git
cd ZhiRAG
```

### 2\. 安装依赖

```
pip install -r requirements.txt
```

### 3\. 配置 API Key

在 `src/config.py` 中配置智谱或 DeepSeek 的 API Key。

### 4\. 准备数据

将教材 PDF 放入 `data/` 目录，运行预处理脚本：

```
python src/preprocess.py --input data/your_textbook.pdf
```

### 5\. 启动服务

```
python app.py
```

访问特定网站即可使用。

## 🤝 协作规范

### 分支策略

本仓库采用 **Git Flow** 简化版，主要分支如下：

| 分支 | 用途 | 说明 |
| --- | --- | --- |
| main | 稳定版本 | 只接受来自 dev 的合并，禁止直接推送 |
| dev | 开发主分支 | 日常开发的集成分支，所有功能分支合并到这里 |
| feature/* | 功能分支 | 从 dev 切出，完成后合并回 dev |
| hotfix/* | 紧急修复 | 从 main 切出，修复后同时合并到 main 和 dev |

**命名规范**：

-   功能分支：`feature/功能名称`，如 `feature/mixed-retrieval`
    
-   修复分支：`hotfix/问题简述`，如 `hotfix/api-timeout`
    

### 提交信息格式

提交信息采用 **Conventional Commits** 规范：

```
<type>(<scope>): <subject>

[body]
```

**type 类型**：

| type | 说明 | 示例 |
| --- | --- | --- |
| feat | 新增功能 | feat(retriever): add BM25 retrieval |
| fix | 修复 Bug | fix(api): fix timeout error |
| docs | 文档更新 | docs(readme): update setup guide |
| style | 代码格式（不影响逻辑） | style(app): format with black |
| refactor | 重构代码 | refactor(chunking): optimize text split |
| test | 测试相关 | test(retriever): add unit tests |
| chore | 构建/工具变动 | chore(deps): update langchain |

**scope** 可选范围：

-   `retriever` - 检索模块
    
-   `reranker` - 重排序模块
    
-   `card` - 卡片生成模块
    
-   `api` - 接口层
    
-   `frontend` - 前端界面
    
-   `docs` - 文档
    

**提交示例**：

```
git commit -m "feat(retriever): add hybrid search with BM25 and vector"
git commit -m "fix(api): resolve connection timeout when calling LLM"
git commit -m "docs(readme): add deployment instructions"
```

### 工作流程

1.  从 `dev` 分支切出新功能分支：
    
    ```
    git checkout dev
    git pull origin dev
    git checkout -b feature/your-feature-name
    ```
    
2.  开发完成后，推送到远程仓库：
    
    ```
    git push origin feature/your-feature-name
    ```
    
3.  在 GitHub 上发起 Pull Request，目标分支为 `dev`。
    
4.  至少一名团队成员 Review 后合并。
    
5.  定期将 `dev` 合并到 `main` 发布稳定版本。
    

### 代码规范

-   Python 代码遵循 **PEP 8** 规范。
    
-   建议使用 `black` 和 `isort` 格式化代码。
    
-   每个函数/类必须包含 docstring。
    
-   敏感信息（如 API Key）禁止硬编码，统一放入 `config.py` 或 `.env` 文件。
    

## 📄 License

本项目为上海大学大学生创新训练计划项目成果，仅供学术研究使用。

## 🙏 致谢

感谢指导老师徐伟老师的技术支持与资源协助。

\[file content end\]
