---
title: Evaluating Structure-Aware Retrieval and Safety in Statute-Centric Legal QA
title_zh: 法规中心法律问答中的结构感知检索与安全性评估
authors: "Kyubyung Chae, Jewon Yeom, Jeongjae Park, Seunghyun Bae, Ijun Jang, Hyunbin Jin, Jinkwan Jang, Taesup Kim"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.2112.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 面向法规中心法律问答的结构与安全评测基准，覆盖消防法规的层级化证据检索
tldr: 法律QA基准多聚焦判例法，忽略了法规证据分散在层级化文档中的检索挑战。SearchFireSafety以消防法规为例进行法规中心问答评测：模型既要跨层级整合零散证据，也要在法规上下文不足时安全拒答而非幻觉。基准采用双轨评估框架，将真实用户问题与缺失上下文情形结合；实验显示常规检索器在法规层级检索上明显不足。该工作为法规中心QA提供了结构感知的检索与安全评测工具。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1501, \"height\": 430, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1408, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 765, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 683, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 824, \"height\": 325, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 796, \"height\": 459, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 797, \"height\": 1636, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long2112/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 784, \"height\": 882, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 813, \"height\": 468, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1564, \"height\": 980, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1625, \"height\": 547, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1577, \"height\": 511, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 806, \"height\": 275, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 699, \"height\": 356, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 809, \"height\": 220, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1584, \"height\": 363, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1500, \"height\": 667, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 671, \"height\": 269, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1732, \"height\": 1696, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1735, \"height\": 1644, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long2112/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1744, \"height\": 1213, \"label\": \"Table\"}]"
motivation: 法规中证据常分布在层级化关联文档里，常规检索器难以跨层级检索，模型还容易在不完整上下文下幻觉。
method: 提出SearchFireSafety基准，用消防法规作为实例，以双轨框架同时评测层级化证据检索情况和信息不足时的安全拒答能力。
result: 揭示法规场景下检索器无法跨层级定位证据，而不完整上下文会诱导模型产生幻觉，说明安全拒答评测至关重要。
conclusion: 为法规中心法律问答提供结构化检索与安全性评估基准，利于发展防幻觉的证据问答方法。
---

## Abstract
Legal QA benchmarks have predominantly focused on case law, overlooking the unique challenges of statute-centric regulatory reasoning. In statutory domains, relevant evidence is distributed across hierarchically linked documents, creating a statutory retrieval gap where conventional retrievers fail and models often hallucinate under incomplete context. We introduce SearchFireSafety, a structure- and safety-aware benchmark for statute-centric legal QA. Instantiated on fire-safety regulations as a representative case, the benchmark evaluates whether models can retrieve hierarchically fragmented evidence and safely abstain when statutory context is insufficient. SearchFireSafety adopts a dual-track evaluation framework combining real-world questions that require citation-aware retrieval and synthetic partial-context scenarios that stress-test hallucination and refusal behavior. Experiments across multiple large language models show that graph-guided retrieval substantially improves performance, but also reveal a critical safety trade-off: domain-adapted models are more likely to hallucinate when key statutory evidence is missing. Our findings highlight the need for benchmarks that jointly evaluate hierarchical retrieval and model safety in statute-centric regulatory settings.

---

## 论文详细总结（自动生成）

## 论文详细中文总结

**论文标题**: Beyond Case Law: Evaluating Structure-Aware Retrieval and Safety in Statute-Centric Legal QA（超越判例法：法规中心法律问答中的结构感知检索与安全性评估）

**会议**: ACL 2026（Long Papers）

---

### 1. 核心问题与研究动机

- **现有研究缺口**：现有法律 AI 基准（LexGLUE、LegalBench、CLERC、LEGAR-BENCH 等）大多聚焦于判例法（Common Law）体系下的案例检索与相似案例匹配，将法律语料视为**扁平化、无结构的文档集合**。这种假设忽略了法规中心（Statute-Centric）领域（如数据保护、消防安全）中法律含义分布在不同层级、相互引用的文件中的事实。
- **核心问题（Statutory Retrieval Gap，法规检索鸿沟）**：法规体系通常呈层级结构（如韩国消防法规体系：Act → Enforcement Decree → Enforcement Rule → Technical Standard，即法律 → 施行令 → 施行规则 → 技术标准）。用户查询往往与高层级法律条文词法对齐，但精确答案却存在于下游技术标准等低层级文档中，两者之间仅靠显式引用链连接，没有语义近似关系，导致常规稠密/稀疏检索器无法有效跨越层级获取证据。
- **安全问题**：在消防法规这类直接影响现实物理安全的领域中，当关键证据缺失时模型必须能够“安全拒答”（abstain），而不是基于参数记忆生成看似合理但缺乏依据的内容。法律问答需要同时评估**层级化证据检索能力**与**不确定性下的安全拒答能力**。

---

### 2. 方法论：核心思想与技术细节

论文提出了 **SearchFireSafety（SEARCH FIRE SAFETY）**评测基准，构建流程分为三个阶段：

#### 2.1 法规语料构建（Corpus Compilation）

- **时间同步**：由于韩国 2022 年将 NFSC 法规拆分为 NFPC 和 NFTC 两套法规，搜索引擎仍常排旧版 NFSC，LLM 也常基于 2022 年前的预训练数据产生过时回答。论文从韩国国家法律信息中心抓取数据，构建了**截至 2025 年 4 月 30 日**的同步语料。
- **多模态摄取管道**：针对约 2% 的含复杂表格和数学公式的图像条文以及 PDF 附件，采用 GPT-4o OCR + 人工校验的 Human-in-the-Loop 流程进行结构化转录。
- **基于结构的切分**：共收集 131 部法律法规，按法律原生层级（条、项、款）切分为 **4,467 个原子检索单元**，而非固定长度窗口；每个单元拼接法律名称作为元数据前缀。

#### 2.2 引用图增强（Graph Augmentation）

- 解析韩国国家法律信息中心嵌入的 `<a>` 超链接，构建文档间显式引用边。
- 针对法律文本内部的“前条”“后条”等**法内引用**缺乏超链接的问题，开发正则表达式解析器，将其映射到规范的 Document ID，从而形成完全连通的引用图 G = (D, E)。

#### 2.3 双源问答构建（Dual-Source QA Construction）

- **真实世界专家 QA（876 对）**：从韩国国民 petition 门户（epeople.go.kr）收集国民向国家消防厅（NFA）咨询的问答。采用半自动流程：从官方答复中抽取引文，用 BM25 匹配语料，再由所有作者在并排查看器中逐条人工核验，建立查询到金标文档的映射。这些真实问题天然需要沿引用链跨文档聚合证据。
- **合成多跳 MCQ（3,395 道）**：采用 **Graph-Guided Generation** 策略，选取显式链接的文档对 (dA → dB)，令 dA 将某一细节委托给 dB，提示 GPT-4o 生成 [查询、选项、答案、解释] 四元组。每条问题构成 **严格条件依赖（Strict Conditional Dependency）**：同时存在 A+B 两个文档才可作答，缺失 A 时模型有选项 5 “无法根据给定信息作答”可供选择。经过两阶段过滤：剔除格式/语法错误及元指涉问题（1,076 问因仅凭 dA 可答被剔除，58 问因即使有完整上下文也无法作答被剔除），共从 5,091 道初始题目筛得 3,395 道。

#### 2.4 提出的检索方法：Structure-Aware Reranking（SAR）

SAR 是在稠密检索基础上的图引导重排框架，核心步骤为：

1. **种子选取**：取基础检索 top-k（k=15）个文档作为投票种子 S，保留其语义相关分数 S_dense。
2. **Robust Voting 结构分数传播**：种子将其语义分数沿显式引用边传播到邻居候选 n，计算公式为：

   B(n) = (1/L(n)) · Σ_{s∈S} I(s→n) · S_dense(s) / L(s)

   其中 I(s→n) 表示种子 s 到邻居 n 的显式链接；L(x) = log(deg(x) + 1) 为对数惩罚函数：deg(s) 为种子的局部出度（惩罚不加区分引用的“枢纽”种子），deg(n) 为全局入度（惩罚如“第 1 条”这类通用超级枢纽）。
3. **Residual Fusion 残差融合**：

   S_SAR(n) = S_dense(n) + β · B(n) · (1 − S_dense(n))

   其中 β=0.3 控制结构信号权重；(1 − S_dense(n)) 作为门控因子，确保结构奖励主要用于提升排序靠后的“鸿沟”文档，不干扰高置信语义锚点。

#### 2.5 领域继续预训练（CPT）

- 在 Qwen3-8B 上对全部线性层（Q、K、V、O 和 MLP）施加 LoRA，r=256、α=32；在 Qwen3-32B 上仅对 Q 和 V 投影层施加 r=16、α=16 的低秩 LoRA 以保证参数效率。
- 使用 2 张 GPU，每设备批大小 2，4 步梯度累积（有效全局批 16）；8-bit AdamW，峰值学习率 1×10⁻⁵，3% 线性预热；刻意设置权重衰减 10.0 以缓解灾难性遗忘；嵌入层和 LM 头用 5×10⁻⁶ 专用学习率微调；全部实验采用 Bfloat16 精度和梯度检查点。

---

### 3. 实验设计

#### 3.1 数据集与评测基准

- **测试语料**：131 部消防法律法规，4,467 个检索单元，含显式引用图标注。
- **Task 1（检索）**：876 对真实世界专家 QA，评测 Recall@K 和 nDCG@K（K=10/20/50）。
- **Task 2（安全/生成）**：3,395 道合成多跳 MCQ，三种上下文设置：
  - **Zero-Shot**（无上下文）：衡量参数记忆。
  - **Full Context**（文档 A+B）：衡量完整证据下的多跳推理。
  - **Partial Context**（仅文档 A，B 被隐藏）：正确答案为“无法确定”，衡量不确定性感知与拒答能力。

#### 3.2 对比方法

- **稀疏检索**：BM25（Jamo 分解）
- **稠密检索**：Qwen3-Emb-0.6B、BGE-M3
- **重排增强策略**：RRF（Reciprocal Rank Fusion）、Rocchio 伪相关反馈（α=0.3、β=0.7）、本文提出的 SAR
- **生成模型**：5 个具备韩语能力的 LLM：GPT-4o（API）、Qwen3-8B、Qwen3-32B、Exaone3.5-7.8B、HyperClovaX-14B（开放权重模型在 FP16 下单卡 RTX-A6000 上运行）

#### 3.3 英文/开放式生成评测

- 在真实专家 QA 上用 ROUGE-1/L、BERTScore 等词法与嵌入指标，外加 LLM-as-a-Judge（GPT-4o）的双任务：参考引导评分（Binary Factuality）与配对比较 Win-Rate，分别比较 Zero-Shot / Retrieve（BGE-M3 top-5）/ Full Context 三种输入策略。

#### 3.4 可选实验

- 领域微调 BGE-M3（InfoNCE 损失 + BM25 难负样本挖掘，训练集 13,331 对问答：3,395 条多跳 + 9,936 条单跳），对比微调前后 SAR 是否仍有增益。

---

### 4. 资源与算力

- **推理资源**：论文明确说明所有开放权重模型在单个 RTX-A6000（48GB）上以 FP16 运行；GPT-4o 通过 OpenAI API 访问。
- **CPT 训练资源**：使用 **2 张 GPU** 进行继续预训练（但论文未指明 GPU 型号），每设备批大小 2、4 步梯度累积，采用 Bfloat16 和梯度检查点。
- **人工投入**：语料构建使用了 Human-in-the-Loop（GPT-4o OCR + 作者人工校验），真实问答映射由全体作者独立审核；合成数据经两阶段过滤。
- **未明确报告的信息**：CPT 总训练时长（token 数、训练步数/轮数）、总 GPU 时数在摘要文本中**未明确说明**；合成 MCQ 生成中 GPT-4o 调用的具体成本与次数也未给出。

---

### 5. 实验数量与充分性

#### 5.1 主要实验组

1. **检索实验（表 4）**：2 种稠密检索模型 × 3 种增强策略（RRF / Rocchio / SAR）+ BM25 基线，覆盖 R@10/20/50、nDCG@10/20/50 共 6 个指标。
2. **SAR 消融/鲁棒性分析（表 6）**：结构权重 β ∈ {0.0, 0.1, 0.3, 0.5, 0.7, 0.9} 的敏感性分析。
3. **领域微调消融（表 7）**：微调后基线与基线对比，及微调后叠加 SAR 的效果。
4. **三种上下文的生成准确率（表 5）**：5 个模型 × 3 种场景。
5. **行为分解分析（表 8）**：将输出分解为 Correct / Wrong / Abstain 三率，对比 Zero-Shot / Full Context / Partial Context 下的模型校准行为。
6. **CPT 域适应实验（图 3）**：Qwen3-8B 与 Qwen3-32B 在 CPT 前后三种场景的准确率变化。
7. **开放式生成实验（表 9）**：5 个模型 × 3 类检索输入策略 × 5 种评价指标（ROUGE-1/L、BERTScore、LLM-Grading、Win-Rate）。
8. **LLM 评判者可靠性实验（表 10）**：GPT-4o 输出的人工标注对比混淆矩阵（TP=61.20%、FN=10.80% 等），Cohen's Kappa = 0.88。

#### 5.2 充分性评估

- **优点**：实验覆盖较全面，检索侧覆盖稀疏/稠密、特征融合/查询扩展/图重排三类范式，并做了 β 敏感性分析和领域微调叠加验证；生成侧包含选择题和多选题两种形式，并使用人工交叉验证 LLM 评判者的偏差。
- **不足**：开放式生成实验中部分辅助指标（如小巧模型 Exaone3.5-2.4B 等）仅出现在正文外的附录，正文 5 个模型的中小型规模（8B–32B）对更大模型泛化性的代表性有限；实验仅覆盖韩语和消防法规单一领域，跨语言/跨法规体系的泛化结论未得到多领域验证；CPT 的训练数据构成与规模细节不透明；检索实验仅考察固定 K 的 Recall/nDCG，未报告 MRR、P@1 等更偏早排位的指标。

---

### 6. 主要结论与发现

1. **法规检索鸿沟真实存在**：BM25 明显落后于稠密检索（Recall@20 30.40 vs 57.72–61.66），说明用户查询（口语化自然表述）与法规文本之间存在严重的词法与语义错配。
2. **SAR 有效且稳健**：SAR 在两种稠密检索模型上均带来一致增益（BGE-M3 上 Recall@10 从 53.77 提升至 54.70，Recall@20 从 61.66 提升至 62.86；Qwen3-Emb 上 Recall@10 从 48.70 提升至 53.26），且增益在 β=0.1–0.5 范围保持稳定，对模型选择不敏感。相反，RRF 未带来一致提升，Rocchio 在 BGE-M3 上出现性能退化（初始 top-K 质量不佳时查询扩展会漂移）。
3. **显式引用图优于语义相似邻域**：PCA 可视化表明，以同样的种子集出发，显式引用图形成 seed → ground-truth 的直接连边概率显著高于余弦 kNN 邻域图（1-hop hit rate 0.156 vs 0.041），结构信息能构建基于语义相似度无法实现的文档桥。
4. **完整证据下多跳推理是可行的**：
