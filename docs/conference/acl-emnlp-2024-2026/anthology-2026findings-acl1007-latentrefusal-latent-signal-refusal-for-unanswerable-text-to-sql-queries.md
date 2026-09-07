---
title: "LatentRefusal: Latent-Signal Refusal for Unanswerable Text-to-SQL Queries"
title_zh: LatentRefusal：针对不可回答文本到SQL查询的隐信号拒答方法
authors: "Xuancheng Ren, Shijing Hu, Zhihui Lu, Jiangqi Huang, Qiang Duan"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1007.pdf"
tags: ["query:faithfulness"]
score: 6.0
evidence: 提出基于隐信号的拒答机制，可作为拒答监督方法迁移到其他生成任务以抑制无依据内容
tldr: 针对LLM在不可回答的文本到SQL查询上会生成误导性甚至违反约束的可执行程序的问题，本文将安全拒答建模为可答性门控，并提出LatentRefusal机制，直接从中间隐状态预测查询能否回答。相较依赖输出指令或不确定性估计的传统拒答方法，它更稳健且开销更低。实验验证了该隐状态信号在识别不可回答查询上的能力，可有效阻止无依据程序生成。该方案可作为拒答监督式策略迁移到其他生成任务以减少幻觉。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1007/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 801, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1007/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1627, \"height\": 691, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1007/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1004, \"height\": 338, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1653, \"height\": 857, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 804, \"height\": 443, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 773, \"height\": 407, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 619, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 735, \"height\": 411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 757, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 688, \"height\": 248, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1007/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 768, \"height\": 606, \"label\": \"Table\"}]"
motivation: 不可回答或含糊查询会让LLM生成误导性甚至危险的可执行SQL程序，现有拒答策略脆弱且开销高。
method: 将安全拒答形式化为可答性门控，利用LLM中间隐状态预测查询可答性，提出LatentRefusal机制。
result: 实验表明隐状态信号可更可靠地判断查询不可回答，以较低复杂度提升拒答安全性。
conclusion: 可答性门控与隐信号拒答能有效减少无依据程序生成，为LLM安全生成提供可迁移的拒答监督思路。
---

## Abstract
In LLM-based Text-to-SQL systems, unanswerable and underspecified user queries may generate not only incorrect text but also executable programs that yield misleading results or violate safety constraints, thus posing a major barrier to safe deployment. Existing refusal strategies for such queries either rely on output-level instruction following, which is brittle due to model hallucinations, or on estimating output uncertainty, which adds complexity and overhead. To address this challenge, we first formalize safe refusal in Text-to-SQL systems as an answerability-gating problem, and then propose **LatentRefusal**, a latent-signal refusal mechanism that predicts query answerability from intermediate hidden activations of an LLM. We introduce the Tri-Residual Gated Encoder (TRGE), a lightweight probing architecture, to suppress schema noise and amplify sparse, localized question–schema mismatch cues that indicate unanswerability. Extensive empirical evaluations across diverse ambiguous and unanswerable settings, together with ablations and interpretability analyses, demonstrate the effectiveness of the proposed scheme and show that **LatentRefusal** provides an attachable, efficient safety layer for Text-to-SQL systems. Across four benchmarks, **LatentRefusal** achieves an average F1 of 88.5% and 88.8% on Llama-3.1-8B and Qwen-3-8B respectively, while adding ~2ms probe overhead.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 核心问题与整体含义（研究动机与背景）

- **问题背景**：在大语言模型（LLM）驱动的 Text-to-SQL 系统中，当用户查询**不可回答**（unanswerable）或**未充分指定**（underspecified）时，LLM 不仅可能生成错误文本，还会生成**可执行但语义错误的 SQL 程序**，进而导致误导性报表、隐私泄露或运营事故。
- **现有方法的缺陷**：
  - **基于提示（prompt）的拒答**：依赖模型输出层遵循指令，但模型在幻觉状态下容易失效，且对提示措辞敏感。
  - **基于不确定性的估计**：如自洽性、语义熵等方法，通常需要多次采样，推理开销大；且判断 SQL 候选间的语义等价往往需要执行 SQL，这与"生成/执行前安全门控"的目标相冲突。
- **核心动机**：LLM 的中间层隐状态已蕴含关于问题与 schema 匹配程度的丰富信息，即使在最终生成阶段出现幻觉，中间表征仍可能保留可靠信号。因此可将拒答从"输出层行为"转变为"表征层级决策"，在生成任何 SQL 之前完成判断。

### 2. 方法论：核心思想、关键技术细节

- **整体框架：LatentRefusal**

  - 将安全拒答形式化为**可答性门控问题**（answerability-gating problem），并约束：必须在生成或执行任何 SQL 之前决策。
  - 方法：冻结基础 LLM，从选定中间层提取隐状态，训练轻量探针预测查询可答性概率 \( \hat{p} \)，若 \( \hat{p} < \tau \)（阈值）则拒绝回答；否则放行 SQL 生成。
  - 设计目标：单次前向传播、生成前决策、免执行、与架构无关（适用于任何可访问中间层激活的冻 LLM，常见于本地私有化部署）。

- **TRGE（Tri-Residual Gated Encoder，三残差门控编码器）探针架构**

  - 针对 schema 密集、拒答线索稀疏且局部化（如缺列、缺 join 路径、约束含糊）的问题，TRGE 在标准 Transformer 块（自注意力 + FFN）基础上增加**第三条残差分支**，使用 **SwiGLU 门控**。
  - 公式（每层）：
    - \( U = Z^{(k-1)} + \text{Attn}(\text{LN}(Z^{(k-1)})) \)
    - \( V = U + \text{MLP}(\text{LN}(U)) \)
    - \( Z^{(k)} = V + \text{SwiGLU}(\text{LN}(V)) \)
  - SwiGLU：\( \text{SwiGLU}(x) = W_d( \text{SiLU}(W_g x) \odot (W_u x) ) \)
  - 设计动机：内容相关的门控可视为软特征选择器，压制 schema 常规信息，增强不匹配信号。
  - 最终分类：对多个 TRGE 层输出做池化（默认均值池化），经线性层 + sigmoid 得到可答性概率。

- **训练与实现细节**
  - 对冻 LLM 提取中间层隐状态，仅训练探针参数（约 19M，< 骨干网络 0.3%）。
  - 使用混合精度可能产生 NaN/Inf，引入数值稳定操作：NaN 置 0、无穷大裁剪为常数 C，再做 token 级 LayerNorm。
  - 优化目标：二元交叉熵；标签平滑 ε=0.1 效果最佳。
  - 在开发集上根据安全/效用需求调阈值 τ 实现可控的门控行为。

### 3. 实验设计：数据集、基准与对比方法

- **数据集（4 个）**
  1. **MD-Enterprise**：中文金融行业内部数据集，覆盖 6 个领域（股票、HR、贷款、零售、风控、监管等），专家标注可答性标签（遵循商业逻辑和安全约束）。
  2. **AMBROSIA**：面向语言歧义基准，包含配对清晰/歧义问题，检验对含糊查询的敏感度。
  3. **SQuAD 2.0**：跨任务阅读理解基准，用于验证从 Text-to-SQL 到机器阅读理解的泛化能力。
  4. **TriageSQL**：医疗意图二元拒答任务，来源为 question-intention 分类基准。
- **基础模型**：Qwen-3-8B、Llama-3.1-8B，使用 bfloat16，最大序列长度 2048。
- **对比基线（3 类）**
  - 输出级不确定性：Self-evaluation（单次 logit）、Semantic Entropy（N=10 采样，T=0.7）
  - 内部状态类：CCS、Eigenscore（无监督 / 谱方法）、HaloScope、SAPLMA、TSV（有监督探针或向量方法）
  - 提示型基线：DeepSeek-Chat API（零样本指令判断）
- **主要评价指标**：F1（在开发集上选择阈值）
- **训练设置**：每个数据集单独训练/评测；训练/验证 8:2 划分；测试集 300 条样例。训练约 300 样本即可，单张 A100-80G 约 10 分钟。

### 4. 资源与算力

- 论文明确提及：训练单探针在**单张 NVIDIA A100-80G GPU** 上约 **10 分钟完成**（无需 warm-up，lr=1e-5，batch size=8）。
- 推理测速在 Qwen-3-8B 上使用单张 A100-80G（bfloat16，2048 序列），探针自身延迟 ~2ms。
- 额外举例：实际部署选型亦可运行于 NVIDIA RTX 4090（案例截图提到），但未给出详细算力清单。
- 未提及 GPU 总数量、其他基线训练资源或能耗等细节。

### 5. 实验数量与充分性

- **实验数量**：
  - 主实验：4 个数据集 × 2 种骨干模型（Llama-3.1-8B / Qwen-3-8B），并附加 1 个 API 基线，共 9 行结果。
  - 效率对比：1 张表（延迟比较）。
  - 消融实验：3 组（架构、层选择、深度）+ 附录中损失函数和 dropout 等超参消融（共 5+ 表）。
  - 此外有案例分析（图）和附录伪代码。
- **充分性与客观性评价**：
  - **优点**：覆盖多类不可回答/歧义场景，并做了跨任务（SQuAD）和跨骨干验证；消融设计较系统，证实 SwiGLU 关键作用、中间层信号最强、模型深度存在最优值。
  - **不足**：
    - MD-Enterprise 为内部数据集，无法公开复现；
    - 表 1 中部分方法（TSV、HaloScope、CCS 等）未加星标，说明用官方实现；但部分基线在 Text-to-SQL 场景可能存在适配偏差；
    - 对语义熵，论文承认用"句法一致"近似语义等价，可能低估该类方法的理想性能；
    - 缺乏对更大参数量模型（>8B）或多语言通用场景的测试；
    - 仅 300 条测试样例，样本数偏小，统计显著性未报告。

### 6. 主要结论与发现

- **有效性与效率**：LatentRefusal 在 Llama-3.1-8B / Qwen-3-8B 上平均 F1 为 88.5% / 88.8%，显著优于所有基线（比最强的 SAPLMA 高 4.2~5.6 点）；探针附加延迟仅 ~2 ms，总延迟比 Semantic Entropy 快约 13.7 倍。
- **对语言歧义更鲁棒**：AMBROSIA 上较语义熵高 18.1 点（Llama 上），说明内部表征信号可捕捉到采样方法难以发现的底层混淆。
- **谱方法的失败原因分析**：Eigenscore 等谱方法依赖采样隐藏状态的谱统计，容易被"句法多样性但语义相同"的 SQL 候选误导，导致将句法方差误判为认知不确定性；而表征级方法直接检测 prompt–schema 失配，不受解码路径干扰。
- **层级定位**：中间层（第 −16 层）包含最准确的拒答信号，较浅层或最终输出层更好，表明 LLM 在中间阶段编码了任务不匹配的信息，后续处理可能将其"坍缩为自信幻觉"。
- **架构决定性**：TRGE 的三残差设计与 SwiGLU 门控是关键；线性探针或其变体性能大幅下降，显示不可答检测需要非线性交互建模与噪声选择能力。
- **可迁移性**：在 SQuAD 2.0 上同样取得 88.6% F1（Qwen-3-8B），表明隐状态中的"不可答信号"具有一定跨任务通用性；两个骨干模型结果接近也启示体系结构间的共性。

### 7. 优点

- **形式化清晰**：将安全拒答严格定义为"生成/执行前门控"，与拒绝选项/选择性分类理论衔接，便于安全审计与可控调参。
- **单前向、免执行**：仅需一次前向传播，无需采样、无需执行 SQL，即为最安全的门控方式。
- **探针架构设计具有针对性**：TRGE 针对 schema 长文本中稀疏信号问题，引入第三条 SwiGLU 残差分支，具备可解释的"门控选择"动机，而非盲目堆叠层。
- **性能-延迟 Pareto 优越**：与多种方法对比后，处于准确率最高、延迟近似最低的帕累托前沿。
- **轻量化与易部署**：探针仅 19M 参数、训练仅需分钟级和数百样本，可快速适配新领域。
- **稳健性分析较充分**：包括数值稳定性处理、损失函数与 dropout 消融、层选择实验等，呈现了较系统的实证分析。

### 8. 不足与局限

- **跨域泛化仍需微调**：探针目前需要针对部署场景单独训练，缺乏零样本 / 少样本跨域迁移能力；作者也承认这是主要限制。
- **内部数据集**：MD-Enterprise 不能公开，复现和第三方核验受限；且中文金融领域本身有更多不可言说的隐含业务规则，其他数据集未必能完全代表真实场景。
- **阈值依赖性**：F1 是固定阈值下计算的，不同阈值下性能稳定性未深入分析，生产部署时阈值的选取可能影响实用性。
- **语义等价近似问题**：对采样类基线用句法一致替代语义一致，可能导致对比不公平，虽然作者已明确说明。
- **深层推理不足**：错误分析发现两类失败模式——语义近似列名（如 `revenue` 与 `gross_profit`）以及需要复杂多跳 join 的查询，探针在选定层捕捉弱不匹配信号时可能失效。
- **骨干模型局限**：只在 8B 两模型上验证，未扩展到更大规模或 API 隐藏状态不可用场景；对开放权重模型的依赖也限制了"架构无关"的完全成立（仍需白盒访问中间层）。
- **未覆盖安全性更广范畴**：主要关注逻辑不可答/含糊，尚未深入讨论隐私性问题（如涉及敏感字段的合法查询是否需要拒答）或其他安全约束场景。

（完）
