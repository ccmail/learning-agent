# 雅思阅读精读 Agent

## 项目简介
雅思阅读精读 Agent 是一个面向个人自学的智能学习助手，通过可复用的工程化架构，把雅思阅读的精读拆解为“文章理解、题目训练、词汇复现、学习记忆”四大模块。系统后端基于 FastAPI 与 LangChain 构建，可调用 GPT-5 模型完成段落分析、题目生成与错题解析；前端提供基于 Vue3 的 Web 交互界面，支持用户上传文章、实时查看精读报告，并同步学习进度。

项目目标是提供轻量、可扩展且易部署的学习体验，让用户能够在浏览器中完成文章精读、词汇复盘与个性化复盘的整套流程。

## 核心功能
- **文章理解**：自动完成段落划分、词汇解释、语法剖析、段落主旨与全文结构总结。
- **题目训练**：生成或解析雅思阅读常见题型（T/F/NG、填空、匹配等），并提供答案解析。
- **词汇复现**：提取高频核心词汇，生成同义替换、例句及测试练习，支持复盘与间隔重复。
- **学习记忆**：记录文章进度、错题统计、生词复现次数，结合 Memory 实现个性化复盘与推荐。
- **交互体验**：Web 界面支持文章上传/粘贴、实时展示精读结果与题目练习，提供结果导出与进度查看。

## 系统架构概览
```
frontend/                # Vue3 + Vite 前端工程
  ├─ src/pages/          # Reader 页面、统计页面
  ├─ src/components/     # 精读报告、题目、词汇等组件
  └─ src/store/          # Pinia 状态管理（学习进度、用户偏好）

app/                     # FastAPI + LangChain 后端
  ├─ main.py             # API 入口与路由注册
  ├─ config.py           # 环境配置（OpenAI Key、数据库）
  ├─ agents/             # 雅思精读 Agent、工具注册与 Prompt 模板
  ├─ services/           # 文章分析、题目生成、词汇处理等领域服务
  ├─ memory/             # 会话记忆、长期记忆与数据库交互
  └─ models/             # Pydantic 模型与数据库 ORM 定义

database/                # SQLite 初始化脚本、迁移文件
scripts/                 # 部署与运维脚本（可选）
```
> 目录结构展示了项目的工程化拆分，便于后续扩展与部署。

## 技术栈
- **前端**：Vite、Vue3、Pinia、Tailwind CSS / Ant Design Vue（可选）
- **后端**：Python 3.11、FastAPI、LangChain、Pydantic、SQLModel/SQLAlchemy
- **模型服务**：OpenAI GPT-5 API（可替换为其他兼容 OpenAI 接口的模型）
- **数据存储**：SQLite（本地开发），后续可无缝迁移到 Supabase/PostgreSQL
- **部署**：Vercel / Cloudflare Workers / Fly.io（根据使用场景选择）

## 快速开始
1. **克隆项目**
   ```bash
   git clone <your-repo-url>
   cd learning-agent
   ```
2. **准备环境变量**
   - 复制 `.env.example`（若不存在可创建）为 `.env`，填写 `OPENAI_API_KEY`、`DATABASE_URL` 等。
3. **安装后端依赖并启动 API**
   ```bash
   cd app
   pip install -r requirements.txt
   uvicorn main:app --reload
   ```
4. **安装前端依赖并启动开发服务器**
   ```bash
   cd frontend
   pnpm install   # 或 npm install / yarn
   pnpm dev
   ```
5. **访问应用**
   - 打开浏览器访问 `http://localhost:5173`，在前端界面上传雅思文章，即可实时查看精读报告与题目练习。

## 开发路线
1. **MVP 原型**：打通段落分析 → 返回词汇解释与主旨总结的完整流程。
2. **记忆系统**：引入数据库与 Memory，记录用户文章与错题数据。
3. **Agent 化**：使用 LangChain Agent & Tools，支持智能任务拆解与工具调用。
4. **Web UI**：完善前端交互，展示精读报告、题目与统计信息。
5. **上线部署**：通过 Vercel/Cloudflare/Fly.io 部署，提供外部访问能力。

## 贡献指南
- Fork 项目后提交 PR，PR 中请简要说明变更内容与测试结果。
- 提交代码前运行单元测试、格式化代码，并在 README 或文档中补充必要说明。

如需进一步的功能规划或模块拆解，可在 Issues 中提出需求，或直接开启新阶段的开发任务。
