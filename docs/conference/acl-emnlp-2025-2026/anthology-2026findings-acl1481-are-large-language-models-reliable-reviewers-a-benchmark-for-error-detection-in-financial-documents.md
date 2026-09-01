---
title: Are Large Language Models Reliable Reviewers? A Benchmark for Error Detection in Financial Documents
title_zh: 大语言模型是可靠的审阅者吗？面向金融文档错误检测的基准
authors: "Ying He, Zhouhong Gu, Zhecheng Hu, Yubo Zhou, Hao Shen, Jiaqing Liang, Zhaoqian Dai, Ma Shuguang, Fei Yu, Yanghua Xiao, Zhixu Li"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1481.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 提出FinED-Bench评估LLM在金融文档中的错误检测能力，直接关联提升LLM在金融领域的事实准确性
tldr: 金融文档准确性至关重要，但LLM在金融错误识别上的能力尚未被系统评估。本文构建FinED-Bench基准，覆盖三个认知复杂度水平和九个真实金融场景，包含超过900份2025年报告。基准揭示LLM在捕捉金融文档错误方面的表现与局限，为提升金融NLP事实可靠性提供评估基础。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 807, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 881, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1625, \"height\": 946, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 723, \"height\": 724, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 510, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1501, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1246, \"height\": 437, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 709, \"height\": 929, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 718, \"height\": 700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1481/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 743, \"height\": 604, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1382, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 721, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1652, \"height\": 691, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1437, \"height\": 498, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1630, \"height\": 336, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1419, \"height\": 967, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1657, \"height\": 843, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 791, \"height\": 534, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 822, \"height\": 431, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1565, \"height\": 395, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1470, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1481/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1710, \"height\": 376, \"label\": \"Table\"}]"
motivation: 金融文档错误检测任务尚未被探索，缺乏系统评估LLM能力的基准。
method: 构建FinED-Bench，涵盖多级认知复杂度和九类金融场景的900余份报告。
result: 基准测试揭示了LLM在金融错误识别上的表现与不足。
conclusion: FinED-Bench为评估和改进LLM金融文档可靠性提供了基础。
---

## Abstract
Ensuring the accuracy of financial documents is critical for economic analysis, regulatory compliance, and corporate decision-making. Several studies have shown that Large Language Models (LLMs) perform well in many financial tasks, such as stock price movements and financial analytics. However, a critical task remains unexplored: the ability of LLMs to identify errors in financial documents. In this paper, we introduce **FinED-Bench**, the first publicly Benchmark for Financial Error Detection across three levels of cognitive complexity. FinED-Bench covers nine real-world financial scenarios, and includes over 900 documents reported in 2025 that are unseen by existing language models. We detail the benchmark construction process and evaluate several advanced LLMs (e.g., GPT-4o, Qwen3-14B) on this tasks, which requires both financial domain knowledge and reasoning capabilities. Experimental results show that current LLMs still struggle with this task, especially in high-complexity cases. Besides, supervised fine-tuning can significantly improve the performance of weaker LLMs on this task. Our data and code are available at https://anonymous.4open.science/r/FinED-Bench-406F.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **金融文档准确性的重要性**：金融文档中的错误对经济分析、监管合规和企业决策有严重影响。论文以2012年摩根大通“伦敦鲸”事件为例——60亿美元损失并非源于市场波动，而是Excel错误，凸显金融行业错误检测的紧迫性。Gartner 2024年的调查显示，18%的金融从业者每天都会出错。
- **现有研究空白**：尽管LLM在股价预测、金融分析等任务上表现优异，但**LLM在金融文档错误检测方面的能力尚未被系统评估**。已有错误检测基准（如语法纠错CoNLL-2014、BEA-2019，临床笔记错误检测MEDEC，数学推理错误ErrorRadar）多聚焦于短文本、通用领域或单一句子级别，难以覆盖金融文档所需的数值推理与长上下文理解能力。
- **核心问题**：LLM能否真正理解复杂金融文档并准确检测其中的细微错误（如术语误用、跨段落数字矛盾、非法时间等）？这直接影响LLM作为金融审阅者的可靠性。
- **论文目标**：填补这一空白，构建首个系统性金融文档错误检测基准FinED-Bench，评估LLM在不同认知复杂度层级错误上的检测能力。

---

## 2. 论文提出的方法论

### 2.1 核心思想
- 构建一个**基于三层认知复杂度分类的金融错误检测基准**，通过半自动流水线将受控错误注入真实金融文档中，形成标准化的评测数据集。
- 设计依据认知-语言学的**话语表征模型**（Kintsch & Van Dijk, 1978），将文本理解分为三层，对应三类错误：

### 2.2 错误分类体系（双层级：3大类 × 15子类）

| 大类 | 定义 | 子类（5个/类） |
|------|------|----------------|
| **GKE 通用知识错误** | 影响文本可读性和表面结构，非专家也能检测 | 非法时间（IT）、冗余表述（RS）、数值格式错误（VFE）、数值缺失（NM）、非数值属性缺失（NNM） |
| **FKE 金融领域知识错误** | 扭曲语义，需领域知识 | 术语误用（TM）、错误法律引用（ILR）、歧义表述（AE）、数值单位错误（NUE）、遗漏金融要素（OFE） |
| **FRE 金融推理错误** | 需跨段落/全文推理验证 | 冲突表述（CE）、时间矛盾（TC）、数值不一致（NI）、计算错误（CaE）、条款冲突（CC） |

### 2.3 半自动构建流水线（图3所示）

1. ** 문서收集与解析**：
   - 收集2025年2月之后发布的金融文档（在评测模型知识截止日期之后，避免数据污染）。
   - 文档转纯文本并清洗，保留表格（转成Markdown格式）。
   - 主数据集限制在16K词以内；另建**FinED-Bench-Hard**（24份文档，32K–120K词）测试超长上下文能力。

2. **错误生成**：
   - 领域专家先定义常见错误种子（真实金融文档中的高频错误模式）。
   - 按错误类型采用不同**文档分割策略**：
     - GKE/FKE → 按章节分割；
     - 计算错误 → 选含3个以上数值的段落；
     - 推理错误 → 合并有重叠数值/术语的相邻段落（或首尾远距段落）。
   - 利用GPT-4o + In-Context Learning在各片段中生成上下文相关的错误。

3. **错误过滤（两级）**：
   - **模型级过滤**：GPT-4o 重新评估注入后的文档，判断错误是否合适；计算错误要求输出计算式验证。
   - **人工验证**：5位金融专家审核保留的错误，删除可能引入新错误的实例，控制每文档错误数（≤4），并更新错误种子定义。

---

## 3. 实验设计

### 3.1 基准数据集

| 数据集 | 文档数 | 平均长度 | 错误数 | 每文档错误数 | 错误分布（GKE/FKE/FRE） |
|--------|--------|----------|--------|-------------|------------------------|
| **FinED-Bench**（主数据集） | 973 | 4,544.7词 | 4,123 | 4.2 | 42.9% / 30.3% / 26.8% |
| **FinED-Bench-Hard** | 24 | 71,536.0词 | 83 | 3.5 | 41.7% / 30.2% / 28.1% |
| **FinED-Bench-EN**（英文补充） | 56 | — | 198 | — | 91个GKE / 37个FKE / 70个FRE |

- 覆盖 **9个真实金融场景**：股票研究报告、行业研究报告、招标公告、保险合同、法律文件、监管文件、公司章程、上市招股书、债券招股书等。
- 与真实世界文档分布相比，FinED-Bench适度提高了FRE占比（26.8% vs 17.8%），使评测更难、更均衡。

### 3.2 评估方法
- 模型被要求输出错误句子 + 错误类型标注。
- 判定正确需同时满足：句子精确包含标准句子、错误类型正确。
- 指标：**Precision、Recall、F1-score**。

### 3.3 对比模型
- **通用LLM**：Qwen2.5-7B-Instruct、Qwen3-8B（含无推理变体）、Qwen3-14B（含无推理变体）、DeepSeek-R1-0528-Qwen3-8B（蒸馏版）、GPT-3.5-turbo、GPT-4o-mini、GPT-4o。
- **金融专用LLM**：Dianjin-R1-7B、Fin-R1。
- **人工基线**：2名金融专业大二学生，在100份随机抽样文档上评估。
- **提示策略消融**：whole vs chunk、multi vs single、few-shot vs zero-shot 共8种组合。

### 3.4 监督微调实验
- 用与基准相同的流水线（但不经人工验证）构建微调数据集：9,515份无错片段 + 8,697份含错片段，由Qwen3-32B和GPT-4o联合判定错误类型与位置。
- 对Qwen3-14B进行微调，并在CFLUE的5个金融任务上验证泛化性。

---

## 4. 资源与算力

- **论文中未明确披露GPU型号、数量、训练时长、API调用量等具体算力信息**。
- 仅能从附录推断：
  - GPT系列实验时间窗口为2025年5月11日至25日（官方API）。
  - 开源模型推理参数配置见表4（如Qwen系列max_tokens=120,000，context window=32,768）。
  - 监督微调使用了Qwen3-32B和GPT-4o作为自动标注器，但微调本身的硬件规模未说明。
- 这是论文信息透明度的不足。

---

## 5. 实验数量与充分性

### 实验总量
论文实验较为**全面丰富**：
- **10个模型的总体性能对比**（表2）+ **15个错误子类细粒度对比**（附录表7，共10个模型×15个类别）。
- **8种提示策略消融**（表6），覆盖whole/chunk、multi/single、few/zero的组合。
- **9个金融场景的跨场景分析**（图5、图6）。
- **监督微调前后对比**（图7：15类错误）+ **微调泛化性验证**（CFLUE 5项任务，表3）。
- **位置感知分析**（首/中/尾，附录表8）。
- **文档长度影响分析**（2.5K→50.2K词，F1从40.16%降至16.66%）。
- **英文数据集验证**（附录表9，9个模型）。
- **人工基线比照**（100份文档）。

### 充分性与公平性评价
- **优点**：实验覆盖了模型类型（通用vs专用）、推理能力（thinking vs no-thinking）、提示策略、文本长度、位置、场景、语言（中/英）等多个维度，交叉验证了主要结论，比较系统充分。
- **公平性**：文档均为2025年2月后发布（避开训练数据），人工验证保证标注质量（Fleiss' κ=0.89），错误判定标准严格（句+类型双重正确）。

---

## 6. 论文的主要结论与发现

1. **当前LLM在金融错误检测上整体表现不佳**：最佳模型GPT-4o总体F1仅48.34%；金融推理错误（FRE）最难，GPT-4o在该类F1仅38.00%，Qwen3-14B仅29.10%。
2. **金融专用LLM受限于基座模型能力**：Dianjin-R1-7B在Qwen2.5-7B基础上提升了15.81% vs 9.85%，Fin-R1反而下降至3.19%。领域微调（用于QA、摘要等）不能显著提升错误检测能力。
3. **GPT-4o呈高召回低精度模式**：过度敏感的检测导致大量误报和错误分类。
4. **推理能力显著增强错误检测**：Qwen3-8B启用thinking后GKE F1从24.93%提升至47.60%；蒸馏R1推理数据虽优于无推理版本，但仍不及原版Qwen3。
5. **文档长度严重制约性能**：最长文档（债券招股书）F1仅9.52%，最短（行业研报）达59.68%。
6. **监督微调显著提升性能**：Qwen3-14B微调后总F1提升10.70%（43.15%→53.85%），且在CFLUE金融5项任务上未下降、部分反而微升，说明微调数据可提升检测能力且不损害泛化性。
7. **位置效应**：模型对文档开头和结尾的错误检测更好，中间最难（符合首因效应和近因效应）。

---

## 7. 优点

- **填补研究空白**：首个专门评估LLM金融文档错误检测能力的公开基准，弥补了现有基准（语法纠错、幻觉检测、医疗错误检测）在金融领域长文档上的缺失。
- **系统工程方法**：提出半自动构建流水线，结合专家定义错误种子、LLM错误注入、两级过滤（模型+人工）和专家验证，平衡了效率与质量。
- **科学的分层错误分类**：基于认知语言学理论（话语表征模型）划分三类错误，由浅入深，15个子类覆盖面广，能细粒度诊断模型能力差异。
- **强数据新鲜度设计**：刻意收集2025年2月后文档，避免训练数据污染，增强评测可信度。
- **多维度评测体系**：覆盖不同模型族、有无思考、提示策略、场景长度、位置、微调效果、中英文，结论交叉验证、相互呼应。
- **丰富的人类基线**：人工评估显示金融专业学生F1也仅63.63%，说明任务难度真实，同时为模型表现提供了参照锚点。
- **开源可用**：数据和代码已在匿名平台公开，便于复现和后续研究。
- **伦理意识**：用合成数据替代敏感信息（联系方式等），降低数据泄露风险。

---

## 8. 不足与局限

- **文档类型覆盖不完整**：论文明确说明未涵盖资产负债表、利润表等核心财务报表——此类文档错误往往源于底层数据源，验证需审查大量历史数据，故排除。这限制了基准对金融实务的全面代表性。
- **多模态缺失**：真实金融文档中的印章、签名等视觉元素未纳入评估，文本专用模型的评测无法反映现实场景的完整需求。
- **语言偏倚**：主数据集以中文为主，英文数据集仅56份文档，规模较小；对其他语言（如日语、德语金融文档）的推广性存疑。
- **错误注入方式与现实偏差**：论文通过LLM+种子模式注入错误，而真实金融文档错误是自然发生的，可能有不同的分布和上下文特征，基准的生态效度有待验证。
- **人工评估规模有限**：人工基线仅2名学生、100份文档，样本量偏小，且学生熟练度可能不如资深金融从业者，对“人类表现”的估计可能不精确。
- **模型范围局限**：评测模型截至2025年年中，不包括更新的模型（如GPT-5、Qwen3-后续版本）；附录英文评测中出现GPT-5，但中文主评测未纳入，对比一致性略显不足。
- **算力信息披露不足**：未报告训练/推理的具体算力（GPU型号和数量），降低了实验可复现性。
- **评价指标二元化**：仅以“句子完全匹配+类型正确”判定，可能低估了部分输出正确但有表达差异的情况；对部分正确的检测未做部分打分。

---

（完）
