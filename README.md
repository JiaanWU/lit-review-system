# 文献阅读系统 · 第二题作业

社科院研究生期末作业 · 第二题（50 分）。本仓库是一套可复用的文献阅读流程：三个 Skill 负责「检索—精读—归档」，一个研究边际 Agent 负责「判断还有哪一块值得做」，同一研究问题跑两轮，第二轮专门寻找最可能推翻第一轮判断的证据。

- 任务书：[第二题-文献阅读系统.md](第二题-文献阅读系统.md)
- 流程图：[第二题-流程结构.html](第二题-流程结构.html)
- 仓库：https://github.com/JiaanWU/lit-review-system

## 研究问题

**算力基础设施部署是否提升了企业创新质量？**

已有研究回答的是「算力是否增加了创新数量」：谷城等（2026）以国家超算中心设立为冲击，识别算力供给的技术创新效应；王倩等（2026）进一步发现智能算力部署促进企业跨区域技术合作。两文的结果变量都偏向创新的规模与协作范围，尚未回答创新的**质量**是否同步提升。

本研究的边际在于：在同一政策情境（国家超算中心 / 智能算力部署）下，把结果变量从「专利数量、合作范围」换成「发明专利占比、专利被引」，检验是否存在**数量扩张而质量滞后**的结构性差异，并说明该差异在何种企业规模与行业中更明显。

> 该问题为初稿。第一轮备忘录可能将其收窄、改写或放弃，实际定稿以 `rounds/round1/memo-1.md` 第 6 节为准。

**入选标准**：2021–2026 年；CSSCI 或北大核心；题名或摘要同时涉及「算力 / 超算 / 数据中心」与「创新 / 专利 / 研发」；同一论文的工作稿与期刊版计一篇。

## 目录与工具路径

| 路径 | 内容 |
|---|---|
| `skills/search/SKILL.md` | 文献搜索 Skill：渠道优先级、检索式构造、筛选与去重、访问受限记录 |
| `skills/read/SKILL.md` | 论文精读 Skill：六类字段、定位标注、附录触发条件、仅摘要时的限制 |
| `skills/archive/SKILL.md` | 文献归档 Skill：命名、索引、双向链接、重复检测、反向链接核查 |
| `agents/research-margin.md` | 研究边际 Agent：四维度并排比较、边际定位、推翻条件、证据不足处理 |
| `vault/` | Obsidian 文献库，用 Obsidian 直接打开该文件夹 |
| `materials/` | 入选论文的材料摘录（Markdown，含版本与原文定位） |
| `rounds/round1/` | 第一轮：`search-log.md`、`cnki-raw.json`、`memo-1.md`、`archive-check.md` |
| `rounds/round2/` | 第二轮：`search-log.md`、`cnki-raw.json`、`memo-2.md`、`verification.md`、`archive-check.md` |
| `sources/` | 论文原始 PDF / 附录，本地留存，因版权与体积不入库（见 `.gitignore`） |

## 调用方式

本项目采用**「按 README 顺序逐份读取并执行」**，不依赖工作台把项目内 Skill 注册为原生命令。原因：三个 `SKILL.md` 位于项目目录而非工作台的全局技能目录，工作台不会自动发现它们；逐份读取可保证教师在任何支持文件读取的工作台中复现。

一次完整调用按下列顺序，每一步的输出即下一步的输入：

```
README.md §研究问题
  → skills/search/SKILL.md      → rounds/roundN/search-log.md + cnki-raw.json
  → skills/read/SKILL.md        → materials/*.md + vault/10-论文笔记/*.md
  → skills/archive/SKILL.md     → vault/00-索引/*、vault/20-主题笔记/*、archive-check.md
  → agents/research-margin.md   → rounds/roundN/memo-N.md
  → 本人回查                     → rounds/round2/verification.md
```

可直接粘贴的启动请求：

> 请读取 `README.md` 与研究问题，按「调用方式」一节的顺序依次读取并执行 `skills/search/SKILL.md`、`skills/read/SKILL.md`、`skills/archive/SKILL.md` 与 `agents/research-margin.md`，保存本轮检索记录、论文笔记、归档索引与第一轮备忘录，列出全部产物路径，完成后停止等待检查。

第二轮请求：

> 请读取 `README.md` 与 `rounds/round1/memo-1.md`，围绕第 7 节的推翻条件补检，用同一套 Skill 处理材料，读取同一个 Agent 定义形成 `rounds/round2/memo-2.md`，比较原判断、补检结果与更新理由，保留第一轮全部文件。

## 环境与配置

| 项 | 配置 |
|---|---|
| 文献库 | 本地 Zotero `C:\Users\31008\Zotero`；检索时只读副本置于 `sessions/zotero-copy/`，不写原库 |
| 知网 | Edge 以独立 profile 启动并通过 CDP 暴露于 `127.0.0.1:9222`，登录机构账号后由其代为检索、抓取题录、下载 PDF |
| Obsidian | 直接以 `vault/` 作为库打开；不使用全局库 `D:\ObsidianVault` |
| Git | 提交身份 `JiaanWU <3100812827@qq.com>`；OAuth 凭据经 `gh auth setup-git` 配置 |

## 实际运行记录

> 按任务书第 72 行要求填写：调用顺序、关键输入、产物路径、重复归档与反向链接核查结果、本人回查结论。待两轮执行完成后补全。

| 阶段 | 读取的定义 | 关键输入 | 产物 |
|---|---|---|---|
| 待补 | | | |

## 提交与追溯

| 项 | 链接 |
|---|---|
| 仓库 | https://github.com/JiaanWU/lit-review-system |
| 首轮结果 commit | 待补 |
| 最终 commit | 待补 |

首轮 commit 对应「第一轮备忘录完成、第二轮尚未开始」的状态，便于教师对照第二轮及后续修改。
