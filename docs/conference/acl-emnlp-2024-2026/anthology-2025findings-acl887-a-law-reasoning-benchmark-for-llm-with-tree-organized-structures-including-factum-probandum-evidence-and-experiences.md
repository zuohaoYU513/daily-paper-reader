---
title: "A Law Reasoning Benchmark for LLM with Tree-Organized Structures including Factum Probandum, Evidence and Experiences"
title_zh: 面向大语言模型的、含待证事实、证据和经验树状结构的法律推理基准
authors: "Jiaxin Shen, Jinan Xu (徐金安), Huiqi Hu, Luyi Lin, Guoyang Ma, Fei Zheng, Fandong Meng, Jie Zhou, Wenjuan Han"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.887.pdf"
tags: ["query:evidence-qa"]
score: 4.0
evidence: 含树状待证事实与证据结构的法律推理基准
tldr: 本工作提出透明的法律推理范式，要求大模型根据案件文本输出包含层次化待证事实、证据和隐含经验的树状结构，以支撑并论证最终裁决，使法律推理可被公开检验、避免偏见。作者构建了首个众包数据集用于评测，并提出TL智能体集成多种法律分析工具来完成该任务。该基准推动法律推理评测从终局正确性走向过程透明度。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 792, \"height\": 817, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 578, \"height\": 746, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1406, \"height\": 799, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 643, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 647, \"height\": 354, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 646, \"height\": 326, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1644, \"height\": 699, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1284, \"height\": 1048, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1307, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1285, \"height\": 709, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1307, \"height\": 575, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1639, \"height\": 1255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1641, \"height\": 1077, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1654, \"height\": 795, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1645, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1618, \"height\": 409, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl887/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1633, \"height\": 986, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 643, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 647, \"height\": 289, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 810, \"height\": 425, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1660, \"height\": 866, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1455, \"height\": 949, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1659, \"height\": 637, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl887/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1655, \"height\": 463, \"label\": \"Table\"}]"
motivation: 法律推理对公平裁判至关重要，但现有评测缺少树状、可检验的结构化推理任务。
method: 建立待证事实-证据-经验的层次化法律推理模式，提出TL智能体并配套众包基准数据集。
result: 构建首个众包法律推理树基准，使LLM可生成可审查的裁判说理结构。
conclusion: 结构化、证据锚定的树状推理基准能提高法律推理的可信性和去偏性。
---

## Abstract
While progress has been made in legal applications, law reasoning, crucial for fair adjudication, remains unexplored. We propose a transparent law reasoning schema enriched with hierarchical factum probandum, evidence, and implicit experience, enabling public scrutiny and preventing bias. Inspired by this schema, we introduce the challenging task, which takes a textual case description and outputs a hierarchical structure justifying the final decision. We also create the first crowd-sourced dataset for this task, enabling comprehensive evaluation. Simultaneously, we propose TL agent that employs a comprehensive suite of legal analysis tools to address the challenge task. This benchmark paves the way for transparent and accountable AI-assisted law-reasoning in the “Intelligent Court”.

---

## 论文详细总结（自动生成）

## 论文详细总结

### 一、核心问题与研究动机

- **问题定位**：现有法律 AI 研究多聚焦于“法律适用”（如罪名预测、判决结果预测、文书摘要），忽略了对司法公正同样关键的“法律推理”环节——即如何从证据材料与间接事实出发，逻辑严谨地构建“最终犯罪事实”。
- **现实痛点**：裁判不公往往源于“经验”的误用。例如著名的 *Rex v. Bywaters and Thompson* 案与国内“南京彭宇案”中，不同经验假设可导向截然不同的犯罪事实认定；这类过程若不透明，无法被公众审查，将损害司法公信力。
- **研究目标**：设计一套**透明、可审计的树状法律推理框架**，将法官心证过程显式化——让证据、中间事实（待证事实）、终极待证事实及所依赖的“人类经验”都可视化，从而有效减少偏见并增强裁决说服力，为“智能法庭”奠定基础。

### 二、方法论

1. **核心思想——法律推理模式（Schema）**
   - 受 Wigmore 图示法与 Anderson 等改进版图示法的启发，构建了一个嵌套树状推理框架，涵盖四种核心元素：
     - **证据（Evidence）**：案卷文本中的最底层事实；
     - **待证事实（Factum Probandum）**：细分为中间待证事实（interim probandum）与终极待证事实（ultimate probandum），粗粒度事实由细粒度事实逐级支撑；
     - **经验（Experience）**：证据连接到事实、事实汇聚为更粗事实时依赖的人类常识与社会经验；
     - **推理边（Inference）**：自下而上的推理关系，即 r: v → f，且该推理在经验 e 下生效。

2. **任务定义——TL（Transparent Law-Reasoning with Tree-Organized Structures）**
   - 输入：非结构化的案件文本描述；
   - 输出：符合该 Schema 的层次化法律推理树结构。
   - 任务细分为三个子任务：
     - **任务 I：待证事实生成**——抽取中间待证事实与生成终极待证事实；
     - **任务 II：证据推理**——提取文本中的证据片段（句子级别定位），并判断某一证据能否推断出给定中间待证事实；
     - **任务 III：经验生成**——揭示证据与中间待证事实之间的隐性人类经验。

3. **技术路线——TL Agent**
   - 采用 ReAct 式智能体范式：LLM 在“思考→推理→规划→选工具→调用工具→反思→再决策”中循环，直至任务完成。
   - 主要工具集包括：
     - **Fact Finding Head**：事实提取、证据提取、证据-事实链接、经验生成等一系列任务工具；
     - **Knowledge Search**：基于向量检索相似文本，用检索结果辅助确认任务结果；
     - **MultiRole Checker**：分别扮演律师、警察、公众/法官等视角讨论任务问题并投票/裁决；
     - **Legal Knowledge**：注入法律定义、法条与示例；
     - **Reflection**：基于先前工具返回的知识对任务结果进行复核修正；
     - **Emotion Check / Pattern Match / Finish**：情感中性校验、模式预分析、任务终止等辅助工具。

### 三、实验设计与评估

- **数据集规模与划分**：
  - 数据来源于“中国裁判文书网”，含 453 个真实案例；
  - 标注总量：2,627 条待证事实、14,578 条证据、16,414 条经验，全语料约 623 万 tokens；
  - 划分：训练集 253 例 / 验证集 100 例 / 测试集 100 例；
  - 标注方式：法律专业人士预标注 15 条用于示范，之后培训 45 名法学院学生众包标注，标注一致性（Pearson/Spearman）超过 0.93，人工复核正确率约 95%。

- **评估方法**：
  - 任务 I 与 III 使用 Rouge-L 类 F1 或精调版 Rouge 打分；任务 II 使用精确率、召回率、F1；
  - 综合分数（S_c）则对树结构的节点和关系同时进行打分。

- **对比方法与实验组**：
  - 第一组：中小规模未在 TL 数据上微调的模型（ChatGLM-6B、LexiLaw、Lawyer Llama v2）；
  - 第二组：以上模型经 TL 指令数据微调后的版本（ChatGLM-6B finetune、Lexilaw finetune、Qwen-6B finetune）；
  - 第三组：API 中文大模型（Spark 4.0 Ultra、ERNIE-4.0 Turbo-8k、Qwen-max、GLM-4-plus、Deepseek-v3）；
  - 第四组：API 英文大模型（Claude-3.5、GPT-4o-mini、GPT-4o）；
  - 进阶对比：GPT-4o/o1、DeepSeek-V3/R1 及 few-shot（3-shot）增强版本；
  - 消融实验：分别移除 Pattern Match、MultiRole Checker、Legal Knowledge、Knowledge Search、Emotion Check 等工具。

- **主要性能结果**：
  - TL Agent的总体综合分 31.50，显著高于未增强的 GPT-4o（25.74）等基线；
  - 在经验生成（任务 III）上 TL Agent表现最佳；经过微调的 6B 模型也能达到甚至超过一些大 API 模型，说明提示词与知识增强具有可观的收益。

### 四、资源与算力

- 论文**未明确报告具体 GPU 型号、卡数、训练时长或调用 API 总成本**；
- 仅提供与数据构建相关的劳动成本统计：标注总时长 566.25 小时，总报酬约 4,246.9 美元；实验成本并未量化；
- 需要指出：无算力细节属于可复现性上的明显短板。

### 五、实验数量与充分性

- **实验组数量较多**：包括 4 组共 13+ 个基线模型、2 种智能体后端（GPT-4o-mini / GPT-4o）、reasoning 模型对比、3-shot 对比、5 项消融以及人工 case study。
- **数据代表性**：主结果确实基于全部 100 条测试样例，但进阶对比和消融实验仅随机抽取测试集的 10%（约 10 条），抽样较小可能带来统计稳定性问题。
- **充分性问题**：
  - 优点是评测视角覆盖了 3 个子任务 + 整体结构分，比较系统；
  - 不足是消融实验样本过少、未观测到置信区间和显著性检验；对 fairness、bias 也没有专门的量化评测。

### 六、结论与主要发现

- 通过 Schema 设计与树状结构化推理，可将非结构化案件文本转化为抽象、系统、可复核的推理树。
- 结构化中间的待证事实与经验显式化，能有效降低对“隐式经验”的误用风险，提升裁判过程的透明性与问责性。
- Agent 方法能显著提升模型在事实、证据、经验抽取与链接上的质量；小模型经微调后也有较强的潜力。

### 七、优点

- **任务创新性强**：较早提出“树状透明法律推理”评测，填补了对裁判过程而非只对终局预测的空白。
- **标注质量把控细致**：预标注、培训、双人标注+第三人裁决、法律专业人员复核等步骤形成较严谨闭环。
- **模式设计系统化**：将经典证据法学中的 Wigmore 图示法与深度学习任务做了操作性转化，伦理框架（如避免 LLM 自动标注偏见）也有考虑。
- **Agent 工具链丰富**：证据、知识检索、多角色核查与反思等工具的组合思路对面向专业领域的 LLM应用有借鉴价值。

### 八、不足与局限

- **隐私与数据偏差**：数据虽然来自公开文书，但存在诉讼当事人代表性偏差、地域偏差；作者也承认无法完全排除标注者固有的潜意识偏见。
- **任务粒度受限**：出于标注可行性，把待证事实压缩到“中间”和“终极”两种粒度，对真实裁判过程中更复杂的中间推理链作了简化。
- **评测指标有限**：Rouge 系指标难以评估语义等价性，经验生成事实性也缺少人工一致性验收之外的多维验证。
- **实验充分性不足**：消融实验只取 10% 样例评估；没有给出多次运行方差/置信区间；没有对“错误类型”做系统性统计。
- **资源与可复现性受限**：代码和数据虽公开，但未报告任何算力配置与训练成本。
- **实际应用局限**：作者明确指出 LMM 不应直接用于最终定案；当前方案更适合辅助审查与教育，真正的司法落地尚需解释性、隐私保护和司法问责机制的进一步研究。

（完）
