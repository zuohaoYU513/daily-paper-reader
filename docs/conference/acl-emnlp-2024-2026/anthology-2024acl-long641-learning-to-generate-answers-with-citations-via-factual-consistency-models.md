---
title: Learning to Generate Answers with Citations via Factual Consistency Models
title_zh: 通过事实一致性模型学习生成带引用的答案
authors: "Rami Aly, Zhiqiang Tang, Samson Tan, George Karypis"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.641.pdf"
tags: ["query:faithfulness"]
score: 8.0
evidence: 利用事实一致性模型过滤引用数据并微调模型，引导生成答案带引用以增强可验证性
tldr: 大语言模型常常生成幻觉内容，影响其在关键任务中的可靠性。该论文提出使用事实一致性模型(FCM)过滤弱标签引用数据并进行弱监督微调，在目标函数中加入聚焦学习以强调事实单元，使模型学会在答案中附带正确的引用。在ALCE少样本引用基准上，所提方法显著提升了引用的准确性和生成内容的可验证性，从而减少无依据内容。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long641/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 810, \"height\": 975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long641/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 809, \"height\": 1150, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long641/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 770, \"height\": 573, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 778, \"height\": 680, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1653, \"height\": 602, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1654, \"height\": 617, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 808, \"height\": 394, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 808, \"height\": 403, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 804, \"height\": 235, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 805, \"height\": 437, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1548, \"height\": 398, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 805, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 807, \"height\": 401, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1650, \"height\": 908, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1650, \"height\": 963, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1654, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1608, \"height\": 1921, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long641/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1608, \"height\": 1692, \"label\": \"Table\"}]"
motivation: 大模型幻觉严重影响可靠性，生成附带准确引用的答案可提升可验证性但难以实现。
method: 提出弱监督微调框架，利用事实一致性模型过滤引用数据，并在损失中对事实单元token施加聚焦学习。
result: 在ALCE few-shot引用基准上，方法提升了生成答案引用准确性与事实一致性。
conclusion: 利用一致性模型筛选弱监督数据并聚焦事实单元训练，可有效提高模型生成可验证文本能力。
---

## Abstract
Large Language Models (LLMs) frequently hallucinate, impeding their reliability in mission-critical situations. One approach to address this issue is to provide citations to relevant sources alongside generated content, enhancing the verifiability of generations. However, citing passages accurately in answers remains a substantial challenge. This paper proposes a weakly-supervised fine-tuning method leveraging factual consistency models (FCMs). Our approach alternates between generating texts with citations and supervised fine-tuning with FCM-filtered citation data. Focused learning is integrated into the objective, directing the fine-tuning process to emphasise the factual unit tokens, as measured by an FCM. Results on the ALCE few-shot citation benchmark with various instruction-tuned LLMs demonstrate superior performance compared to in-context learning, vanilla supervised fine-tuning, and state-of-the-art methods, with an average improvement of 34.1, 15.5, and 10.5 citation F 1 points, respectively. Moreover, in a domain transfer setting we show that the obtained citation generation ability robustly transfers to unseen datasets. Notably, our citation improvements contribute to the lowest factual error rate across baselines.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

大语言模型（LLMs）在信息寻求任务中表现出色，但存在严重的幻觉问题，即生成内容缺乏事实依据，这阻碍了它们在关键任务场景中的可靠性。为了提升生成内容的可验证性，一种主流解决方案是让LLM在生成内容的同时提供对检索到文本片段的引用（citations）。

然而，准确生成引用本身是一个重大挑战：
- 最先进模型（如ChatGPT、Bing Chat）对生成语句的引用准确率不足60%（Gao et al., 2023b; Liu et al., 2023）。
- 常见引用错误包括：生成内容与引用的源文本不一致（幻觉内容）、引用标注的篇章与所述内容不匹配等（论文图1展示了典型错误）。
- 长文本问答（LFQA）场景下，高质量引用标注数据的稀缺性以及微调可能导致模型原有语言能力和泛化能力受损。

论文核心目标是：**在不显著牺牲语言能力的前提下，教会LLM在检索增强的长文本问答中生成包含准确引用的回答**。

## 2. 论文提出的方法论

### 2.1 核心思想：CaLF 框架

论文提出 **CaLF**（Citation Learning via Factual Consistency Models），利用**事实一致性模型（FCM）**作为训练信号的弱监督迭代微调框架。FCM用于衡量一条声明（claim）与其引用段落之间的事实一致性。

CaLF整体是一个**迭代训练流程**，每一轮迭代k包含两个交替阶段：
1. **弱监督数据生成**：由当前模型生成多样化的带引用答案，通过FCM过滤得到高质量训练数据。
2. **聚焦学习微调**：在标准NLL目标基础上，根据FCM度量的token事实重要性重新加权损失函数。

### 2.2 技术细节

**阶段一：弱监督训练数据生成（Answer Generation for Training）**
- 假设集合包含：问题集 X、预期答案的原子事实列表 A、外部检索器 R 生成的检索段落 P。
- 使用多种解码策略（核采样、温度缩放、多样化beam search）从当前模型生成多样化的候选答案；还通过对生成句子中的引用进行替换（依据检索器得分进行抽样）来增强多样性。
- 使用质量保证函数 Q 对候选答案过滤：
  - **Citation-Recall**：句子层面的引用覆盖率（使用 FCM 对句子和引用段落的打分）。
  - **Citation-Precision**：每条引用（被引段落）对句子的单独支持程度以及移除该引用后剩余引用是否仍能支持句子。
  - **Correctness**：生成的答案中覆盖了多少预期事实 A。
- 动态确定阈值Θ（默认0.9，若过滤后数据量不足3条则降低0.1），直到满足最小样本量。
- 停止条件：当过滤后的样本比例不再提高时停止（或达到最大迭代次数K）。

**阶段二：聚焦学习（Focused Learning）**
标准 NLL 损失（对所有token均权）被重新加权为以下形式：

\[
L_{FL} = -\frac{1}{|y|}\sum_{t=1}^{|y|} w_t \log p_\theta(y_t | q, P, y_{<t})
\]

其中 w_t 是第 t 个token的重要性权重，计算流程如下：
1. **Shapley值计算**：使用FCM ϕ 对句子 si 和其引用段落 Ci 的一致性打分 oi = ϕ(si, Ci)，然后计算每个token的Shapley值。
2. **归一化**：对每个句子内的token重要值进行min-max归一化，避免句子长度差异导致的偏差。
3. **Token对齐**：由于FCM与LLM的tokenizer可能不同，设计对齐函数将FCM token的重要性映射到LLM token上——找到最短可对齐token span，以平均权重赋予LLM token。
4. **引用标记处理**：为引用标记（如"[1]"）赋予权重1（因它们不含语义但需学习生成）。

### 2.3 相关说明
- 训练数据来源为四样本D（few-shot示例），不使用验证集进行超参调优。
- 使用LoRA参数高效微调技术。
- FCM选用AlignScore（355M参数）作为主FCM。

## 3. 实验设计

### 3.1 数据集与场景
- **主要基准（in-domain）**：ALCE citation benchmark中的**ASQA**（歧义消解型问答题，基于Wikipedia，检索器GTR）和**ELI5**（开放领域问答，基于CommonCrawl，检索器BM25）。
- **域迁移实验**：源数据集包括ELI5、ASQA、**Hagrid**（基于Wikipedia，检索器GTR，人类标注335条）；目标数据集为ASQA和ELI5。
- **事实性评测**：**BIO**（传记生成，基于Wikipedia，检索器Contriever-MS MARCO），使用FactScore指标。
- 每个测试集包含1000条随机采样样本。

### 3.2 评估指标包括
- **Similarity (ROUGE-L)**、**Fluency (MAUVE)**、**Correctness (EM Recall)**、**Citation F1**（包含Citation Recall和Citation Precision，用NLI训练的T5-11B TRUE模型评估）、**Passage-grounded Correctness**。

### 3.3 对比方法
- 在相同指令微调LLM上对比：**In-context learning**、**Few-shot fine-tuning（Few-shot FT）**。
- SOTA模型对比：**Self-RAG 7B**、**ChatGPT (gpt-3.5-turbo-0301)**、**GPT-4**、**AGREE (PaLM2)**、**Blueprint (T5-3B)**。
- 使用的LLM：**Llama2-7B-chat**、**Mistral-Instruct-7B**、**MistralOrca-7B**。

## 4. 资源与算力

论文在附录A.2中说明了部分算力信息：
- 使用了 **A100 40GB** 和 **A10G 23GB** GPU的组合。
- 训练时长（仅一个A100上测量）：CaLF全程约 **13小时51分钟**，Few-shot FT基线约 **1小时2分钟**。
- 没有明确说明使用GPU的**精确数量**，也没有给出总训练时间和并行训练策略的信息。
- 计算开销最大的部分是多样化的答案候选生成，而Shapley值计算因FCM较小（AlignScore 355M）而较为高效。

## 5. 实验数量与充分性

论文进行了较为全面的实验设计与验证，包括：

1. **主实验结果**（Table 1与附录Table 11）：覆盖3种LLM × 2个数据集（ASQA/ELI5）× 3个随机种子，对比三种训练方法以及模型状态（In-context, Few-shot FT, Ours）。主结果用均值和标准差统计。
2. **域迁移实验**（Table 2与附录Table 12）：多种源-目标数据集组合（ELI5→ASQA, ASQA→ELI5, Hagrid→ASQA, Hagrid→ELI5），覆盖两种LLM，对比Zero-Shot、Few-shot FT、FT和Self-RAG。
3. **FactScore事实性评测**（Table 3）：对比多个SOTA模型及引入检索过滤的变体。
4. **消融实验**（Table 4、附录Table 9-10）：3种模型各自对比LLM+WS、LLM+WS+LFL的效果增量。
5. **迭代训练行为分析**（Figure 4）：观察8轮迭代过程中的指标变化轨迹。
6. **FCM选择敏感性分析**（Table 5）：4种不同FCM的质量与最终Citation F1的关系。
7. **对抗性基线测试**（Table 6）：6种对抗性策略检验自动指标的鲁棒性。
8. **人工评估**（Table 7）：4名标注者对180个实例，从引用质量、信息量、连贯性、流畅度四个维度对CaLF与Few-shot FT进行对比。

**充分性评估**：实验整体较充分，覆盖多模型、多数据集、多指标、消融与转移泛化验证，并使用多种随机种子。但ELI5端效果增益普遍弱于ASQA，部分数据集未进行人工评估验证。少数SOTA基线结果引自原文而非本论文环境下重新测量，公平性尚有轻微限制，但Cite as main comparison strategy可接受。

## 6. 论文的主要结论与发现

- **Citation F1大幅提升**：在三款7B规模指令微调模型上，相比In-context learning平均提升约34.1个点，相比Few-shot FT平均提升约15.5个点。相比Self-RAG平均提升24.8点，相比ChatGPT平均提升10.5点。
- **带引用的正确性提升**：CaLF使Passage-grounded Correctness显著提升，即生成内容中可被检索片段支撑的正确信息更多，降低了未经依据的内容生成比例。
- **域迁移能力显著**：从源数据集训练后，在完全不使用目标域in-context样例的条件下，引用质量和grounded正确性能在两个目标数据集上均超越基线。
- **事实性错误率最低**：在FactScore上获得83.4分（加检索过滤后88.9分），优于Self-RAG 13B等。
- **消融分析显示两大组件均有贡献**：弱监督训练数据+聚焦学习两步增量均对引用质量有明显帮助。
- **FCM选择影响性能**：更强FCM大体对应更好引用质量；但若评估模型与训练模型相同，可能带来指标虚高。
- **CaLF能保持原文质量**：自动与人工评估的流畅性、连贯性、信息量大体不亚于甚至优于微调基线。

## 7. 优点

- **创新性**：首次将事实一致性模型与Shapley值可实现机制直接结合，引入LLM的微调目标函数中，并成功将任务转换为“弱监督+聚焦学习”。
- **弱监督降低数据标注成本**：以已有FCM为反馈信号，能够主动扩充高质量训练数据，无需大量人工标注。
- **保持语言能力**：聚焦学习使得仅强调“事实token”的学习，比传统均权微调更少损害LLM语言生成质量（如MAUVE、ROUGE等指标保持或改善）。
- **推理阶段无额外开销**：与Self-RAG或后处理引用方法相比，CaLF推理时共享Few-shot FT的效率，不存在树解码或额外编辑步骤。
- **较大规模的评估体系**：覆盖多个LLM、多个域、自动与人工评测、消融、对抗测试和域迁移，较为严谨。
- **泛化验证细致**：对源域差异、目标的脆弱点与检索局限做了深刻讨论。

## 8. 不足与局限

- **简化假设**：假定每个生成的句子都应当有引用，不符合真实场景（例如引导性语句“Of course I can help!”无法也不需要引用），降低了实用性。
- **依赖FCM质量**：FCM如有偏见会使过滤结果与聚焦权重发生偏斜，影响最终效果（论文也观察到FCM质量与最终Citation F1的关系并不完全单调，并讨论了“评估模型泄漏”风险）。
- **模型适用性局限**：token对齐算法是针对所使用LLM/FCM的分词特点专门设计的（Llama/ RoBERTa等），未做全面的tokenizer差异经验测试，未实现通用即插即用。
- **检索质量制约实际事实性**：质量较差的检索结果（不相关/不完整/错误信息）会限制引用益处，甚至可能引发出“用引用掩盖误导事实”的潜在负面影响，作者也承认此问题无法彻底避免。
- **存在对抗性滥用风险**：带引用生成技术可能被用于选择性引用支持偏见观点，需社会性警惕。
- **训练计算开销较高**：相比Few-shot FT，额外训练时间约多13倍，适合离线或批量优化的情境，不适合轻量快速调节。
- **部分指标不够全面**：如ELI5上MAUVE偶有下降；未报告TruthfulQA等的其他通用能力基准测评；未对“每个句子必须引用”约束之外有自由对话能力的情景进行探究。

（完）
