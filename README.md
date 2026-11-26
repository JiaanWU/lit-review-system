# 文献阅读系统 · 第二题作业

社科院研究生期末作业 · 第二题（50 分）。本仓库是一套可复用的文献阅读流程：三个 Skill 负责「检索—精读—归档」，一个研究边际 Agent 负责「判断还有哪一块值得做」，同一研究问题跑两轮，第二轮专门寻找最可能推翻第一轮判断的证据。

- 任务书：[第二题-文献阅读系统.md](第二题-文献阅读系统.md)
- 流程图：[第二题-流程结构.html](第二题-流程结构.html)
- 仓库：https://github.com/JiaanWU/lit-review-system

## 研究问题

**算力基础设施部署如何改变企业创新质量在企业之间的分布？**

已有研究分两层。**数量层**：谷城等（2026）以国家超算中心设立为冲击，识别算力供给对专利申请数量的效应，并用同城企业专利申请数的变异系数检验「创新鸿沟」；王倩等（2026）发现智能算力部署促进企业跨区域技术合作。**质量层**：徐振华（2026）与张纪录（2026）以绿色口径、余明桂等（2026）以 AI 口径、谢璇等（2026）以数字技术口径，分别报告算力提升了创新质量；其中谢璇等还比较了**大企业与小企业**的质量效应差异。

两层合起来给出一个明确的空白：**质量一侧停在均值与分组均值**。五种质量度量（发明专利占比、绿色创新质量、绿色量质并置、AI 创新质量、数字技术创新质量）没有一种报告过企业间的离散度、分位差或基尼系数；唯一的分布度量（变异系数）落在数量上；谢璇的规模异质性是比较两个分组的均值，不是对离散程度的度量。

本研究的边际因此不是「研究质量」，也不是「检验企业间质量差异」，而是**「把质量差距当作连续分布统计量来估计」**：在同一政策情境与同一数据窗口下，把谷城的变异系数检验从数量口径换成质量口径，并把两组结果并列，检验「数量差距收敛」与「质量差距收敛」是否同向。

> 第一轮提出该方向（`rounds/round1/memo-1.md` 第 6 节），第二轮补检后**收窄并保留**（`rounds/round2/memo-2.md` 第 4 节）。收窄要点：同时报告均值与分布、质量口径用两个指标（发明专利占比 + 被引或维持年限）、锁定 2007–2023 与谷城（2026）可比。
>
> **两次边界更正，均因发现漏检文献**。第一次（11-26 23:40）：补录余明桂等（2026，《经济研究》第 8 期）后，「尚未回答质量是否提升」不再成立——非绿色口径的质量均值已有顶刊工作，表述改为「均值已做、分布未做」。第二次（11-27 00:50）：召回补正核查捞出谢璇等（2026，《经济与管理研究》47(7)），该文与谷城同政策、同样本、同方法，且报告「大企业数量、小企业质量」的异质性——**按规模分组的质量差异也被做掉了**，表述再收窄为「分组均值已做、连续分布未做」。
>
> 两处漏检的原因不同：余明桂是关键词不含「创新质量」；谢璇是主题词用「数字技术创新」而非「创新」，落在检索式词面之外。核查过程见 `rounds/round2/recall-check.md`，归档见 `vault/10-论文笔记/` 序号 7、8（均为仅摘要）。

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
| `rounds/round2/` | 第二轮：`search-log.md`、`cnki-raw.json`、`memo-2.md`、`verification.md`、`citation-tracing.md`、`recall-check.md` |
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

| 阶段 | 读取的定义 | 关键输入 | 产物 |
|---|---|---|---|
| 首轮·检索 | `skills/search/SKILL.md` | README 研究问题、Zotero 本地库、知网机构会话 | `rounds/round1/search-log.md`、`cnki-raw.json` |
| 首轮·精读 | `skills/read/SKILL.md` | search-log 入选清单 6 篇 | `materials/*.md`（6）、`vault/10-论文笔记/*.md`（6） |
| 首轮·归档 | `skills/archive/SKILL.md` | 6 篇笔记 | `vault/00-索引/*`、`vault/20-主题笔记/*`、`archive-check.md` |
| 首轮·判断 | `agents/research-margin.md` | 研究问题 + 检索记录 + 归档笔记 | `rounds/round1/memo-1.md` |
| 二轮·检索 | `skills/search/SKILL.md` | memo-1 第 7 节的三条推翻条件 | `rounds/round2/search-log.md`、`cnki-raw.json` |
| 二轮·判断 | 同一份 `agents/research-margin.md` | memo-1 + 补检结果 | `rounds/round2/memo-2.md`（另存） |
| 二轮·引文追溯 | `skills/search/SKILL.md`（引文追溯条款） | 两篇全文 PDF、知网 `RF=参考文献` 字段 | `rounds/round2/citation-tracing.md` |
| 二轮·回查 | 无（本人执行） | 三处原文 + Obsidian Backlinks 面板 | `rounds/round2/verification.md` |
| 二轮·补充归档 | `skills/archive/SKILL.md` | 引文追溯发现的漏检文献 1 篇（余明桂等 2026） | `materials/余明桂2026.md`、`vault/10-论文笔记/余明桂2026-公共算力与AI创新.md`、索引与两篇主题笔记同步更新、`archive-check.md` 第五节 |
| 二轮·召回补正 | `skills/search/SKILL.md`（访问受限与召回缺口条款） | `search-log.md` 第五节的补正措施 | `rounds/round2/recall-check.md`、`materials/谢璇2026.md`、`vault/10-论文笔记/谢璇2026-超算中心与数字技术创新.md`、`archive-check.md` 第六节 |

关键结果：T1「算力 × 创新质量 × 分布」零命中，T4、T5 两个补充表述同样零命中，同会话对照 T0 返回 9 条以排除限流误判；三条推翻条件均未触发，方向收窄保留。引文追溯：后向 97 条参考文献中质量与分布类词汇零命中，前向反查 17 条无一条涉及质量分布。召回补正：把算力类词扩到「智算」「人工智能计算中心」、质量轴扩到单字「质量」后，同一题目得 208 条，是 T0 的 23 倍；分布轴加宽检索仍为零。

**两次边界更正，都是自己发现自己改的。**

第一次（11-26 23:40）：引文追溯捞出余明桂等《数字基础设施建设、公共算力供给与AI创新》（《经济研究》2026 年第 8 期）。该文摘要含「AI 创新质量」而关键词不含「创新质量」，主题检索未命中。据此把边界由「没人做质量」改为「**均值已做、分布未做**」。

第二次（11-27 00:50）：召回补正核查捞出谢璇等《算力基础设施如何影响企业数字技术创新?》（《经济与管理研究》2026 年第 7 期）。该文与谷城同政策冲击、同样本窗口、同方法，且报告「大企业数量、小企业质量」的异质性——**按规模分组的质量差异已有人做**。边界再收窄为「**分组均值已做、连续分布未做**」，并把设计改为「质量鸿沟与数量鸿沟并列，检验两者是否同向」。

两处漏检均未事后修饰：T0 的 9 条清单、第一轮全部文件、`memo-1.md` 一律保持原样，更正以带时间戳的补记方式追加。

现有 8 篇归档：全文精读 2 篇、仅摘要 6 篇；重复归档 0 条；反向链接 8 对中 6 对为文件级与面板双重校验、2 对仅文件级（面板未再复核，已如实标注）。

## 提交与追溯

| 项 | 链接 |
|---|---|
| 仓库 | https://github.com/JiaanWU/lit-review-system |
| 首轮结果 commit | https://github.com/JiaanWU/lit-review-system/commit/feebde1 |
| 最终 commit | https://github.com/JiaanWU/lit-review-system/commit/a56f24a |

首轮 commit `feebde1` 对应「第一轮备忘录完成、第二轮尚未开始」的状态，便于教师对照第二轮及后续修改。`a56f24a` 为全部内容交付物齐备（两轮产物、本人回查、引文追溯、漏检文献补录与边界更正）的提交；其后提交为 Obsidian 配置、忽略规则、本表链接与个别表述的精确化，不改变任何结论。完整历史：https://github.com/JiaanWU/lit-review-system/commits/main
