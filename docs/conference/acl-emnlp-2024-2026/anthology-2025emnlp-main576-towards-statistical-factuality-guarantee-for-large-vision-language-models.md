---
title: Towards Statistical Factuality Guarantee for Large Vision-Language Models
title_zh: 面向大规模视觉语言模型的统计事实性保障
authors: "Zhuohang Li, Chao Yan, Nicholas J Jackson, Wendi Cui, Bo Li, Jiaxin Zhang, Bradley A. Malin"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.576.pdf"
tags: ["query:faithfulness"]
score: 6.0
evidence: 面向生成事实性的统计保形框架，过滤与输入证据不一致的不可靠声明，可迁移至证据约束生成
tldr: 大型视觉语言模型的生成文本常与图像输入不一致，安全关键应用中亟需可靠的事实保障。ConfLVLM 将每个生成细节视为假设，用高效的不确定度量做统计检验，并基于保形预测提供有限样本无分布的事实性保障。在通用图像理解、医学影像报告和文档等场景的实验显示它能有效过滤不可靠声明。该方法为证据约束生成中的事实性筛选提供了统计可迁移的工具。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1595, \"height\": 906, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 586, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 586, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 587, \"height\": 634, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 786, \"height\": 641, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 798, \"height\": 534, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 779, \"height\": 269, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 700, \"height\": 1102, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 802, \"height\": 300, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 801, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 804, \"height\": 301, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 701, \"height\": 288, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 581, \"height\": 313, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 576, \"height\": 311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 575, \"height\": 309, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 635, \"height\": 1484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 633, \"height\": 1484, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 635, \"height\": 1488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 806, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 807, \"height\": 721, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 805, \"height\": 712, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 791, \"height\": 927, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 790, \"height\": 940, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 790, \"height\": 931, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1447, \"height\": 1949, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1636, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main576/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1630, \"height\": 879, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main576/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 679, \"height\": 480, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main576/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 785, \"height\": 519, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main576/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 524, \"label\": \"Table\"}]"
motivation: 视觉语言模型在图像条件文本生成中仍会出现与视觉输入不一致的幻觉，阻碍安全关键场景应用。
method: 提出 ConfLVLM，用保形预测框架将生成的每个细节作为假设，通过不确定性量度进行统计检验并过滤不可靠声明。
result: 在通用场景理解、医学放射报告生成和文档等应用上验证了该方法能有效滤除幻觉，提供统计保障。
conclusion: ConfLVLM 为图像条件文本生成提供了可保证的事实性方法，其声明过滤思想可推广到证据约束生成。
---

## Abstract
Advancements in Large Vision-Language Models (LVLMs) have demonstrated impressive performance in image-conditioned text generation; however, hallucinated outputs–text that misaligns with the visual input–pose a major barrier to their use in safety-critical applications. We introduce ConfLVLM, a conformal-prediction-based framework that achieves finite-sample distribution-free statistical guarantees to the factuality of LVLM output. Taking each generated detail as a hypothesis, ConfLVLM statistically tests factuality via efficient heuristic uncertainty measures to filter out unreliable claims. We conduct extensive experiments covering three representative application domains: general scene understanding, medical radiology report generation, and document understanding. Remarkably, ConfLVLM reduces the error rate of claims generated by LLaVa-1.5 for scene descriptions from 87.8% to 10.0% by filtering out erroneous claims with a 95.3% true positive rate. Our results further show that ConfLVLM is highly flexible, and can be applied to any black-box LVLMs paired with any uncertainty measure for any image-conditioned free-form text generation task while providing a rigorous guarantee on controlling hallucination risk.

---

## 论文详细总结（自动生成）

# 《面向大规模视觉语言模型的统计事实性保障》（ConfLVLM）论文要点总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：大型视觉语言模型（LVLMs）结合了 LLM 与视觉模块，在图像条件下的文本生成方面表现出色，已被应用于病理分析、GUI 智能体、自动驾驶等场景。
  
- **核心问题**：LVLMs 生成的文本常常与视觉输入不一致，即出现“幻觉”（hallucination）——包括物体幻觉（虚构不存在的物体）、属性幻觉（颜色/形状/材料错误）、关系幻觉（空间关系、交互错误等）。这在医疗、金融等安全关键领域严重制约了模型的可信采用。

- **现有方法局限**：
  - 一条研究路线建立幻觉 benchmark 与度量指标，但多数聚焦于判别式 VQA 中的物体幻觉，较少覆盖自由文本生成；且只是分析而非修正。
  - 另一条路线是训练/微调阶段的干预或推理阶段的解码优化（如 VCD、ICD），但资源开销大，需要模型重训练或白盒访问，灵活性低。
  - 事后修正类方法虽兼容黑盒模型，但本质依赖启发式策略，缺乏严格的统计事实性保障。

- **整体含义**：本文提出的 ConfLVLM 是第一个面向 LVLM 自由文本生成任务、基于保形预测实现对幻觉风险进行有限样本、无分布假设的统计保证的通用框架，为安全关键场景中的多模态内容可信性提供了可量化的控制手段。

## 2. 方法论：核心思想、关键技术细节与算法流程

### 2.1 核心思想
- 将 LVLM 生成的自由文本分解为一系列独立的、可验证的“声明”（claims），把每个声明当作假设（hypothesis）。
- 用判别性机制（LVLM 自身或外部轻量模型）计算每个声明与图像之间的“一致性分数”（conformity score）。
- 借助 **Split Conformal Prediction (SCP)** 校准过滤阈值，过滤低置信声明，以实现用户指定的误差控制目标：
  \[
  P(L(Y^*_{n+1}, I_{n+1}) \le \lambda) \ge 1-\alpha
  \]

### 2.2 算法流程（四个算子）
1. **初始假设生成**：从 LVLM 采样初始响应 \(Y_{n+1}\)。
2. **分解（D）**：将响应分解为独立的声明集合 \(C_{n+1} = D(Y_{n+1})\)。
3. **个体假设检验（F）**：通过过滤算子 \(F(C_{n+1};\tau):=\{C_j: r(C_j,I) > \tau\}\)，仅保留评分超过阈值的声明。
4. **合并（M）**：将过滤后的声明合并成最终响应 \(Y^* = M(F(C_{n+1};\tau))\)。

### 2.3 校准过程
- 对每个校准样本，定义一致性分数为可使过滤后损失控制在容忍度内的最小阈值：
  \[
  S(C_i, I_i) = \inf\{ \tau : L(F(C_i;\tau),I_i) \le \lambda \}
  \]
- 阈值 \(\hat{\tau}\) 取校准集中所有一致性分数的第 \(\lceil (n+1)(1-\alpha)\rceil / n\) 分位数。
- **Theorem 3.1**（基于 SCP）：在可交换性假设下，对任意 \(\alpha \in (1/(n+1), 1)\)：
  \[
  P(L(\hat{F}(C_{n+1}), I_{n+1}) \le \lambda) \ge 1-\alpha
  \]
  若损失函数是单调的，还满足几乎 tight 的上界：
  \[
  1-\alpha+\frac{1}{n+1} \ge P(\cdot)
  \]

### 2.4 一致性评分的具体实现
- **内部分数（Internal Scores）**：
  - LogP-Text：仅基于文本提示的语言先验概率；
  - LogP-Image：基于文本提示+视觉特征的联合条件概率；
  - LogP-Ratio：两者对数概率之差（用于度量视觉信息增益，抑制语言先验主导的幻觉）。
- **外部分数（External Scores）**：使用能量模型（如 CLIP、BiomedCLIP、LayoutLMv3）计算文本声明与图像的匹配度（如负能量或余弦相似度）。

## 3. 实验设计：数据集 / 场景 / 基准与对比方法

### 3.1 三个应用场景及数据集
| 场景 | 数据集 | 任务 |
|------|--------|------|
| I. 通用场景理解 | MSCOCO 验证集（500 张图） | 生成详细图像描述 |
| II. 医学报告生成 | MIMIC-CXR（500 张胸部 X 光片） | 生成放射学报告 |
| III. 文档理解 | SROIE 发票数据集（500 张） | 发票条目识别/信息抽取 |

### 3.2 考察的 LVLMs
- 场景 I：LLaVA-1.5、Phi-3.5-vision-instruct、Llama-3.2-11B-Vision（开源）和 GPT-4o-mini（闭源）
- 场景 II：LlaVa-Med、CvT2DistilGPT2（用不重叠 MIMIC-CXR 子集重训以防数据泄漏）、MAIRA-2
- 场景 III：LLaVA-Next、Phi-3.5-vision-instruct

### 3.3 外部评分模型
- 场景 I：CLIP-ViT-Base（patch 32）与 CLIP-ViT-Large（patch 14）
- 场景 II：BiomedCLIP
- 场景 III：LayoutLMv3

### 3.4 基线/对比方法
- **Vanilla LVLM**：无过滤的原始输出。
- **Random Filtering**：均匀随机丢弃 α 比例的声明。
- 附录中的启发式对比：Woodpecker（外部工具模型驱动的事后纠正）、Chain-of-Verification (CoVe)、Visual Contrastive Decoding (VCD)、Instruction Contrastive Decoding (ICD)。

### 3.5 错误标注与损失函数
- 场景 I：五类错误——物体识别（loss=3）、属性、空间关系、交互/动作、定量信息（各 loss=1）。
- 场景 II：三项错误——冲突错误（loss=3）、不合理错误（loss=2）、似是而非错误（loss=1）；标注时提供医生撰写的地面真实报告给 GPT-4o 辅助判断。
- 场景 III：字段误解与条目错误（loss=2）、数值/日期错误（loss=3）、其他（loss=1）。
- 使用 GPT-4o 辅助标注，并通过人类标注者的 ICC 验证（ICC = 0.85）且与 Gemini-1.5-pro 对照 ICC = 0.81。

## 4. 资源与算力

- 论文正文未明确报告 GPU 类型、数量或训练/推理时间等具体算力配置。
- 仅在部分说明中提及使用开源模型（LLaVA-1.5 等）和专有闭源 API（GPT-4o-mini、GPT-4o、Gemini-1.5-pro）作为辅助标注/评分的工具，以及重训 CvT2DistilGPT2 以避免数据泄漏（未给出重训资源）。
- 建议读者关注其代码库（论文未给出链接）或相关开源仓库获取可复现环境信息。

## 5. 实验数量与充分性评估

- **数据规模与实验量**：
  - 共覆盖 **81,000+ 条声明**，来自 8 个流行 LVLM，三大类任务。
  - 每个场景约 500 张图，按 400/100 切分校准/测试集，50 次随机切分取平均。
  - Table 1 展示了 4 个 LVLM 在 α=0.1, λ=0 时相对于 Vanilla 与 Random Filtering 的 claim 级 TPR/F1 对比。
  - Table 3 补充不同 (α, λ) 组合下响应级与声明级结果。
  - Table 2 与 Woodpecker、CoVe、VCD、ICD 等事后/解码式方法对比（100 张图、788 条声明）。

- **消融与分析维度**：
  - 不同评分函数（3 种内部 + 1-2 种外部）与不同 LVLM 的交互。
  - 误差容忍度 λ（0、1、2、3）对过滤率、弃权率的影响。
  - 校准数据规模（n=50~400）对覆盖率和方差的稳健性。
  - 人类评分者与原模型内部置信度之间的关系。

- **充分性评估**：
  - **优点**：任务类型多（通用、医学、文档）、模型覆盖度广（开源+闭源、专用+通用）、评分函数多元（黑盒模型、外部判别模型、专用领域模型），且涵盖了与大流量启发式解码方法的对照。
  - **不足**：医学与文档任务中各只选一个外部评分模型（BiomedCLIP / LayoutLMv3），缺少跨评分模型充分对比；启发式对比仅在 LLaVA-1.5 + 场景 I 的小样本（100张图）上进行，规模略弱；校准/测试集可交换性假设仅依赖随机划分，未验证天然分布漂移下的边界行为。

## 6. 主要结论与发现

1. **有效性**：ConfLVLM 可显著降低 LVLM 生成内容的幻觉率。如 LLaVA-1.5 在场景描述中错误率从原始 87.8% 降至 10.0%（α=0.1, λ=0 时），且以 95.3% 的真实阳性率过滤错误声明。
2. **通用性**：对任意黑盒 LVLM + 任意评分函数均可实现期望覆盖率（empirical coverage≈desired coverage），对模型架构、复杂度与应用目的没有约束。
3. **灵活性**：误差容忍度 λ 提供了“覆盖率-效用”调节旋钮；用户可依据任务风险选择最严格（λ=0）或较宽松配置；较高的 λ 可显著提高保留的信息量并降低弃权率。
4. **外部模型优于内部评分**：在多数任务中专用/小型判别模型（CLIP、BiomedCLIP、LayoutLMv3）的评分比 LVLM 自身内部置信度更好，过滤得少但更精准，说明轻量判别模型适合用来作为性能较高且成本低的事实性审核器。
5. **校准数据量影响有限**：n=50 即可达到目标覆盖率（方差略大），增大校准集可减小方差但中位数稳定。
6. **模型能力差距**：GPT-4o-mini 原始事实性最好，需要过滤/弃权的比例也最低；医学专用模型（CvT2DistilGPT2、MAIRA-2）明显优于通用书生模型 LLaVA-Med。

## 7. 亮点与优点

- **理论保障首度落地**：第一次系统地、以数学证明的形式把 conformal prediction 的有限样本无分布覆盖率保证迁移到 LVLM 图像条件自由文本生成这一开放性任务上，提供通用、可量化的幻觉风险控制。
- **框架模块化且可扩展**：分解（D）、评分（r）、过滤（F）、合并（M）各模块均可独立替换/改进；
- **黑盒友好**：无需模型重训练、微调或白盒访问，与现有专有 API 兼容。
- **丰富的误差与损失定义**：将不同类型幻觉映射为差异化损失（更严重的对象/数值/日期错误赋予更高权重），更贴近真实世界风险等级。
- **严格的数据防泄漏**：对 CvT2DistilGPT2 在不重叠数据集上重训，避免因原模型在 MIMIC-CXR 上训练导致的评估作弊问题。
- **提供了大量的经验验证与基准对照**：特别是与 Woodpecker、CoVe、VCD、ICD 的直接比较较为少见，证明本框架优于现有启发式手段。

## 8. 不足与局限

- **理论适用条件**：标准保形框架要求校准集与测试集可交换，文中未对实际流式环境的分布漂移问题做系统评测；仅在讨论中提示可通过更新校准集或引入 OOD 检测层缓解。
- **效用与事实性的固有冲突**：更强的保证意味着过滤更多有效内容、增加弃权率，会降低信息量（recall）。本文未解决“保留高覆盖率的同时不牺牲信息利用率”的深层问题。
- **评分函数的优劣依赖任务**：场景 I 中的 CLIP 对大而长的复杂声明（如 GPT-4o-mini 的多细节描述）处理能力有限，导致过滤效率比在小声明上低；目前仍缺乏一个通用的“最强”评分机制。
- **错误标注依赖 LLM**：主要使用 GPT-4o 标注（虽经验证 ICC 较高），仍无法完全排除 LLM 标注偏差对 loss/覆盖率计算的潜在影响。
- **未进行大规模计算资源优化讨论**：虽然声称框架通用，但并没有与更轻量或模型内建的不确定性估计方法（如自一致性采样、分散校准）做系统对比，也缺少真正小样本与长尾场景的系统分析。
- **应用边界**：在处理开放域自由目标、或幻觉定义特别模糊（如断言性问题的“部分正确”）时，本文的声明划分与损失设定仍较粗，需要针对特定领域仔细调参。

（完）
