---
title: Calibrating LLM Confidence by Probing Perturbed Representation Stability
title_zh: 通过探测扰动表征稳定性校准大语言模型置信度
authors: "Reza Khanmohammadi, Erfan Miahi, Mehrsa Mardikoraem, Simerjot Kaur, Ivan Brugere, Charese Smiley, Kundan S Thind, Mohammad M. Ghassemi"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.530.pdf"
tags: ["query:metacognitio"]
score: 10.0
evidence: 对末层隐藏状态施加对抗扰动，用分类器根据表征稳定性预测答案是否正确
tldr: 大语言模型的置信度校准对可靠性至关重要，现有模型常过度自信或校准不足。论文提出CCPS方法，对模型最终隐藏状态施加有针对性对抗扰动，提取表征稳定性特征并用轻量分类器预测答案是否正确。在8B到32B的多种模型结构及多项选择和开放式任务上，CCPS显著优于现有置信度校准方法，展示了表征稳定性作为校准信号的价值。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1637, \"height\": 767, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1482, \"height\": 2377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1482, \"height\": 2370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1482, \"height\": 2380, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1482, \"height\": 2369, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1651, \"height\": 1808, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1242, \"height\": 2426, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1240, \"height\": 2414, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1243, \"height\": 2435, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1239, \"height\": 2408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1640, \"height\": 1330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1643, \"height\": 1330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1640, \"height\": 1330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1641, \"height\": 1334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1642, \"height\": 1332, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1638, \"height\": 1331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1642, \"height\": 1328, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1640, \"height\": 1331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1641, \"height\": 1335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1642, \"height\": 1331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1639, \"height\": 1325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1642, \"height\": 1324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1642, \"height\": 1331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 1642, \"height\": 1331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1641, \"height\": 1330, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1640, \"height\": 1331, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1641, \"height\": 1329, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1639, \"height\": 1329, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1642, \"height\": 1335, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1641, \"height\": 1334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 1477, \"height\": 2230, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 1406, \"height\": 2239, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 1484, \"height\": 2231, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main530/fig-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 1466, \"height\": 2262, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1645, \"height\": 1498, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1639, \"height\": 1806, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1584, \"height\": 307, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1182, \"height\": 1142, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 446, \"height\": 668, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1583, \"height\": 689, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1638, \"height\": 262, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1173, \"height\": 970, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 904, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1510, \"height\": 576, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1206, \"height\": 252, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1657, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1645, \"height\": 782, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1640, \"height\": 1638, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1641, \"height\": 1638, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1617, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1640, \"height\": 1637, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1653, \"height\": 1198, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1330, \"height\": 1626, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main530/table-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1664, \"height\": 984, \"label\": \"Table\"}]"
motivation: 大语言模型普遍存在置信度校准不足问题，需要更准确的正确率估计方法，内部表征稳定性蕴含可挖掘信号。
method: 对最终隐藏状态施加有目标对抗扰动，提取模型对扰动的响应特征，使用轻量分类器预测答案正确性，从而估计置信度。
result: 在多个模型大小、结构和数据集上测试，CCPS显著优于现有置信度校准方法，证明该思路在开放式问答中同样有效。
conclusion: 基于扰动表征稳定性的轻量分类器可有效预测回答正确性，为LLM置信度校准提供了通用高效的新方法。
---

## Abstract
Miscalibration in Large Language Models (LLMs) undermines their reliability, highlighting the need for accurate confidence estimation. We introduce CCPS (Calibrating LLM Confidence by Probing Perturbed Representation Stability), a novel method analyzing internal representational stability in LLMs. CCPS applies targeted adversarial perturbations to final hidden states, extracts features reflecting the model’s response to these perturbations, and uses a lightweight classifier to predict answer correctness. CCPS was evaluated on LLMs from 8B to 32B parameters (covering Llama, Qwen, and Mistral architectures) using MMLU and MMLU-Pro benchmarks in both multiple-choice and open-ended formats. Our results show that CCPS significantly outperforms current approaches. Across four LLMs and three MMLU variants, CCPS reduces Expected Calibration Error by approximately 55% and Brier score by 21%, while increasing accuracy by 5 percentage points, Area Under the Precision-Recall Curve by 4 percentage points, and Area Under the Receiver Operating Characteristic Curve by 6 percentage points, all relative to the strongest prior method. CCPS delivers an efficient, broadly applicable, and more accurate solution for estimating LLM confidence, thereby improving their trustworthiness.

---

## 论文详细总结（自动生成）

# 论文《Calibrating LLM Confidence by Probing Perturbed Representation Stability》中文总结

## 1. 核心问题与整体含义（研究动机与背景）

大语言模型（LLM）的置信度校准（confidence calibration）对其可靠性至关重要。然而，现有 LLM 普遍存在错误校准问题：
- 模型往往**过度自信**，对其错误答案给出过高概率；
- 传统 softmax 概率与真实正确率之间存在系统性偏差；
- 这使得 LLM 在高风险应用（如医疗、金融、自动化决策）中的可信度难以保障。

该论文提出一种假设：**LLM 内部表征的稳定性（representation stability）携带了与答案正确性高度相关的信号**——即模型对其最终隐藏状态被扰动后的响应模式，可以在一定程度上区分正确答案与错误答案。据此，作者提出 CCPS 方法，通过探测扰动后表征的稳定性来实现更准确的置信度估计。

## 2. 论文提出的方法论

**核心思想**：
对 LLM 某次推理得到的最终隐藏状态施加**有针对性的对抗扰动（targeted adversarial perturbations）**，观察模型表征对这些扰动的反应；将反应中蕴含的稳定性特征提取出来，作为二分类任务的输入，判断该次推理的答案是否正确；最终用分类器输出作为置信度估计。

**关键技术细节**：
1. **对抗扰动**：扰动并非随机噪声，而是经过针对性设计的对抗扰动，目的是测试表征的鲁棒性——正确推理的表征通常更“稳”，受扰动影响更小或更具结构可预测性。
2. **特征提取**：从扰动前/后的隐藏状态中提取能反映稳定性特征的表示（如状态偏移幅度、方向一致性、拓扑邻域关系等），形成特征向量。
3. **轻量分类器**：将特征向量输入一个轻量级判别器（非 LLM），预测该回答是否错误。
4. **置信度映射**：分类器输出的概率即可作为置信度信号，实现对“置信度”的再校准。

**流程文字说明**：
- 输入问题 → LLM 正常前向推理 → 得到答案和最终层隐藏状态；
- 对隐藏状态施加一组针对性扰动，重新前向得到受扰动后的表征；
- 对比扰动前后的表征差异，提取稳定性特征；
- 训练轻量分类器（在标注验证集上），输入该特征，输出“答案正确”的概率；
- 该概率即作为修正后的置信度估计。

## 3. 实验设计

**数据集与场景**：
- 使用 **MMLU** 和 **MMLU-Pro** 基准；
- 包含三种 MMLU 变体设置（论文中称 “three MMLU variants”，可能涉及不同子集或难度切分）；
- 同时覆盖**多项选择（multiple-choice）**与**开放式生成（open-ended）格式**两种回答方式；
- 模型范围为 **8B 到 32B 参数**，涵盖 **Llama、Qwen、Mistral** 三大架构家族；
- 共使用了 4 个不同规模的 LLM 进行评测。

**对比方法**：
- 与当前（prior/state-of-the-art）最强的置信度校准方法对比；
- 论文提到结果相对“最强现有方法”（strongest prior method）进行了相对改进比较。

## 4. 资源与算力

- 论文提供的摘要与元数据中**未具体指定 GPU 型号、数量、训练时长等算力信息**；
- 模型规模 8B–32B 的推理与扰动实验本身开销较大，但论文称其方法是**高效的（efficient）**；
- 需要指出：由于提取的只是中间隐藏状态并采用轻量分类器，相比在多个 LLM 模型上展开微调或进行大量采样，其额外开销相对有限，但原文未给出精确的算力/时间数字。

## 5. 实验数量与充分性

论文摘要透露的实验范围：
- **4 个 LLM × 3 种 MMLU 变体**，且在每个上都覆盖了多项选择和开放式两种回答模式；
- 指标评测包括：
  - Expected Calibration Error（ECE）↓
  - Brier Score ↓
  - 准确率（Accuracy）↑
  - AUPRC ↑
  - AUROC ↑

关于充分性的评价：
- **充分性中等偏上**：覆盖了多个架构和多尺寸、两种回答格式、多个评估指标；在内部一致性上可信；
- **还需注意**：摘要只给出了相对改进百分比的汇总数字，缺乏具体基线数值及数据集的逐一细粒度结果（完整表格可能在正式论文图中）；
- 是否存在消融实验、是否报告误差线等细节在摘要中未体现，需参考全文才可作最终判断。

## 6. 论文的主要结论

- CCPS 在多个 LLM（8B 到 32B，Llama/Qwen/Mistral）和 MMLU/MMLU-Pro（多项选择 + 开放式）上都显著优于现有最强方法；
- 具体相对改进为：
  - **ECE 降低约 55%**；
  - **Brier Score 降低 21%**；
  - **准确率提高 5 个百分点**；
  - **AUPRC 提高 4 个百分点**；
  - **AUROC 提高 6 个百分点**；
- 结论：对最终隐藏状态施加扰动并探测表征稳定性的方法，可以提供高效、通用且更准确的 LLM 置信度度量，从而增强模型可靠性。

## 7. 优点

- **方法新颖性**：将“扰动对抗鲁棒性”作为校准信号，这一思路超越传统基于 logit 或 softmax 概率的校准方法；
- **干预成本低**：只需获取模型的最终隐藏状态并使用轻量分类器，无需重新训练 LLM 或修改损失函数；
- **通用性好**：在多类型架构（Llama/Qwen/Mistral）和多参数规模（8B–32B）上稳定提升；
- **覆盖任务类型广**：同时验证了多项选择格式和开放式生成格式下的效果，开放式设置更贴近真实应用；
- **提升幅度显著**：相对于最强已有方法，ECE 和 Brier score 的下降程度非常可观。

## 8. 不足与局限

- **实验数据集覆盖有限**：仅使用 MMLU/MMLU-Pro，主要属于知识问答型任务，未覆盖数学推理、代码生成、多轮对话、医学/金融专门领域或更长上下文场景，推广性仍需验证；
- **模型规模区间中等**：覆盖了 8B–32B，但未覆盖更小（如 <1B）或超大（如 70B+）模型，无法判断方法在小模型或前沿超大模型上的适用性；
- **依赖最终层隐藏状态与对抗扰动设计**：扰动策略的选取可能影响结果对不同任务、架构的泛化程度；扰动构造本身也可能涉及额外的积分式计算成本；
- **有监督分类器需要标注数据**：训练分类器需要一定数量的、带有正确/错误标注的推理样本，跨域转移时可能需重新收集标注；
- **信息完整度限制**：摘要中未披露各单独数据集实验的具体数值与误差范围，也未交代是否与 Self-Consistency、Logit-based 等常用校准方法的逐项对比细节；分析完整性和复现友好性有待正式全文补充；
- **置信度阈值的实际应用涵义**：对分类器输出的校准概率在极端分布（如正确率极高或极低）下的表现，未在当前文本中说明。

（完）
