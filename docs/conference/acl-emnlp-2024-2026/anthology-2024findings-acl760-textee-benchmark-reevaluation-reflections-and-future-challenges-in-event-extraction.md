---
title: "TextEE: Benchmark, Reevaluation, Reflections, and Future Challenges in Event Extraction"
title_zh: TextEE：事件抽取基准、重估、反思与未来挑战
authors: "Kuan - Hao Huang, I-Hung Hsu, Tanmay Parekh, Zhiyu Xie, Zixuan Zhang, Prem Natarajan, Kai-Wei Chang, Nanyun Peng, Heng Ji"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.760.pdf"
tags: ["query:evidence-qa"]
score: 6.0
evidence: 标准化的多数据集事件抽取评测基准
tldr: 事件抽取研究普遍存在评测不一致问题，导致报告分数不能反映真实性能。该论文提出TextEE基准，统一16个数据集、覆盖八个领域的预处理脚本和数据划分，降低数据假设与分词等差异引入的偏差，并重新评估现有方法。其标准化流程有助于检测数据集和划分偏差并提升结果可复现性，为公平比较与未来事件抽取数据集及评价协议建设提供了参考。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl760/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 795, \"height\": 131, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1648, \"height\": 677, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1542, \"height\": 757, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 909, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1248, \"height\": 959, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1636, \"height\": 1118, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 732, \"height\": 885, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 802, \"height\": 817, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1489, \"height\": 1533, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1490, \"height\": 1488, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1574, \"height\": 1320, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1281, \"height\": 929, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1631, \"height\": 1856, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1609, \"height\": 977, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl760/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1597, \"height\": 1299, \"label\": \"Table\"}]"
motivation: 事件抽取领域中不同数据假设和预处理造成评测不一致，模型性能被高估，可复现性不足。
method: 提出TextEE标准化事件抽取基准，统一多个数据集的预处理、划分和评测流程并重估现有方法。
result: 通过统一协议揭示原有评测偏差并提升可复现性，为后续研究提供公平基座。
conclusion: 标准化评测基准是事件抽取研究的必要条件，有助于公平比较和领域进步。
---

## Abstract
Event extraction has gained considerable interest due to its wide-ranging applications. However, recent studies draw attention to evaluation issues, suggesting that reported scores may not accurately reflect the true performance. In this work, we identify and address evaluation challenges, including inconsistency due to varying data assumptions or preprocessing steps, the insufficiency of current evaluation frameworks that may introduce dataset or data split bias, and the low reproducibility of some previous approaches. To address these challenges, we present TextEE, a standardized, fair, and reproducible benchmark for event extraction. TextEE comprises standardized data preprocessing scripts and splits for 16 datasets spanning eight diverse domains and includes 14 recent methodologies, conducting a comprehensive benchmark reevaluation. We also evaluate five varied large language models on our TextEE benchmark and demonstrate how they struggle to achieve satisfactory performance. Inspired by our reevaluation results and findings, we discuss the role of event extraction in the current NLP era, as well as future challenges and insights derived from TextEE. We believe TextEE, the first standardized comprehensive benchmarking tool, will significantly facilitate future event extraction research.

---

## 论文详细总结（自动生成）

## 论文核心问题与整体含义
事件抽取（Event Extraction）是 NLP 中一项基础任务，但作者发现现有评测存在严重的公平性和可复现性问题，导致论文中报告的性能分数不能真实反映模型实际能力，阻碍了领域正常发展。

论文指出三个评测层面的核心问题：
- **不一致性（Inconsistency）**：不同研究对数据假设不同（如多词触发词、重叠论元等）、预处理脚本不同（如分词工具或包版本导致数据差异）、使用外部资源（如 POS 标签或黄金实体）也不同，导致论文之间数据不可比。
- **不充分性（Insufficiency）**：大部分研究仅使用 ACE05 和 RichERE，覆盖面窄；且多采用单一固定数据划分，存在数据划分偏差。
- **低可复现性（Low Reproducibility）**：许多方法未公开代码，或官方代码缺乏标准化和数据细节，复现困难。

为系统性解决这些问题，作者提出了 **TextEE基准平台**。

## 方法论：核心思想与技术细节
**核心思想**：通过标准化基准对事件抽取进行公平、全面、可复现的评测，并利用标准化评测重新审视领域发展现状（尤其对比现有最好的小模型与 LLM 在此任务的能力）。

关键设计：
- **统一数据假设**：采用最宽松的假设（允许多词触发词、考虑重叠论元、不过滤长文本），更接近真实场景。
- **标准化预处理**：所有数据集的预处理均使用统一的分词工具（`stanza 1.5.0` 做输入文本切分与词元切分，`RoBERTa` tokenizer 做子词切分），并缓存偏移量避免因包版本不同导致的数据变化。
- **数据划分标准化**：16 个数据集均将多个原始官方的 train/dev/test 合并并重新划分，每数据集提供 5 组不同的数据划分，缓解数据划分偏差；同时优化划分使训练/验证/测试集分布差异尽可能缩小。
- **附加资源处理**：对需要额外标签的方法，如 POS 标签、AMR 等，用预训练模型标签替代；对需要实体边界的方法，用训练集训出的新的 NER 预测器，不使用验证/测试真实标签。
- **新增评测指标（AI+/AC+）**：区分论元所属的具体触发词，解决了原指标无法区分同事件类型多个触发词的问题。

评测维度分为三类：
1. E2E（End-to-End 事件抽取）
2. ED（Event Detection 事件检测）
3. EAE（Event Argument Extraction 事件论元抽取）

## 实验设计
**数据集**：包含 16 个数据集、覆盖 8 个领域：
- 新闻：ACE05、RichERE、M2E2、MUC-4、RAMS
- 生物医学：MLEE、Genia2011、Genia2013
- 网络安全：CASIE
- 药物警戒：PHEE
- 流行病领域：SPEED
- 维基百科领域：WikiEvents、MEE
- 通用领域：MAVEN、FewEvent、GENEVA

**模型的涵盖与实现**：
- 端到端联合训练模型（如 DyGIE++、OneIE、AMR-IE 等）
- 分类模型：EEQA、RCEE、Query&Extract、TagPrime（C/CR）、UniST、CEDAR 等
- 生成式模型：DEGREE、BART-Gen、X-Gear、PAIE、AMPERE 等

**对比 LLM**：GPT-3.5-Turbo、Llama-2-13b/70b-chat、Zephyr-7b-alpha、Mixtral-8x7B-Instruct 等 5 个模型，以 few-shot 情境提示的方式评测（ED 和 EAE 分别在不同 shot 组合下测试），由于成本原因随机对数据集抽取 250 个文档进行评测。

为保证公平，分类模型统一用 RoBERTa-large、生成模型统一用 BART-large，并在所有实验中使用相同的预处理结果。

## 资源与算力
论文未申明用于训练或推理的 GPU 型号、数量或训练时长。不过在方法部分说明了在 LLM 评测阶段“受成本与时间所限”只对各数据集抽 250 个文档。实验具体执行的硬件资源在论文中未做任何披露。

## 实验数量与充分性
- 覆盖 16 个数据集，3 个子任务（E2E、ED、EAE ）各利用 5 组数据划分平均结果。
- 在 TextEE 中实现了 14 个代表性新近模型，并进行重估（对比不同组合），规模远超历史工作。
- 开展 5 个 LLM 在 ED/EAE 上的 few-shot 评测（即每数据集采样 250 文档）。
- 对 LLM 错误进行了人工案例分析，归纳为 3 类错误。

实验规模及覆盖面相当充分，同时多种数据划分设计本身也体现了对客观公平的比较考量。

## 核心结论与发现
1. 不同方法（此前均用单一划分汇报）在 E2E 和 ED 上都没有出现明显的统一统治性模型 —— 说明既有报告的性能提升很可能是受数据集偏差与划分选取偏差影响的产物。
2. TagPrime、PAIE 在 EAE 上为最稳定优越的两个方案。
3. AI/AC 与 AI+/AC+ 之间存在显著差距，原有的评测方式不能精确反映论元隶属关系的质量，建议今后使用 AI+/AC+ 精确评估。
4. LLM 在 ED/EAE 上表现远逊于基准小模型，在零样本情境下精度明显低。主要错误有：
   - **过度攻击预测**：因不理解事件类别边界而大量输出误报触发词；
   - **生成区间与偏移不精确**：难以预测精确的起止边界；
   - **幻觉或改写**：生成输入中不存在的内容（后处理也难以正确处理）。
   这说明在复杂结构化语义抽取上，LLM 离实际可用还有相当距离。
5. 主张事件抽取在未来可作为“事实导向的结构化工具”服务于 LLM，但也为高效统一通用事件抽取的设计提出新挑战。

## 优点
1. **公平性和标准化的落实**（统一文本切分、缓存的偏移、统一模型 encoder、5 组数据划分），有力解决了此前评测文献里的对比错觉。
2. **覆盖面大**：从单数据集依赖扩展到多领域共 16 个数据集，并同时纳入 E2E/ED/EAE 三种任务。
3. 在实现上，对未开源代码方法进行了无偏地再实现、对额外标注作出透明声明，保证了对历史方法的可比性。
4. 超越单一分数的“微结果”分析：提出敏感的论元所属评测和 LLM 错误模式归类。指出标准评测不彻底之处，并给出未来可以用更高要求的指标继续进行评测的途径。
5. 对“事件抽取在 LLM 时代的意义”提出了具有前瞻性的反思与讨论（定位为工具，为上层 LLM 提供精确事实入口）。

## 不足与局限
1. **某些已提出的数据与模型没有覆盖**。作者已承认会遗漏一些可能重要的工作，无法保证所有具备学术价值的方案都被重新测试（例如仅支持无法获得或未公开进一步数据的部分数据集）。
2. **某些无原始代码工作的重实现技巧存在偏差的风险** —— 因参数、框架与细节可能不同，无法确保得分与原作者的预期得分完全一致。
3. **对于 LLM 评估采样规模偏小**（每数据集 250 个文档，且去掉了 SPEED 和 MUC-4），验证的置信度恐不如全量评测。
4. 未报道使用的算力硬件设置与对应训练的显隐开销（效率指标），这对应用其设计大规模评测的复现提出一定困难。
5. 当前引入人类标注模板和事件类型名依赖的方法仍需要有特殊的构建流程，不够完全全自动化；此外作为“基准平台”的整体设计未能讨论对低资源、更多通用场景的覆盖。

（完）
