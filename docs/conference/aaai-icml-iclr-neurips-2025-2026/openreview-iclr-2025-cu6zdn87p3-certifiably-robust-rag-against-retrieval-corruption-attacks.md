---
title: Certifiably Robust RAG against Retrieval Corruption Attacks
title_zh: 针对检索污染攻击的可认证稳健检索增强生成
authors: "Chong Xiang, Tong Wu, Zexuan Zhong, David Wagner, Danqi Chen, Prateek Mittal"
date: 2024-09-25
pdf: "https://openreview.net/pdf?id=cU6ZdN87p3"
tags: ["query:hallu-rag"]
score: 6.0
evidence: RobustRAG以隔离聚合方式抵御检索污染攻击，减少恶意或错误证据对生成结果的影响，与可靠RAG相关。
tldr: 针对检索增强生成易受检索污染攻击、被恶意注入内容诱导产生错误回答的问题，本文提出RobustRAG防御框架。其核心思想是先隔离分组检索段落，再对每组生成的文本响应进行安全聚合，并设计了基于关键词和解码的聚合算法。作者证明了该框架可以获得可认证的稳健性，即能够形式化保证在部分检索被污染时仍输出安全回答。该工作为保障证据检索环节的可信度提供了重要思路。
source: ICLR-2025-Rejected-Public
selection_source: conference_retrieval
motivation: RAG易受检索污染攻击，攻击者注入恶意段落可诱导模型输出不准确回答，影响证据可靠性。
method: 提出隔离再聚合策略：将检索段落分成互不相交的组，逐组生成后再使用关键词或解码算法安全聚合为最终输出。
result: RobustRAG能对检索污染攻击提供可证明的稳健性，保证部分段落被污染时输出仍安全。
conclusion: 通过隔离聚合缓解检索环节被攻击的风险，提升了RAG在不可信证据下的可信度。
---

## Abstract
Retrieval-augmented generation (RAG) has been shown vulnerable to retrieval corruption attacks: an attacker can inject malicious passages into retrieval results to induce inaccurate responses. In this paper, we propose RobustRAG as the first defense framework against retrieval corruption attacks. The key insight of RobustRAG is an isolate-then-aggregate strategy: we isolate passages into disjoint groups, generate LLM responses based on the concatenated passages from each isolated group, and then securely aggregate these responses for a robust output. To instantiate RobustRAG, we design keyword-based and decoding-based algorithms for securely aggregating unstructured text responses. Notably, RobustRAG can achieve certifiable robustness: we can formally prove and certify that, for certain queries, RobustRAG can always return accurate responses, even when an adaptive attacker has full knowledge of our defense and can arbitrarily inject a small number of malicious passages. We evaluate RobustRAG on open-domain QA and long-form text generation datasets and demonstrate its effectiveness and generalizability.

---

## 论文详细总结（自动生成）

## 基于提供材料的论文总结

> 说明：以下总结基于论文摘要与元数据信息。由于提供的材料仅含摘要，未包含正文详细内容，因此部分要点只能基于摘要进行推断或标注“未提供”。

### 1. 核心问题与整体含义
- **研究背景**：检索增强生成（Retrieval-augmented Generation, RAG）通过外部检索段落辅助模型生成回答，但检索结果本身并不可信。
- **核心问题**：RAG 容易遭受**检索污染攻击**（retrieval corruption attacks），攻击者可将恶意构造的段落注入检索结果，诱导模型输出错误或不准确的回答。
- **研究意义**：现有工作缺乏对此类攻击的系统性防御。本文提出 **RobustRAG**，据称为**首个**针对检索污染攻击的防御框架，并提供了**可认证的稳健性保证**，对提升 RAG 在不可信检索环境下的可靠性具有重要价值。

### 2. 方法论
- **核心思想**：采用 **“隔离再聚合”**（isolate-then-aggregate）策略。
- **算法流程**：
  1. **隔离**：将检索到的段落划分成多个互不相交的子组；
  2. **生成**：对每一个隔离组内部的拼接段落，独立调用 LLM 生成文本响应；
  3. **聚合**：将所有隔离组的响应进行安全聚合，得到最终稳健输出，从而避免某一组被污染后直接改变全局结果。
- **关键技术设计**：
  - 针对非结构化文本响应，设计了**基于关键词的聚合算法**与**基于解码的聚合算法**。前者可能通过提取关键信息进行交叉校验；后者可能通过解码空间上的对齐或投票来合成最终结果。原文未给出更具体的数学公式。
- **可认证稳健性**：
  - RobustRAG 能提供**形式化证明**：即使攻击者具备**自适应能力**、完全了解防御机制，并且能够**任意注入少量恶意段落**，对某些查询，RobustRAG 仍可保证输出准确回答。该性质属于可认证的稳健性（certifiable robustness）。

### 3. 实验设计
- **任务场景**：摘要明确提到评估覆盖两类任务：
  - **开放域问答**（open-domain QA）；
  - **长文本生成**（long-form text generation）。
- **数据集/Benchmark**：摘要中未给出具体名称（如 NaturalQuestions、TriviaQA 等），也未说明数据规模。
- **对比方法**：摘要未提及任何基线或对比方法。
- **客观性与公平性**：因缺少具体基准和对比细节，无法从摘要判断实验的公平性。

### 4. 资源与算力
- 摘要和元数据中**均未提及** GPU 型号、数量、训练或推理时长、显存占用等任何算力资源信息。
- 因此，无法评估其实验成本及可复现性所需的计算条件。

### 5. 实验数量与充分性
- 摘要仅提到在两大类任务上进行了评估，但**未列举实验组数、消融实验、参数敏感性分析、不同攻击强度测试**等。
- 由于缺少具体结果表格与统计分析，难以判定实验是否充分。
- 从摘要可见**实验覆盖范围有限**：仅两种场景且无对比对象，若原文也未补充更多实验，则充分性存疑。

### 6. 主要结论与发现
- RobustRAG 是首个能够针对检索污染攻击提供**可认证稳健性**的防御框架。
- 通过隔离再聚合策略，即使部分检索段落被恶意注入，模型仍能在特定查询上保持准确输出。
- 在开放域问答和长文本生成任务上的评估表明其具有**有效性**与**可泛化性**。

### 7. 优点
- **理论贡献强**：提供了形式化的可认证稳健性保证，而非仅凭经验对抗攻击。
- **攻击模型严格**：考虑了自适应攻击者，攻击者知晓防御机制并可任意注入少量恶意段落。
- **方法设计巧妙**：“隔离再聚合”能有效阻断恶意段落对整体响应的直接操纵。
- **适配非结构化输出**：针对 LLM 生成的开放文本，设计了关键词聚合和解码聚合两类方案，增进了方法的适用范围。
- **问题重要且前沿**：瞄准 RAG 实际部署中检索环节的不可信问题，具有现实意义。

### 8. 不足与局限
- **可认证范围有限**：认证保证针对“某些查询”和“少量恶意注入”成立；当污染段落数量超过阈值或查询不满足条件时，稳健性可能无法保证。
- **方法本身可能引入信息损失**：隔离分组会破坏全局上下文，每个组看到的证据有限，可能影响回答质量。
- **针对长文本生成的聚合更难**：对非结构化长文本进行安全聚合（尤其基于解码的方法）可能增加计算开销，并可能限制生成内容的多样性和流畅性。
- **实验验证不透明**：未提供数据集名称、对比基线、具体指标、消融实验等关键信息，读者难以客观判断其实际提升幅度。
- **算力与部署成本未知**：文内未说明计算资源，无法评估实际应用成本。
- **只针对检索污染攻击**：未提及对提示注入、模型后门等其他类型攻击的防御能力。

（完）
