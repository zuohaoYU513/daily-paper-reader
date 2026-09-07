---
title: "ParamMute: Suppressing Knowledge-Critical FFNs for Faithful Retrieval-Augmented Generation"
title_zh: ParamMute：抑制知识关键前馈网络以实现忠实的检索增强生成
authors: "Pengcheng Huang, Zhenghao Liu, Yukun Yan, Haiyan Zhao, Xiaoyuan Yi, Hao Chen, Zhiyuan Liu, Maosong Sun, Tong Xiao, Ge Yu, Chenyan Xiong"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=CyUq9D99vE"
tags: ["query:faithfulness"]
score: 8.0
evidence: 揭示内部参数化知识使模型忽略检索证据的机制，并提出抑制关键前馈网络增强忠实性
tldr: 针对模型在拥有相关且准确的检索上下文时仍会生成矛盾内容的问题，论文探索内部机制，发现中深层前馈网络中的特定子集在不忠实生成时被过度激活，主要体现为参数化知识压过外部证据。据此提出ParamMute，在解码阶段抑制这些知识关键网络，以降低内部先验的影响。实验表明该方法能减少生成内容与检索证据的冲突，说明调节模型内部知识通路是提升证据约束生成忠实性的重要补充。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 即使检索上下文相关且准确，模型内部参数化知识仍可能导致不忠实输出，现有方法主要关注外部上下文利用而忽略内部知识影响。
method: 定位不忠实生成中过度激活的中深层前馈网络子集，并在解码阶段抑制这些知识关键网络，以增强对检索证据的依赖。
result: 抑制关键前馈网络后，模型生成内容与检索上下文的矛盾减少，忠实度得到提升。
conclusion: 不忠实生成不仅源于外部上下文利用不足，内部参数知识的持续影响同样关键，定向抑制特定网络可增强检索增强生成的忠实性。
---

## Abstract
Large language models (LLMs) integrated with retrieval-augmented generation (RAG) have improved factuality by grounding outputs in external evidence. However, they remain susceptible to unfaithful generation, where outputs contradict retrieved context despite its relevance and accuracy. Existing approaches aiming to improve faithfulness primarily focus on enhancing the utilization of external context, but often overlook the persistent influence of internal parametric knowledge during generation. In this work, we investigate the internal mechanisms behind unfaithful generation and identify a subset of mid-to-deep feed-forward networks (FFNs) that are disproportionately activated in such cases. Building on this insight, we propose Parametric Knowledge Muting through FFN Suppression (ParamMute), a framework that improves contextual faithfulness by suppressing the activation of unfaithfulness-associated FFNs and calibrating the model toward retrieved knowledge. To evaluate our approach, we introduce CoFaithfulQA, a benchmark specifically designed to evaluate faithfulness in scenarios where internal knowledge conflicts with accurate external evidence. Experimental results show that ParamMute significantly enhances faithfulness across both CoFaithfulQA and the established ConFiQA benchmark, achieving substantial reductions in reliance on parametric memory. These findings underscore the importance of mitigating internal knowledge dominance and provide a new direction for improving LLM trustworthiness in RAG. All codes are available at https://github.com/OpenBMB/ParamMute.

---

## 论文详细总结（自动生成）

# ParamMute：抑制知识关键前馈网络以实现忠实的检索增强生成——论文总结

## 1. 核心问题与研究动机

- **背景**：大语言模型（LLMs）与检索增强生成（RAG）结合后，通过引入外部证据提升了生成的事实性。
- **核心问题**：即便检索到的上下文**相关且准确**，模型仍然可能产生**不忠实（unfaithful）的生成**——即输出与检索证据相矛盾的内容。
- **现有方法的不足**：已有提升忠实性的研究大多聚焦于**增强外部上下文的利用**（如改进检索、重排序、提示设计等），但普遍**忽视了模型内部参数化知识在生成过程中的持续影响**。
- **核心洞察**：不忠实生成的根源不仅在于外部证据利用不足，更在于**内部参数知识压过外部证据**——模型过度依赖记忆中的先验知识，导致输出与检索上下文冲突。

## 2. 方法论：ParamMute

### 核心思想

- 从机制层面定位与不忠实生成**强相关**的模型内部组件，并在解码阶段**定向抑制**这些组件的激活，从而将模型的生成偏好从「内部先验知识」校准到「外部检索证据」上。

### 关键技术细节

- **机制分析**：通过探针式分析，识别出不忠实生成过程中**中深层前馈网络（mid-to-deep FFNs）** 中有一**特定子集**被**不成比例地过度激活**——这些 FFN 可视为「知识关键网络」，它们承载着模型内部参数化知识的读取与表达。
- **方法名称**：Parametric Knowledge Muting through FFN Suppression（ParamMute），即「通过前馈网络抑制实现参数知识静音」。
- **具体流程（文字描述）**：
  1. **定位阶段**：识别在不忠实输出中过度激活的 FFN 子集，建立「不忠实生成 ↔ FFN 过度激活」的关联；
  2. **抑制阶段**：在解码时对这些被标记的 FFN 的激活进行**抑制（suppression）** ，削弱内部参数知识的表达强度；
  3. **校准阶段**：通过抑制内部先验，使模型被迫**更多地依赖检索到的上下文证据**进行生成，从而减少输出与证据之间的冲突。

## 3. 实验设计

### 基准与数据集

- **CoFaithfulQA（自建 benchmark）** ：论文专门设计了这一基准，用于评测「内部知识与准确外部证据冲突」场景下的忠实性——即检索上下文是准确的，但模型内部先验知识与之相悖。
- **ConFiQA（已有基准）** ：与已建立的 ConFiQA 基准进行对比验证，确保方法在已有评测体系下同样有效。

### 对比与评估

- 论文在 CoFaithfulQA 和 ConFiQA 两个基准上评估了 ParamMute 的效果。
- 摘要中未详细列出具体对比的基线方法，但从问题设定来看，隐含的对比对象包括：标准 RAG 方法以及其他增强上下文利用的忠实性优化方法。

## 4. 资源与算力

- **未明确说明**：论文提供的摘要和元数据中**未提及** GPU 型号、数量、训练/推理时长等算力信息。
- 但ParamMute 的**推理阶段抑制策略**不需要额外训练大模型，属于轻量级干预，推断其资源开销相对可控。

## 5. 实验数量与充分性

- **实验数量**：从摘要可确认的实验包括：
  - 在**两个基准（CoFaithfulQA + ConFiQA）**上的效果评测；
  - 报告了**依赖参数记忆的减少（reliance on parametric memory）** 作为评估维度。
- **消融实验**：元数据中未明确列出详细的消融研究，但机制分析（定位 FFN 子集）本身就构成了一种验证性分析。
- **充分性评估**：由于缺少具体实验细节（基线数量、参数量规模、多模型泛化测试等），**无法从摘要层面充分判断实验的全面性与公平性**；方法在多大模型上验证、是否跨多种模型系列推广等问题尚待正文确认。

## 6. 主要结论与发现

- **机制发现**：不忠实生成与**中深层 FFN 特定子集的过度激活**存在强关联，表明内部参数化知识在生成过程中会持续施加影响，甚至压过外部证据。
- **方法有效**：ParamMute 通过抑制知识关键 FFN，在两个基准上都**显著提升了忠实性**，并**大幅降低了对参数记忆的依赖**。
- **方向性结论**：调节模型内部知识通路（而非仅优化外部上下文利用）是提升 RAG 忠实性的一个**重要且有效的新方向**，对增强 LLM 在 RAG 场景下的可信度具有启示意义。

## 7. 优点

- **问题视角新颖**：从**内部机制层面**解释 RAG 不忠实问题的根源，突破了以往只关注「外部上下文利用」的思维定式，提出「内部知识主导」这一关键因素。
- **机制与方法的闭环**：从机制定位（发现 FFN 子集过度激活）出发、基于该洞察设计干预方法，方法有明确的**可解释性依据**，而非纯启发式调参。
- **自建高质量 benchmark**：设计 CoFaithfulQA，专门针对「检索正确但内部知识冲突」这一此前缺乏评测的场景，弥补了现有基准在测试忠实性上的盲区。
- **轻量级干预**：抑制特定 FFN 的激活属于推理阶段的定向干预，**无需重新训练模型**，实用性强、部署成本低。

## 8. 不足与局限

- **模型规模与泛化性不明确**：方法是否在多种模型规模、不同模型架构（如 MoE 模型）上均有验证，摘要中未说明，存在泛化性疑问。
- **FFN 抑制的潜在副作用**：强制抑制模型内部知识可能同时**削弱模型的正常推理能力**（某些情况下内部知识是有益的），论文需要验证这种方法是否会导致性能在一般任务上下降。
- **过度抑制的风险**：如果检索证据本身有误（尽管 benchmark 保证其准确），该方法在面对低质量检索时会怎样表现，尚待讨论。
- **基准覆盖面有限**：CoFaithfulQA 集中于知识冲突场景，真实世界 RAG 中还有多跳推理、证据分散、信息缺失等复杂情况，方法在这些场景下的表现未知。
- **实验细节披露不足**：由于本文基于论文的元信息与摘要，基线方法、消融实验、统计显著性等多处细节尚未明确，公平性和充分性的最终判断依赖于阅读论文全文。
- **算力信息与复现成本未提供**。

---

（完）
