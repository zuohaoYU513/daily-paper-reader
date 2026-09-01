---
title: Mitigating Hallucinations in LM-Based TTS Models via Distribution Alignment Using GFlowNets
title_zh: 基于GFlowNets分布对齐缓解语言模型语音合成中的幻觉
authors: "Chenlin Liu, Minghui Fang, Patrick Zhang, Wei Zhou, Jie Gao, Jiqing Han"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.emnlp-main.976.pdf"
tags: ["query:hallu-rag"]
score: 4.0
evidence: 语言模型语音合成中的幻觉缓解，与LLM文本幻觉主题关联较弱
tldr: 基于语言模型的语音合成系统常生成偏离输入文本的幻觉语音，现有缓解方法代价高或延迟大。论文提出GOAT，通过GFlowNets进行后训练分布对齐，利用幻觉与模型不确定性的强正相关，将语音生成重构为轨迹流优化问题，并引入增强的子轨迹平衡目标。该方法在不增加推理开销的前提下缓解幻觉，为语音合成幻觉治理提供了轻量级方案。
source: EMNLP-2025-Main
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 798, \"height\": 686, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 791, \"height\": 530, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1502, \"height\": 621, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1658, \"height\": 353, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 679, \"height\": 551, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 734, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1496, \"height\": 415, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1503, \"height\": 1197, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1492, \"height\": 553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1489, \"height\": 420, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1490, \"height\": 1508, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-main/anthology-2025emnlp-main976/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 733, \"height\": 579, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1662, \"height\": 916, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 829, \"height\": 325, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 802, \"height\": 414, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 675, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 792, \"height\": 288, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 709, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-main/anthology-2025emnlp-main976/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 799, \"height\": 215, \"label\": \"Table\"}]"
motivation: LM语音合成中的幻觉会生成偏离文本的语音，现有缓解方法代价高，且与模型不确定性相关。
method: 提出GOAT后训练框架，用GFlowNets将TTS生成建模为轨迹流优化，并通过分布对齐缓解幻觉。
result: 整体验证表明GOAT能在不依赖大规模资源或增加推理开销的情况下有效缓解LM-TTS幻觉。
conclusion: 分布对齐和不确定性建模为语音合成幻觉缓解提供了高效可扩展的新方向。
---

## Abstract
Language Model (LM)-based Text-to-Speech (TTS) systems often generate hallucinated speech that deviates from input text. Existing mitigation strategies either demand excessive training resources or introduce significant inference latency. In this paper, we propose GFlOwNet-guided distribution AlignmenT (GOAT) for LM-based TTS, a post-training framework that mitigates hallucinations without relying on massive resources or inference cost. Specifically, we first conduct an uncertainty analysis, revealing a strong positive correlation between hallucination and model uncertainty. Based on this, we reformulate TTS generation as a trajectory flow optimization problem and introduce an enhanced Subtrajectory Balance objective together with a sharpened internal reward as target distribution. We further integrate reward temperature decay and learning rate optimization for stability and performance balance. Extensive experiments show that GOAT reduce over 50% character error rates on challenging test cases and lowering uncertainty by up to 58%, demonstrating its strong generalization ability and effectiveness.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义

**研究动机与背景：**

- **问题定义**：基于语言模型（LM）的语音合成（TTS）系统（如 VALL-E、CosyVoice 2 等）采用"下一 token 预测"的范式生成语音，但会生成**偏离输入文本的幻觉语音**（hallucinated speech），具体表现为：
  - 发音错误（mispronunciations）
  - 词语遗漏（word omissions）
  - 不自然的重复（unnatural repetitions）
  - 长句、复杂句中更为严重
- **现有方案的不足**：
  - **训练时扩展**（增大模型参数和数据规模）：计算成本高昂，数据收集负担重，资源受限场景下不可行。
  - **测试时扩展**（增加推理计算）：引入显著推理延迟，不利于实时 TTS 应用。
- **核心发现**：论文通过不确定性分析，发现 **模型不确定性与幻觉之间存在强正相关**（Pearson 系数 0.636，Spearman 系数 0.649，p < 1E-4），因此可以通过引导模型走向更"确定性"的解码路径来抑制幻觉。

**整体含义**：论文提出一种**轻量级后训练框架 GOAT**，在不依赖大规模数据/算力、不引入推理延迟的前提下，通过 GFlowNets 分布对齐有效缓解 LM-based TTS 的幻觉问题。

---

## 2. 论文提出的方法论

### 2.1 核心思想

- 将 TTS 的自回归生成过程视为**序列级状态转移过程**（trajectory flow）。
- 利用 **GFlowNets** 学习一个前向采样策略，使采样到的完整 token 序列的边际似然与目标奖励函数成正比，即：

\[
P^{\top}(a^{\top}) \propto R(a^{\top})  \quad \forall a^{\top} \in \mathcal{X}
\]

- 目标是把模型的分布从"低置信度、易幻觉"的区域**对齐**到"高置信度、高质量"的序列区域。

### 2.2 关键技术细节

**（1）GFlowNets 适配 LM-based TTS**

- 初始状态 \( s_0 \)：空 token 序列。
- 状态转移：每一步从 \( P_{\text{GFN}}(s_t | s_{t-1}, q, \theta) \) 采样下一个 token。
- 终止：采样到终止 token \(\top\)。
- 由于 TTS 自回归生成中每个状态只有唯一的父状态，**后向策略恒为 1**（\( P_B \equiv 1 \)），这使得轨迹概率等于序列概率的连乘：

\[
P(\tau) = \prod_{i=1}^{|a^{\top}|} P_{\text{GFN}}(a_i | a_{1:i-1}, q, \theta)
\]

**（2）增强的 Subtrajectory Balance (SubTB) 损失**

- 采用 **SubTB** 损失替代 Trajectory Balance（TB），允许模型从不同长度的子序列中学习，解决长句生成中**片段式崩溃**（fragmentary collapse）问题。
- 利用流守恒 \( F(x) = R(x) \)，将状态流替换为奖励函数，无需参数化流函数，最终目标为：

\[
\mathcal{L}(a^{\top}, q; \theta) = \sum_{0 \le i \le j \le |a^{\top}|} \left( \log \frac{ R(a_i) \prod_{k=i}^{j-1} P_{\text{GFN}}(a_{k+1} | a_{1:k}, q, \theta) }{ R(a_j) } \right)^2
\]

**（3）内部奖励函数（Internal Reward）**

- 不使用外部奖励模型，直接用**模型自身的 token 采样概率**作为奖励信号：
  \[
  R(a_k | q) = p_{\text{LM}}(a_k | q)^{1/T} = \left( \prod_{i=1}^{k} p_{\text{LM}}(a_i | a_{1:i-1}, q) \right)^{1/T}
  \]
- 通过逆温度 \( T \)（\( 0 < T < 1 \)）**锐化**奖励分布，使模型偏向全局最优序列。
- 作者强调这与解码时的 low-temperature sampling 有本质区别：GOAT 的低温作用于**整个序列的奖励分布**，而 low-temperature sampling 只调整每一步的局部分布，只能达到局部最优。

**（4）奖励黑客抑制（Reward Hacking Suppression）**

- **Reward Temperature Decay (RTD)**：奖励温度从 1 线性衰减到预设下限，兼顾训练初期稳定性和最终性能。
- **Learning Rate Optimization (LRO)**：采用 warm-up + cosine annealing 的学习率调度，防止模型学到"异常短序列"等高奖励但错误的投机行为。

---

## 3. 实验设计

### 3.1 数据集

| 用途 | 数据集 | 语言 | 规模 |
|------|--------|------|------|
| 训练 | LibriTTS（train-clean-100 子集） | 英文 | 随机选 1000 个 prompt 样本 + 1000 个目标文本 |
| 训练 | WenetSpeech4TTS（premium 子集） | 中文 | 同上 |
| 训练 | 中英混合（各 500 样本） | 中英 | 1000 样本总量 |
| 评估 | SeedTTS-Eval benchmark | 中/英 | test-zh（~2000）、test-en（~1000）、test-hard（~400 挑战样本） |

### 3.2 基线模型与对比方法

- **基础模型**：CosyVoice 2（标准 LM-based TTS 架构）
- **对比方法**：
  - baseline + RMS（随机多项式采样）
  - baseline + RAS（重复感知采样，CosyVoice 2 默认策略）
  - baseline + LT-RMS / LT-RAS（低温采样）
  - CV2-GOAT-zh / en / mix（分别在中/英/混合数据上训练的 GOAT 模型）
  - **训练步数配置**：1500S / 2500S（LRO 总步数）
- **消融实验**：
  - TB vs. SubTB（目标函数消融）
  - RTD 有无
  - LRO 有无
  - 最小奖励温度（0.925 / 0.875 / 0.825 / 0.775 / 0.725）
  - LRO 总步数（1500 / 2500 / 3500）
  - 最大学习率（5e-5 / 1e-5 / 5e-6）
- **评估指标**：
  - 内容一致性：CER（中文，Paraformer-zh）、WER（英文，Whisper-large V3）
  - 说话人相似度：SS（CAM++ 模型余弦相似度）
  - 语音质量：UTMOS

---

## 4. 资源与算力

- **训练硬件**：4 × NVIDIA H100 Hopper GPUs
- **评估硬件**：1 × NVIDIA V100 GPU
- **显存占用**：每 GPU 约 70 GB
- **训练时长**：约 7 小时完成全部训练（15 轮，约 3500 全局步）
- **微调方式**：使用 LoRA（Low-Rank Adaptation）对 LLM 组件进行后训练

> ✅ 论文明确提供了上述算力信息。

---

## 5. 实验数量与充分性

### 实验矩阵概览

| 实验类型 | 数量/设置 | 评估维度 |
|----------|-----------|----------|
| 主实验 | 3 训练数据（zh/en/mix）× 2 步数（1500/2500）× 2 采样（RMS/RAS），在 3 个测试集上与 baseline、LT 变体、Human 对比 | CER/WER、SS、UTMOS |
| 消融-目标函数 | TB vs SubTB | test-hard 上 CER/SS/UTMOS |
| 消融-RTD | 有无 RTD + 5 档最低温度 | 训练稳定性（序列长度）+ WER |
| 消融-LRO | 有无 LRO + 3 档 LRO 步数 + 3 档最大学习率 | 训练稳定性 + WER |
| 不确定性分析 | 全模型 × 全测试集的 UUR 对比 | 熵（不确定性） |
| 推理延迟 | 2000 样本 RTF 累积分布 | 实时率 |

### 充分性评价

- **较为充分**：覆盖了跨语言训练/评估、混合语言训练、两种采样策略、两档训练步数、多个消融维度，以及推理延迟分析。
- **公平性较好**：与 baseline 在同一采样策略下对比（RMS vs RMS，RAS vs RAS），并额外对比低温采样以区分方法差异。
- **美中不足**：仅验证了**单一基础模型（CosyVoice 2）**，未在 VALL-E、MELL-E 等其它 LM-TTS 架构上验证泛化性，作者在 Limitations 中也承认了这一点。

---

## 6. 论文的主要结论与发现

1. **幻觉与不确定性强正相关**：模型对输出越不确定（高熵），越容易产生幻觉；相关系数 ~0.64，统计显著。
2. **GOAT 大幅降低幻觉**：
   - 在 test-hard 挑战集上，CER 从 baseline 的 13.72%（RMS）降至 6.61%（zh-1500S RMS），**降幅超过 50%**。
   - 在普通 test-zh / test-en 集上也系统性优于 baseline，部分指标甚至接近/超过 Ground Truth。
3. **优于低温采样**：GOAT 比 LT-RMS/LT-RAS 在 CER/WER 上领先超过 30%，验证了"全局序列级对齐"优于"局部 token 级低温"的论点。
4. **不确定性显著降低**：平均 UUR（Utterance Uncertainty Ratio）最低降至 0.39（即降低 58%），且跨语言设置下仍有显著下降。
5. **跨语言泛化能力强**：中文训练的模型在英文测试集上仍有提升，混合训练模型在两种语言上均表现良好。
6. **SubTB 优于 TB**：TB 在 test-hard 上 CER 仅从 13.72% 降至 11.72%，而 SubTB 降至 6.61%，说明**细粒度子序列学习**对长句/复杂句片段崩溃至关重要。
7. **RTD 与 LRO 有效抑制 reward hacking**：去除 RTD 或 LRO 会导致训练不稳定、序列长度骤降、性能退化。
8. **推理延迟无显著增加**：RTF 与 baseline 基本一致，保持实时生成能力。

---

## 7. 优点

- **方法创新性强**：首次将 GFlowNets 用于语音合成任务的分布对齐与幻觉抑制，提供了新的优化视角。
- **轻量高效**：
  - 后训练仅需 1000 样本，4×H100 训练 7 小时，无需大规模数据或全参数微调（LoRA）。
  - 不引入额外推理延迟，适合实时 TTS 部署。
- **免外部奖励模型**：内部奖励直接利用模型自身采样概率锐化，降低对标注数据和外部模型的依赖。
- **理论上区分了与低温和贪婪采样的本质差异**：全局序列级奖励 vs. 局部 token 级调整，并用实验验证。
- **不确定性分析系统性强**：从 token/character/utterance 三粒度分析了熵与幻觉的关系，为后续研究提供了可复用的分析方法。
- **消融实验设计完整**：逐一验证了 SubTB、RTD、LRO、温度、学习率等关键组件的必要性。

---

## 8. 不足与局限

- **覆盖范围有限**：
  - 仅在 **CosyVoice 2** 一个基础模型上验证，未在 VALL-E、MELL-E 等其他主流 LM-TTS 架构上评估。
  - 幻觉现象比不确定性更复杂，GOAT 目前只能解决其中一部分（不确定性相关的那部分）。
- **相关性仅中等**：CER 与不确定性的 Pearson/Spearman 系数约为 0.64，说明仍有大量方差来自其他因素（如 ASR 误差、过度自信型错误等），部分幻觉无法被不确定性捕获。
- **特定幻觉类型无效**：附录中的细粒度分析显示，过度自信导致的重复错误、韵律错误（错位停顿、多余静音）等，与不确定性没有一致的相关模式，GOAT 难以覆盖。
- **内部奖励依赖模型自身概率假设**：GOAT 假设"高概率序列 = 高质量序列"，这在理论上可通过 GFlowNet 分布锐化进行增强，但极端情况下可能进一步放大模型的系统性偏好（如倾向短句、回避难字），存在潜在的偏差放大风险。
- **评估指标局限**：CER/WER 依赖 ASR 系统，ASR 自身的识别误差会引入噪声；SS 在数值较高时（>0.7）区分度有限；UTMOS 是客观预测指标，缺少大规模主观听感测试（MOS）。
- **主要针对中英两种语言**，对更多语种的泛化能力及其对跨语言文本的鲁棒性验证尚不充分。

---

（完）
