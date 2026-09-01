---
title: Prompt-Guided Internal States for Hallucination Detection of Large Language Models
title_zh: 提示引导的大语言模型幻觉检测内部状态方法
authors: "Fujie Zhang, Peiqi Yu, Biao Yi, Baolei Zhang, Tong Li, Zheli Liu"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.acl-long.1058.pdf"
tags: ["query:hallu-rag"]
score: 9.0
evidence: 利用提示引导内部状态的跨领域幻觉检测
tldr: 现有的基于内部状态的监督式幻觉检测器在跨领域时泛化能力有限，通常只能使用领域内数据训练。本文提出 PRISM 框架，利用合适的提示引导大语言模型内部状态的结构变化，使训练好的检测器在不引入目标领域数据的情况下也能迁移到新领域。通过这种方式，PRISM 在多个领域间提升了幻觉检测的跨域性能，为仅靠领域内数据提升检测器泛化能力提供了新思路，并通过提示来利用模型的语义知识增强检测器的判别能力。
source: ACL-2025-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1058/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1495, \"height\": 732, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1058/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 689, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-long/anthology-2025acl-long1058/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 693, \"height\": 472, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1654, \"height\": 392, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1616, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1629, \"height\": 347, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1628, \"height\": 349, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1602, \"height\": 160, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1620, \"height\": 404, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 765, \"height\": 306, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 806, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 626, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 771, \"height\": 244, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-long/anthology-2025acl-long1058/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 811, \"height\": 333, \"label\": \"Table\"}]"
motivation: 跨领域幻觉检测器的泛化性差，难以用单一领域数据适应新领域。
method: 使用提示引导大语言模型内部状态的结构变化，让监督检测器学会迁移。
result: 在多个领域上的实验验证了 PRISM 能显著提升跨域幻觉检测性能。
conclusion: 为仅用领域内数据的跨域幻觉检测提供了一种有效的提示引导方案。
---

## Abstract
Large Language Models (LLMs) have demonstrated remarkable capabilities across a variety of tasks in different domains. However, they sometimes generate responses that are logically coherent but factually incorrect or misleading, which is known as LLM hallucinations. Data-driven supervised methods train hallucination detectors by leveraging the internal states of LLMs, but detectors trained on specific domains often struggle to generalize well to other domains. In this paper, we aim to enhance the cross-domain performance of supervised detectors with only in-domain data. We propose a novel framework, prompt-guided internal states for hallucination detection of LLMs, namely PRISM. By utilizing appropriate prompts to guide changes to the structure related to text truthfulness in LLMs’ internal states, we make this structure more salient and consistent across texts from different domains. We integrated our framework with existing hallucination detection methods and conducted experiments on datasets from different domains. The experimental results indicate that our framework significantly enhances the cross-domain generalization of existing hallucination detection methods.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义

- **研究动机**：大型语言模型（LLM）在生成文本时可能出现“幻觉”——即逻辑连贯但事实错误的内容。检测幻觉对于防止用户被误导至关重要。
- **现有方法的痛点**：基于内部状态的数据驱动监督式检测器（如 MM、SAPLMA）在特定领域上训练后，跨领域泛化性能往往明显下降。例如，在肯定句上训练的检测器难以迁移到否定句、合取句等结构。
- **研究问题**：**能否仅利用领域内数据，提升监督式检测器的跨领域性能？**
- **整体贡献**：提出了 **PRISM** 框架（Prompt-Guided Internal States），通过合适的提示引导 LLM 内部状态中与“文本真实性”相关的结构发生有利变化，使该结构在不同领域间更显著、更一致，从而在不引入新领域数据的情况下增强检测器的跨域泛化能力。

## 2. 方法论

### 核心思想
- LLM 内部状态编码了丰富的语义信息，但这些信息主要服务于下一个 token 预测，并未专门优化用于真实性判断。直接提取的嵌入包含大量领域特有信息，掩盖了与“真实性”相关的结构。
- 利用 LLM 强大的指令跟随能力，通过**提示模板**引导内部状态朝“真实性判别”方向变化，让真/假语句的几何结构更凸显、更一致，从而便于检测器学习。

### 关键技术细节
- **真值方向（Truthfulness Direction）** ：
  \[
  \theta = \frac{1}{N^+}\sum_{i=1}^{N^+} v_i^+ - \frac{1}{N^-}\sum_{i=1}^{N^-} v_i^-
  \]
  其中 \(v^+\)、\(v^-\) 分别为真/假语句的嵌入向量。
  
- **结构显著性指标（Variance Ratio）** ：
  - 计算总方差 \(V_T = \text{Trace}(\Sigma)\)
  - 计算沿真值方向的方差 \(V_\theta = \frac{\theta^T \Sigma \theta}{\|\theta\|^2}\)
  - 定义 ratio \(R = V_\theta / V_T\)，用于衡量真值结构的显著性，并作为提示选择的依据。

- **结构一致性指标**：利用不同子数据集之间真值方向的余弦相似度 \(c_{ij} = \frac{\theta_i \cdot \theta_j}{\|\theta_i\|\|\theta_j\|}\) 来衡量跨域结构的稳定性。

### 算法流程（PRISM）
1. **提示生成**：手动构造简单的初始提示（如 Prompt 1），再使用 LLM（如 GPT-4o）生成大量语义相似但形式多样的候选提示模板。
2. **提示选择**：在带标签的领域内数据上，对每个提示计算方差比 \(R\)，选择 \(R\) 最高（结构最显著）的模板作为最终提示。
3. **特征提取**：将提示与待评论文本拼接后输入 LLM，提取最后一个 token 在最后一层的上下文嵌入作为特征向量。
4. **训练检测器**：将提示引导下的内部状态特征与相应幻觉标签一起用于训练现有的检测器（如 MM、SAPLMA）。
5. **推理**：对新文本同样使用选中提示获取内部状态，输入训练好的检测器得到幻觉标签。

## 3. 实验设计

### 数据集
- **True-False 数据集**（Azaria & Mitchell 2023）：6 个子数据集（animals, cities, companies, elements, facts, inventions），真假语句数量均衡，文本结构相似但主题不同。
- **LogicStruct 数据集**（Bürger et al. 2024）：24 个子数据集，涵盖 6 个主题 × 4 种语法结构（肯定句、否定句、逻辑合取、逻辑析取）。主要用于评估从肯定句到其他结构的迁移。
- **TruthfulQA 数据集**：真实场景下的问答数据集，790 个问题，37 个类别，用于验证框架在真实场景中的有效性。采用 BLEURT 阈值划分正负样本，使用 AUROC 作为指标。

### 对比方法（Baselines）
- **LN-PP**：基于生成 token 平均概率的无监督方法
- **EUBHD**：参考无关的基于不确定性的检测方法
- **MIND**：自动生成数据集训练检测器的无监督方法
- **MM**：基于质量均值探针的线性判别方法
- **SAPLMA**：基于 MLP 的监督检测器
- **PRISM-MM / PRISM-SAPLMA**：将 PRISM 与 MM 和 SAPLMA 集成的方法
- 另外在 TruthfulQA 上还对比了 **SelfCheckGPT** 无监督一致性方法

### 实验设置
- 使用模型：**LLaMA2-7B-Chat** 和 **LLaMA2-13B-Chat**
- 特征向量：默认取最后一层最后 token 的嵌入；消融中考察第 16 层（中间层）
- 训练策略：训练集与验证集 4:1 划分，10 个 epoch，选择验证集准确率最高的模型参数，最终结果为 3 个随机种子的平均
- 跨域评估：对每个子数据集，用其他子数据集训练，然后在目标子数据集上测试并取平均

## 4. 资源与算力

- **论文中未明确说明**具体的 GPU 型号、数量、训练时长等硬件算力信息。
- 仅提及使用了 LLaMA2-7B-Chat 与 LLaMA2-13B-Chat 两个模型进行推理与特征提取，以及使用 GPT-4o 辅助生成提示模板。
- 整体实验属于“基于预训练模型内部状态”的轻量级检测器训练（MLP 等），算力需求相对不高，但具体规模不得而知。

## 5. 实验数量与充分性

### 主要实验
1. **True-False 数据集**上的跨主题泛化实验（7B/13B 两个模型，各 6 个子数据集），共 2 张结果表。
2. **LogicStruct 数据集**上的跨语法结构迁移实验，训练于肯定句，测试于否定/合取/析取句。
3. **TruthfulQA 真实场景实验**，对比 SelfCheckGPT 等，并测试三种 BLEURT 阈值。
4. **消融实验**：
   - 提示选择：对 10 个模板全部进行测试，并与方差比排名对比，计算 Pearson 相关系数。
   - 层选择：使用中间层（16 层）特征重复实验。
   - 内部状态 vs 直接输出：比较基于 Yes/No token 概率比与基于内部状态的准确性。
5. **附录分析**：PCA 可视化、真值方向方差比对比、余弦相似度矩阵（Prompt 1 和 Prompt 3 均覆盖）。

### 充分性与客观性评价
- 实验覆盖面较广：涵盖不同主题、不同语法结构、真实问答场景，以及两个规模不同的 LLM，具有较强的说服力。
- 消融设计较为完整，验证了提示生成、提示选择、层选择、内部状态必要性等多个环节。
- 对比方法多样，包括无监督和监督基线，且与原文设置保持一致。
- 一个潜在不足是实验主要基于 LLaMA2 系列，未在更多模型上验证泛化性；每个数据集规模不大，且未报告方差/显著性检验（除 Pearson 相关系数外）。

## 6. 主要结论与发现

- 引入合适提示可以显著提升 LLM 内部状态中真值结构的**显著性和跨域一致性**。
- 基于方差比选择的提示模板能有效指导 detector 学习到可迁移的底层结构。
- 在所有实验设置下，PRISM 显著提升 MM、SAPLMA 等现有方法的跨域泛化性能；在 LogicStruct 上，从肯定句到否定句/合取句的迁移提升尤为明显。
- 在 TruthfulQA 真实场景中，PRISM 稳定优于 SelfCheckGPT 和原始监督方法。
- 直接利用 LLM 对提示的“Yes/No”输出判断真实性，其准确率远低于基于内部状态训练的检测器，说明内部状态中蕴含更多深层真实性信息。

## 7. 优点

- **方法新颖且轻量**：通过提示工程“无痛”改造内部状态，无需额外收集目标领域数据。
- **理论分析扎实**：使用方差比、余弦相似度等指标系统性地验证了提示对内部状态的影响，具有较强的解释性。
- **普适性强**：框架可以灵活集成到多种现有检测器（MM、SAPLMA）中，并在多个数据集上提升效果。
- **注意选择可量化**：提出基于方差比的自动提示选择机制，且实验证明该指标与实际准确率显著正相关（Pearson = 0.7708，p = 0.0055）。
- **实验设计全面**：覆盖不同主题、语法结构、模型规模、层选择，并针对真实场景进行了验证。

## 8. 不足与局限

- **依赖内部状态访问**：实际中可能无法直接获得目标 LLM 的内部激活，需借助代理模型或接口，限制了应用场景。
- **信息利用不完整**：未充分利用生成过程中的 token 概率、生成文本本身等信息，未来可融合多种信号。
- **模型覆盖有限**：仅在 LLaMA2 系列（7B/13B）上验证，未测试 GPT、Mistral 等其他架构；提示选择过程依赖 GPT-4o，可能引入额外成本或模型相关偏差。
- **指标单一**：主要报告准确率（或 AUROC），未提供精确率/召回率/F1 等指标，可能在类别不平衡场景下不够全面。
- **领域范围有限**：实验数据多为事实性陈述和简单问答，对于复杂推理、多轮对话、开放域生成等场景的推广性尚需验证。
- **实验可复现细节**：未明确报告硬件资源、训练时间、随机种子具体取值等，可能影响复现的便利性。

（完）
