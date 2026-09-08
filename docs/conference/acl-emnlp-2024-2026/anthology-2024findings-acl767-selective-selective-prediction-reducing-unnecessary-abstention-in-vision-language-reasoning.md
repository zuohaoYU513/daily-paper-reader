---
title: "Selective “Selective Prediction”: Reducing Unnecessary Abstention in Vision-Language Reasoning"
title_zh: 选择式预测再选择：减少视觉语言推理中的不必要弃权
authors: "Tejas Srinivasan, Jack Hessel, Tanmay Gupta, Bill Yuchen Lin, Yejin Choi, Jesse Thomason, Khyathi Chandu"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.findings-acl.767.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 降低视觉语言模型低置信度时的过度拒答，通过补充提取图像线索来优化选择预测。
tldr: 在视觉语言选择性推理中，当系统对错误容忍度很低时，直接按置信度斥答往往过于谨慎而导致许多本可答对的样本被弃权。论文提出推理期算法ReCoVERR：当低置信度预测出现时，算法不立刻弃权，而是启动LLM在图像中寻找与预测相关的证据来复核，并据此决定是否收回该预测。实验表明它能在不提高错误率的前提下显著降低弃权比例，为基于自判断的自适应接受与拒答路由提供了可迁移的方法。
source: ACL-2024-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl767/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 220, \"height\": 152, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl767/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 802, \"height\": 129, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl767/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1580, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl767/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1577, \"height\": 511, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-findings/anthology-2024findings-acl767/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 793, \"height\": 419, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 1011, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 825, \"height\": 727, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 708, \"height\": 574, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 711, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 765, \"height\": 575, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1511, \"height\": 538, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1743, \"height\": 2326, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-findings/anthology-2024findings-acl767/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1706, \"height\": 655, \"label\": \"Table\"}]"
motivation: 在错误容忍度较低的选择性预测场景中，模型容易过度谨慎，把许多正确预测也一并弃权。
method: 提出ReCoVERR算法，在低置信度时不直接弃权，而是让LLM从图像中寻找相关性证据来支持预测。
result: 实验显示该方法在维持系统错误率不增加的同时有效减少不必要的弃权。
conclusion: 以证据复核替代单纯的置信度拒答，可在选择性推理中兼顾准确率和覆盖率。
---

## Abstract
Selective prediction minimizes incorrect predictions from vision-language models (VLMs) by allowing them to abstain from answering when uncertain. However, when deploying a vision-language system with low tolerance for inaccurate predictions, selective prediction may be over-cautious and abstain too frequently, even on many correct predictions. We introduce ReCoVERR, an inference-time algorithm to reduce the over-abstention of a selective vision-language system without increasing the error rate of the system’s predictions. When the VLM makes a low-confidence prediction, instead of abstaining ReCoVERR tries to find relevant clues in the image that provide additional evidence for the prediction. ReCoVERR uses an LLM to pose related questions to the VLM, collects high-confidence evidences, and if enough evidence confirms the prediction the system makes a prediction instead of abstaining. ReCoVERR enables three VLMs (BLIP2, InstructBLIP and LLaVA-1.5) to answer up to 20% more questions on the VQAv2 and A-OKVQA tasks without decreasing system accuracy, thus improving overall system reliability. Our code is available at https://github.com/tejas1995/ReCoVERR.

---

## 论文详细总结（自动生成）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：视觉语言模型（VLM）在视觉推理任务（如 VQA）上表现出色，但为了部署时需要控制错误率，系统应允许模型在不确定时主动弃权（abstain），即选择性预测（Selective Prediction）。典型做法是设置置信度阈值，低于阈值的预测直接弃权。
- **核心问题**：在错误容忍度低的应用场景下，基于阈值的"朴素的"选择性预测往往**过度保守**——大量本来正确的预测也被弃权，导致覆盖率极低、系统实用性大打折扣。文中举例：若要求 BLIP2 在 A-OKVQA 上至少有 90% 的准确率，朴素选择性预测仅能回答 4% 的问题，**94% 的正确预测被白白弃权**。
- **核心洞察**：VLM 虽然对某些问题回答的置信度较低，但它往往能以高置信度正确回答该问题的**子问题**（即提取图像中的隐含证据）。例如，模型不确定"地板有几种颜色"，但能高置信度回答"地板是红白相间"，后者的证据足以验证前者的预测。
- **整体含义**：该论文挑战了"低置信度即弃权"的单一做法，提出通过推理时的**证据收集与验证**来判别弃权是否确实必要，从而在不降低系统可靠性的前提下减少不必要的弃权。

## 2. 论文提出的方法论

### 2.1 整体框架

提出 **ReCoVERR**（Reason by Collecting Visual Evidences that are Reliable and Relevant）——一个**推理时算法**，无需任何额外训练即可应用。

### 2.2 核心思想

当 VLM 对原始问题给出低置信度预测时，不立即弃权，而是启动**多轮检索-验证机制**：用 LLM 生成与原始问题相关的子问题，提问 VLM 获得答案；保留其中**可靠的**（VLM 高置信度）且**相关的**（对判断原预测正确性有用）证据；若收集到的证据以足够高的置信度**蕴含（entail）原预测**，则回答原问题，否则弃权。

### 2.3 算法流程（文字说明）

1. **初始预测**：VLM 对问题 $(I, Q)$ 生成答案 $a$ 及置信度 $\pi_{VLM}(a)$。
2. **阈值判断**：若 $\pi_{VLM}(a) \ge \gamma@r$（$r$ 为用户指定的风险容限），直接返回 $a$；否则进入验证阶段。
3. **假设转换**：用语言模型 $M_{QA→S}$ 将问答对 $(Q, a)$ 改写为声明式**假设句** $H$（如 Q: "地板上瓷砖有几种颜色？" A: "两种" → H: "地板有两种颜色的瓷砖"）。
4. **初始化证据**：通过一组视觉工具（LVIS 目标检测 + Qwen-VL 区域描述）获取图像的通用视觉描述，将其纳入证据集。
5. **多轮证据收集（至多 N 轮）**：
   - 使用问题生成模型 $M_{QGen}$（GPT-3.5 等）基于原始问题和已有可靠证据，生成 K 个子问题；
   - 将每个子问题输入 VLM，获得答案、置信度和改写后的声明句，构成证据 $e_j$；
   - **可靠性筛选**：仅保留 VLM 置信度 $\pi_{VLM}(a_j) \ge 1-r$ 的证据；
   - **相关性筛选**：使用 NLI 模型的**可废止推理**（defeasible reasoning）计算相关性分数——即对比证据句及其反事实句对假设蕴含概率的影响差 $\delta(e_j) = |\pi_{NLI}(H|S_j) - \pi_{NLI}(H|\bar{S_j})|$，仅保留 $\delta(e_j) \ge \delta_{min}$ 的证据；
   - **充分性检验**：将所有可靠且相关的证据句拼接为前置条件，计算 $H$ 的蕴含概率 $\pi_{NLI}(H|S_{RR})$；若 $\ge \pi_{NLI}^{min}$，则返回原预测 $a$。
6. **最终弃权**：N 轮后仍无法验证则返回 ∅。

### 2.4 两个关键前提

- **置信度校准**：VLM 的置信度估计需要校准良好。作者对比了三种置信度获取方式（token 概率乘积、token 概率均值、**Self-Prompting**——即让 VLM 自问自答"该答案是否正确"，再看 yes/no 的归一化概率），并结合 Platt Scaling 校准。
- **可验证性**：VLM 能以高置信度检索出图像中与原始低置信度预测相关的事实性线索。

## 3. 实验设计

### 3.1 数据集

| 数据集 | 用途 | 规模 |
|---|---|---|
| **A-OKVQA** | 主要实验基准（需外部知识与常识推理） | 验证集 1,075 问 |
| **VQAv2** | 迁移/泛化验证 | 验证集抽取 1,000 问 |
| **OK-VQA** | 任务迁移测试 | 验证集 5,046 问 |
| **Sherlock** | 任务迁移测试（反事实推理） | 561 个三元组（经作者改写为二分类格式） |

### 3.2 评估指标

- **Risk (R)**：已预测问题中的错误率；
- **Coverage (C)**：系统做出预测的题数占比；
- **Effective Reliability (Φ₁)**：正确预测奖励 1、错误预测惩罚 1、弃权 0；
- **Selective Prediction Recall (RSP)**：正确预测中被系统回答出来的比例。

答案正确性用 **LAVE（GPT-3.5）** 评测，而非严格的精确字符串匹配。

### 3.3 基线方法

- **Vanilla Select Prediction**：简单置信度阈值法。
- **Vision Tools**：只做一步证据注入（将 LVIS 检测、Qwen-VL 区域描述等直接送入 NLI 模型），没有多轮问答收集环节。

### 3.4 消融与扩展实验

- 分别移除/放宽 ReCoVERR 的**可靠性**与**相关性**约束；
- 更换问题生成模型（GPT-3.5 vs. Mistral-7B vs. Tulu-2-7B）；
- 将 A-OKVQA 上校准好的 ReCoVERR **直接迁移**到 OK-VQA 与 Sherlock（不重新调参）；
- 每个配置跑 3 个随机种子取均值。

## 4. 资源与算力

- 论文**没有明确给出** GPU 型号、卡数、训练/推理时长等算力信息；
- 从方法性质推断：ReCoVERR 是纯推理时算法，不需要额外训练；其主要开销来自多轮 VLM 推理调用、LLM（GPT-3.5）问题生成、NLI 模型推理，会有较高的响应延迟与 API 成本，但论文未量化这些开销；
- 作者在文中也承认了**推理时间开销**是该方法的一个实际工程弱点。

## 5. 实验数量与充分性

### 5.1 实验数量

整体实验数量较为充足：

- **主实验**：3 种 VLM（BLIP2/InstructBLIP 各含 off-the-shelf 与 calibrated 两个版本、LLaVA-1.5）× 2 个风险容限（A-OKVQA）× 3 种方法，共约 30 组条件；VQAv2 上 3 组 VLM × 3 种方法；
- **消融实验**：可靠性消融 + 相关性消融（2 个 VLM）共 8 组；
- **问题生成模型对比**：3 个 LLM × 2 个 VLM共 6 组；
- **任务迁移实验**：2 个任务 × 2 个 VLM × 2 种方法共 8 组；
- **定性分析**：典型案例 2 例 + 部分成功/失败机理分析；
- 另有详尽的置信度校准曲线对比。

### 5.2 充分性与公平性

**优点**：
- 对比了不同 VLM（训练/未训练于目标任务）、不同置信度估计方法、不同模型规模，结论覆盖面较广；
- 包含多组消融，能指向方法有效性的来源；
- 测试了跨任务迁移的鲁棒性；
- 多随机种子取均值，降低了 LLM 采样随机性的影响。

**不足**：
- 验证集规模较小（A-OKVQA 1,075 题；VQAv2 只抽取 1,000 题），统计显著性未检验；
- 语言仅限英语；
- 未与其它选择性预测增强方法（如 Post-Abstention 类方法）做横向对比；
- 10% 风险容限下，ReCoVERR 经常超出风险容限 1–4%，说明在低容限下方法的风险控制能力欠佳；
- 跨任务迁移（OK-VQA）时风险超限达 5%，说明迁移性并不完美。

## 6. 主要结论与发现

- ReCoVERR 能在**不增加系统错误率**的前提下，显著提高选择性预测系统的覆盖率：在 A-OKVQA 上使三种 VLM 回答更多问题（覆盖率提升可达 20 个百分点，召回提升 25–33 个百分点）；
- 对**未在目标任务上微调过的 BLIP2**，提升幅度最大（覆盖率提升约 20%，RSP 提升约 30%），说明该方法对冷启动/通用模型的场景尤其有用；
- **置信度的质量**是决定性因素——当 VLM 的置信度校准良好时（如 calibrated InstructBLIP 和 LLaVA-1.5），ReCoVERR 在 20% 风险容限下能严格守住风险线，同时带来最大增益；
- 在 **10% 低风险容限**下，新增的风险和覆盖率主要来自初始视觉工具，而非多轮证据收集；
- 在较具挑战性的 **A-OKVQA** 上收益远大于相对简单的 **VQAv2**，说明 ReCoVERR 更适用于复杂推理场景；
- 问题生成模型的**具体选择**（ChatGPT vs. Mistral vs. Tulu）对最终性能影响不大；
- **可废止推理式的相关性筛选**对 InstructBLIP 有明显作用（去除后 RSP 下降约 3%、Φ₁ 下降），但对 BLIP2 作用不明显；
- ReCoVERR 在迁移到新任务时有一定效果，但**需要一定程度的任务级调优**才能保持风险稳定。

## 7. 优点

| 维度 | 亮点 |
|---|---|
| **问题定义** | 切入角度新颖——不是教模型"何时弃权"，而是反过来减少"不必要的弃权"，与主流"learning to abstain"思路形成互补 |
| **方法设计** | 无需训练即可用；模块化；将置信度估计（Self-Prompting + Platt Scaling）与可废止推理、NLI 验证组合成统一流水线，设计逻辑清晰、可解释性强 |
| **机制透明** | 每一步证据（可靠/相关/蕴含验证）都有明确物理含义，用户可审查证据以理解系统为何决定回答或弃权——对高风险应用很重要 |
| **实验广度** | 覆盖多种 VLM（是否经过目标任务微调）、多种置信度估计方法、多组消融、跨任务迁移、不同模型做问题生成等，探索了主要变量 |
| **分析深入** | 通过校准曲线和置信度分布解释为什么某些 VLM 提升明显（如 off-the-shelf BLIP2 高置信度正确答案更多），提供了机理层面的理解 |

## 8. 不足与局限

- **难以证明的一个假设**：为了保证新增回答正确率 ≥ 1−r，ReCoVERR 要求收集到的每条证据的置信度 ≥ 1−r，但其实**证据的正确率只是预测正确率的上界而非下界**——正确的证据不一定能推出正确结论，NLI 模型本身的误差也被视为可忽略；在 10% 风险容限下多次超出容限正是这一问题（尤其在 BLIP2 上超限达 4%）的体现；
- **工程复杂度与延迟**：多轮证据收集（最多 10 轮 × 每轮 10 个子问题）涉及大量 VLM+LLM 顺序调用，响应速度慢；虽提到可在流式场景中用更小模型或并行化缓解，但未实证验证；
- **计算资源未报告**：未说明 GPU 型号、数量与具体推理开销；
- **风险控制不够严格**：在 10% 风险容限和跨任务迁移到 OK-VQA 时，实际风险超出用户指定容限 1–5%，意味着该方法对"严格风险上限"这一承诺兑现得不完美；
- **实验范围有限**：仅英语、仅四类 VQA/推理 benchmark，未覆盖多语言、多模态输入的广泛真实场景；也未包含与问题图像无关/对抗性输入/不安全内容等弃权相关场景；
- **NLI 模型的能力边界**：ReCoVERR 高度依赖 FlanT5-XL 作为 NLI/蕴涵判断器的能力，复杂推理链下蕴涵判断本身可能有系统性偏差；
- **依赖外部工具**：使用了 LVIS 与 Qwen-VL 等外部视觉工具来初始化证据，这些工具的覆盖范围和偏好可能对系统造成隐性偏差。

（完）
