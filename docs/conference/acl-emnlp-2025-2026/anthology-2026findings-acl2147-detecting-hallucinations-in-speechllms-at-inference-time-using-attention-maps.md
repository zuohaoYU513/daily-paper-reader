---
title: Detecting Hallucinations in SpeechLLMs at Inference Time Using Attention Maps
title_zh: 使用注意力图在推理时检测语音大语言模型中的幻觉
authors: "Jonas Waldendorf, Bashar Awwad Shiekh Hasan, Evgenii Tsymbalov"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2147.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 基于注意力图的语音大语言模型幻觉检测方法，与文本幻觉检测技术相通
tldr: 语音大语言模型（SpeechLLM）在实际部署中容易出现幻觉，而现有检测方法要么依赖成本高昂的金标准输出，要么没有针对音频特有的错误信号进行设计。本文从模型的注意力分布中提取四种指标，包括 AudioRatio、AudioConsistency、AudioEntropy 和 TextEntropy，并基于这些特征训练轻量级逻辑回归分类器，在推理阶段高效识别幻觉。在自动语音识别和语音到文本翻译两项任务上，使用 Qwen-2-Audio 和 Voxtral-3B 的实验表明，该方法能够明显提升幻觉检测效果且不需要金标准输出。这套基于注意力模式的检测框架为语音大语言模型的可靠性保障提供了实用且可迁移的解决方案。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2147/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1641, \"height\": 547, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2147/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 773, \"height\": 643, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2147/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1644, \"height\": 1641, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 817, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 816, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 814, \"height\": 739, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 813, \"height\": 736, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 817, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 816, \"height\": 677, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 816, \"height\": 676, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 768, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 849, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 570, \"height\": 383, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 657, \"height\": 408, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2147/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 659, \"height\": 412, \"label\": \"Table\"}]"
motivation: 语音大语言模型推理时易产生幻觉，现有检测依赖金标准且未利用音频特有信号。
method: 提取四种注意力衍生指标并训练轻量级逻辑回归分类器，进行推理时幻觉检测。
result: 在语音识别和语音到文本翻译任务上验证了该方法无需金标准即可有效检测幻觉。
conclusion: 提供了一种轻量、可迁移的语音LLM幻觉检测方案，也可启发其他模态的检测。
---

## Abstract
Hallucinations in Speech Large Language Models (SpeechLLMs) pose significant risks, yet existing detection methods typically rely on gold-standard outputs that are costly or impractical to obtain. Moreover, hallucination detection methods developed for text-based LLMs do not directly capture audio-specific signals. We investigate four attention-derived metrics: AudioRatio, AudioConsistency, AudioEntropy, and TextEntropy, designed to capture pathological attention patterns associated with hallucination, and train lightweight logistic regression classifiers on these features for efficient inference-time detection. Across automatic speech recognition and speech-to-text translation tasks, evaluations on Qwen-2-Audio and Voxtral-3B show that our approach outperforms uncertainty-based and prior attention-based baselines on in-domain data, achieving improvements of up to +0.23 PR-AUC, and generalises to out-of-domain ASR settings. We further find that strong performance can be achieved with approximately 100 attention heads, improving out-of-domain generalisation compared to using all heads. While effectiveness is model-dependent and task-specific training is required, our results demonstrate that attention patterns provide a valuable tool for hallucination detection in SpeechLLMs

---

## 论文详细总结（自动生成）

# 论文总结：Detecting Hallucinations in SpeechLLMs at Inference Time Using Attention Maps

## 1. 核心问题与整体含义（研究动机与背景）

- 语音大语言模型（SpeechLLM）在语音识别（ASR）和语音到文本翻译（S2TT）等任务中可能产生幻觉输出——即流畅但未基于输入音频的虚假内容，带来严重风险。
- 现有幻觉检测方法存在两大不足：
  - 多依赖金标准（gold-standard）输出进行比对，标注成本高、实际部署中难以获取。
  - 文本LLM的幻觉检测方法未针对音频模态的特有信号（如音频帧与输出token之间的长序列对齐关系）进行设计。
- 本文的核心动机是：利用SpeechLLM内部的注意力模式，在推理时无需金标准即可高效检测幻觉，为实现轻量、可在线部署的幻觉过滤提供方案。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：当模型生成未基于输入的幻觉内容时，注意力图会呈现病态模式，例如：
  - 音频-文本的对角对齐结构退化；
  - 注意力回退到音频输入的早期片段。
- **四大注意力指标**（每个指标在每个解码步计算，再对所有时间步取平均，形成每层每头的特征）：
  - **AudioRatio**：注意力分配到音频输入token与自回归文本token的比率，衡量模型对音频的依赖程度。
  - **AudioConsistency**：相邻解码步之间音频注意力向量的Pearson相关系数，捕捉注意力“回退”到音频开头导致分布相似度升高的情况。
  - **AudioEntropy**：对注意力权重在音频token上重归一化后计算的熵，反映对音频输入的不确定性。
  - **TextEntropy**：对文本输入token注意力重归一化后的熵，捕捉文本注意力头的不确定性。
- **分类器**：将各指标的层×头特征拼接为特征向量，训练**轻量级逻辑回归（Logistic Regression）** 分类器作为幻觉检测器。
- **特征选择**：
  - L2正则化模型按系数幅度（乘以原始特征标准差）排序选择Top N头；
  - L1正则化模型进行特征剪枝，保留在5折交叉验证中≥4折非零的特征，称“Stable Features”模型。
- 整体流程：提取注意力特征 → 特征标准化（Min-Max） → 训练逻辑回归 → 推理时输出幻觉概率。

## 3. 实验设计

- **任务与数据集**：
  - **ASR**：
    - VoxPopuli（英、德、法、西，共7,080条测试句，40,000条训练句）
    - CALLHOME（英文，3,916条，作为域外测试集）
  - **S2TT**：FLEURS（英→德/西/法，德/西/法→英，共4,613条测试样本）
- **模型**：Qwen-2-Audio、Voxtral-3B
- **幻觉标注**：
  - ASR：人工标注1,950条校准自动标注阈值，自动标注公式为 `Hallucination = I[WER + SHS > 0.7]`，高精度（0.979）、低召回（0.443）。
  - S2TT：用XCOMET-XL分数将最低5%的样本标记为幻觉。
- **对比方法（Baselines）**：
  - 不确定性估计：Mean Entropy、Perplexity
  - 注意力基线：RAUQ Entropy、Attention Score
  - 随机猜测
- **评估指标**：F1、Precision、Recall、PR-AUC，以及预测拒绝比（PRR@10%或30%）。

## 4. 资源与算力

- 文中明确说明：
  - 使用**8块A100-40GB GPU**。
  - 推理速度约4.5样本/秒。
  - 一次完整实验覆盖约57,000条ASR句子和21,000条S2TT句子，需约38.5 GPU小时。
  - 开发和评估阶段进行了约6轮完整迭代，总计约230 GPU小时，加上XCOMET评分和SHS计算，估计上限约300 GPU小时。

## 5. 实验数量与充分性

- 实验数量丰富：
  - 两个SpeechLLM、两个任务（ASR/S2TT）、多个数据集与语言方向；
  - 多种特征配置（Combined、AudioRatio Only、Top N、Top 25、Stable Features）；
  - 多个基线对比；
  - 域内/域外泛化测试；
  - 特征数量消融（图2展示PR-AUC随注意力头数变化）；
  - 任务间头部重叠分析（表8）；
  - 定性案例分析（附录E）。
- 充分性评价：
  - 覆盖了主要任务和数据集，对比了多种基线和特征组合，实验设计整体合理且客观。
  - 但仅使用两个模型、四个语言，且自动标注策略低召回可能带来偏差，限制了结论的普适性。

## 6. 主要结论与发现

- **注意力特征有效**：在域内ASR上，本文方法优于不确定性基线和已有注意力基线，Voxtral-3B上PRAUC提升最高达+0.23。
- **域外泛化依赖模型**：Voxtral-3B在CALLHOME上表现良好；Qwen-2-Audio在CALLHOME上因阈值偏移导致F1下降，但PR-AUC仍与域内相当。
- **约100个注意力头即可**：减少特征数量可在牺牲少量域内性能的同时提升域外泛化（Stable Features模型在CALLHOME获得最高PR-AUC 0.64）。
- **ASR与S2TT之间不可迁移**：ASR训练的模型在S2TT上几乎随机；S2TT需要任务专属训练数据，且任务间注意力头重叠低。
- **S2TT上方法仍有效**：在S2TT数据上训练后，相比基线明显提升（Qwen-2-Audio PRAUC 0.25→0.44；Voxtral-3B 0.17→0.44）。
- **不确定性基线在噪声数据上更强**：CALLHOME的噪声特性使其不确定性指标更有效，而注意力方法在更干净的数据上优势更明显。

## 7. 优点

- **无需金标准**：完全基于内部注意力信号，推理时即可检测，适合在线过滤和低成本的离线筛选。
- **轻量高效**：逻辑回归分类器简单、计算开销小，且提取注意力特征的开销远低于完整模型推理。
- **音频定制化**：四个指标专门针对音频-文本注意力动态设计，如AudioConsistency捕捉音频长序列中的注意力回退。
- **系统性实验**：覆盖两种任务、多语言、多数据集，进行了特征数量、模型差异、任务迁移等多维分析，并附带定性示例。
- **可解释性**：利用注意力头选择分析揭示任务依赖性和模型差异，为后续研究提供洞察。

## 8. 不足与局限

- **标注偏差**：自动标注策略高精度低召回（0.979/0.443），许多真实幻觉被遗漏，可能影响训练信号质量。
- **任务不可迁移**：ASR训练的检测器无法泛化到S2TT，需任务专属训练数据，限制了方法的即插即用性。
- **模型依赖性强**：不同模型表现差异大（Qwen-2-Audio域外泛化较弱），方法有效性缺乏跨模型稳定性。
- **覆盖范围有限**：仅两个SpeechLLM、四种语言（英德法西），未覆盖更多语言、方言或更复杂语音场景。
- **仅二分类**：只区分严重幻觉与非幻觉，未建模幻觉类型或严重程度。
- **额外的推理开销**：虽然相对模型推理较轻，但提取注意力图仍需额外计算和内存，对延迟敏感部署可能构成负担。
- **未与参考式方法直接对比**：未与依赖金标准的监督方法（如Frieske & Shi 2024）进行定量比较，仅强调其部署成本高。

（完）
