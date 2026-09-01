---
title: Rethinking Retrieval-Augmented Generation as a Cooperative Decision-Making Problem
title_zh: 将检索增强生成重新思考为合作决策问题
authors: "Lichang Song, Ting Long, Yi Chang"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.2157.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 从合作决策视角重构检重排序器与生成器关系以增强知识锚定
tldr: 现有RAG系统中重排序器与生成器往往是不对称依赖，生成质量受重排序结果制约。该工作提出CoRAG框架，将二者视为同等决策者，面向共同目标联合优化，鼓励双方协作。实验表明CoRAG增强了外部证据的利用与生成效果，为RAG系统设计提供了新视角。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2157/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 804, \"height\": 405, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2157/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 752, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2157/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 801, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl2157/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 826, \"height\": 538, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2157/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 620, \"height\": 256, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2157/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1601, \"height\": 1194, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2157/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2157/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 779, \"height\": 360, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2157/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 781, \"height\": 287, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl2157/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 829, \"height\": 272, \"label\": \"Table\"}]"
motivation: 传统RAG中生成器过度依赖重排序结果，存在不对称依赖局限。
method: 将reranker与生成器建模为对等决策者，联合优化共享任务目标。
result: 实验显示CoRAG提升了知识密集型任务的生成质量和证据利用。
conclusion: 协作式决策范式可改善RAG的整体性能。
---

## Abstract
Retrieval-Augmented Generation (RAG) has demonstrated strong effectiveness in knowledge-intensive tasks by grounding language generation in external evidence. Despite its success, many existing RAG systems are built based on a ranking-centric, asymmetric dependency paradigm, where the generation quality of the generator is highly dependent on reranking results of the reranker.To overcome this limitation, we propose Cooperative Retrieval-Augmented Generation (CoRAG), a framework that treats the reranker and the generator as peer decision-makers rather than being connected through an asymmetric dependency pipeline. By jointly optimizing their behaviors toward a shared task objective, the reranker and generator are encouraged to cooperate, ensuring that document reranking and generation work in concert to improve the final response.Experimental results demonstrate good generalization and improved generation stability of CoRAG, even when the model is trained on only around 10K PopQA samples. Our model released in https://github.com/CoderrrSong/CoRAG

---

## 论文详细总结（自动生成）

## 论文详细中文总结

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **传统 RAG 的结构性局限**：现有 RAG 系统普遍采用"以排序为中心、不对称依赖"的范式——重排序器（reranker）产生固定的文档排序，生成器（generator）严格依赖这些排在最前的文档进行回答。在这种串联管道中：
  - 生成质量对重排序结果的细微变化高度敏感；
  - 若重排序器将不相关文档误置顶端，即使正确的文档仍在 Top-N 集合内，生成器也可能产出错误答案；
  - 从优化视角看，学习多个高度相关文档之间的精确全序（总排序）本质上比学习宽松的相对排序更困难，导致系统性偏差。
- **核心研究问题**：如何打破重排序器与生成器之间的不对称依赖，使二者能够协同决策？
- **提出的解决思路**：将 RAG 重新概念化为一个**合作式多智能体决策问题**——重排序器与生成器作为对等的决策参与者，在共享任务奖励的引导下联合优化，而非通过固定的前向管道串联。
- **论文整体含义**：通过合作式优化范式，让重排序器面向最终答案质量学习更适宜的文档排序，同时让生成器不再盲目依赖严格的排序信号，从而同时提升生成的稳定性与整体性能。

### 2. 论文提出的方法论

#### 2.1 核心思想

- 将 RAG 建模为**合作式多智能体问题**：重排序器与生成器是两个决策角色不同但目标一致的智能体。
- 共享的目标函数定义为：

  ```
  max E_{D' ~ S_θ(·|q,D), â ~ G_φ(·|q,D')} [R(a*, â)]
  ```

  其中 θ、φ 分别为重排序器和生成器参数，R(a*, â) 为基于生成答案的任务导向奖励（回答包含正确结果则奖励为 1，否则为 0）。

#### 2.2 重排序器（Reranker）

- 实现：基于 BGE-Reranker-v2-m3，对查询 q 与候选文档 dᵢ 计算相关性分数 sᵢ = S_θ(q, dᵢ)。
- 根据分数取 Top-K 文档构成 D'，输入给生成器。

#### 2.3 生成器（Generator）

- 实现：基于 Llama-3-Instruct 8B 的自回归语言模型。
- 输入查询 q 与重排序器选出的 Top-K 文档 D'，生成最终回复 â。

#### 2.4 联合优化

- **奖励设计**：任务导向奖励 r = R(a*, â)，即生成回复是否包含标准答案；在训练中使用 0/1 信号。
- **重排序器优化（GRPO 风格）**：
  - 将延迟的任务级奖励降级为**文档级随机偏好信号**：统计每个文档历次被纳入 Top-K 时的成功/失败信号，计算经验成功率 ¯l(q, dᵢ)；
  - 将成功率映射为平滑 Bernoulli 参数 p(q, dᵢ) = α + (1 - 2α)·¯l(q, dᵢ)，采样得到随机偏好标签 pᵢ；
  - 在期望上等价于 GRPO（组相对偏好），但为降低方差，进一步将随机偏好降级为**确定性成对排序损失**：

    ```
    L_rank = Σ_{d+∈D+} Σ_{d-∈D-} max(0, s_θ(q,d-) - s_θ(q,d+) + γ)
    ```

  - 论文明确指出该排序损失虽不是 GRPO 的严格等价物，但在期望上保留了组相对偏好，作为稳定且高效的替代代理。

- **生成器优化（GRPO 标准式）**：

  ```
  L_gen = -E_{â~π_φ} [Â(â) · log π_φ(â | q, D')]
  ```

  组相对优势 Â(â) 由同批次内其他回复的奖励作为基线计算。

- **整体训练流程**（Algorithm 1）：
  1. 计算文档相关性分数 → 2. 选择 Top-K 文档 → 3. 生成答案 → 4. 计算奖励 → 5. 估计文档级成功信号 → 6. 采样偏好标签 → 7. 更新重排序器（L_rank）→ 8. 更新生成器（L_gen）。

### 3. 实验设计

#### 3.1 数据集与 Benchmark

| 数据集 | 用途 | 训练规模 | 测试规模 |
|---|---|---|---|
| PopQA | 训练+测试 | 12,868 | 1,399 |
| TriviaQA | 仅测试（泛化） | — | 11,313 |
| Natural Questions (NQ) | 仅测试（泛化） | — | 3,610 |
| ASQA | 仅测试（泛化） | — | 948 |
| 2WikiMultiHopQA | 仅测试（泛化） | — | 12,576 |

- **关键设计**：CoRAG 只在 PopQA 上训练，其余数据全部用于零样本泛化评估。
- 指标：除 ASQA 报告 EM、引用精确率（precision）和引用召回率（recall）外，其余数据集统一使用准确率（accuracy）。

#### 3.2 对比方法

- **无检索基线**：Vanilla Zero-shot（ChatGPT、Llama-3-Instruct 8B/70B）；
- **RAG 无训练**：In-Context RALM、Few-shot Demo w/ Instruction、InstructRAG-ICL；
- **RAG 有训练**：Vanilla SFT、Self-RAG（Llama-2 7B/13B、Llama-3 8B）、RetRobust、InstructRAG-FT。

#### 3.3 实验组别概览

- **主实验（RQ1）**：五个数据集上与全量基线对比。
- **消融实验（RQ2）**：五种变体（仅训练重排序器、仅训练生成器、替换双组件、替换生成器、替换重排序器）。
- **交叉验证（RQ2 补充）**：CoRAG 的重排序器/生成器与 Self-RAG、InstructRAG 的组件互相替换。
- **Top-N 分析（RQ3）**：Top-1/3/5 文档数量对性能的影响，对比 InstructRAG、RetRobust。
- **跨任务评估（RQ4）**：代码生成（HumanEval、HumanEval+）和表格问答（WikiTable Questions）。
- **LLM-as-a-judge 评估（RQ5）**：用 LlaMa、GPT-4o、DeepSeek-v3.2、Qwen3-VL 四个外部 LLM 评估答卷质量。
- **鲁棒性实验（附录 C）**：对文档顺序进行随机打乱，对比乱序 vs. 原始排序状态下的性能。

### 4. 资源与算力

- 论文在正文中**未明确说明**具体 GPU 型号、数量与训练时长。
- 已知的实现细节包括：
  - 采用 **LoRA 高效微调**策略；
  - 重排序器学习率为 5e-5，生成器学习率为 1e-5；
  - 训练数据仅约 1 万条 PopQA 样本，计算开销应显著低于全量微调（但具体硬件规格不可考）。

### 5. 实验数量与充分性

#### 5.1 实验数量

- 实验数量较为丰富，覆盖：
  - 5 个知识密集型 QA 数据集的主评测；
  - 5 组消融变体 + 4 组交叉组件组合；
  - 3 种文档数量设置下的对比；
  - 3 个跨域任务数据集；
  - 4 个不同 LLM 评判者的评测；
  - 文档乱序鲁棒性专项实验。

#### 5.2 充分性评估

- **优点**：主实验、消融、泛化、鲁棒性均有覆盖，尤其交叉组件实验设计有助于揭示组件间的协同关系；仅用 10K 样本训练即实现多数据集泛化，实验设计具有较强的说服力。
- **局限**：
  - 所有训练数据单一来自 PopQA（事实型短答案数据集），对多答案/长文生成任务（如 ASQA）的适用性未得到验证，ASQA 上的表现不佳也印证了这一点；
  - 消融实验中 GTrain 与 GReplace 的提升远大于 RTrain 与 RReplace，说明生成器的贡献权重被放大，重排序器的独立贡献有限，评估的公平性存在一定潜在偏差；
  - 未报告统计显著性检验，且多数数据集只报告 single-run 的准确率。

### 6. 论文的主要结论与发现

- **CoRAG 显著优于基线**：在仅用 PopQA 训练的前提下，在 PopQA（71.2%）、TriviaQA（81.0%）、NQ（72.4%）、2WikiMultiHopQA（58.2%）四个数据集上达到 SOTA，超越 InstructRAG-FT 和 RetRobust 等训练类方法。
- **ASQA 上欠佳**：多源合成与歧义问题与 PopQA 的事实型问答任务差异过大，协同模式未能有效迁移。
- **联合优化优于独立训练**：消融实验显示单独微调重排序器或生成器均不如联合优化。
- **生成器在整体提升中贡献更大**：交叉验证表明，联合优化使生成器降低了对细粒度排序信号的依赖，但相应地削弱了重排序器独立提升的可观测收益。
- **鲁棒性强**：文档数量增加时 CoRAG 性能稳定上升（InstructRAG 反而下降）；打乱文档顺序后 CoRAG 几乎不受影响，而基线明显下降。
- **跨任务泛化良好**：在代码生成（HumanEval/HumanEval+ pass@10）和表格问答（WTQ）上达最佳或次佳水平。
- **外部 LLM 评判一致偏好**：在四种不同 LLM 评判下，CoRAG 均获最高得分（平均 71.35%，远高于 InstructRAG 的 64.60% 和 RetRobust 的 45.69%）。

### 7. 优点

- **视角创新**：将 RAG 从"排序-生成"不对称管道重构为合作决策问题，概念上具有启发性。
- **技术适配性好**：GRPO 风格的重排序优化有效规避了标准 MARL 与排序任务的结构性不匹配（如重复选同一文档导致无效排序）问题。
- **训练高效**：仅需约 10K 训练样本即可跨多个数据集泛化，计算成本低。
- **降方差策略务实**：将随机 GRPO 目标降级为确定性成对排序损失，既保留组相对偏好又在期望上与 GRPO 对齐，工程实现稳定可控。
- **鲁棒性设计验证充分**：乱序实验和 Top-N 分析直接回应了"生成器不对称依赖重排序结果"的核心痛点，实证数据令人信服。
- **跨任务验证加分**：不只限于 QA 范围，还覆盖了代码生成与表格推理，展示了一定普适性。

### 8. 不足与局限

- **训练数据单一性**：仅在 PopQA 上训练（事实型、单答案），对多答案、长文、综合型任务（如 ASQA）迁移效果有限，限制了方法在更广应用场景下的说服力。
- **重排序器独立价值有限**：交叉实验表明，CoRAG 的生成器对文档顺序高度鲁棒，反而削弱了重排序器的边际贡献，这意味着"协作"可能部分转化为"生成器单方面妥协"；作者也承认存在这一张力。
- **任务奖励定义粗糙**：奖励只定义为"回答是否包含标准答案"（0/1），对部分正确、多跳推理、语义等价等场景缺乏细粒度刻画。
- **文档级信用分配粗糙**：用文档被纳入时的整体成功信号近似单文档贡献，在多文档联合作用下存在噪声归因的问题（作者亦承认）。
- **算力信息缺失**：未报告 GPU 型号、数量、训练时长等可复现性关键信息。
- **统计验证不足**：未提供多次运行的标准差或显著性检验，无法确认性能提升的统计稳定性。
- **评判者偏差隐患**：LLM-as-a-judge 实验中，CoRAG 从 LlaMa 微调而来，在 LlaMa 评审中得分显著偏高（89.21% vs. 其他方法），可能包含模型家族偏好偏差，论文对此的解释虽合理但未做进一步控制实验。

（完）
