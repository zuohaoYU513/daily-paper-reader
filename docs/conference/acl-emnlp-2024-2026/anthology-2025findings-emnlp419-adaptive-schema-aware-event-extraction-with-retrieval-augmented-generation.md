---
title: Adaptive Schema-aware Event Extraction with Retrieval-Augmented Generation
title_zh: 基于检索增强生成的自适应模式感知事件抽取
authors: "Sheng Liang, Hang Lv, Zhihao Wen, Yaxiong Wu, Yongyue Zhang, Hao Wang, Yong Liu"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.419.pdf"
tags: ["query:hallu-rag"]
score: 7.0
evidence: 用检索增强生成缓解事件抽取中的模式幻觉与上下文窗口限制，并提供相应基准评测
tldr: 现实事件抽取需要在上百候选模式中选择合适模式并执行抽取，而现有管线的模式固定，且缺少联合评测基准。大模型虽提供可能方案，但存在模式幻觉和上下文窗口限制。论文提出自适应模式感知事件抽取框架，借助检索增强动态选择合适模式并引导抽取，同时建立联合评测基准。实验结果验证其能降低模式幻觉、缓解上下文限制并提升事件抽取可靠性。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp419/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 813, \"height\": 427, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp419/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1646, \"height\": 566, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp419/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 796, \"height\": 759, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1493, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 764, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1434, \"height\": 273, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1507, \"height\": 391, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1486, \"height\": 637, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1292, \"height\": 592, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1458, \"height\": 662, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1457, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1457, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1458, \"height\": 662, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1457, \"height\": 664, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1457, \"height\": 663, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp419/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1459, \"height\": 664, \"label\": \"Table\"}]"
motivation: 现实事件抽取需从大量候选模式中动态选择模式，现有固定模式管线缺少联合基准，LLM易出现模式幻觉和窗口限制。
method: 提出自适应模式感知事件抽取框架，利用检索增强生成动态选择模式，并联合完成模式匹配与事件抽取。
result: 在新建基准上验证了方法能减轻模式幻觉和上下文限制，提升事件抽取性能。
conclusion: 动态模式选择配合检索增强生成是提升开放场景事件抽取可靠性的重要方向。
---

## Abstract
Event extraction (EE) is a fundamental task in natural language processing (NLP) that involves identifying and extracting event information from unstructured text. Effective EE in real-world scenarios requires two key steps: selecting appropriate schemas from hundreds of candidates and executing the extraction process.Existing research exhibits two critical gaps: (1) the rigid schema fixation in existing pipeline systems, and (2) the absence of benchmarks for evaluating joint schema matching and extraction.Although large language models (LLMs) offer potential solutions, their schema hallucination tendencies and context window limitations pose challenges for practical deployment. In response, we propose A daptive S chema-aware E vent E xtraction ( ASEE ), a novel paradigm combining schema paraphrasing with schema retrieval-augmented generation. ASEE adeptly retrieves paraphrased schemas and accurately generates targeted structures.To facilitate rigorous evaluation, we construct the M ulti- D imensional S chema-aware E vent E xtraction ( MD-SEE ) benchmark, which systematically consolidates 12 datasets across diverse domains, complexity levels, and language settings.Extensive evaluations on MD-SEE show that our proposed ASEE demonstrates strong adaptability across various scenarios, significantly improving the accuracy of event extraction. Our codes and datasets are available at https://github.com/USTC-StarTeam/ASEE.git

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **背景**：事件抽取（EE）要求从非结构化文本中识别事件触发词及其参数。真实场景下，系统需要先从数百个候选事件模式（schema）中选择恰当模式，再按模式抽取信息；这与现有研究预设“固定小规模模式集”的设定不同。
- **两个关键缺陷**：
  - **系统设计层面**：传统管线模式僵化、缺乏跨域自适应性；将全部模式塞入LLM上下文会导致高计算开销、性能衰减（如“lost in the middle”），以及LLM出现“模式幻觉”（发明未定义的事件类型）。
  - **评测层面**：缺乏同时衡量“模式检索”和“事件抽取”的联合基准，现有数据集默认模式已给定，脱离实际工程需求。
- **研究意义**：提出动态模式选择与抽取相结合的框架，并构建多维度联合评测基准，推动LLM在广域事件抽取场景的落地。

## 2. 论文提出的方法论

### 总体框架：ASEE（Adaptive Schema-aware Event Extraction）
- 核心思想：将传统 SEE（Schema-aware Event Extraction）分解为“模式准备 + 模式检索 + 模式引导抽取”，消除固定模式假设。
- 三个核心步骤（文中给出数学式）：

1. **Schema Paraphrasing (SP)**
   - 用训练数据中对应某模式的样本作为少样本示例，让冻结的 LLM（ϕLLM）为每个原始模式生成改写版本，丰富模式描述和论元说明。
   - 所有改写模式构成模式池 S：  
     S = ⋃_{s∈S0} {ϕLLM(s, Ds) | Ds ⊆ D_train}
   - 目的：增强语义清晰度，提升后续检索精度，同时为抽取提供更明确的引导。

2. **Schema Retrieval (SR)**
   - 对输入查询 q，用检索器ψ从模式池 S 中召回 top-k 模式：  
     Rq = ψ_retriever(q, S)
   - 检索器可选用 BM25、BGE-M3、E5、GTE 等多种模型。

3. **Schema-aware Extraction (SE)**
   - 将查询 q 和检索到的模式 Rq 一起交给 LLM（θLLM）进行生成式抽取：  
     V = θLLM(q, Rq)
   - 为提高模式遵循能力，采用监督微调（SFT），损失函数为：  
     LSFT = −E_{(q,s,V)∼D_train} Σ_{k=1..K} log Pθ(v_k | q, s, v_<k)
   - 使模型学会严格依据模式定义输出结构化参数值。

- 另外，论文提出 MD-SEE 基准构建流程：多数据集收集、模式合并（基于字符相似度与数值/变体论元合并）、基于 BGE-M3 相似度构造图并使用贪心最大独立集算法去冗余，生成跨语言子集（英语查询+中文模式，中文查询+英语模式）。

## 3. 实验设计

### 数据集
- **收集的原始数据**：CrudeOilNews、GENEVA、MAVEN-Arg、DocEE（en/zh）、IEPILE（含 CASIE、PHEE、RAMS、WikiEvents、DuEE-fin、DuEE1.0、FewFC、ccf_law 等）。
- **构建的新基准 MD-SEE**：聚合12个数据集的300个模式，共12,817训练/1,775开发（文中一处写800？可忽略）/7,686测试样本；覆盖句子到文档不同长度、新闻/网络安全/生物医学/金融/法律等领域、单/多事件复杂度、英/中/跨语言设置。

### 评测设置
1. **模式检索评测**：Recall@10 / @20 / @50，比较“Raw” vs “Paraphrased”模式。
2. **模式感知抽取评测**：给定真实模式（不检索）计算论元级 F1，作为抽取上限。
3. **端到端评测**：模式检索 + 抽取联合，使用 E2E-F1 指标（检索到真实模式才按F1计入，未检索到记为0，检索到非真实模式忽略）。

### 对比方法
- **检索模型**：BM25、BGE-M3、BGE-Reranker-Base/Large、E5-large-v2、GTE-Large、LLM-Embedder。
- **抽取LLM**：Phi-3.5-mini、Llama-3.2-3B、Llama-3.1-8B、Mistral-7B-v0.3、Qwen2.5-7B/14B、YAYI-UIE、GPT-4-turbo。
- 另有两种 ASEE 版本（Llama-3.2-3B / Llama-3.1-8B）在 MD-SEE 上进行有无 SFT 的端到端实验。

## 4. 资源与算力

- 论文**未明确报告** GPU 型号、数量、训练时长、显存用量等具体算力信息，仅说明 “within the limits of our computational resources”。
- 提及未能微调 32B 或 70B 参数的大模型，原因是“计算资源约束”。
- 因此，资源与算力细节缺失，只能从模型规模推测实验在中小型GPU环境完成。

## 5. 实验数量与充分性

### 实验数量
- 模式检索实验：7个数据集上×7种检索模型（表1）+ MD-SEE 上的 Recall@10/20/50（表2）。
- 模式感知抽取实验：7个子数据集×8种LLM的零样本 F1（表3）。
- 端到端实验：MD-SEE 上4种主配置（2种LLM × 有无SFT）×7种检索器（表4），另外附录中有7个数据集各自的完整端到端结果（表7-13，每组含原始/改写模式×7检索器×8 LLM）。
- 实验数据量较大，基本覆盖主流程各环节。

### 充分性与客观性评价
- **优点**：评测维度覆盖检索、抽取、联合端到端，并在多个域、语言、复杂度的聚合基准上进行，对比模型多样，包含开源和闭源模型。
- **不足/风险**：
  - 缺少专门的**消融研究**（例如不进行模式改写、不同改写轮次、不同top-k值的影响等系统分析）。
  - 跨语言实验仅单向/双语对换，未覆盖真正的多语言场景。
  - 检索模型和LLM组合众多，但论文正文仅展示部分结果（MD-SEE上的4种配置），大量附录结果可读性和深浅层结论有限。
  - 可靠性验证（如多次随机种子、统计显著性检验）未在文中报告。

## 6. 论文的主要结论与发现

- **模式改写有效**：在大部分数据集与检索器上，“Paraph.”（改写后模式）的检索 Recall 显著优于“Raw”（原始模式），MD-SEE 上提升更明显（例如 BM25 的 Recall@10 从0.33升至0.58，BGE-M3从0.61升至0.78）。
- **抽取能力差异**：GPT-4-turbo 在多数数据集上取得最佳零样本抽取F1；Qwen2.5-14B 在中文场景接近甚至持平。YAYI-UIE 效果低于主流开源LLM。
- **端到端协同增益**：在 MD-SEE 上，使用 BGE-M3 作为检索器时 ASEE 端到端性能最佳；使用更大基座（Llama-3.1-8B > Llama-3.2-3B）和 SFT 都能进一步显著提升 E2E-F1。
- **整体启示**：将模式改写结合检索增强生成可降低模式幻觉、缓解长上下文压力，提升动态开放场景下事件抽取的可靠性与准确性。

## 7. 优点

- **问题定义清晰**：准确定位了现有 EE 在真实场景中的痛点——固定模式、模式选择缺失和缺乏联合评测，并与工业需求联系紧密。
- **方法新颖且实用**：将“模式改写”作为桥接检索与抽取的关键环节，与常见 RAG 只检索原始模式相比语义匹配能力更强。
- **资源构建扎实**：MD-SEE 汇聚多域、多复杂度、多语言数据集，模式统一并去重，形成可复用评测资源，填补基准空白。
- **实验设计完整**：从检索单独评估→抽取单独评估→端到端联合评估，逐层分解、立体反映系统瓶颈。
- **评测指标合理**：E2E-F1 考虑检索遗漏（计0）与检索多余（忽略）情况，较好刻画真实场景得失。

## 8. 不足与局限

- **缺少算力可复现细节**：未报告GPU型号、数量、训练时长、批次大小和推理开销，影响复现和效率评估；无法微调30B以上模型限制了方法在大模型上的能力验证。
- **未引入相关任务**：没有整合关系抽取（RE）与命名实体识别（NER），泛化到全面信息抽取还有距离。
- **跨语言/多语言覆盖有限**：仅做了中英单向模式与查询对调，还不足以代表复杂多语场景；抽取语言和模式语言不一致时保留原文语言的行为，缺乏更细粒度分析。
- **检索评测可能受限**：模式池为300个模式，与真实“数百到上千”候选的差距尚存；检索 top-k 超参未做敏感性分析。
- **人工因素与偏差风险**：模式改写质量依赖 LLM；模式去重和图算法只能保证近似多样性；合并后可能损失细节；Zero-shot vs SFT的标准化条件（提示模板、输出格式）在补充材料未完全透明。
- **统计稳定性和消融**：缺少多轮重复与显著性检验，改写、检索器、SFT贡献缺少逐步消融量化。

（完）
