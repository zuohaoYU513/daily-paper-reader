---
title: "AQuAECHR: Attributed Question Answering for European Court of Human Rights"
title_zh: AQuAECHR：面向欧洲人权法院的归因问答
authors: "Korbinian Q. Weidinger, Santosh T.Y.S.S, Oana Ichim, Matthias Grabmair"
date: 2025-07-01
pdf: "https://aclanthology.org/2025.findings-acl.74.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 面向欧洲人权法院的归因问答基准，将答案关联到作为证据的判决
tldr: 该工作提出AQuAECHR基准，面向欧洲人权法院判例法中的信息型问题，将每个问题关联到可作为证据的相关判决，从而实现带归因的法律问答。作者给出了自动数据策展策略来构建该资源，以缓解大模型法律回答中的幻觉并增强事实可核查性。该基准为高利害法律场景下的证据问答和输出溯源提供了评测阵地，也示范了如何自动构造此类数据。
source: ACL-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl74/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1331, \"height\": 1649, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2025-findings/anthology-2025findings-acl74/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1324, \"height\": 1139, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 649, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1447, \"height\": 377, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1668, \"height\": 914, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 942, \"height\": 291, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 503, \"height\": 302, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 776, \"height\": 274, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1677, \"height\": 575, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1671, \"height\": 1004, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1665, \"height\": 1522, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1670, \"height\": 855, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1558, \"height\": 2411, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1490, \"height\": 2288, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1648, \"height\": 837, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1643, \"height\": 1171, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2025-findings/anthology-2025findings-acl74/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1647, \"height\": 975, \"label\": \"Table\"}]"
motivation: 法律问答中LLM回答常产生幻觉，缺少对真实源判决的归因，难以支持高利害场景使用。
method: 基于ECHR判例，用自动策展方法构造问题-判决归因对，形成带证据的法律问答基准。
result: 构建AQuAECHR基准并提供可溯源线索，使法律问答可在判决原文上验证。
conclusion: 归因是提升法律QA事实性与可核查性的关键，AQuAECHR为后续研究提供评测基础。
---

## Abstract
LLMs have become prevalent tools for information seeking across various fields, including law. However, their generated responses often suffer from hallucinations, hindering their widespread adoption in high stakes domains such as law, which can potentially mislead experts and propagate societal harms. To enhance trustworthiness in these systems, one promising approach is to attribute the answer to an actual source, thereby improving the factuality and verifiability of the response. In pursuit of advancing attributed legal question answering, we introduce AQuAECHR, a benchmark comprising information-seeking questions from ECHR jurisprudence along with attributions to relevant judgments. We present strategies to automatically curate this dataset from ECHR case law guides and utilize an LLM-based filtering pipeline to improve dataset quality, as validated by legal experts. Additionally, we assess several LLMs, including those trained on legal corpora, on this dataset to underscore significant challenges with the current models and strategies dealing with attributed QA, both quantitatively and qualitatively.

---

## 论文详细总结（自动生成）

# AQuAECHR 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有 LLM 在法律信息检索与问答中存在严重的幻觉问题，回答常与现行判例法和法理不一致，可能误导专家并造成社会危害。若让模型给出可溯源至真实判决的归因（attribution），则可增强回答的事实性与可验证性，促进高利害法律场景下 LLM 的可信部署。

- **背景**：
  - 已有新闻事件显示律师依赖 ChatGPT 做法律研究后提交了含有虚构判例的法庭文件，凸显幻觉风险。
  - 法律与一般领域（如科学、医学）不同，法律具有管辖权特异性：不同法域的标准和结构差异很大（如 EXPERTQA 中的法律问题多基于美国管辖权），需要专门构建针对特定法域的高质量归因问答基准。
  - 现有归因问答数据集（如 ASQA、QAMPARI、ELI5、HAGRID 等）主要面向网页等一般非结构化文档或知识库，缺乏法律领域的带金标引用的问答对。

- **研究目标**：构建 AQuAECHR 基准，涵盖欧洲人权法院（ECHR）判例法中的寻证型问题与对应判决归因，系统评估现有 LLM（包括法律预训练模型）在带归因的法律问答上的表现。

## 2. 论文提出的方法论：核心思想、关键技术细节、算法流程

### 2.1 任务定义
- 输入为法律问题 q 和从 ECHR 判决中提取的文本段落库 D；系统需生成包含 n 个句子的回答 t = {t₁, …, tₙ}，且每个陈述 tᵢ 后接文内引用 Cᵢ = {cᵢ,₁, cᵢ,₂, …}，其中每个 cᵢ,ⱼ ∈ D。

### 2.2 数据策展（Data Curation）
数据来源：ECHR 判例法指南（Case-Law Guides），涵盖 28 个条文类指南与 8 个专题类指南。这些指南讨论各公约条文下法律概念，并提供指向 ECHR 判决段落级引用的精确标注。

QA 对构建流程分为三个阶段：

1. **问题生成**：利用 GPT-3.5-turbo-16k-0301，依据按顺序选取的多个指南段落生成可被这些段落回答的问题。提示词由 ECHR 法律专家协作设计，明确引导模型避免提及具体案件名，强调将事实模式与特定法律原则（doctrines）相匹配，构建通用信息查询场景。论文加入法律专家定义的外部推理路径（Legal-1、Legal-2），指导 LLM 分析国家裁量余地、积极义务、必要性理由、权利有效性与合理措施等要素。
2. **语义相似度搜索以补全信息**：用 `text-embedding-3-small` 将生成的问题嵌入并与指南中全部段落进行语义检索，找出讨论同一信息点但不在原始序列中的其余段落，取 top-k 与原始种子段落一起作为候选集合，确保答案全面性（comprehensiveness）。
3. **句子级答案抽取**：指示 GPT-3.5 从上述多段落的句子中抽取与该问题相关的句子作为答案（而非让模型重新生成摘要答案），避免生成式改写引入不忠实信息；同时移除无关内容以保证简洁性。

### 2.3 判例段落语料采集
- 从 ECHR 官方数据库 HUDOC 获取 HTML 格式判决全文，保留英文文档；通过手写启发式规则解析段落边界，处理不统一 HTML 结构、子段落编号干扰和跨引用引入的虚假段落编号问题。

### 2.4 自动过滤策略（G-EVAL）
- 参照 G-EVAL 框架，用 GPT-3.5 作为无所参考答案的评估器，按流畅度、全面性、间接性三项对 QA 对打分，得分 ≤3 判定为低质量。
- 经与专家标注的 300 对数据验证：整体 F1 = 63.38；维度层面，Fluency 的 F1 最高（96.9），Conciseness 最具主观挑战性（F1 = 77.7）。
- 实际使用：对每条生成数据依次用 Legal-2、Legal-1、CoT 策略变体重试，直至获得高质量；随后基于 embedding 余弦相似度阈值 0.8 去除重复问题；最后剔除引用无段落号或引用非英文判决的对。

### 2.5 最终数据集规模
- 1116 对 QA；答案平均 295 tokens、约 5 句；平均引用 7.8 个判决段落；问题平均 49 tokens。

## 3. 实验设计

### 3.1 基准与数据集
- 任务所用语料库：基于上述 AQuAECHR 数据集（1116 对 QA），以 ECHR 判例段落作为引用文档库。
- 用 AQuAECHR 目标回答与法律专家标注，综合多种自动化指标衡量生成回答质量与引用质量。

### 3.2 对比模型
- Mistral-7B-instruct
- SaulLM-7B-instruct（初创于 Mistral-7B 并在英文法律语料上继续训练后进行指令微调）
- Llama-3-8B-instruct
- Llama-3-70B-instruct
- 检索器：GTR（T5-XXL 初始化）。

### 3.3 对比方法（Attributed QA 策略）
1. **Closed-book + Posthoc - vanilla**：模型直接闭卷生成回答，事后为每个句子检索最优段落作为引用。
2. **Post-hoc Retrieval - RARR**：闭卷生成后对每个句子判断是否需要证据，检索证据并基于"研究后修订"方式编辑回答以与证据一致。
3. **Retrieve-then-Generate - vanilla**：先按问题检索 top-k 段落，将检索结果连同问题一起提供给 LLM，生成带引用的回答。
4. **Retrieve-then-Generate - LLatrieval**：LLM 迭代式反馈缺失信息并重新检索文档，评估+选择检索到的文档后最终生成带引用的回答。

### 3.4 自动评估指标（四维）
- **Answer Fluency**：MAUVE。
- **Answer Correctness**：ROUGE-L F1、BERTScore、基于 TrueTeacher（T5-11B NLI）的句子级声明召回（判断目标回答的每条声明是否被生成回答蕴含）。
- **Citation Faithfulness**（文本-引用对齐）：对带引用的生成句子进行 NLI（TrueTeacher），判断被引段落是否能蕴含该句子，报告声明级召回。
- **Evidence Similarity / Citation Quality**：与参考回答中的引用比较，用 Exact Match F1 以及 NLI 语义匹配（逐参考引用块检查是否被生成引用蕴含）。

### 3.5 人类评估
- 从 Mistral-7B 的输出中随机抽 20 个问题 × 4 种方法 = 80 条回答，由 ECHR 法律专家围绕三个标准打分排名：答案正确性（与目标答案接近程度）、生成文本对引用的忠实程度、证据质量；最后评估自动指标排名结果与专家排名的 Spearman 相关性。

## 4. 资源与算力

- 论文原文中未明确提及受测 LLM 推理所使用 GPU 型号、数量或总体算力消耗，也没有报告数据策展时调用 GPT-3.5 / embedding 接口的调用体量或费用。只提到了所测试的模型规格（Mistral-7B、Saul-7B、Llama-3-8B、Llama-3-70B）以及使用 NLI 模型 TrueTeacher（T5-11B）进行评估等细节。

## 5. 实验数量与充分性

可以从几个角度评估实验的覆盖度和充分性：

- **数据集质量验证**：
  - 对 300 个人工专家标注 QA 对进行质量评估（覆盖 4 种策略变体 + 法律推理路径 2 个变体）。
  - 对 300 个标注数据进行了 G-EVAL 自动打分可靠性验证（混淆矩阵 + F1，覆盖 Fluency/Comprehensiveness/Conciseness/Overall 四类）。
  - 最终数据集统计分布、重复过滤和引用质量审查。
- **策略与方法评测**：4 个模型 × 4 种主流归因生成策略（闭卷+事后检索 vanilla、闭卷+事后检索 RARR、检索增强生成 vanilla、检索增强生成 LLatrieval），自动化指标含流畅度、答案正确性、引用忠实度、证据相似度。
  - 观察到多种内在矛盾/差异（模型 x 方法）：如 SaulLM 在 Posthoc 方法 MAUVE 高但 RAG 方法不如其他模型；不同模型在 LLatrieval 方法下往往有不同表现（例如改进 Mistral-70B 却降低 Llama-8B）。
  - 个案分析（Example 1/2/3）深入讨论不同模型生成回答相对于参考答案在法律专家眼中的适用性、完整性等差异。
- **有效性度量的相关性检验**：用小型人工排名（80 个回答）检验自动度量的有效性：指标大多数与专家排名的相关性——NLI 类方法（Citation Faithfulness Recall：0.45；Evidence NLI Similarity：0.52）与专家正相关较强且显著，BERTScore 正相关较弱（0.33）；词面 ROUGE-L 几乎无相关。
- **局限**：人工评价只有一位法律专家标注，且标注样本量相对较少（300 QA 质量 + 80 回答排名），无法独立分析专家间分歧或进行统计稳健性验证；在完整 AQuAECHR 数据只跑 4 种方法来对比，缺失一些消融（例如不同文档数 k 的影响、不同检索器影响），因此实验覆盖相对有限。

总体结论：论文做了一定量的自动与人工实验，确保了基本合理性；但由于高额人工专家成本，实验规模有限、缺少大规模人工评估集、缺少多样化模型与检索器，因此严格来说不算全面、也不能完全排除测试偏差。

## 6. 论文的主要结论与发现

- **闭卷回答 + 事后检索方法的缺陷**：
  - 仅靠闭卷知识生成的回答没有针对句子检索到合适的上下文，因此所产生的引用数量较少、往往不对应真实文本，证据质量和引用忠实度均偏低；即使使用 RARR 对回答进行编辑，也只是小幅提升（主要靠增加引用的数量）而不能真正提高忠实度。原因是 LLM 本身"同意确认偏见"使模型很少认为自身回答有问题，编辑率极低（Llama-3-8B 最高，也仅编辑 3.23% 的句子）。
- **检索增强生成（RAG）的相对优势**：
  - Retrieve-then-Generate（含 LLatrieval）具有更强的归纳偏置，更忠实于检索到的文档，因而引用忠实度显著高于 post-hoc 方法。
  - LLatrieval 的自我反馈/再检索思路对某些模型（如 Mistral-7B、Llama-3-70B）能提升证据质量和引用效果，但会导致另一些模型（SaulLM、Llama-3-8B）性能下降——这些模型在提出缺失信息查询时表现不佳。
- **法律预训练模型（SaulLM）的"过拟合"**：
  - SaulLM 在法律语料上的预训练在表层生成更接近"法言法语"（获得较高的 MAUVE，闭卷时 ROUGE 更高），但它出现了能力遗忘（catastrophic forgetting）——指令跟随能力相对基础 Mistral 下降，在检索增强场景中较少使用/引用给定文档、对引用忠实度和证据涵盖度造成明显下降（Citation Faithfulness 远低于同类模型，如 vanilla RAG 中只有 14.6，而 Mistral 为 54.2）。
- **自动评价与专家评价的差异**：
  - 法律专家更看重精确引用与引用权威性、上下文含义；自动化 NLI 类指标对证据级排名有较好指示性，但对答案正确性（尤其是复杂语义关系）与专家判断的关联仍偏弱。
- **整体**：当前模型与策略在长篇幅性法律归因问答上仍面临较大挑战，包括语义歧义性检索难、LLM 准确识别支持证据难、领域微调可能损害通用指令能力等问题。

## 7. 优点（方法或实验设计上的亮点）

- **数据构建流程的高可扩展性与可控成本**：与以往必须雇佣大量法律专家人工撰写问答不同，本方法利用法学专家协同设计推理结构提示词将 ECHR 判决指南段落自动转化为检索型问题-证据对，并利用语义检索辅助全面性、句子抽取提升简洁性。整个过程只需一位法学专家审核反馈，大幅降低高质量法律 QA 数据集构建门槛，未来可推广到其他法域与法律文本来源。
- **引用与陈述逐句映射的数据结构设计**：采用"陈述级内联引用"的输出形式，便于做细粒度自动评估（引用忠实度、声明蕴含、证据检索 质量），也便于用户核查具体判例句；把答案作为 extractive 句子（而非由 LLM rephrase 的摘要答案）来降低幻觉风险的思路很务实。
- **质量监督与筛选**：将 LLM-as-a-judge（类 G-EVAL）用于数据集质量过滤，并严谨地用 300 个专家标注样本对其检测能力进行验证；最后在数据集中还融入专家设计的法律推理路径和迭代（n-1）补救过程，确保当前公共数据的高质量问题率已大幅降低。
- **评估体系较全面**：从流畅度、正确性、引用忠实度、证据相似度四个维度综合自动评测；补充 80 条人类专家排名以及相关度系数（Spearman）检验自动评估的可靠性，还有定性的案例分析与 RARR 编辑率统计，让读者可以较清楚看到各方法与指标的实际表现和差距。
- **发现的领域独特洞察**：发现领域 SOTA（如 SaulLM）在单一法律语料上预训练反而会恶化下游指令和引用能力——对当前“法律大模型定制的技术路线工业界有干预性警示。

## 8. 不足与局限

- **语言与法域扩展性**：AQuAECHR 全部基于英文与 ECHR 判例，且只包含英语和官方语言中的英语文档，无法覆盖法国及其他 ECHR/官方语言内容，也不能直接作为其他法域（如普通法系等）归因问答评测标准。
- **标注主体不足**：人评严重依赖个别法律专家，而法律判断具有较强主观性，在引用质量、权威性评等方面比较容易受个体经验影响（没有评估者间一致性检验），可能造成系统偏差。
- **LLM 生成问题的质量问题**：虽然经过质量筛选，整个流程仍依赖 GPT-3.5 根据判例指南自动生成提问，不能完全排除生成问题在使用性和信息焦点上与真实法律专业人员的查询意图不一致的风险；研究仅从专家主观分数间接验证了它“相对好”，没有大规模全维度验证。
- **评估偏重自动化 NLI 的方法**：NLI 模型要求一个论断所有陈述需逐项蕴含来源，而法律专家往往使用背景知识和更宽范围内的推理。所以自动指标往往偏严格（低分），无法捕捉权威性、区分观点主体（Court vs. 申请人）和“为何反驳”之类语义；行文从头到尾都用非常细粒度的句子级蕴含来控制，往往忽略整段上下文。
- **基准问题可能存在引用偏倚**：参考回答来自判例指南，指南选案例有自身的选择性偏见；虽然结果里补充 NLI 语义对比减轻了部分，但不能彻底解决同一问题上不同判例交叉引用导致的引用策略差异（不同“正确引用”的存在）。
- **检索器与方法的评估覆盖有限**：只采用 GTR 单一检索器；未对比不同检索模型在归因质量中的影响，也没有注明 k 的取值与灵敏分析，后续应在更大范围内做消融（包括证据抽取数量、句合并策略等参数）。
- **RARR 有效性不足和改进困难的分析细致度有限**：虽然没有明确说明“哪些指令模板下模型同意确认偏置能够被缓解”，研究也停留在观察层，没有给出如何克服这一方法论障碍的具体建议。
- **数据集规模偏小**：最后仅 1116 对，测试LLM时采用生成式长答案模式、每问引用数目不多，相对高方差、稳健性风险较大。

（完）
