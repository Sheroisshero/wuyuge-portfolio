# 知栈 · 企业知识库问答

> 每个答案都能回到原文。

收录于 [吴宇歌个人作品集 2026](https://sheroisshero.github.io/wuyuge-portfolio/#p06)。

课程实战复现：React 19 + NestJS + LangChain.js + pgvector，复刻类火山方舟知识库的核心链路。

## 为什么做

企业知识散在 PDF、Excel、Wiki 里，搜索靠关键词，问一句"这个流程要走几步"就只能人工翻。专用向量库方案又要多维护一套存储，业务库和向量库双写，一致性出了问题很难查。

## 它是什么

知栈是一个 TypeScript 全栈 RAG 知识库：文档入库、自动切片、向量化、混合检索、带引用回答，SSE 流式输出。存储只用一份 PostgreSQL + pgvector，业务元数据与向量表同库。

## 四层架构

Web 前端（React 19 · 知识库 / 文档 / 切片 / 问答）→ API 层（NestJS · SSE 流式 · 入库 / 检索 / 问答）→ RAG 引擎（LangChain.js · Loader → Splitter → Embedding → Retrieval → Prompt）→ 存储层（PostgreSQL + pgvector，业务表与向量表同库）。

同一份 PostgreSQL 里既有 knowledge_bases / documents，也有 rag_chunks 向量表——少一套双写，就少一类一致性事故。

## 可公开的技术细节

- 切片：RecursiveCharacterTextSplitter，按标点与段落递归，保留 chunkNo 便于回溯。
- 检索：按 kbId 过滤后再做相似度，避免跨库串答案。
- 流式：SSE 推送 token，前端边收边渲染，首字延迟明显下降。
- 契约层：Zod schema + 共享 DTO，前后端不靠口头约定。
- FDE 视角：先问规模与运维现状，再决定要不要引入专用向量库。
- 评测：以"答案可回溯到原文片段"为第一标准，而不是只看回答流畅度。

## 存储选型判断

| 方案 | 优势 | 代价 |
| --- | --- | --- |
| 专用向量库 + 业务库 | 检索性能强 | 两套存储、双写一致性、运维成本高 |
| PostgreSQL + pgvector | 一套存储、事务一致 | 大规模场景需调优 |

结论：知识库规模在千万级 chunk 以内、且已有 PG 运维能力时，同库存储的收益大于专用向量库的性能优势。

## 亮点

- 同库存储，避免双写不一致。
- 链路透明：Loader → Splitter → Embedding → Retrieval → Prompt → Streaming，每步可观测、可替换。
- 多知识库隔离：chunk 元数据带 kbId / documentId / chunkNo，检索按 kbId 过滤。
- 可交付：pnpm monorepo，前后端共享 DTO 与流式事件类型，一条命令起 PG。

—— 吴宇歌 · 新加坡国立大学 科学人工智能硕士
