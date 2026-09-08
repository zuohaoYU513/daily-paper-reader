---
title: "Self-Contrast: Better Reflection Through Inconsistent Solving Perspectives"
title_zh: Self-Contrast：通过不一致求解视角改进反思
authors: "Wenqi Zhang, Yongliang Shen, Linjuan Wu, Qiuying Peng, Jun Wang, Yueting Zhuang, Weiming Lu"
date: 2024-08-01
pdf: "https://aclanthology.org/2024.acl-long.197.pdf"
tags: ["query:metacognitio"]
score: 8.0
evidence: 针对反思中自我评价反馈不稳定、过度自信或高随机的问题，通过多视角对比提升自评质量
tldr: 针对大语言模型依靠自我评价进行反思时反馈质量差、常过度自信或高度随机的问题，论文提出Self-Contrast方法：自适应探索该问题的多种求解视角，对比不同答案之间的差异并总结不一致之处，从而生成更可靠的自评反馈。实验显示这种方法能有效缓解自我评价的不稳定，促进模型产生更高质量的反思结果，为无需外部反馈的自省能力改进提供了新思路。
source: ACL-2024-Long
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 840, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 95, \"height\": 66, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1635, \"height\": 352, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 771, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 839, \"height\": 550, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 769, \"height\": 486, \"label\": \"Figure\"}, {\"url\": \"assets/figures/acl-2024-long/anthology-2024acl-long197/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 777, \"height\": 496, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 826, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 803, \"height\": 445, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 804, \"height\": 303, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 817, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1656, \"height\": 556, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 816, \"height\": 335, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 785, \"height\": 267, \"label\": \"Table\"}, {\"url\": \"assets/tables/acl-2024-long/anthology-2024acl-long197/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 836, \"height\": 372, \"label\": \"Table\"}]"
motivation: 大语言模型内在反思不稳定，关键瓶颈在于自我评价反馈质量低且过度自信或随机。
method: 自适应探索多个求解视角，对比并总结视角间差异，利用分歧生成更稳定的自我评价反馈。
result: 实验表明该方法能显著改善自评反馈质量并促进更有效的反思修正。
conclusion: 多视角对比可增强LLM自我评价的稳定性，无需外部反馈即可改进反思。
---

## Abstract
The reflection capacity of Large Language Model (LLM) has garnered extensive attention. A post-hoc prompting strategy, e.g., reflexion and self-refine, refines LLM’s response based on self-evaluated or external feedback. However, recent research indicates without external feedback, LLM’s intrinsic reflection is unstable. Our investigation unveils that the key bottleneck is the quality of the self-evaluated feedback. We find LLMs often exhibit overconfidence or high randomness when self-evaluate, offering stubborn or inconsistent feedback, which causes poor reflection. To remedy this, we advocate Self-Contrast: It adaptively explores diverse solving perspectives tailored to the request, contrasts the differences, and summarizes these discrepancies into a checklist which could be used to re-examine and eliminate discrepancies. Our method endows LLM with diverse perspectives to alleviate stubborn biases. Moreover, their discrepancies indicate potential errors or inherent uncertainties that LLM often overlooks. Reflecting upon these can catalyze more accurate and stable reflection. Experiments conducted on a series of reasoning and translation tasks with different LLMs serve to underscore the effectiveness and generality of our strategy.

---

## 论文详细总结（自动生成）

## 论文总结：Self-Contrast：通过不一致求解视角改进反思

### 1. 论文的核心问题与整体含义（研究动机与背景）
- **反思能力的重要性与现状**：大型语言模型（LLM）的自我反思能力（如 Reflexion、Self-Refine）广受关注。这类方法通常采用“初始响应→自我评价→修订”的三阶段框架进行事后修正，试图实现无外部反馈下的自我纠错；但近期研究怀疑 LLM 缺乏真正可靠的内在反思能力。
- **发现的根本瓶颈**：作者通过实验发现，反思失效的关键在于 **自评反馈质量太差**——模型在自我评价中常表现出：
  - **过度自信（Overconfidence）**：对错误答案固执己见（约占无效反馈的 46.7%）；
  - **高度不一致/随机（Inconsistency）**：同一回答多次评价得出的反馈互相矛盾（占 45.7%）。
- **切入思路**：直接生成高质量反馈对 LLM 而言过于困难，但**对比多个回答间的差异**则相对更容易、更稳定。该方法利用分歧来暴露潜在错误和易忽视的逻辑陷阱，从而生成更可靠的修订依据。

### 2. 论文提出的方法论（Self-Contrast）
核心思想是**用“对比”替代直接“评价”**，通过营造多个不一致的求解视角，将视角之间的分歧转化为反思清单，指导模型重新审视并消除差异。主要包括三个阶段：

**阶段一：创建多样视角（Create Diverse Perspectives）**
- 由 LLM **自我设计（self-curated）** 适应每个用户请求的多条提示词（Prompt），每条提示词配有不同的角色、思维方式、侧重点或语气，引导模型从不同角度生成解答。例如：在翻译中做直译/意译/文化视角，在数学题中使用“自上而下”/“自下而上”/“类比思维”。
- 提示词数量不固定，由模型自行决定（通常为 2~9 条，经验值多为 4 条）。

**阶段二：对比视角间分歧（Contrast Inter-Perspective Discrepancies）**
- 使用 **K-Medoids 聚类**（基于语义相似度）对生成的所有回答进行筛选，保留代表不同特性的簇中心，剔除高度相似的冗余结果。
- 将挑选出的候选（通常 k=3）配对送入 LLM，要求其回答：
  - 两种回答是否存在差异？
  - 差异具体体现在方向/步骤中？
  - 造成差异的深层次原因是什么？
- 对每对回答找出不一致之处作为后续反思线索。

**阶段三：消除分歧（Eliminate Discrepancies）**
- LLM 将成对差异归纳为一份**“检查清单”（Checklist）**，内含多条具体、可执行的复核指令（如“核对是否理解原题意图”“检查第2步中的计算错误”“判断译文是否符合英文表达习惯”等），比传统的“请再检查一遍”更细粒度、信息量更大。
- 使用 JSON 结构化提示（请求、候选回答、差异描述、清单）让模型逐条反思修订，**最终输出所有视角下答案一致的修正结果**；若仍有不一致，则继续迭代直至收敛。

> 算法流程概括为：  
> `输入请求 → 自适应生成N条视角提示词 → 生成N个回答 → 聚类筛选 → 对K个差异回答做两两对比 → 总结Checklist → 基于Checklist逐项反思修订 → 输出多个一致作答`

### 3. 实验设计
- **Benchmark 数据集与任务**：
  - **数学推理**：GSM8K（高难度、复杂运算）、SVAMP（中等难度、组合运算）。
  - **创意翻译**：CommonMT（“hard”子集，含大量习语、隐喻等非标准中文表达需配合语境理解）。
- **使用的 LLM 模型**：GPT-3.5-Turbo-0613、GPT-4-0613、Llama2-Chat（7B/13B/70B）。
- **对比基线（Baselines）**：
  - 标准 CoT Prompt；
  - Self-Reflection（原生反思）；
  - Self-Consistency 的不同变体：`SC-Vote`（投票）、`SC-Select`（自我选择）、`SC-Reflect`（自我择优后反思）；
  - Multi-Agent Debate（多智能体辩论，3 个智能体 3 轮）；
  - ExpertPrompt、Hint-Prompt、Math-Prompt 等其余提示优化方法。
- **评估方式**：
  - 数学任务比较最终答案的精确率；
  - 翻译任务用 **BLEURT** 作为句子质量自动度量；
  - 每种设置在温度 0.2 下采用零样本多批次（10 组不同提示）取平均结果，并进行单尾 t 检验显著性分析。

### 4. 资源与算力
- 论文正文**未明确说明**所使用的 GPU 型号、数量、训练/推理时长或总计算量（FLOPs）。
- 仅在实验中通过“API/LLM 调用次数（#Call）”（如 Self-Contrast 约 7.8 次/题，Multi-Agent 约 9 次/题）作为计算成本代理指标用于横向对比，说明本方法消耗更少的调用次数而又优于多智能体辩论。
- 总体属于纯 Prompt/Zero-shot 推断式方法，不涉及额外模型训练开销。

### 5. 实验数量与充分性
- **实验覆盖面较广**：
  - 2 类完全不同性质的任务（数学推理、创意翻译）；
  - 5 种不同规模的商用/开源 LLM；
  - ≥9 种方法基线；
  - 完整包含主实验、模型规模对比、动态提示数量和效果对比等多种条件下的大量数据表格。
- **消融与剖析实验丰富**：
  1. **反馈类型统计**：区分 Invalid（✗→✗）、Valid（✗→✓）、Toxic（✓→✗）等反思效果，并人工分类反馈为四种类型（自洽确认错误、固执错误、不一致、过度自信），用于推断反思失效的微观原因；
  2. **对比正确与错误混合方案**：对比“一对正确+错误”“两错误相似”“两错误不同”等情形，验证对比差异的价值；
  3. **对比自评与对比评估的准确率**（正确 vs. 错误样本）；
  4. **不同 Self-Select 策略**（随机选、聚类+随机、聚类+LLM选、聚类+负向视角）的差异比较；
  5. **模型置信度影响实验**：替换初始回答的模型来源（如 Llama-2 → GPT-3.5）证明反思受初始方案影响强烈，说明反思维度更易偏向信任原回答；
  6. **对比直接评估 vs. 自评 Top-2 / Top-5 / 多次采样**等场景。
- **总体评价**：实验设计在覆盖范围和对照逻辑上**较为充分和客观**；通过多种模型与三类任务评估提升结论可信度。但仍是在有限任务（两类）中评测，在通用性、真实世界复杂场景（编程、对话、代码生成等）维度的检验仍需补充。

### 6. 主要结论与发现
- LLM “内在反思”普遍无效且不稳定：只靠自身评价+修订，在不同的推理或翻译任务上几乎没有稳定提升（仅 15.1% 的错误初始回答能被纠正）；性能波动基本不显著。
- 根因在于自评反馈的两种致命缺陷：**过度自信**或**高度不一致/随机**，使模型难以准确甄别问题所在。
- **Self-Contrast 通过对比生成反思反馈可以显著改善反思效果**：
  - 数学推理平均提升达到 **+7.2%**（GSM8K、SVAMP 上 GPT-3.5 分别为 +7.8%、+9.2%；Llama2-70B 分别为 +11.6%、+9.3%）；
  - 翻译任务在大多数模型上取得正向提升（优于 vanilla reflection 的 -1.6，提升达到 +0.95），且对于无法用投票完成的任务同样适用；
  - 减少了 **Invalid 反思**（GPT-3.5 降 30.8%）和 **Toxic 反思**（降 78.9%）；
  - 在 Llama2-7B 上效果弱于 Self-Consistency/Multi-Agent，这种偏差由小模型指令跟随和对比能力不足导致，需要外部工具辅助才能发挥更好效果。
- **对比比评价更稳定**：设计实验证明单纯将“评价改为对比”就可将反思结果显著性从 0.6613 改良至 0.0933，大幅降低了自评的不确定性。

### 7. 优点（方法或实验设计的亮点）
1. **准确识别病灶与对症下药**：先用细粒度人工反馈分类实验明确证明自评反馈中的“过度自信/高随机性”是反思失败的核心原因，为后续方法设计提供了数据支撑。
2. **新颖且认知上可解释的解决途径**：将“评价”转换为“对比”，构造“多种视角→对比差异→检查清单→修订达成共识”更符合多解判断的人脑认知过程，且无需外部工具或基准答案。
3. **自适应、无需人工配置**：视角的数量和具体设计全部由 LLM 按用户请求动态生成，无需预定义智能体个数/角色，灵活适应多元任务。
4. **通用性好**：同时兼容了数学等确定性推理与翻译等开放性文本生成任务；对比了一些不可直接用于翻译的自投票等基线，展示了更广的泛化覆盖。
5. **替代多智能体辩论的更优方案**：在成本和效果上同时优于辩论策略（调用次数更少、性能提升更高），本质是把“对话协作”转变成更强“有针对性的对比+清单检验”。

### 8. 不足与局限
1. **对小参数模型支持不足**：在 Llama2-7B 这类指令跟随能力较弱的模型上，效果低于 Self-Consistency/Multi-Agent；自主探索和对比差异能力受限。引入外部 `difflib` 的启发被提出为未来路径，但暂未实现验证。
2. **自评自身校验仍有残余偏差**：虽然差异对比减少主观纠错偏见，但在错误高度相似或模型本身推理一致性弱时依然作用不大；不能完全替代外部反馈（如真值或工具输出）。
3. **面向的任务范围有限**：仅覆盖数学推理与翻译两域，未涉及代码、长文本推理、问答等更高阶任务；用 BLEURT 和答案精确率做评估也略显单一，缺少开放性任务中人工评测的补充。
4. **资源开销描述缺失**：缺少 GPU 数量、具体推理时间、总 token 消耗等量化数据，无法深入评价部署成本和效率。
5. **视角引入自定义风险**：提示自动生成的过程不受显性规则强约束，可能出现同一请求生成视角高度雷同或风格散乱现象，聚类与筛选流程依赖语义相似度计算的稳定性。
6. **对比处理的分歧准确性仍需人验**：对比部分的正确率虽高于直接评估，但仍非 100%，有出现“不准确对比”风险（如对两错误相似回答无法定位根源），对反思提升的上限产生一定影响。

（完）
