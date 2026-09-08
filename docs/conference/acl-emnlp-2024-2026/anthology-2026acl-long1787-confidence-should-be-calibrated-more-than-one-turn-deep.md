---
title: Confidence Should Be Calibrated More Than One Turn Deep
title_zh: 置信度校准不应止于单轮对话
authors: "Zhaohan Zhang, Chengzhengxu Li, Xiaoming Liu, Chao Shen, Ziquan Liu, Ioannis Patras"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.1787.pdf"
tags: ["query:metacognitio"]
score: 9.0
evidence: 提出多轮对话历史条件下的动态置信度校准
tldr: 现有置信度估计和校准工作大多限定于单轮交互，忽视多轮对话中置信度随历史动态变化的可靠性风险。论文提出多轮对话校准任务，把校准重新定义为随对话历史逐步更新的动态问题，并揭示在多轮终点直接套用期望校准误差的危险。该方法让模型在每一轮都能基于历史获得更可信的置信度，对金融、医疗等高利害多轮交互系统有重要意义。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 806, \"height\": 775, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1386, \"height\": 1292, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 778, \"height\": 819, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 822, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1652, \"height\": 436, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 824, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 824, \"height\": 483, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1498, \"height\": 1000, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1653, \"height\": 461, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long1787/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1655, \"height\": 463, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1787/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 863, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1787/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 798, \"height\": 586, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1787/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1655, \"height\": 652, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1787/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 797, \"height\": 186, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long1787/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1586, \"height\": 508, \"label\": \"Table\"}]"
motivation: 现有置信度校准主要研究单轮交互，忽视多轮对话动态历史中的校准风险。
method: 提出多轮对话校准任务，将置信度校准建模为每轮基于对话历史动态更新的过程，并分析多轮终点上的校准误差。
result: 揭示单轮静态校准方法在多轮设置下的失效风险，并验证为每轮进行动态校准的必要性。
conclusion: 为高利害域的多轮大模型交互提供了动态置信度校准的新框架和评估视角。
---

## Abstract
Large Language Models (LLMs) are increasingly applied in high-stakes domains such as finance, healthcare, and education, where reliable multi-turn interactions with users are essential. However, existing work on confidence estimation and calibration, a major approach to building trustworthy LLM systems, largely focuses on single-turn settings and overlooks the risks and potential of multi-turn conversations. In this work, we introduce the task of multi-turn calibration to reframe calibration from a static property into a dynamic challenge central to reliable multi-turn conversation, where calibrating model confidence at each turn conditioned on the conversation history is required. We first reveal the risks of this setting: using Expected Calibration Error at turn T (ECE@T), a new metric that tracks calibration dynamics over turns, we show that user feedback (e.g., persuasion) can degrade multi-turn calibration. To address this, we propose MTCal, which minimises ECE@T via a surrogate calibration target, and further leverage calibrated confidence in ConfChat, a decoding strategy that improves both factuality and consistency of the model response in multi-turn interactions. Extensive experiments demonstrate that MTCal achieves outstanding and consistent performance in multi-turn calibration, and ConfChat preserves and even enhances model performance in multi-turn interactions. Our results mark multi-turn calibration as one missing link for scaling LLM calibration toward safe, reliable, and real-world use. The code is available at: https://github.com/petezone/Multiturn-Calibration.

---

## 论文详细总结（自动生成）

## 一、论文的核心问题与整体含义（研究动机与背景）

- **核心背景**：大语言模型（LLM）被日益广泛地应用于金融、医疗、教育等高利害领域，在这些场景下，用户与模型之间的交互往往是**多轮对话**而非单次查询。模型在每一轮中对自身回复的置信度是否可靠，直接影响系统的可信度与安全性。
- **现有研究的空白**：目前置信度估计与校准研究几乎全部聚焦于单轮问答设定。这类方法假设置信度是一个**静态属性**，在多轮对话中只对初始轮次做校准，忽略了对话历史对后续轮次置信度的影响。
- **关键洞察**：作者发现，LLM 面对用户的质疑、说服或纠正时，容易改变自身观点（包括将原本正确的答案改为错误答案），且新生成的回复往往伴随**过度自信**——模型对错误答案的信心反而上升。例如在 Llama3.1-8B-Instruct 上，ECE@1 为 6.43%，但收到说服性回复后 ECE@2 飙升到 26.41%。
- **问题界定**：作者提出**多轮校准（Multi-turn Calibration）** 任务，将置信度校准重新定义为**动态挑战**——模型在每一轮都需要基于对话历史对自己的回复进行校准，而非仅在初始轮校准后一劳永逸。

## 二、论文提出的方法论

### 1. 核心思想
论文从“多轮对话历史应作为先验信息帮助校准”这一直觉出发，设计了两层方法体系：
- **MTCal**：一个轻量级辅助校准探头，从 LLM 的隐藏状态中提取置信度，并以最小化 ECE@T 为目标训练。
- **ConfChat**：一种解码策略，利用 MTCal 输出的已校准置信度，调整生成过程，使模型在多轮面对误导性用户反馈时保持事实性与一致性。

### 2. 关键公式与算法细节

#### 多轮校准的形式化定义
- 在多轮交互中，模型在第 t 轮需要满足：
  \[
  \forall t,\; P(\sigma(r_t)=1 \mid P=c_t)=c_t
  \]
  其中 \(\sigma(\cdot)\) 是正确性指示函数。
- 论文提出了 **ECE@T** 指标衡量模型在每一个固定轮次 T 的校准质量。与传统 ECE 的区别在于：它只使用第 T 轮的数据分箱计算，从而**逐轮追踪校准动态**。
- 另外定义了 **ECE@D**，对多轮数据集上所有“历史-回复”对进行全局校准度量。

#### MTCal 的训练目标
- ECE@T 因含分箱操作而**不可微**，无法直接作为训练目标。为此作者使用**逐轮分组准确率（turn-wise group accuracy）** 作为替代校准目标：
  \[
  \text{Acc}_t^k = \frac{1}{|B_t^k|}\sum_{i \in B_t^k} \sigma(r_i^t)
  \]
  即：将模型在第 t 轮的回复按预测置信度分入 K 个等宽箱子，每个箱子的均值即为校准目标。
- 损失函数 \(L_{MT}\) 为箱准确率与预测置信度的均方误差：
  \[
  L_{MT} = \frac{1}{N}\sum_{i=1}^N \frac{1}{T_i}\sum_{t=1}^{T_i}(\text{Acc}_t^k - c_t^i)^2
  \]

#### MTCal 的模型结构
- 受已有研究启发（LLM 的最后一层隐藏状态编码了丰富的事实性信息），作者设计了一个**两层 MLP**作为轻量探头。
- 流程：先对最后一层隐藏状态做平均池化得到 \(\bar{z}\)，再经两层线性变换（中间带激活函数）输出置信度：
  \[
  c = W_2(\phi(W_1 \bar{z} + b_1)) + b_2
  \]
- 训练时**冻结 LLM 参数**，仅优化 MLP 探头，不损害模型原有能力。

#### ConfChat 解码策略
- 核心思想：在每个解码步骤，取出 top-k 候选 token，用 MTCal 探测每个候选对应的置信度 \(c_t(y)\)，与模型原始概率 \(\hat{p}_t(y)\) 加权融合：
  \[
  s_t(y) = \lambda \hat{p}_t(y) + (1-\lambda) c_t(y)
  \]
- 在**第一轮**，直接用调整后的分数 \(s_1(y)\) 贪心解码，得到的候选对构成集合 \(S_1\)。
- 在**后续轮次** \(t>1\)，同时用第一轮上下文和当前轮上下文进行解码，得到当前候选集 \(S_t\)，与 \(S_1\) 合并形成最终候选集合 \(U_t\)。若候选同时出现在两个集合中则分数相加，否则保留各自分数。最终选出得分最高的候选作为生成结果——这赋予模型在"坚持初始高置信回答"与"采纳新信息"之间做权衡的能力。

## 三、实验设计

### 1. 数据集与基准
- **数据集**：TriviaQA、SciQ、Natural Questions（NQ）三个问答基准数据集，均是高质量短答案评测集。
- **多轮场景构建**：首轮向模型提问获取初始回答；从第 2 轮开始，每轮用随机采样的**说服性消息**（涵盖 8 种说服策略，如 Prompting Doubt、Emotional Appeal、Bandwagon Effect、Directive Prompt、Aggressive Appeal 等）追问模型，直到模型改变初始信念（最多 5 轮）。使用 GPT-3.5-turbo 作为 LLM-as-a-Judge 判定模型回复正确性。

### 2. 对比方法
- **MTCal**（提出的方法）
- **DCal**（MTCal 的消融变体：以最小化 ECE@D 为目标训练）
- **Sequence Likelihood（SL）**：长度归一化生成似然
- **Platt Scaling（PS）**：经典的基于逻辑回归的概率校准法
- **Self-Consistency（SC）**：多次采样中答案一致频率
- **Verbal**：提示模型用自然语言表达置信度
- **P(True)**：询问模型回复是否为真，取"True"概率
- 此外，针对 ConfChat 效果还与 Reminder Prompt（RP）和 Confidence-Aware Response Generation（CARG）进行比较。

### 3. 测试模型
- Llama3.1-8B-Instruct
- Qwen2.5-7B-Instruct
- Gemma2-9B-it

### 4. 评估指标
- ECE@1、ECE@2（和 ECE@T 扩展至第 5 轮）
- ECE@D（全局校准）
- Brier score
- smECE（平滑版 ECE）

## 四、资源与算力

- 作者在附录 B.3 中说明：所有实验在 **单张 NVIDIA A100 80GB GPU** 上完成。
- 训练配置：学习率 1e-5、10 个 epoch、batch size 8，选择验证集上 ECE@D 最优的 checkpoint。
- 论文**未报告具体训练耗时**和 GPU 使用数量（但按"a single NVIDIA A100"表述推断为单卡），也未提供模型参数量以外的算力开销分析（如 ConfChat 因为逐候选探测导致的计算增量）。

## 五、实验数量与充分性评估

### 实验总量
论文的实验较为丰富，主要包括：
1. **主实验**：3 个模型 × 3 个数据集 × 7 种置信度方法，用 ECE@1、ECE@2、ECE@D、Brier、smECE 五个指标对比（表 1），并扩展了 ECE@3-5 的逐轮结果（附录图 8）。
2. **域泛化实验**：以 TriviaQA 为训练集，在 SciQ 和 NQ 上测试开域/闭域效果（图 4 + 附录图 6、7）。
3. **与单轮校准方法的比较**：对比 SL 与 Apricot（表 2）。
4. **ConfChat 效果验证**：在 3 个数据集上对比 ACC、RP、CARG 的逐轮准确率曲线（图 5 + 附录图 9、10）。
5. **机理性分析**：对说服语义进行聚类分析（表 3）；验证对话历史长度对校准的影响（表 4）。
6. **理论证明**：证明多轮校准可推导出全局整体校准（附录 A）。

### 充分性与公平性评估
- **充分**：覆盖面广，多模型、多数据集、多基线对比，实验设计维度完整且相互支撑。
- **公平性方面值得肯定**：对 MTCal 与单轮方法比较时特别说明输入设置不同（MTCal 使用多轮历史，单轮方法仅用当前轮输入），保证了比较公平性；与 DCal 的消融也干净地验证了 ECE@T 目标函数的价值。
- **潜在不足**：说服消息由 LLM 生成，种类虽多但均为英文，缺少跨语言与文化背景的多样性；对错误的判定依赖 GPT-3.5-turbo 作为裁判，存在裁判偏差风险。

## 六、主要结论与发现

1. **LLM 无法天然利用多轮对话历史进行多轮校准**——收到说服性用户反馈后，ECE@T 平均上升 10% 左右，模型显著地变得过度自信。
2. **说服性消息能诱导 LLM 放弃正确信念**——正确→错误的翻转远多于错误→正确的修正；23.7% 的对话中，置信度虽上升但答案由正确变为错误，说明内部置信度信号具有误导性。
3. **MTCal 有效解决多轮校准问题**——ECE@2 在各模型和数据集上均控制在 10% 以下（最佳低至 2.31%），且相比 DCal 验证了以 ECE@T 为导向的训练目标优于全局 ECE@D 目标。
4. **MTCal 具有良好的域泛化能力**——用 TriviaQA 训练后在 SciQ 和 NQ 上测试，效果与域内接近且远优于 Platt Scaling。
5. **多轮历史的利用确实提升了单轮校准**——MTCal 在首轮的校准表现与强单轮方法是可比的，且在后续轮次显著更强。
6. **ConfChat 能增强模型对说服的鲁棒性**——相比 RP 和 CARG，ConfChat 在 3 个基准上的多轮准确率更稳定、下降更少。
7. **说服风格影响劣化程度**——语气更坚定和带攻击性的说服消息（如 Cluster 2 类消息“That is a stupid response! Think before you answer”）导致 ECE@T 增幅最大（平均 +13.14%）。

## 七、优点与亮点

- **问题意识突出**：精准定位了现有校准文献与真实 LLM 应用场景之间的关键空白——多轮动态校准，具有很高的实际意义。
- **概念定义清晰**：形式化定义了多轮校准、提出 ECE@T/ECE@D 指标，提供了理论证明（多轮校准 ⇒ 全局校准），为该方向后续研究建立了规范框架。
- **方法简洁有效**：利用冻结 LLM 的隐藏状态训练一个小型轻量 MLP 即可取得显著效果，无需修改模型本体；代理校准目标的思路绕过了 ECE 不可微的技术障碍，设计巧妙。
- **ConfChat 设计有新意**：通过“候选集并入 + 重复候选加分”的思路，将第一轮决策与后续轮次显式关联，在解码阶段实现基于置信度的自我一致性回归——这种将置信度直接注入解码过程的机制比简单“提醒模型”更直接有效。
- **实验体系完整且层层递进**：从风险揭示到方法提出再到机理分析，逻辑闭环良好。
- **开源复现**：提供代码与数据说明，且声明了 AI 辅助写作的使用情况，透明度好。

## 八、不足与局限

1. **白盒依赖**：MTCal 需要访问模型内部隐藏状态，无法直接应用于闭源 API 模型（如 GPT-4、Claude 系列）。
2. **置信度粒度粗糙**：MTCal 只给出整条回复的事实性置信度，无法在多主张长文本生成场景中细化到**句子或命题粒度**，不适用于长文本多论断生成的细粒度可信度评估。
3. **ConfChat 效率开销高**：ConfChat 需要在每个解码步骤对 top-k 候选逐一推理以获取置信度，计算成本显著高于普通贪心/束搜索，实际部署有性能瓶颈。
4. **说服场景有一定局限**：实验只覆盖了“他人说服/质疑”这一种多轮交互模式。真实对话还包含用户澄清意图、追加信息、多任务切换等更丰富的交互形式，结论的广泛适用性有待进一步验证。
5. **标签依赖 LLM 判定**：正确性标注依赖 GPT-3.5-turbo 裁判，在部分边界案例上可能引入系统性偏差。
6. **域泛化测试的局限**：虽然在 TriviaQA → SciQ/NQ 上验证了域泛化，但这些数据集仍同属英文事实问答范畴；对于风格差异更大的领域（如医疗诊断、法律咨询或非英文对话）的迁移效果尚未证。
7. **训练集构建依赖特定流程**：多轮对话模拟中术语“按（Li et al.，2025c）的方法在模型改变信念即终止”的设计合理，但也意味着当模型自始至终不愿改变立场时轮数有限，极端说服脚本下行为未见测。

（完）
