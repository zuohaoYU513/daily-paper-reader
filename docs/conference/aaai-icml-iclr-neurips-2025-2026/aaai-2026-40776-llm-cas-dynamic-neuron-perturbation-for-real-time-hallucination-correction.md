---
title: "LLM-CAS: Dynamic Neuron Perturbation for Real-Time Hallucination Correction"
title_zh: LLM-CAS：动态神经元扰动实现实时幻觉纠正
authors: "Jusheng Zhang, Ningyuan Liu, Yijia Fan, Zihao Huang, Qinglin Zeng, Kaitong Cai, Jian Wang, Keze Wang"
date: 2026-03-17
pdf: "https://ojs.aaai.org/index.php/AAAI/article/download/40776/44737"
tags: ["query:faithfulness"]
score: 6.0
evidence: 基于强化学习的动态神经元扰动可实时纠正幻觉，可迁移用于受限生成场景
tldr: 大模型常生成缺乏事实或上下文支撑的幻觉内容，传统方法依赖昂贵微调或静态参数编辑。本文将实时幻觉纠正定义为分层强化学习问题，LLM-CAS训练智能体根据上下文选择最优临时神经元扰动。该方法可针对不同情境动态干预生成过程，在减少计算和遗忘风险的同时纠正幻觉。该研究为推理期纠错提供了一种可灵活迁移的通用范式。
source: AAAI-2026-Accepted
selection_source: conference_retrieval
motivation: 微调和RLHF成本高，静态参数编辑无法处理上下文相关错误，需要推理期动态纠错。
method: 用分层强化学习训练agent在推理时选择并施加临时神经元扰动，以纠正幻觉内容。
result: 实验表明LLM-CAS能依据上下文实时纠正幻觉，同时避免灾难性遗忘和昂贵训练。
conclusion: 动态神经元扰动为低成本、情景自适应的推理期幻觉抑制提供了新方案。
---

## Abstract
Large language models (LLMs) often generate hallucinated content lacking factual or contextual grounding, hindering their reliability in critical applications. Traditional methods like supervised fine-tuning and reinforcement learning from human feedback are data-intensive and computationally expensive, while static parameter editing struggles with context-dependent errors and catastrophic forgetting. To overcome these limitations, we introduce LLM-CAS, a framework that formulates real-time hallucination correction as a hierarchical reinforcement learning (HRL) problem. LLM-CAS trains an agent to learn a sophisticated policy, dynamically selecting optimal, temporary neuron perturbations during inference based on the immediate context. This learned, policy-driven approach provides greater adaptability than prior dynamic methods that rely on heuristic or pre-defined adjustments. As a result, LLM-CAS achieves significant performance gains across various LLMs, improving accuracy by 10.98 percentage points on StoryCloze, 2.71 points on TriviaQA, and 2.06 points on TruthfulQA's MC1 score, thereby outperforming static methods like ITI and CAA, as well as the dynamic SADI framework. This context-aware, efficient approach promises enhanced reliability for LLMs in high-stakes domains, with future potential for multimodal extensions.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

LLM-CAS 针对大语言模型（LLM）在实际部署中普遍存在的 **幻觉（hallucination）问题**——即模型生成的内容缺乏事实依据或与上下文不一致，严重阻碍其在关键任务中的可靠应用，提出一种**基于分层强化学习（HRL）的实时幻觉纠正框架**。

- **既有方法的两难困境**：
  - **训练/微调类方法**（SFT、RLHF）：效果好但依赖大规模高质量标注数据，计算成本高昂，且存在泛化能力下降与灾难性遗忘风险；
  - **静态参数编辑类方法**（如模型编辑技术的 “locate-then-edit” 范式）：只针对孤立事实修正，难以应对上下文相关的多样性幻觉，且多次编辑会产生副作用累积，甚至导致**灾难性遗忘**；
  - **已有动态干预方法**（如 ITI、CAA）：虽然只在推理期干预，但注入的转向向量往往是预先计算的、跨输入固定；较近的 SADI 虽具备语义自适应，但其生成机制仍依赖预定义规则或简单优化，**缺乏真正的学习与适应能力**。
- **核心论断**：临时、上下文特定的神经元扰动（即只修改推理期的激活状态，而非永久修改权重）可以在不损害模型整体能力的前提下，有效纠正幻觉输出。
- **核心思路**：首次将实时幻觉纠正建模为**分层强化学习（HRL）问题**，训练一个智能体学习上下文感知的干预策略——在推理过程中根据输入状态动态选择和施加最优的**临时神经元扰动**。

## 2. 方法论

### 2.1 核心思想
LLM-CAS 不修改模型的永久参数 W，而是通过训练一个分层强化学习智能体，在线决定“在哪些功能性神经元上、施加何种类型和强度的临时扰动”，使模型的激活状态被修正后，输出从幻觉答案 y_h 转向正确回答 y_c，整个过程**保持基础模型权重完整不变**。

### 2.2 问题形式化（MDP）

- 目标：学习最优分层策略 π* 最大化期望累积折扣奖励：  
  π* = argmax_π E[Σ γᵗ Rₜ₊₁]
- 状态 sₜ = concat(Emb(x), Scores_baseline, Scores_best, Steps_norm)，其中：
  - Emb(x)：输入语义嵌入；
  - Scores_baseline：未扰动时基线输出的打分；
  - Scores_best：本回合迄今最优分数；
  - Steps_norm：标准化交互步数。
- 动作 aₜ = (aᴴ, aᴸ) 分层解耦：
  - **高层动作 aᴴ**：从预定义集合 Aᴴ = {C₁, C₂, ..., C_NH} 中选择宏观目标——一个功能性神经元类别/网络（如前文图 2 中提到的 “Language Network” 等）；
  - **低层动作 aᴸ = (a_typeᴸ, a_magᴸ)**：在高层选定类别下，确定扰动类型（如 noise / zero / scale 等）和扰动幅度（离散档位 m₁...m_NM）。

### 2.3 奖励设计
奖励 Rₜ = wₕ·ΔScoreₕ + wᵣ·ΔScoreᵣ + w_f·ΔScore_f + R_exp,t，即同时衡量幻觉减少（ΔScoreₕ）、相关性（ΔScoreᵣ）与流畅度（ΔScore_f）的变化，并加入探索奖励 R_exp 鼓励智能体尝试新策略。奖励公式依赖**相对分数变化**而非绝对分数，以缓解 LLM 裁判的系统性评分偏差。

### 2.4 分层强化学习智能体（HRL + PPO）

- 采用 **PPO（近端策略优化）** 作为训练算法，高层（宏观目标）和低层（细节扰动）分别有各自的 actor-critic 网络：
  - 高层策略 πᴴ(aᴴ|s) 与价值网络 Vᴴ(s)：MLP，将状态映射到宏观网络的概率分布；
  - 低层策略 πᴸ(aᴸ|s, aᴴ) 与 Vᴸ(s, aᴴ)：以状态 s 与高层动作 aᴴ 的嵌入拼接为输入，输出具体扰动参数分布。
- 训练循环：“坏样本 x → 智能体选择动作 → 环境施加扰动 → LLM 生成新输出 → 评估模块打分 → 奖励回报 → 更新策略”。

### 2.5 两阶段自适应掩码与因果追踪

- **阶段 1——学习通用稀疏掩码**：对每个功能类别 Cₖ 与每一层 ℓ，定义可学习掩码 Mₖ,ℓ，通过 Gumbel 风格门控 σ(θ/τ_gate) 输出每个神经元的选中强度，用 L₁ + 近似 L₀ 稀疏惩罚以最小化附带干扰；
- **阶段 2——输入相关自适应**：利用神经元级因果追踪（如 Integrated Gradients 等梯度归因方法）计算当前输入 x 下每个神经元的归因分数 Attr_ℓ(x)，再与通用掩码做逐元素调制，得到最终操作掩码：  
  M_op,k,ℓ(i) = Mₖ,ℓ(i) ⊙ normalize(|Attr_ℓ(x, i)|)
- 该机制使得掩码既具备“通用知识经验”，又能针对新输入即时调整，避免了每个输入都重新训练掩码。

### 2.6 评估反馈
开放式生成任务主要用 **Llama2-7B-Instruct 充当“裁判 LLM”**，构建 prompt_eval 对幻觉、相关性、流畅度三个维度打分；多项选择任务则直接采用任务自带的客观指标（如选项 logits、正确率、EM 等）。

## 3. 实验设计

### 3.1 数据集与场景

| 任务类型 | 数据集 |
|---|---|
| 多项选择（多选题、判断题） | StoryCloze、SST-2、BoolQ、Winogrande |
| 开放生成（知识问答） | TriviaQA（指标：Exact Match） |
| 开放生成（安全/毒性） | ToxiGen（用 toxigen_hatebert 打分） |
| 开放生成（真实性） | TruthfulQA（评判：truthfulqa-truth-judge 与 truthfulqa-info-judge，基于 Llama2-7B 微调得到） |

### 3.2 目标模型（Target LLMs）

- 主模型：**LLaMA2-7B-Chat**；
- 泛化验证模型：**Mistral-7B-Instruct-v0.3** 和 **Gemma-1.1-7b-it**，用于验证方法跨越不同架构的鲁棒性。

### 3.3 对比基线
- **ITI**（Inference-Time Intervention）：静态、固定转向向量；
- **CAA**（Contrastive Activation Addition）：预计算固定激活加性向量；
- **SADI**（Semantics-Adaptive Activation Intervention）：语义自适应转向向量，目前最接近的动态方案；
- 另有“Baseline”（不干预的原始模型）。

### 3.4 实验组构成
完整实验包括：
1. 多项选择任务 4 个数据集上的主实验（表 1）；
2. 开放生成任务 3 类数据集的全面实验（表 2，含 TriviaQA、ToxiGen、TruthfulQA 的 MC1/MC2/MC3/True/Info 等细粒度指标）；
3. TruthfulQA 按真实性问题类别（如事实性、指称、文化健康等）细分，验证方法的细化效果（表 4）；
4. 跨模型泛化实验（Table 5）——在 Mistral 和 Gemma 上对比基线准确率；
5. 消融实验（表 6）——“仅随机掩码”“仅随机动作”“随机掩码+随机动作”三种退化设置与完整 LLM-CAS 的对比；
6. 推理延迟/开销对比实验（Figure 3）。

## 4. 资源与算力

论文中给出的信息有限：

- 明确说明所有实验在 **8 块 NVIDIA A100 GPU** 上完成；
- **未明确说明**：训练总时长、单次实验/消融的 GPU 小时数、数据量等细节均未披露。

## 5. 实验数量与充分性评估

### 5.1 数量与覆盖
- 主实验横跨 4 个多选题数据集与 3 个开放式生成数据集，类别覆盖常识叙事（StoryCloze）、情感分类（SST-2）、阅读理解（BoolQ）、指代消解（Winogrande）、知识问答（TriviaQA）、毒性缓解（ToxiGen）和真实性测试（TruthfulQA），在任务分布上较全面。
- 模型层面覆盖了 LLaMA、Mistral、Gemma 三个不同的 7B 级开源模型，具有基本架构多样性。
- 消融实验涵盖了动态掩码与 PPO 两核心组件的独立删除与共同删除，对归因分析比较合理，验证了“掩码+PPO”的协同效应。

### 5.2 客观性与公平性
- 多选题任务基于答案 logits 判定，指标客观；
- TriviaQA 使用 Exact Match；ToxiGen 和 TruthfulQA 使用公开可获得的微调评判模型（Hugging Face 部署），降低裁判偏差风险；
- 相对分数变化（ΔScore）的奖励设计能过滤系统偏好，是一种合理的公平性设计；
- 不足之处：开放式生成的主观评估主要依赖自动 LLM 裁判，论文也承认未做大规模人类对齐评估；未提供跨多个随机种子或重复运行的标准差/置信区间；未与 SFT/RLHF/LoRA 等基于训练的方法对比，使方法定位主要限制在同为推理期干预的 ITI/CAA/SADI 框架内。

## 6. 主要结论与发现

### 6.1 定量结论
- **多项选择任务**：完整模型平均准确率 73.68%，超过 ITI（71.70）、CAA（73.36）和 SADI（69.65），尤其在 StoryCloze 上较基线提升 **+10.98 个百分点**，也大幅超过 SADI；
- **开放生成任务**：
  - 在 TriviaQA 上较基线提升 **+2.71 分**（41.60 → 44.31）；
  - 在 TruthfulQA 的 MC1 上 +2.06 分（33.41 → 35.47），MC3 上也取得优于全对比方法的成绩；
  - 在 ToxiGen 中毒性分数从 49.71 降至 47.63（分数越低越好）；
- **跨模型泛化**：在 Mistral-7B 和 Gemma-1.1-7b-it 上，LLM-CAS 均能提高 StoryCloze、SST-2、Winogrande 三项任务的准确率。
- **消融结果**：
  - 去掉动态掩码（换成随机掩码），StoryCloze 下降 5.84 点，BoolQ 下降 7.37 点；
  - 去掉 PPO（随机动作选择），StoryCloze 大幅下降 9.17 点，BoolQ 下降 10.15 点；
  - 两个组件同时移除后平均精度跌至 63.41，比完整模型低 10.27 点，说明其协同重要性。

### 6.2 主要论断
- 分层强化学习 + 动态掩码的技术组合对上下文相关幻觉的纠正确有实效，且不需永久修改模型权重；
- 与静态方法（ITI、CAA）和现有动态方法（SADI）相比，学到的高效分层策略能做出更精细、更灵巧的推理期干预；
- LLM-CAS 在推理时效与动态决策上具有实用性，具备部署到高可靠性场景的潜力。

## 7. 优点

- **方法视角新颖**：首次将幻觉纠正明确建模为分层强化学习 MDP，突破静态编辑与启发式动态干预—在干预决策中引入学习能力；
- **非侵入式架构**：推理期临时、局部扰动，不改变模型参数，可规避灾难性遗忘与长期副作用；
- **精细归因与可解释性**：掩码学习结合神经元级因果追踪，使干预有明确的、可解释的定位依据；
- **系统化的组件设计**：环境、RL Agent、因果归因、自适应掩码、LLM 裁判形成闭环训练框架，模块逻辑清晰；
- **面向现实约束**：对比实验和消融实验较全面，动态掩码 + PPO 的协作效应证据明确；
- **评测维度多元**：多选题采用确定性指标，开放生成同时覆盖事实性、相关性、流畅度、毒性等多个维度，一定程度上降低了单一评判的偏差。

## 8. 不足与局限

- **LLM 裁判偏差**：TruthfulQA、ToxiGen 的部分评判仍依赖自动打分模型，论文承认潜在偏见，虽通过“分数差”设计有所缓解，但最终仍缺乏严格的人类一致性验证；
- **实验细节披露不充分**：未报告训练时长、训练集规模、随机种子数、方差统计、推理时延的精确起止维度等信息，复现门槛较高；
- **开放生成的自动评估局限**：一次性字面质量评估难以捕捉长程语义一致性；“True+Info”在部分设置中提升幅度有限（+4.28），而 Info 项本身甚至下降 5.29 分，提示存在纠错时信息量损失的副作用；
- **适用范围边界**：以 7B 级模型为主，未覆盖更大规模（如 30B/70B 及以上）模型，也缺少对真实业务场景中长对话、长文档的评测；方法对训练分布外“坏样本”的稳定性尚需验证；
- **数据集侧重**：多选题侧重于判断题，缺少更多的复杂多选推理类数据集，纠偏能力在复杂推理任务上的效力证据仍有限；
- **纠错触发条件**：方法假定已能识别“哪些输入会引发幻觉”并给定少量参考样本 S_small，但完整流程对已存在的幻觉检测精度高度依赖，论文对真实场景中如何自动化识别坏样本的讨论偏少；
- **未来方向**：论文只提到多模态扩展的潜力，未给出跨模态或更大参数量模型下的实验验证。

**（完）**
