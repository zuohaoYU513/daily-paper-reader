---
title: Fine-grained Knowledge Enhancement for Retrieval-Augmented Generation
title_zh: 用于检索增强生成的细粒度知识增强
authors: "Jingxuan Han, Zhendong Mao, Yi Liu, Yexuan Che, Zheren Fu, Quan Wang"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.522.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 通过细粒度句子级知识增强RAG以缓解幻觉
tldr: 现有RAG主要基于文档级语义相似度检索，容易忽略文档内句子级的细粒度信息。本文提出细粒度知识增强方法（FKE），利用解耦的思维链提示从外部语料检索句子级知识，并开发解码增强策略。该方法旨在弥补RAG中的知识缺口，从而缓解大语言模型的幻觉问题。实验表明FKE能更充分地利用外部知识，提升生成的事实准确性。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl522/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl522/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1629, \"height\": 659, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl522/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl522/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 780, \"height\": 608, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl522/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 786, \"height\": 609, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1619, \"height\": 587, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 227, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 194, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 789, \"height\": 310, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1636, \"height\": 710, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 783, \"height\": 555, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl522/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 789, \"height\": 490, \"label\": \"Table\"}]"
motivation: RAG虽能缓解幻觉，但基于文档的语义检索忽略了句子级细粒度必要信息，导致知识利用不充分。
method: 提出FKE方法，通过解耦的思维链提示从外部语料检索句子级知识，并结合解码增强策略。
result: 实验验证了FKE能有效利用细粒度外部知识，提高生成答案的事实准确性并减少幻觉。
conclusion: 细粒度句子级知识增强能够显著改善RAG的知识利用效率，为缓解幻觉提供了有效手段。
---

## Abstract
Retrieval-augmented generation (RAG) effectively mitigates hallucinations in large language models (LLMs) by filling knowledge gaps with retrieved external information. Most existing studies primarily retrieve knowledge documents based on semantic similarity to assist in answering questions but ignore the fine-grained necessary information within documents. In this paper, we propose a novel fine-grained knowledge enhancement method (FKE) for RAG, where fine-grained knowledge primarily includes sentence-level information easily overlooked in the document-based retrieval process. Concretely, we create a disentangled Chain-of-Thought prompting procedure to retrieve fine-grained knowledge from the external knowledge corpus. Then we develop a decoding enhancement strategy to constrain the document-based decoding process using fine-grained knowledge, thereby facilitating more accurate generated answers. Given an existing RAG pipeline, our method could be applied in a plug-and-play manner to enhance its performance with no additional modules or training process. Extensive experiments verify the effectiveness and generality of our method.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：大规模语言模型（LLM）虽然在诸多任务上表现出色，但在训练数据中缺乏、尤其是时效性强和领域特定的知识上仍存在明显不足，容易产生幻觉。
- **现有 RAG 的缺陷**：当前主流 RAG 方法主要基于文档级的语义相似度检索外部知识，并将整篇检索到的文档作为输入。这种方式容易忽略文档内部对回答问题至关重要的句子级细粒度信息——如图 1 所示，一个包含关键词但不含关键信息的错误文档可能获得更高的检索分数，导致最终答案错误。
- **核心问题**：如何从文档中挖掘并利用句子级的细粒度知识，以弥补文档级检索的不足，从而提升 RAG 生成答案的准确性。
- **论文含义**：提出一种无需额外模块或训练的“即插即用”方法 FKE，可在现有 RAG 管道上直接应用，通过细粒度知识增强来减少幻觉、提高事实准确性。

## 2. 论文提出的方法论

### 2.1 总体框架
FKE 包含两个核心组件：
1. **细粒度知识检索（Fine-grained Knowledge Retrieval）**
2. **解码增强策略（Decoding Enhancement）**

两个组件以即插即用的方式集成到现有基础 RAG 管道（如 DRAGIN、CRAG）中，无需额外模块或训练。

### 2.2 细粒度知识检索——解耦提示（Disentangled Prompting）
- **核心思想**：受 Chain-of-Thought 启发，将“检索细粒度知识”这一任务解耦为两个步骤：
  1. **识别知识片段**：先让 LLM（即现有生成器模型）显式识别文档中对回答问题有益的知识片段；
  2. **抽取查询聚焦句子**：基于这些知识片段，再从文档中抽取与问题相关的句子作为细粒度知识。
- **实现方式**：采用一次性（one-shot）方式，直接调用现有生成器模型，对检索到的文档进行处理，得到句子级细粒度知识集合 S = (s₁, s₂, ..., sₘ)。
- **意义**：相比标准提示（直接要求抽取相关句子），解耦提示能更准确地区分“与问题语义相关”和“真正有助于回答问题”的句子，提高细粒度知识的质量。

### 2.3 解码增强策略
- **核心思想**：在解码阶段同时利用两种知识——原始检索文档（文档级）和细粒度检索句子（句子级），通过对比解码的方式融合两种概率分布，约束生成过程。
- **具体流程**：
  1. **细粒度概率分布**：将问题 q 与细粒度知识 S 封装进生成模板 T，输入生成器，得到基于细粒度知识的逐 token 概率分布 p_θ(y_s,t | x_s, y_s,<t)，即 softmax(z_s,t)；
  2. **文档级概率分布**：将问题 q 与原始检索文档 D 封装进同一模板，输入生成器，得到文档级概率分布 p_θ(y_d,t | x_d, y_d,<t)，即 softmax(z_d,t)；
  3. **增强概率分布**：通过以下公式融合两种分布：
     p_θ(y_t) = [softmax(z_d,t / τ_d) + α·softmax(z_s,t / τ_s)] / (1 + α)
     其中 α 为控制强度，τ_d、τ_s 为温度参数；
  4. **截断处理**：借鉴 top-k 采样思想，对 logits 进行截断，去掉不可靠的尾部 token，得到最终的增强分布并采样生成答案。
- **作用**：细粒度分布提供句子级监督，使生成更聚焦于问题所需信息；文档级分布则保留上下文相关的碎片化知识，两者互补，提升生成质量。

## 3. 实验设计

### 3.1 数据集
| 任务类型 | 数据集 | 规模/说明 |
|---------|--------|----------|
| 多跳 QA | 2WikiMultihopQA | 102k 样本，需多步推理，结合 Wikipedia 与 Wikidata |
| 多跳 QA | HotpotQA | 113k 样本，跨文档多跳推理，提供句子级支持事实 |
| 单跳 QA | PopQA | 14k 样本，长尾 Wikidata 知识 |
| 单跳 QA | ARC-Challenge | 2.5k 科学常识选择题，对检索算法具有挑战性 |
| 测试规模 | — | 2Wiki 和 HotpotQA 各 1.0k，PopQA 1.4k，ARC 1.2k |

### 3.2 基础 RAG 管道
- **DRAGIN**（多跳 QA）：基于 LLM 自注意力的动态检索增强生成，代表多轮检索组；
- **CRAG**（单跳 QA）：带轻量级检索评估器的纠正式 RAG，代表单轮检索组。

### 3.3 对比基线
- **多跳任务**：wo-RAG、SR-RAG、FL-RAG、FS-RAG、FLARE；
- **单跳任务**：LLaMA2-7B/13B、Alpaca-7B/13B、Self-RAG（GPT-4 标注辅助）。

### 3.4 评估指标
- 多跳 QA：EM（Exact Match）、F1；
- 单跳 QA：Accuracy（准确率）。

## 4. 资源与算力

- 论文仅在实现细节中提及“整个过程可在 1 块 NVIDIA A800 GPU 上运行”，未明确说明训练时长、总 GPU 数量、具体推理时间或能耗。
- 由于 FKE 方法为“即插即用”、无训练过程，算力开销主要体现在推理阶段的额外一次细粒度知识抽取（one-shot 调用 LLM）和双路径解码上。
- 论文明确说明未在 70B 级大模型上进行评估，原因是资源需求过高。

## 5. 实验数量与充分性

### 5.1 实验数量
论文共进行了以下几组实验：
1. **主实验**：两种基础管道（DRAGIN、CRAG）× 四个数据集，共 8 组对比结果；
2. **消融实验一**：解耦提示 vs. 标准提示 vs. 原始文档级知识（PopQA 数据集）——验证解耦提示的有效性；
3. **消融实验二**：仅用细粒度知识 vs. 仅用文档级知识 vs. 两者结合（PopQA 数据集）——验证对比解码策略的必要性；
4. **消融实验三**：不同控制强度 α（PopQA 数据集）——确定最优 α=1.0；
5. **消融实验四**：不同模型规模（Llama2-7B vs. 13B，2Wiki 数据集）——验证跨规模泛化性；
6. **消融实验五**：不同温度 τ_s（PopQA 数据集）——确定最优 τ_s=0.2；
7. **人工评估**：从每个数据集随机抽样 200 条输出（共 800 条），3 名标注者从正确性（C）和相关性（R）两个维度打分，并计算 Fleiss' Kappa 一致性。

### 5.2 充分性评价
- **优点**：实验覆盖了多跳/单跳两类任务、四种数据集、两种主流 RAG 管道、多种消融维度（提示方式、知识来源、控制强度、模型规模、温度），设计相对全面；人工评估进一步增强了结论的可信度。
- **不足**：
  - 主实验仅对比了两个基础管道（DRAGIN 和 CRAG）的增强前后效果，未与现有其他细粒度 RAG 方法（如 FILCO、REAR、GeAR）进行直接对比；
  - 消融实验主要基于 PopQA 数据集，论文称结果在其他数据集上一致，但未展示完整数据；
  - 未在更大规模 LLM（如 70B）上验证，泛化性有一定局限。

## 6. 论文的主要结论与发现

1. **FKE 能显著提升 RAG 性能**：
   - 在 2WikiMultihopQA 上，DRAGIN+FKE 的 EM 提升 2.8、F1 提升 3.2；
   - 在 HotpotQA 上，EM 提升 4.9、F1 提升 3.5；
   - 在 PopQA 上，CRAG+FKE 准确率提升 6.3；
   - 在 ARC 上，准确率提升 5.4。
2. **解耦提示优于标准提示**：先识别知识片段再抽取句子，比直接抽取相关句子能获得更高质量的细粒度知识（Acc 75.2% vs. 69.0%，且知识长度更短）。
3. **细粒度知识与文档级知识互补**：单独使用细粒度知识（66.7%）优于单独使用文档级知识（61.8%），两者结合（68.1%）效果最佳。
4. **控制强度 α=1.0 最优**：在 0~1 范围内，α 越大性能越好；超过 1.0 后不再提升。
5. **方法跨模型规模有效**：在 Llama2-7B 和 13B 上均能稳定提升 DRAGIN 性能。
6. **温度鲁棒性**：在不同 τ_s 取值下，CRAG+FKE 均优于基础 CRAG（61.8%），说明方法对温度不敏感。
7. **案例验证**：FKE 能有效解决“缺少必要信息”和“误导信息干扰”两类典型检索失败场景。

## 7. 优点

1. **真正即插即用**：无需额外模块、无需训练、无需外部标注（如 GPT-4），可直接应用于现有 RAG 管道。
2. **创新性地引入细粒度知识**：将 RAG 的知识粒度从文档级扩展到句子级，弥补了现有方法的盲区。
3. **解耦提示设计巧妙**：将“抽取句子”分解为“识别知识片段→抽取相关句子”两步，有效提升了细粒度知识的质量，且设计思路具有可迁移性。
4. **对比解码策略合理**：融合文档级和句子级两种概率分布，既保留了上下文完整性，又增加了查询聚焦性，是一种轻量而有效的解码增强方式。
5. **实验设计较全面**：覆盖多跳/单跳、四种数据集、两种主流管道、多项消融，并有案例分析和人工评估，说服力较强。

## 8. 不足与局限

1. **计算开销增加**：虽然无需训练，但推理时需要额外调用 LLM 抽取细粒度知识（one-shot），且解码时需同时计算文档级和句子级两组概率分布，实际推理成本约为基础管道的两倍，论文对此量化分析不足。
2. **细粒度知识依赖初始文档检索质量**：论文的实现是先检索 10 篇文档再从中抽取细粒度知识（附录 A.1），如果初始检索完全遗漏了包含答案的文档，则细粒度知识无从谈起。论文在 Limitations 中也承认了这一点。
3. **大规模模型未验证**：未在 70B 级模型上实验，虽然在 7B/13B 上表现良好，但更大模型上能否保持优势未知。
4. **基线对比不够充分**：主实验只对比了增强前后的两个基础管道，未与 FILCO、REAR、GeAR 等其他细粒度 RAG 方法横向对比，定位“最先进”的说服力有所不足。
5. **消融实验覆盖面有限**：多数消融仅在 PopQA 上展示，论文声称其他数据集结果一致，但未提供完整数据供读者核实。
6. **潜在偏差风险**：外部知识库可能包含偏见、错误或过时信息，论文虽然在 Ethics Statement 中提及该风险，但未在方法层面提供任何过滤或防御机制。
7. **超参数依赖经验设定**：τ_d、τ_s、α 的取值对性能有一定影响，论文虽进行了敏感性分析，但未给出自适应调节方案。

（完）
