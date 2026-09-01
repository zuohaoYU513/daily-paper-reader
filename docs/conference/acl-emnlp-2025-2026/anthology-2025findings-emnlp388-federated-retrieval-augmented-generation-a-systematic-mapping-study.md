---
title: "Federated Retrieval-Augmented Generation: A Systematic Mapping Study"
title_zh: 联邦检索增强生成：系统映射研究
authors: "Abhijit Chakraborty, Chahana Dahal, Vivek Gupta"
date: 2025-11-01
pdf: "https://aclanthology.org/2025.findings-emnlp.388.pdf"
tags: ["query:hallu-rag"]
score: 8.0
evidence: 联合检索增强生成的系统综述，聚焦通过外部知识增强事实准确性
tldr: 检索增强生成通过在外部知识中锚定输出可以提升事实准确性，但隐私敏感场景需要联邦学习来保护数据。该综述首次对联邦检索增强生成(Federated RAG)进行系统映射，覆盖2020至2025年文献，梳理了结合联邦学习与RAG的框架设计。研究显示该范式在医疗、金融等领域有广阔前景，并为后续研究提供了结构化分类。
source: EMNLP-2025-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp388/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1659, \"height\": 199, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp388/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1651, \"height\": 1183, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp388/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 682, \"height\": 726, \"label\": \"Figure\"}, {\"url\": \"assets/figures/emnlp-2025-findings/anthology-2025findings-emnlp388/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 789, \"height\": 480, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp388/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 664, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp388/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 600, \"height\": 250, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp388/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 636, \"height\": 286, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp388/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 744, \"height\": 551, \"label\": \"Table\"}, {\"url\": \"assets/tables/emnlp-2025-findings/anthology-2025findings-emnlp388/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1526, \"height\": 1636, \"label\": \"Table\"}]"
motivation: 隐私敏感场景需要在不暴露原始数据的前提下实现基于外部知识的知识密集型NLP。
method: 采用Kitchenham指南对2020-2025年联邦RAG文献进行系统映射与分类。
result: 给出了联邦RAG的研究现状与分类框架，指出未来方向。
conclusion: 联邦RAG是保障隐私的知识增强生成重要方向，该综述为此领域奠基。
---

## Abstract
Federated Retrieval-Augmented Generation (Federated RAG) combines Federated Learning (FL),which enables distributed model training without exposing raw data, with Retrieval-Augmented Generation (RAG), which improves the factual accuracy of language models by grounding outputs in external knowledge. As large language models are increasingly deployed in privacy-sensitive domains such as healthcare, finance, and personalized assistance, Federated RAG offers a promising framework for secure, knowledge-intensive natural language processing (NLP). To the best of our knowledge, this paper presents the first systematic mapping study of Federated RAG, covering literature published between 2020 and 2025. Following Kitchenham’s guidelines for evidence-based software engineering, we develop a structured classification of research focuses, contribution types, and application domains. We analyze architectural patterns, temporal trends, and key challenges, including privacy-preserving retrieval, cross-client heterogeneity, and evaluation limitations. Our findings synthesize a rapidly evolving body of research, identify recurring design patterns, and surface open questions, providing a foundation for future work at the intersection of RAG and federated systems.

---

## 论文详细总结（自动生成）

# 联邦检索增强生成：系统映射研究（Federated RAG: A Systematic Mapping Study）

## 1. 论文的核心问题与整体含义

**研究动机与背景：**
- 大型语言模型（LLM）在医疗、金融、个性化助手等隐私敏感领域的部署日益广泛，引发了对数据隐私、所有权和合规性的担忧。
- **联邦学习（FL）** 允许跨分布式客户端训练模型而不交换原始数据；**检索增强生成（RAG）** 通过外部知识库检索为模型输出提供事实支撑、减少幻觉。
- 两个范式的交叉——**联邦检索增强生成（Federated RAG）**——使 LLM 能以隐私保护方式访问分布式知识源，兼具数据本地化、个性化检索和上下文感知生成的优势。
- 该方向此前缺乏系统性的文献梳理与分类框架，本文是**首次**对 Federated RAG 领域进行系统映射研究。

## 2. 论文提出的方法论

**核心方法：遵循 Kitchenham 的证据导向软件工程系统映射指南，对 2020–2025 年文献进行结构化分类分析。**

**关键技术细节与流程：**
- **文献检索**：在 NLP、ML 和安全领域顶级会议中检索“federated learning”“retrieval-augmented generation”“federated search”等关键词，并从 50 篇候选中筛选出 18 篇符合纳入标准的研究。
- **文献编码**：每篇文献按三个维度编码——(a) 研究焦点、(b) 贡献类型、(c) 应用领域，并记录发表年份以观察时间趋势。
- **分类体系构建**：建立了统一分类方案（图 1）和架构分类法（图 2），覆盖联邦检索（朴素聚合、选择性查询路由、安全索引与查询）与联邦生成（集中式、客户端特定、混合/集成式）。
- **统一目标函数**：提出概念性的 Federated RAG 联合优化目标：

  \[
  L_{FedRAG}(\theta) = \sum_{i=1}^{M} \frac{n_i}{N} \left( L^{(i)}_{retrieve}(\theta_r) + L^{(i)}_{generate}(\theta_r, \theta_g) \right)
  \]

  其中 \( M \) 为客户端数，\( n_i \) 为客户端 i 的样本数，\( N \) 为总样本数，\( \theta_r \) 为检索器参数，\( \theta_g \) 为生成器参数——体现检索与生成可在联邦设置中联合优化。

## 3. 实验设计

**说明：本文是系统映射研究（综述），而非提出新方法的实验论文。**

**研究对象 / 语料：**
- 覆盖 2020–2025 年发表的 50 篇候选论文，最终纳入 18 篇主要研究。
- 研究对象来自 NLP、信息检索（IR）、机器学习（ML）和安全领域的主流会议。

**相关 Benchmark 与数据集（文中提及）：**
- **FeB4RAG**：覆盖 16 个 BEIR 派生领域的联邦检索基准。
- **MIRAGE**：面向联邦临床 QA 的医学基准。
- **MKP-QA**：跨语种企业多产品问答基准。
- **RAGAS**：联邦 RAG 评估工具包。

**对比方式：**
- 基于表 5 的 18 篇研究综合对比，比较各系统报告的收益指标（如准确率提升、延迟、隐私保证）。
- 按研究焦点、贡献类型、应用领域三个维度进行分类与频次统计。

## 4. 资源与算力

- **论文未明确报告任何 GPU 型号、数量、训练时长或计算资源消耗。**
- 作为文献综述类论文，文中未包含原始训练实验，因此没有可直接引用的算力信息。
- 仅部分被综述的工作报告了实验效率相关指标（如 FRAG 的延迟相比明文基线的 3–5 倍开销），但未说明具体硬件配置。

## 5. 实验数量与充分性

**实验规模：**
- 论文本身不涉及实验，而是对 **18 篇主要研究**进行编码和分类。
- 统计分布：研究焦点方面，隐私与安全 6 篇、模型集成 3 篇、个性化 2 篇、检索效率 2 篇；贡献类型方面，新模型/框架 3 篇、数据集/基准 2 篇、评估分析 1 篇、综述 1 篇；应用领域方面，医疗 3 篇、通用/多域 2 篇、金融法律 1 篇、企业多语言 1 篇、推荐 1 篇。

**充分性评估：**
- 作为首篇系统映射研究，覆盖规模虽小但为该领域奠基，分类维度合理。
- 局限性客观存在：样本量小、部分领域（金融/法律、教育）研究极少，结论外推需谨慎；缺少对灰色文献和行业部署的系统覆盖。

## 6. 论文的主要结论与发现

- **研究趋势**：Federated RAG 研究在 2024 年显著激增，驱动力来自 LLM 在高风险领域的部署及监管压力。
- **架构模式分化**：检索端出现朴素聚合、选择性查询路由、加密搜索三种主要模式；生成端包括集中式、客户端特定和混合式。
- **隐私保护是核心关注点**：近半数研究聚焦隐私与安全，典型方案包括可信执行环境（TEE/SGX）、同态加密（HE）和差分隐私（DP）。
- **设计权衡**：隐私保护带来延迟开销（如 FRAG 加密检索 3–5 倍延迟）；选择性路由降低流量（RAGRoute 减少 75% 冗余查询）但可能牺牲覆盖率。
- **评估缺口**：联邦设置下的检索与生成缺乏统一评估标准和隐私—效用帕累托基准。
- **未来方向**：CRDT 风格索引同步、元学习检索器个性化、实时流式排行榜、隐私—效用联合基准。

## 7. 优点

- **首次系统化综述**：填补了 Federated RAG 领域缺乏结构化文献梳理的空白。
- **方法论规范**：严格遵循 Kitchenham 指南进行系统映射，检索与筛选流程透明、可复现。
- **多维分类体系**：从研究焦点、贡献类型、应用领域三个维度建立分类，架构分类法清晰直观。
- **理论与实践结合**：除静态映射外，提出统一目标函数为理论视角，并提炼可操作的设计模式供实践者参考。
- **面向行动的综合表**：表 5 将 18 篇研究的贡献、收益与产出对齐，便于快速理解和比较。

## 8. 不足与局限

**外部效度：**
- 仅覆盖 18 篇论文语料，可能遗漏工业界专有系统或非主流索引领域的研究。
- 研究地理分布以西方和东亚学术与企业生态为主，不完整代表全球研究图景。

**构造效度：**
- Federated RAG 边界尚存模糊性，不同社区对何为“联邦 RAG 系统”定义不一，分类可能受概念多样性影响。
- 忽略了灰色文献、技术文档和非存档系统（如已部署原型）。

**结论效度：**
- 基于小样本的结论需谨慎推广，2024 年的研究激增可能只是短期高峰。
- 快速演变的定义和工具意味着分类体系仅是某一时点的快照。

**其他限制：**
- 使用非常规术语或来自企业内部的成果可能被遗漏，影响可复现性。

（完）
