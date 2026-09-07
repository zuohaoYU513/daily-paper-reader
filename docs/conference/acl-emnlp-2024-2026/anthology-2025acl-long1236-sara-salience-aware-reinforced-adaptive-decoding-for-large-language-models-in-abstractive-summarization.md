---
title: "SARA: Salience-Aware Reinforced Adaptive Decoding for Large Language Models in Abstractive Summarization"
title_zh: "SARA: 面向大模型抽象摘要的显著感知强化自适应解码"
authors: "Nayu Liu, Junnan Zhu, Yiming Ma, Zhicong Lu, Wenlei Xu, Yong Yang, Jiang Zhong, Kaiwen Wei"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1236.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 通过显著信息感知与强化自适应解码减少摘要对源文档的偏离，增强生成忠实性
tldr: 大模型在抽象摘要中仍可能产生与源文档不一致的幻觉。现有 PMI 解码能减轻对先验知识的依赖，但未显式利用显著上下文且超参数固定。作者提出 SARA，通过强化学习自适应调节上下文与先验知识的平衡，并把显著信息纳入解码奖励。实验表明该方法能更灵活地提升摘要忠实度，减少生成内容偏离源文档的情况。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1236/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 799, \"height\": 742, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1236/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1558, \"height\": 881, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1236/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1236/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 785, \"height\": 1085, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1636, \"height\": 1592, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1606, \"height\": 977, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1599, \"height\": 374, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 811, \"height\": 566, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 802, \"height\": 210, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 799, \"height\": 1136, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 807, \"height\": 523, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 658, \"height\": 581, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 750, \"height\": 456, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1236/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1497, \"height\": 318, \"label\": \"Table\"}]"
motivation: 抽象摘要存在幻觉，现有 PMI 解码忽略显著上下文且使用固定超参数，不够灵活。
method: 提出 Salience-Aware Reinforced Adaptive decoding (SARA)，在解码中引入显著信息，并通过强化学习动态权衡上下文与先验知识。
result: 实验显示该方法有效提升摘要忠实度并降低幻觉，优于依赖固定平衡的对应方法。
conclusion: 显著信息感知的自适应解码为文本摘要忠实度提升提供了一条可行路径。
---

## Abstract
LLMs have improved the fluency and informativeness of abstractive summarization but remain prone to hallucinations, where generated content deviates from the source document. Recent PMI decoding strategies mitigate over-reliance on prior knowledge by comparing output probabilities with and without source documents, effectively enhancing contextual utilization and improving faithfulness. However, existing strategies often neglect the explicit use of salient contextual information and rely on static hyperparameters to fix the balance between contextual and prior knowledge, limiting their flexibility. In this work, we propose Salience-Aware Reinforced Adaptive decoding (SARA), which incorporates salient information and allows the model to adaptively determine reliance on the source document’s context, salient context, and the model’s prior knowledge based on pointwise mutual information. Moreover, a tokenwise adaptive decoding mechanism via reinforcement learning is proposed in SARA to dynamically adjust the contributions of context and prior knowledge at each decoding timestep. Experiments on CNN/DM, WikiHow, and NYT50 datasets show that SARA consistently improves the quality and faithfulness of summaries across various LLM backbones without modifying their weights.

---

## 论文详细总结（自动生成）

# SARA：面向大模型抽象摘要的显著感知强化自适应解码

## 1. 核心问题与研究动机

- 大规模语言模型显著提升了抽象摘要生成的流畅性与信息量，但仍普遍存在“幻觉”问题：生成内容偏离源文档、添加源中不支持的细节。
- 已有PMI（Pointwise Mutual Information）解码策略通过对比“有无源文档条件下”的输出概率，降低对模型先验知识的过度依赖，从而提升忠实性；但仍存在两个关键缺陷：
  1. 未显式利用源文档中的显著（salient）上下文；
  2. 采用静态超参数在序列层面固定上下文与先验知识的权重，灵活性不足。
- 论文提出 **SARA（Salience-Aware Reinforced Adaptive decoding）**，旨在解决这些问题，在不修改模型权重的前提下提升摘要生成质量与忠实度。

## 2. 方法与关键技术

### 2.1 核心思想

- 在解码的每一步，同时利用三类输入：
  1. **主序列 XQ**：源文档+查询提示；
  2. **显著序列 SQ**：提取出的关键句+查询提示；
  3. **先验序列 Q**：仅有查询提示，无源文档。
- 基于互信息公式融合三类序列的输出概率（logits），并通过强化学习在“token级”动态调节各序列的权重。

### 2.2 显著上下文选择

- 直接使用 **BERTSum** 作为抽取式模型，对文档句子打分并选择高显著性的句子构成显著上下文 S。
- 为覆盖摘要所需的关键内容，放宽抽取阈值，提取更多关键句（实验中使用10句）。

### 2.3 显著感知解码

- 核心解码公式（对每个时间步 t）：
  \[
  y_t \sim \mathrm{softmax}\{(1+a_t)[b_t\logit(p_\theta(y_t|XQ_{<t})) + c_t\logit(p_\theta(y_t|SQ_{<t}))] - a_t\logit(p_\theta(y_t|Q_{<t}))\}
  \]
- 权重约束：\(a_t,b_t,c_t \in (0,1)\)，且 \(b_t + c_t = 1\)。
- 该公式将显著上下文纳入PMI框架，使生成内容更依赖源文档关键信息，削弱先验知识带来的幻觉。

### 2.4 Token级自适应强化解码

- 将三类序列同时输入LLM，取最后一层隐藏特征，并拼接后送入一个**轻量MLP**；
- MLP输出每个时间步的三组权重 A、B、C，经过 softmax/sigmoid 归一化以满足约束；
- 训练时使用 **Self-Critical Reinforcement Learning**：
  - 奖励函数综合了 ROUGE-1/2/L 和 FactKB（忠实度指标）：
    \[
    r(\hat Y) = R_1 + R_2 + R_L + \lambda\cdot FKB
    \]
  - 通过梯度上升优化 MLP，使权重分配能最大化生成摘要的质量和忠实度。
- 该MLP不修改LLM权重，仅用于决定三类logits的融合比例，因此保持LLM通用能力不退化。

## 3. 实验设计

### 3.1 数据集

- **CNN/DM**：新闻摘要基准；
- **WikiHow**：指令型文章摘要，更具抽象性；
- **NYT50**：纽约时报注释语料库的过滤版本（摘要长度≥50词）。

### 3.2 大模型 backbone

- 覆盖多种规模和架构的开源LLM：
  - GPT-Neo（3B）
  - LLaMA-2-Chat（7B）
  - OPT（7B）
  - Mistral-Instruct-v0.2（7B）

### 3.3 对比方法

- **Vanilla**：标准解码；
- **CAD（Context-Aware Decoding）**：已有的PMI解码方法，使用静态超参数固定上下文与先验知识的比例；
- **SARA（本文方法）**。

### 3.4 评价指标

- ROUGE-1/2/L、SacreBLEU、BERTScore-P、FactKB；
- 另使用 **GPT-4** 进行质量与忠实度的排序评价。

## 4. 资源与算力

- 论文在附录中明确给出RL训练的超参数表；
- 每个数据集使用 **单张A100 GPU**（表6注明：GPU A100 ×1）；
- 训练步数：2,000步；批次大小4；学习率5e-5或1e-5；
- 算法在每个实验上平均运行 **3次**；
- 但论文**并未报告具体训练时长或总的GPU小时数**，只在推理速度比较中给出了每batch毫秒数（如GPT-Neo上Vanilla约5143ms/batch，CAD约6429ms/batch，SARA约8571ms/batch），显示SARA推理开销高于Vanilla和CAD。

## 5. 实验数量与充分性

### 5.1 实验数量
该论文进行了较丰富的实验：

- **主实验**：3个数据集 × 4个模型 × 3种解码方法，共计36组性能对比表；
- **权重配置分析**：手工设置多组 a/b/c 权重，对比固定权重与自适应权重的效果；
- **消融实验**：
  - 移除主序列、显著序列、先验序列分别的实验；
  - 移除FactKB奖励或ROUGE奖励的实验；
- **显著序列长度分析**：3、5、10、15、20个句子对ROUGE和FactKB的影响；
- **GPT-4人工偏好评估**：包括分别评估质量/忠实度以及联合评估两种设置；
- **推理速度比较**。

### 5.2 充分性与客观性

- 多数据集、多模型、多指标的实验设计具有较强的信服力；
- 包含与PMI基线CAD的对比，并验证了显著上下文与RL自适应机制的必要性；
- GPT-4评估为相对中立的第三方偏好判断，增强了结论的可信性；
- 但所有评测均基于英文数据集和英文摘要生成任务，未覆盖跨语言/多语言场景；实验仅聚焦于开源模型（7B及以下），未在更大模型（如70B）或API模型上验证。

## 6. 主要结论与发现

- SARA在CNN/DM、WikiHow、NYT50上 consistently 优于Vanilla和CAD，在ROUGE、SacreBLEU、BERTScore-P和FactKB等指标上均获得更高分数；
- 在偏抽取式摘要的CNN/DM和NYT50上提升更明显；在偏抽象式的WikiHow上仍能保持质量与忠实度的平衡；
- 显著序列的引入有效提升了对关键信息的利用，先验序列的去除会引起性能大幅下降，说明三序列均必不可少；
- RL能学到优于手工固定权重的token级动态权重分配；
- 同时使用ROUGE与FactKB奖励比只用其中一种更能平衡质量和忠实度；
- GPT-4评价中，SARA的胜出率超过50%，进一步验证其增强忠实性的效果。

## 7. 优点

- **创新性**：将“显著上下文”显式引入PMI解码，突破已有PMI方法仅使用完整源文档的局限；
- **灵活性**：用强化学习实现token级自适应权重调节，代替序列级固定超参数，使模型能根据当前生成内容动态决定信任何种知识来源；
- **即插即用**：不修改LLM权重，只需额外一个轻量MLP，兼容多种开源LLM；
- **实验扎实**：多数据集、多骨干模型、多维指标与多种辅助分析，形成较完整证据链；
- **可复现**：公开代码和详细超参数，便于复现。

## 8. 不足与局限

- **适用范围有限**：仅在英文抽象摘要任务验证，未验证跨语言摘要或传统encoder-decoder摘要架构中的有效性；
- **先验序列计算开销大**：需同时运行三个序列的LLM前向，推理时间显著超过Vanilla和CAD，影响实际部署效率；论文也指出其更适用于“性能优先于推理速度”的场景；
- **显著上下文依赖外部抽取器**：使用BERTSum等模型，若抽取质量不稳定可能限制效果，理想情况应探索端到端显著感知机制；
- **奖励设计依赖现有指标**：ROUGE和FactKB与本领域评测口径相关，可能存在指标偏差；
- **权重网络训练规模有限**：仅使用了约2000步的训练和少量采样序列，RL训练稳定性和模型规模敏感性尚未展开充分验证；
- **未在更大规模LLM上测试**：7B量级不能代表所有当代LLM；大模型推理成本也使得此类多路解码方法更具挑战。

（完）
