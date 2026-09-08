---
title: "From Query to Counsel: Structured Reasoning with a Multi-Agent Framework and Dataset for Legal Consultation"
title_zh: 从查询到咨询：面向法律咨询的多智能体结构化推理框架与数据集
authors: "Mingfei Lu, Yi Zhang, Mengjia Wu, Yue Feng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.acl-long.776.pdf"
tags: ["query:evidence-qa"]
score: 7.0
evidence: 法律咨询问答数据集与基于法条依据的多智能体框架
tldr: 法律咨询问答与一般法律QA不同，面临高质量训练数据少、任务组合复杂、上下文依赖强等挑战。本文构建逾4.3万条真实中文咨询的JurisCQAD数据集，用专家校验的正负样本支持训练评测，并设计将查询拆解为融合实体、事件、意图和法律争点的要素图的方法，再配合支持动态路由、法条锚定与风格优化的JurisMA多智能体框架。该工作为法律领域可核查的问答系统提供了规模化数据和结构化推理方案。
source: ACL-2026-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long776/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 818, \"height\": 685, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long776/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1655, \"height\": 891, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-long/anthology-2026acl-long776/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 829, \"height\": 404, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 779, \"height\": 208, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 843, \"height\": 211, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 838, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1670, \"height\": 981, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1654, \"height\": 882, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 809, \"height\": 596, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 823, \"height\": 747, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 820, \"height\": 1136, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1661, \"height\": 2715, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1719, \"height\": 1730, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1661, \"height\": 1272, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 689, \"height\": 409, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 667, \"height\": 516, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-long/anthology-2026acl-long776/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1680, \"height\": 420, \"label\": \"Table\"}]"
motivation: 法律咨询问答的高质量数据稀缺、任务链条长且强依赖条文语境，给传统法律问答带来困难。
method: 构建JurisCQAD并设计将咨询查询转为法律要素图的结构化分解；提出JurisMA多智能体框架动态调用法条并优化回答。
result: 数据集规模达4.3万真实中文咨询；结合要素图与多智能体框架可在法律咨询问答中发挥效用。
conclusion: 为法律领域可溯源、可分解的问答系统提供了数据与方法支撑。
---

## Abstract
Legal consultation question answering (Legal CQA) presents unique challenges compared to traditional legal QA tasks, including the scarcity of high-quality training data, complex task composition, and strong contextual dependencies. To address these, we construct JurisCQAD, a large-scale dataset of over 43,000 real-world Chinese legal queries annotated with expert-validated positive and negative responses, and design a structured task decomposition that converts each query into a legal element graph integrating entities, events, intents, and legal issues. We further propose JurisMA, a modular multi-agent framework supporting dynamic routing, statutory grounding, and stylistic optimization. Combined with the element graph, the framework enables strong context-aware reasoning, effectively capturing dependencies across legal facts, norms, and procedural logic. Trained on JurisCQAD and evaluated on a refined LawBench, our system significantly outperforms both general-purpose and legal-domain LLMs across multiple lexical and semantic metrics, demonstrating the benefits of interpretable decomposition and modular collaboration in Legal CQA.

---

## 论文详细总结（自动生成）

## 论文总结：From Query to Counsel: Structured Reasoning with a Multi-Agent Framework and Dataset for Legal Consultation

### 1. 核心问题与研究动机

- **核心问题**：法律咨询问答（Legal CQA）不同于传统法律 QA，面对的是真实世界用户的个性化法律困境，需要生成有法律依据、可执行的建议。
- **三大挑战**：
  1. **高质量训练数据稀缺**：真实咨询叙述模糊、非正式，缺乏专家标注数据；
  2. **任务组合复杂**：一次咨询需识别法律关系、因果关系、法律争点并进行条文匹配；
  3. **上下文依赖强**：需要理解实体、关系与用户意图，且法律依据需要动态适配。
- **既有方法的不足**：领域预训练方法监督信号质量低、效果有限；检索增强（retrieve-then-read）只做静态条文级匹配，难以处理多面且具动态法律事实的咨询问题。

### 2. 方法论

#### 核心思想
将法律咨询转化为"结构化图分解 + 多智能体协作推理"的可解释流程，并配套专家校验的正/负样本数据用于偏好对齐训练。

#### 关键技术细节
- **JurisCQAD 数据构建**：由 43,000+ 真实中文咨询构成三元组（q, y⁺, y⁻）；
  - 负样本由 LLM 按受控提示生成"表面合理但含法律瑕疵"的回答，由法律专家审查；
  - 专门控制无效干扰：避免语法错误、明显的法条误拼、荒谬矛盾及刻板印象与编造法条。
- **Phase I——法律要素图（Element Graph）构建**：
  - 类比 Hart 的初级/次级规则与 Kelsen 的规范层级理论；
  - 将查询分解为实体、事件、用户主张、关键事实、法律关系、法律争点等节点/边，模型为 G=(V,E)，以 JSON 序列化后与用户查询拼接进入下游。
- **Phase II——多智能体迭代优化**：Algorithm (简化描述)
  - `DraftAgent` 基于结构化输入生成初稿；
  - `ManagerAgent` 依据"语言清晰度 + 法律完整性（法条引用是否缺失）"动态判断当前草稿是否达标，并路由到相应 Agent：
    - 若格式/表达有问题 → 调 `FormatCheckAgent` 给出修改建议，由 `DraftAgent` 执行；
    - 若法条缺失或不足 → 调 `LawSearchAgent` 检索条文，由 `DraftAgent` 整合；
  - 循环迭代至多 5 轮；若 Manager 判定"Pass"则提前终止。
- **Phase III——内容修订（Content Check）**：在保持法律立场不变的前提下打磨语言，输出双段式结构：面向用户的回复 + 权威法律依据（含条文内容）。
- **DPO 训练目标**：
  - Δθ(x,y⁺,y⁻) = log πθ(y⁺|x) − log πθ(y⁻|x)；
  - Pθ = σ(β·Δθ)；L_DPO = −E[log Pθ]。
  - 用于增强模型区分"法律上正确"与"看似合理但有瑕疵"回答的能力。

### 3. 实验设计

- **评测基准**：对 LawBench 500 测试问题先做人工+LLM 混合修正（340 题存在法律或事实错误），共 500 条问题作为测试集。
- **主要对比基线**：
  - 通用 LLM：GPT-4o、Qwen3-14B、Qwen2.5-14B；
  - 法律领域 LLM：ChatLaw-33B、Fuzi-mingcha、Hanfei、LawGPT、Lawyer-LLaMA、LexiLaw、Wisdom-Interrogatory 等；
  - Agent/检索方法：ReAct、AutoGen-Flat、AutoGen-Tree、MMEP、LexRAG、Parser。
- **数据集有效性实验**：将 JurisCQAD 与 LawGPT 语料对比，在 Qwen2.5-3B/7B/14B 上做 DPO 前后效果对比。
- **跨域泛化实验**（用于检验鲁棒性）：
  - 英文 LEGAL BENCH（RuleQA 子集）；
  - LawBench 2–5 阅读理解任务（交叉任务）；
  - 韩文 KoBLEX（跨语言、跨法域）。
- **消融实验**：移除要素图（KG）、移除 Manager 动态路由、移除 Revision 迭代修改。
- **评价方式及指标**：在 Lexical vs 0.5 之间选择 ROUGE/BLEU；BERTScore/BLEURT；LLM Scoring；**人工评价**（法律稳健性/推理质量/回答完整性）。

### 4. 资源与算力

- 论文明确说明用 HuggingFace + DeepSpeed (Stage 2) 在**至多 2× A100 80GB** GPU 上完成 DPO 训练。
- 配置细节：LoRA（rank=8，α=16），每设备 batch size 8，梯度累积 8（有效 batch size 128）；bf16 混合精度；AdamW、cosine 调度、学习率 1×10⁻⁵、无 warm-up；**训练 3 epochs**，最大序列长度 1024；DPO β=0.1；每 100 步存一次 checkpoint。
- **训练总时长未明确报告**。

### 5. 实验数量与充分性

- **实验数量充足**：主结果、数据集对比（3 种尺寸模型、与 LawGPT 语料对比）、消融研究、人工评估、案例分析、跨基准泛化评估（英文 RuleQA、LawBench 阅读理解、韩国 KoBLEX）。
- **结果总体公平客观**：
  - 零样本设置，统一 prompt 模板，多次随机种子求平均；
  - 对 LawBench 测试集的 340 条问题做了透明化修正并记录；
  - 消融覆盖图构建、Manager 路由、迭代修订三大核心。
- **需注意的问题**：跨域实验样本量较小（如 RuleQA 子集仅 50 条），人工评测细节（评分人数、评分者间信度）未充分披露。

### 6. 主要结论与发现

- **JURISMA 全面超过通用和法律领域大模型**：在 ROUGE、BLEU-2/N、BERTScore、GPT-4o LLM-Score上均取得最优，BLEURT 上第二；且差异在统计上显著（p < 0.05）。
- **数据集有效性**：在 Qwen2.5-3B/7B/14B 上使用 JurisCQAD 做 DPO 均带来一致提升；用 LawGPT 语料微调反而下降，说明该数据在更新性、去噪与标注质量上更好。
- **消融结论**：
  - 迭代修改（Revision）影响语义质量最大（BERTScore 最多下降 5.49 分），说明多轮修订能提升流畅性和法律清晰度；
  - Manager 协调有利于一致性、要素图有利于法律事实落地。
- **泛化能力**：在跨语言、跨任务、跨法域的三类基准中均体现较好迁移性，表明结构化要素分解 + 多智能体协作带来的收益并不局限于训练分布。
- **案例分析**：在"2011 年醉酒驾驶是否影响孩子就读军校"等时间敏感问题上，JURISMA 能正确援引《刑法》第 133-1 条并运用"不溯及既往"原则；对照模型易啰嗦或漏引最相关条文。

### 7. 优点

- **数据集设计亮点**：来源真实论坛，专家纠正和校验负样本；法律条文更新至 2021民法典之后；兼具对比式监督与开放性。
- **结构化可解释**：要素图使多步推理中的法律实体、意图、关键事实显式可见，并支持人为干预。
- **模块化 Agent 设计**：Manager 动态路由做到"按需激活"，避免僵化流水线，同时支持 LawSearch 的动态法条同步与 FormatCheck 润色，便于扩展。
- **对齐策略稳健**：强调"细微但关键"的法律瑕疵构造，避免语法低劣或明显荒谬，训练出的模型更有分辨能力。
- **评价较为全面**：在词面匹配之外加入语义指标、LLM 与人工评审判定，并做了泛化和消融分析。

### 8. 不足与局限

- **法律与计算策略的成本**：多 Agent 架构增加推理时间，不利于实时部署。
- **数据覆盖有偏风险**：语料向高频咨询场景倾斜，对罕见或高度专业领域泛化有限，存在潜在的偏差。
- **缺乏长期可用性论证**：人类评估规模受限，仍未覆盖真实业务中的长期可靠性、反馈闭环及伦理压力测试。
- **跨域实验规模相对有限**：如英文 RuleQA 仅为 50 条样本的小验证。
- **生成与测试集规模细节略少**：具体测试子集数量和领域分布报告不够细致。

（完）
