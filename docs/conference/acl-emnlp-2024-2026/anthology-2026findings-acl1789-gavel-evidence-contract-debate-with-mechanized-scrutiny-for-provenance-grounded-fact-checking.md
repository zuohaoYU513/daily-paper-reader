---
title: "GAVEL: Evidence-Contract Debate with Mechanized Scrutiny for Provenance-Grounded Fact-Checking"
title_zh: GAVEL：证据契约辩论与机械化审查的溯源事实核查
authors: "Ruoyu Xu, Gaoxiang Li, Victor S. Sheng"
date: 2026-07-01
pdf: "https://aclanthology.org/2026.findings-acl.1789.pdf"
tags: ["query:evidence-qa"]
score: 9.0
evidence: 通过证据契约将原子子主张绑定到证据单元并机械化审查溯源
tldr: 事实验证不仅需要判断真伪，还要能返回句子、表格单元格等多文档链路的细粒度证据。GAVEL提出多代理辩论框架，要求辩手将每个原子子主张与显式证据单元绑定，并设置中立审查者机械化核查证据链，从而防止生成有理据但无溯源的内容。该框架强化了细粒度证据归因，可为证据约束下的信息抽取与问答提供支持。
source: ACL-2026-Findings
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1789/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1651, \"height\": 834, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2026-findings/anthology-2026findings-acl1789/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1654, \"height\": 731, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1789/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1652, \"height\": 399, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1789/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1649, \"height\": 365, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1789/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 808, \"height\": 213, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1789/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 719, \"height\": 217, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2026-findings/anthology-2026findings-acl1789/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 807, \"height\": 320, \"label\": \"Table\"}]"
motivation: 大模型事实核查可产出看似合理但溯源不足的解释，需要细粒度证据归因约束。
method: 用证据契约约束多代理辩论，每个子主张强制绑定证据单元并接受Scrutinizer审查。
result: 在需要多跳与异构证据的事实核查任务上增强输出的可归因性。
conclusion: 证据契约机制能有效提升事实核查的溯源严谨性，对证据可验证提取有借鉴意义。
---

## Abstract
Evidence-grounded fact-checking requires predicting claim veracity while returning faithful evidence at fine granularity, including exact sentences, table cells, and complete multi-document chains. Although large language models enable decomposition, planning, and multi-agent verification, they can still produce convincing rationales with weak provenance, especially under heterogeneous evidence and multi-hop requirements. We propose GAVEL, a multi-agent debate framework that enforces evidence grounding throughout inference. GAVEL introduces an Evidence Contract that requires debaters to state atomic subclaims and bind each to explicit evidence units, and a Mechanized Chain of Scrutiny in which a neutral Scrutinizer audits outputs and performs deterministic validation of cited identifiers and quoted spans. A Judge then selects a sufficient evidence set and produces the final decision. Experiments on FEVEROUS and HOVER in an open-book setting show that GAVEL improves provenance-aware metrics that jointly require correct labels and correct, complete evidence over strong recent baselines. Ablations confirm that both evidence binding and mechanized citation validation are key to the gains.

---

## 论文详细总结（自动生成）

# GAVEL 论文详细中文总结

## 1. 论文的核心问题与整体含义

**研究动机与背景：**
- 自动化事实核查（Automated Fact-Checking）在现代信息系统中日益重要，它不仅要输出“真/假”的判定标签，还必须返回可独立核查、可复用、细粒度的证据
- 现有大语言模型（LLM）虽具备分解、规划与多代理验证能力，但仍会生成**表面上流畅、但溯源薄弱（weak provenance）** 的理由，尤其在异构证据（文本+表格）和多跳推理（multi-hop）要求下问题更为突出
- 两个核心基准任务凸显挑战：
  - **HOVER**：声明可需要跨最多四个维基百科文章的证据，考验检索规划与跨文档推理
  - **FEVEROUS**：要求从非结构化文本和结构化表格中同时提取细粒度证据，证据归因难度显著高于纯句子验证

**核心关注问题：**
大模型可以输出看似合理但缺乏严谨依据的论证——即“有理据幻觉”，这本质上是**溯源约束不足**导致的推理可信度问题。

## 2. 论文提出的方法论

### 2.1 核心思想

论文提出 **GAVEL（Grounded Audited Verification with Evidence-Locked debate）**，一种多代理辩论框架，通过在全推理过程中强制证据归因来提升事实核查的可信度，其核心是两大机制：

### 2.2 Evidence Contract（证据契约）
- 要求每一位辩手将论证拆分为**原子子主张（atomic subclaims）**，并将每个子主张绑定到明确的证据单元
- 输出结构化记录：O = {(cᵢ, Eᵢ, tᵢ, rᵢ)}，其中：
  - cᵢ：原子子主张
  - Eᵢ：证据单元集合（句子元组 ⟨p, s⟩ 或表格单元格元组 ⟨p, t, r, c⟩）
  - tᵢ：局部蕴含标签（SUPPORTS/REFUTES/INSUFFICIENT）
  - rᵢ：短理由
- **契约规则**：任何未被表述为“原子子主张+绑定证据”的声明一律视为无支撑内容，由Scrutinizer惩罚、由Judge在最终决策中打折

### 2.3 Mechanized Chain of Scrutiny（机械化审查链）
Scrutinizer（中立审查者）在每轮辩论后进行三阶段审查：

**阶段 1：分解与确定性证据验证**
- 将辩手输出分解为证据主张与推理步骤
- 调用**确定性证据检查器**，执行：
  - Schema合法性检查（句子元组与表格单元格元组）
  - 存在性检查（引用的单元是否在检索上下文中）
  - 引用匹配检查（引用片段是否逐字出现在对应证据单元中）
  - 重复与冲突检查
- 输出标志位集合 F（如无效ID、索引越界、引用不匹配等）

**阶段 2：逻辑与谬误审计**
- 识别循环论证、稻草人谬误、草率概括、无支撑跳跃等常见推理失败模式

**阶段 3：审计日志作为约束性干预**
- 产出审计日志 Lᵣ，列举无效引用、缺失证据与修正要求
- 审计日志被追加到共享上下文，成为下一轮辩论的**硬性约束**

### 2.4 代理角色与辩论协议

| 代理 | 角色 | 职责 |
|------|------|------|
| 正方辩手 A | 偏向 SUPPORTS | 检索证据并构建证据绑定的支持论证 |
| 反方辩手 B | 偏向 REFUTES | 检索证据并构建证据绑定的反驳论证 |
| Scrutinizer S | 中立 | 不做新检索，审计双方输出、检查逻辑与引用有效性 |
| Judge J | 中立裁决 | 综合辩论历史与审计日志输出最终标签与证据集 |

**算法流程：**
1. 初始化共享上下文 C₀
2. 最多进行 Rmax = 3 轮辩论：
   - 正反方在证据契约约束下生成论证
   - 确定性证据检查器检查引用
   - Scrutinizer 产出审计日志
   - 更新上下文并进入下一轮
3. 当 Scrutinizer 报告没有新违规时提前停止
4. Judge 按“证据有效性→证据充分性→推理一致性”的证据优先准则输出最终判定

## 3. 实验设计

### 3.1 数据集与基准
- **FEVEROUS**：异构证据（文本+表格），标签为 {SUPPORTS, REFUTES, NOT ENOUGH INFO}
- **HOVER**：多跳验证，官方二元标签 {SUPPORTED, NOT SUPPORTED}
- 两者均在**开放书（open-book）设置**下测评——只能使用从语料库中检索到的信息

### 3.2 评估指标
- **FEVEROUS score**：要求标签正确 + 预测证据包含至少一个完整金标准证据集（子集匹配）
- **HOVER score**：要求标签正确 + 每个金标准支持页面至少有一条句子被引用
- 辅助指标：标签准确率、证据 F1、文档召回率

### 3.3 对比基线
- **ZS + CoT**：单模型零样本+思维链提示
- **ProgramFC**（N=1, N=5）：程序引导的声明分解与推理
- **PACAR**：基于规划的自定义动作推理框架
- **LoCal**：多代理逻辑与因果核查协作框架

### 3.4 实现细节
- 所有代理使用 **gpt-3.5-turbo** 作为基座模型，temperature = 0
- 共享两阶段 BM25 检索后端（页面检索→证据单元检索），所有方法统一证据格式控制检索变量
- 每声明最多 3 轮辩论，动态提前停止

## 4. 资源与算力

论文中**未披露**GPU型号、数量、训练时间等算力信息。原因是：
- GAVEL是一种**推理时协议**，不需要模型训练
- 仅需调用 gpt-3.5-turbo API 完成多代理交互
- 实验成本主要以 **LLM API 调用次数**和**检索调用次数**衡量（见表5），而非本地算力开销

从效率表来看：GAVEL每声明约18次LLM调用和6次检索调用，高于单代理基线但低于多数多代理框架。

## 5. 实验数量与充分性

论文开展了较为丰富的实验设计，总计包括：

| 实验类型 | 数量与内容 |
|----------|-----------|
| 主实验 | 2个数据集（FEVEROUS + HOVER）× 约6种方法对比 |
| 消融实验 | 5组：去掉证据契约、去掉确定性检查器、去掉Scrutinizer、仅单轮、共享检索 |
| 细粒度分析 | FEVEROUS按证据类型分列（纯文本/需表格）；HOVER按跳数分层（1-4跳） |
| 案例研究 | 2个代表性实例（FEVEROUS实体混淆案例 + HOVER缺失中间跳案例） |
| 错误分析 | 人工抽样检查残余失败模式 |
| 效率统计 | LLM调用次数/检索调用次数对比 |

**充分性评价：**
- ✅ 消融设计完整，能清晰剥离各组件贡献
- ✅ 共享检索后端与统一证据格式，控制了检索差异变量
- ✅ 细粒度分层分析增加了结论的深度
- ⚠️ 基座模型单一（仅gpt-3.5-turbo），缺少对不同模型的泛化验证
- ⚠️ 主实验每组方法只报告一个分数，未见标准差/多次运行统计显著性检验信息

## 6. 论文的主要结论与发现

1. **整体效果领先**：GAVEL在FEVEROUS和HOVER上均取得最优成绩
   - FEVEROUS score：41.80%（比最强基线高 4.20%）
   - HOVER score：49.60%（比最强基线高 4.10%）
2. **证据契约是关键**：消融显示移除证据契约导致最大性能下降（FEVEROUS从41.80%降至36.50%，HOVER从49.60%降至44.20%），说明显式证据绑定对阻止无支撑声明在辩论中扩散至关重要
3. **确定性验证不可或缺**：移除机械化检查器显著损害证据质量指标（FEVEROUS证据F1从47.20%降至43.10%，HOVER文档召回从66.40%降至62.80%）
4. **迭代审计有增益**：移除Scrutinizer或限制单轮均造成性能下降，说明多轮审计反馈提供了超出简单双代理对抗的额外价值
5. **细分场景增益规律**：
   - 表格需求型声明提升更大（38.90% vs 33.70%）
   - 跳数越高增益越明显（1跳+2.40%，4跳+4.80%），说明审计驱动的修正对补齐中间证据链有效

## 7. 优点

1. **问题定位精准**：直击LLM事实核查中“流畅但溯源薄弱”的核心缺陷，将证据约束提升为一等公民
2. **方法设计新颖**：
   - 证据契约将多代理辩论的“口头约束”转化为结构化强制要求
   - 机械化审查结合确定性验证与LM逻辑审计，兼顾可靠性与灵活性
3. **协议级方法**：不依赖模型特定训练，可迁移到不同基座模型，通用性强
4. **实验设计规范**：
   - 统一检索后端控制变量，保证对比公平
   - 多维度分析（主实验+消融+细分+案例）全面支撑结论
   - 与任务官方指标严格对齐，结论可信度高
5. **评估指标对齐实际需求**：强调溯源感知指标（标签正确+证据正确/完整），而非单纯准确率

## 8. 不足与局限

1. **推理成本偏高**：多代理+多轮交互带来显著额外的LLM调用（GAVEL约18次/声明），可能不适用于高吞吐或低延迟场景
2. **受制于检索质量**：
   - 当检索器无法返回所需页面/句子/表格时，证据契约与审计无法恢复缺失信息
   - 对HOVER的中间实体发现与FEVEROUS的冷门表格识别尤其脆弱
3. **语义验证深度有限**：
   - 确定性检查器只验证引用格式与存在性，不保证语义正确
   - 对数值比较、聚合运算、隐式归一化等推理仍可能产生“逻辑连贯但语义错误”的解读
4. **基座模型覆盖不足**：仅使用gpt-3.5-turbo且temperature=0，缺少对更强商业模型（如GPT-4）或开源权重模型的泛化验证
5. **数据域局限**：仅限维基百科证据与预定义声明分布，在跨领域、跨语言或对抗性设置下的表现未经验证
6. **报告细节缺失**：无多次运行的方差/显著性检验信息，无算力资源披露，可能影响对方法稳定性的全面评估

---

（完）
