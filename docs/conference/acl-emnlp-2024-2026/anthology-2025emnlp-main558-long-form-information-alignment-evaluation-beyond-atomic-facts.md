---
title: Long-Form Information Alignment Evaluation Beyond Atomic Facts
title_zh: 超越原子事实的长文本信息对齐评估
authors: "Danna Zheng, Mirella Lapata, Jeff Z. Pan"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.558.pdf"
tags: ["query:faithfulness"]
score: 9.0
evidence: 提出联合验证事实间依赖的评测指标DoveScore与基准MontageLie
tldr: "该文指出现有细粒度事实评估器忽略事实间依赖，易被由真实陈述拼接的误导性文本欺骗。作者构建MontageLie基准，并发现多个评估器AUC-ROC低于65%。进一步提出DoveScore，联合验证事实准确性及事实间关系，显著提升长文本事实对齐评估的稳健性。该工作推动评测方法超越原子事实，适应更复杂的信息对齐场景。"
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 762, \"height\": 605, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 634, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1604, \"height\": 618, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1618, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1624, \"height\": 828, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 758, \"height\": 573, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 760, \"height\": 574, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1627, \"height\": 2333, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1621, \"height\": 925, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main558/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1626, \"height\": 442, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main558/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 796, \"height\": 246, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main558/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 795, \"height\": 258, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main558/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1383, \"height\": 784, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main558/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 804, \"height\": 253, \"label\": \"Table\"}]"
motivation: 现有细粒度事实评估只逐个检验原子事实，不考察事实间依赖，存在被拼接谎言欺骗的脆弱性。
method: 构建MontageLie欺骗性叙事基准，并提出联合验证事实及关系的DoveScore评估框架。
result: 现有评估器在MontageLie上表现差，DoveScore显著增强了事实对齐评估鲁棒性。
conclusion: 强调了超越原子事实、联合验证关系的评估方法对于长文本一致性的重要性和有效性。
---

## Abstract
Information alignment evaluators are vital for various NLG evaluation tasks and trustworthy LLM deployment, reducing hallucinations and enhancing user trust. Current fine-grained methods, like FactScore, verify facts individually but neglect inter-fact dependencies, enabling subtle vulnerabilities.In this work, we introduce MontageLie, a challenging benchmark that constructs deceptive narratives by “montaging” truthful statements without introducing explicit hallucinations.We demonstrate that both coarse-grained LLM-based evaluators and current fine-grained frameworks are susceptible to this attack, with AUC-ROC scores falling below 65%.To enable more robust fine-grained evaluation, we propose DoveScore, a novel framework that jointly verifies factual accuracy and event-order consistency. By modeling inter-fact relationships, DoveScore outperforms existing fine-grained methods by over 8%, providing a more robust solution for long-form text alignment evaluation. Our code and datasets are available at https://github.com/dannalily/DoveScore.

---

## 论文详细总结（自动生成）

# 《超越原子事实的长文本信息对齐评估》论文总结

## 1. 核心问题与研究动机

**核心问题：现有信息对齐评估器存在一个关键盲区——它们只逐个检验原子事实的真实性，却忽略了事实之间的依赖关系和因果顺序，因而容易被“由真实陈述拼接而成的误导性叙事”（montage-style lies）所欺骗。**

- **背景脉络**：信息对齐评估器是多种 NLG 评估任务和可信 LLM 部署的核心组件。现有细粒度方法（如 FactScore）将目标文本分解为原子事实后逐条验证，但每条事实即使单独正确，**重新排序后可能逆转隐含的因果链**，从而在不引入任何显式幻觉的情况下误导读者。
- **核心举例**（论文 Figure 1）：“Mike 打了 Amy → Mike 和 Amy 分手 → Amy 和 John 看电影”这一真实顺序若被调整为“Amy 和 John 看电影 → Mike 打了 Amy → Mike 和 Amy 分手”，每条陈述都真实，但叙事含义被操纵——暗示 Amy 的行为引发了暴力。
- **本质挑战**：这类“蒙太奇式谎言”是真实世界 misinformation 中常见的操纵手法，现有评估框架在原理上无法检测——因为它们在设计上就假设事实之间相互独立。

## 2. 方法论：基准构建与评估框架

### 2.1 MontageLie 基准

通过三个主要阶段构造：

1. **种子数据采样**：从 BookSum 和 SummScreen 两个长文本摘要数据集中采样 (source, summary) 对。
2. **蒙太奇式谎言生成**——分为三步：
   - **事件分解**：用 LLM 将正确的目标文本分解为按时间顺序排列的事件列表 E = [e₁, e₂, …, eₙ]；
   - **受控难度的事件乱序**：定义 ShuffleD（基于逆序对的归一化乱序度），将乱序分为四个难度等级——easy（D∈[0.80, 0.90]）、medium（D∈[0.55, 0.65]）、hard（D∈[0.30, 0.40]）、extreme hard（D∈[0.05, 0.15]）；使用 **Lehmer codes 算法**精确构造具有目标逆序数的排列；
   - **增量式谎言文本生成**：逐步将事件拼接为连贯文本，避免 LLM 丢失顺序控制。
3. **改写（Paraphrasing）** ：用不同叙事技巧（顺叙、倒叙、插叙、补叙）生成改写版本，测试评估器对叙事变化的稳健性。

### 2.2 DovScore 评估框架

由三个核心组件构成：

- **分解器（Decomposer）** ：将文本分为两类事实——
  - **事件事实（Event Facts）** ：与时间相关、可排序的行为或状态变化（如“Dr. Lin submitted her resignation”）；
  - **描述性事实（Descriptive Facts）** ：与时间无关的稳定属性（如“Octopuses have three hearts”）。
- **事实检查器（Fact Checker）** ：逐条将事实与源文本比对，得到正确事件事实集合 Fᶜ_E 和正确描述性事实集合 Fᶜ_D，计算 Event Score S_E = |Fᶜ_E|/|F_E| 和 Descriptive Score S_D = |Fᶜ_D|/|F_D|。
- **排序器（Sorter）** ：将已验证的正确事件事实分别基于源文本顺序和目标文本顺序排序，计算事件顺序得分 S_EO = 1 − ShuffleD(Sorted(Fᶜ_E, s), Sorted(Fᶜ_E, t))。

最终得分公式：

> DoveScore = α · S_E · S_EO + (1 − α) · S_D

其中 α = |F_E| / (|F_E| + |F_D|)，根据事件事实在目标文本中的相对频率动态加权。该式子的核心创新在于：**S_E 和 S_EO 相乘**——事件事实不仅要正确，顺序也必须正确，才算对齐。

## 3. 实验设计

### 3.1 Benchmark 与数据

- **MontageLie** 包含 **1,303 个数据实例**：637 条来自 BookSum，666 条来自 SummScreen。
- 源文本词数范围 312–9,937（平均 4,201.79），目标文本词数范围 62–991（平均 258.61）。
- 数据由 gpt-4o-mini 生成，经人工质量评估确认（语义偏移、事件完整性、连贯性等指标均在 94% 以上）。

### 3.2 对比的评估器

**粗粒度评估器：**
- ROUGE-1/2/L；
- LLM-as-Evaluator（基于 G-Eval 模板）：gpt-4o-mini、Qwen-3 系列（1.7B/4B/8B/14B/32B）、Llama-3 系列（1B/3B/8B/70B）。

**细粒度评估器：**
- SummaC-ZS、SummaC-Conv（NLI-based，句子级）；
- AlignScore（统一对齐函数，句子级）；
- FactScore（LLM 原子事实分解，gpt-4o-mini 为 backbone）。

### 3.3 评估方式

- 使用 AUC-ROC 作为核心指标，分别评估各难度层级下正确文本与对应谎言的可区分度。
- 所有 LLM 评估采用零样本设置、temperature=0，保证确定性输出。

## 4. 资源与算力

论文在显式的算力信息上几乎没有披露：

- **未提及** GPU 型号、数量、训练时长或推理总成本等信息。
- 从实验设计推断，所有 LLM 均以零样本推理方式使用（包括 gpt-4o-mini API 调用及多种开源模型的本地推理），不涉及模型训练或微调，因此算力需求主要是推理开销。
- 人工评估由两位标注者完成，规模较小（50 个实例、200 条谎言、200 条改写）。

## 5. 实验数量与充分性

### 实验规模概览

| 实验类型 | 内容 | 数量级 |
|---------|------|--------|
| 主实验 | 12 种粗粒度评估器 × 4 难度 + 4 种细粒度方法 × 4 难度 | ~16 组条件 |
| DovScore 对比 | 与各基线最好成绩在 4 个难度上对比 | 4 组 |
| 子分数分析 | S_E、S_EO、S_D 分数分布对比 | 3 组 |
| Ablation（隐性） | 通过子分数分布分析反映 S_EO 的贡献 | 隐含 |
| 稳健性测试 | 原始 vs 改写版本的分数分布对比 | 定性分析 |

### 充分性评估

- **不足方面**：没有显式的消融实验（如移除 S_EO 或 S_D 后的性能对比），而是通过子分数分布间接表明 S_EO 的贡献——这在方法归因上说服力有限。也没有不同 LLM backbone 的 DovScore 版本对比。
- **公平性与客观性**：主实验在统一零样本、temperature=0 条件下进行，较为公平。部分实验结论（如 Qwen3 优于 Llama3）并非从表 3 中看出（Qwen-3-8B 比 Llama-3.1-8B 高 3.89%，Qwen-3-32B 比 Llama-3.3-70B 高 4.78%），但基础版本差异仅在 50% 附近；不过这种差别的确能说明更小的模型在该任务上的不足。总体而言，实验提供了充分的多维度证据，但消融/变体实验偏少。

## 6. 主要结论与发现

1. **现有评估器普遍无法检测蒙太奇式谎言**：最佳模型 gpt-4o-mini（粗粒度）平均 AUC-ROC 仅 64.23%，细粒度方法全部低于 57%。
2. **细粒度分解越细，反而越脆弱**：FactScore（原子事实级）比基于句子的 SummaC/AlignScore 表现更差，且比同 backbone 的粗粒度 gpt-4o-mini 评估低 13.78%——细分到原子事实放大了对事实间依赖的忽视。
3. **小型 LLM（<4B）在该任务上基本失效**：AUC-ROC 接近 50%（接近随机猜测）。
4. **LLM 对叙事改写稳健**：原始文本与改写版本的分数分布高度一致，说明不会因换一种叙事技巧而被误判。
5. **DovScore 显著提升鲁棒性**：平均 AUC-ROC 达 65.25%，比最强细粒度基线高出 8%+，较 FactScore（同 backbone）提升 14.8%；尤其在 easy 和 medium 难度上明显领先。
6. **事件顺序一致性是可行的改进方向**：S_EO 子分数对区分真假目标文本贡献关键。

## 7. 优点

- **问题定义新颖且有现实意义**：指出“原子事实全部正确但叙事误导”这一信息评估盲区，连接了对抗性 prompting、 misinformation 与信息对齐评估，而非局限于幻觉检测。
- **基准构造技术精妙**：用逆序数 + Lehmer codes 精确控制乱序程度，将难度梯度量化，方法论可复现且可扩展。
- **区分描述性/事件性事实是洞察性设计**：意识到并非所有事实都需要排序验证，避免了过度约束，提升了框架的适用面。
- **DovScore 模块化设计**：分解器、事实检查器、排序器各自独立，便于后续分别改进与替换 backbone。
- **评估考虑了改写鲁棒性**：排除“叙事风格”这一混淆变量，使评估更纯粹地聚焦于事件关系操纵的检测。
- **基准质量经人工验证**：多层质量指标（语义偏移、事件完整性、连贯性等）均有人工标注确认。

## 8. 不足与局限

- **数据完全由 LLM 生成**：作者也承认这一点。这可能导致分布伪影无法反映真实人类写作的 misinformation 模式，外部效度受限。
- **仅覆盖英文**：缺乏多语言验证。
- **DovScore 实际提升幅度有限**：虽然比细粒度方法提升 8%+，绝对 AUC-ROC 为 65.25%（较 FactScore 提升 14.8%），意味着在 extreme hard 难度下区分能力接近随机。事件乱序检测在难度越高时越接近随机水平，这说明对“极难”的微妙操纵依然力不从心，但这也说明基准的难度设置是有效的。
- **缺少系统的消融实验**：对 S_EO 贡献的论证主要依赖分数分布的可视化观察，而非严格的消融对比。
- **排序器局限性**：输入全量事件列表做全局重排，可能在大规模事件场景下产生偏差或性能瓶颈；作者表示这算是一个开放问题。
- **评估器比较略显不公平**：FactScore 使用 gpt-4o-mini 作为 backbone，而 SummaC 和 AlignScore 使用专用微调模型，不同 backbone 的能力差异可能混淆了“分解粒度”这一自变量的效应。
- **实际应用层面试探性不足**：应用场景在结论中以设想为主，尚未在真实 misinformation 检测流水线中验证。

## 简评：整体价值评估

该论文以“蒙太奇式谎言”为核心研究对象，数据构造与难度控制方法论严谨可靠，标准实验流程透明可复现。在建模策略上，DovScore 提出了文本中事件类与非事件类事实需区分建模、事件类需做相对顺序校验的框架，在细粒度事实评估相关方向上具备方法论增量价值。不过，真正制约信息对齐评估器在复杂伪装文本上表现的因素，可能在于对“叙事含义”层面的理解与常识推理能力，这在现有框架中尚未显式建模——也是该任务维度上的下一步关键方向。

（完）
