# Awesome Agent

一个持续更新的 AI Agent 模型索引，重点收集开放权重或开源的 agentic model，以及它们在代码、工具调用、长程搜索和科学研究等评测中的公开成绩。

[结构化数据](data/agents.json) · [贡献指南](CONTRIBUTING.md)

> [!IMPORTANT]
> 表中成绩来自项目方公开的模型卡或代码仓库，除非特别说明，尚未由本仓库独立复现。相同名称的榜单也可能使用不同 agent scaffold、上下文长度、采样参数和运行次数，不能只凭单个数字判断模型强弱。

## 快速对照

| 模型 | 开放形式 | 参数规模 | 上下文 | 主要方向 | 代表性公开成绩 |
|---|---|---:|---:|---|---|
| [Laguna XS 2.1](https://huggingface.co/poolside/Laguna-XS-2.1) | 开放权重；OpenMDW-1.1 | 33B MoE / 3B active | 未在本页统一列示 | 本地 agentic coding、工具调用 | SWE-bench Verified 70.9；Multilingual 63.1；Pro 47.6；Terminal-Bench 2.0 37.5 |
| [Laguna S 2.1](https://huggingface.co/poolside/Laguna-S-2.1) | 开放权重；OpenMDW-1.1 | 118B MoE / 8B active | 1,048,576 | 长程 agentic coding、工具调用 | Terminal-Bench 2.1 70.2；SWE-bench Multilingual 78.5；Pro 59.4；DeepSWE 40.4 |
| [BTL-3](https://github.com/Badtheorylabs/BTL-3) | 开源代码；Apache-2.0 模型 | 27B；Rank-32 PEFT adapter | 262,144 架构上限 | 代码生成、结构化工具调用、本地推理 | HumanEval 95.12；BFCL v4 AST 88.5；LiveCodeBench v6 88.1 |
| [Agents-A1](https://huggingface.co/InternScience/Agents-A1) | 开放权重；许可证以模型仓库为准 | 35B MoE / 3B active | 未在本页统一列示 | 长程搜索、工程、科学研究、工具调用 | Seal-0 56.36；GAIA 96.04；FrontierScience-Research 40.0；IFBench 80.61 |
| [Ornith 1.0 9B](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B) | 开放权重；MIT | 9B dense | 262,144（推荐服务配置） | 单 GPU agentic coding、自改进 RL | Terminal-Bench 2.1 43.1；SWE-bench Verified 69.4；Pro 42.9；NL2Repo 27.2 |
| [Solar Open 2](https://huggingface.co/upstage/Solar-Open2-250B) | 开放权重；Upstage Solar License | 250B MoE / 15B active | 1,000,000 | 长程 Agent、办公、文档与代码任务 | SWE-bench Verified 70.4；LiveCodeBench v6 92.4；IFBench 80.0；Ko-GDPval 86.8 |
| [Macaron-V1](https://macaron.im/mindlab/research/introducing-macaron-v1) | 开放权重；许可证以模型仓库为准 | Venti 748B；Tall 50B | 未在本页统一列示 | 通用 Agent、个人智能、代码、生成式 UI | Venti：SWE Verified 85.6；TerminalBench 2.1 87.6；DeepSWE 58.4；UI4ABench 87.8 |
| [Holo3.1](https://hcompany.ai/holo3.1) | 开放权重；Apache-2.0 | 0.8B / 4B / 9B / 35B-A3B | 未在本页统一列示 | Web、桌面与移动端 Computer Use | 35B-A3B：OSWorld 80.0；AndroidWorld 79.3；ScreenSpot-Pro 71.5；OSWorld-G 78.8 |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | 开放权重；Apache-2.0 | 4B total / 3B non-embedding | 262,144 | 本地个人助理、工具调用、办公与代码 Agent | SWE-bench Verified 63.6；Pro 46.9；Terminal-Bench 2.0 44.1；Pinch-Bench-V2 74.7 |
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | 开放权重；Apache-2.0 | 35B MoE / 3B active | 262,144 | Agentic coding、终端任务、工具调用 | SWE-bench Verified 69.40；Multilingual 63.00；Pro 45.96；Terminal-Bench 2.1 41.02 |
| [QUEST](https://github.com/OSU-NLP-Group/QUEST) | 模型开放权重；代码、数据与训练脚本开放；模型 Apache-2.0 / 代码 MIT | 2B–35B；旗舰 35B-A3B | 未在本页统一列示 | Deep Research、长程搜索、引用与报告生成 | 35B-RL：BrowseComp 45.5；GAIA 80.8；DeepResearch Bench 48.2；LiveResearchBench 68.2 |

“上下文”一栏区分模型架构上限和项目方公开的推荐服务配置；未能从首要来源确认时不作推测。

## 模型记录

### Laguna XS 2.1

Poolside 面向本地开发环境发布的轻量 MoE 编程 Agent 模型。模型卡给出的规模为 33B 总参数、每个 token 激活 3B 参数，可在 36 GB 内存的 Mac 上运行。它混合使用滑动窗口注意力和全局注意力，支持工具调用之间的交错推理、按请求开关 thinking，以及 FP8 KV cache。官方提供 FP8、NVFP4、INT4、GGUF 等版本，并给出 vLLM、SGLang、Transformers、TRT-LLM、llama.cpp 和 Ollama 的部署说明。

| Benchmark | Score | 说明 |
|---|---:|---|
| SWE-bench Verified | 70.9% | 模型卡报告 |
| SWE-bench Multilingual | 63.1% | 模型卡报告 |
| SWE-bench Pro (Public Dataset) | 47.6% | 模型卡报告 |
| Terminal-Bench 2.0 | 37.5% | 模型卡报告 |

来源：[模型卡](https://huggingface.co/poolside/Laguna-XS-2.1) · [发布文章](https://poolside.ai/blog/introducing-laguna-xs-2-1) · [技术报告](https://poolside.ai/assets/laguna/laguna-m1-xs2-technical-report.pdf)

### Laguna S 2.1

Poolside 的 118B MoE 模型，每个 token 约激活 8B 参数。模型包含 256 个 routed experts 和 1 个 shared expert，采用 grouped-query attention，并在 48 层中交错使用全局注意力与 512-token sliding window attention。它支持 1,048,576-token 上下文、工具调用间的原生推理和 DFlash speculative decoding。

| Benchmark | Score | 说明 |
|---|---:|---|
| Terminal-Bench 2.1 | 70.2% | 模型卡报告 |
| SWE-bench Multilingual | 78.5% | 模型卡报告 |
| SWE-Bench Pro (Public Dataset) | 59.4% | 模型卡报告 |
| DeepSWE | 40.4% | 模型卡报告 |
| SWE Atlas (Codebase QnA) | 46.2% | 模型卡报告 |
| Toolathlon Verified | 49.7% | 模型卡报告 |

模型卡注明成绩截至 2026-07-21，并公开了完整 evaluation trajectories。来源：[模型卡](https://huggingface.co/poolside/Laguna-S-2.1) · [评测轨迹](https://trajectories.poolside.ai/)

### BTL-3

Bad Theory Labs 发布的 27B 代码与工具调用模型。高质量版本是基于固定版本 `Qwen/Qwen3.6-27B` 的 Rank-32 PEFT adapter；另有 8.39 GB 的 BTL-3 Compact 独立 GGUF，面向 Mac、工作站和离线部署。模型强调 thinking-mode 生成、单次/多次/并行工具调用、失败后的多轮恢复，以及不需要工具时主动 abstain。

| Benchmark | Score | 说明 |
|---|---:|---|
| HumanEval | 95.12% (156/164) | pass@1，thinking mode |
| BFCL v4 AST | 88.5% (1097/1240) | complete official full set |
| LiveCodeBench v6 | 88.1% (170/193) | thinking mode |
| BigCodeBench-Hard Instruct | 26.35% (39/148) | official strict pass@1 |

Compact 的 92.2% conditional tool-contract retention 来自项目内部 100-turn gate，不属于公开 frontier benchmark，因此没有放进快速对照表。来源：[代码仓库](https://github.com/Badtheorylabs/BTL-3) · [模型权重](https://huggingface.co/badtheorylabs/BTL-3) · [Compact 权重](https://huggingface.co/badtheorylabs/BTL-3-Compact)

### Agents-A1

InternScience 发布的 35B MoE Agent 模型，每个 token 激活约 3B 参数。项目覆盖长程搜索、工程任务、科学研究、指令遵循、通用 Agent 任务和科学工具使用，并随仓库开放了部分领域的评测代码。其训练重点不是单纯增大参数量，而是扩展长程轨迹和异构 Agent 能力。

| Benchmark | Score | 方向 |
|---|---:|---|
| BrowseComp | 75.51 | 长程搜索 |
| XBench-DS-2510 | 86.0 | 长程搜索 |
| Seal-0 | 56.36 | 长程搜索 |
| GAIA | 96.04 | 通用 Agent |
| SciCode | 44.33 | 工程 |
| FrontierScience-Olympiad | 79.0 | 科学研究 |
| FrontierScience-Research | 40.0 | 科学研究 |
| IFBench | 80.61 | 指令遵循 |
| IFEval | 94.82 | 指令遵循 |
| MolBench-bind | 56.8 | 科学 Agent |

来源：[模型卡](https://huggingface.co/InternScience/Agents-A1) · [技术报告](https://arxiv.org/abs/2606.30616)

### Ornith 1.0 9B

DeepReinforce 面向单 GPU 部署发布的 9B dense agentic coding 模型。项目使用强化学习同时优化 solution rollout 和驱动 rollout 的 scaffold，使模型学习更有效的搜索轨迹。模型支持 reasoning parser、结构化工具调用、vLLM/SGLang/Transformers 部署，模型卡给出的推荐服务上下文为 262,144 tokens。

| Benchmark | Score | 评测配置摘要 |
|---|---:|---|
| Terminal-Bench 2.1 (Terminus-2) | 43.1 | 5 runs；128K context |
| Terminal-Bench 2.1 (Claude Code) | 40.6 | 5 runs；Claude Code 2.1.126 |
| SWE-bench Verified | 69.4 | OpenHands；256K context |
| SWE-bench Pro | 42.9 | OpenHands；256K context |
| SWE-bench Multilingual | 52.0 | OpenHands；256K context |
| NL2Repo | 27.2 | 400K context；48K output |
| Claw-eval Avg | 63.1 | 256K context |

来源：[模型卡](https://huggingface.co/deepreinforce-ai/Ornith-1.0-9B)

### Solar Open 2

Upstage 发布的 250B-A15B 开放权重 MoE 模型，面向工具调用、代码和办公文档等长程 Agent 任务。模型共有 48 层，按 1 层 softmax attention、3 层 linear attention 的方式交错排列，不使用位置编码；只有 12 层保留 KV cache，因此能以较低的长上下文内存开销支持 1M-token 窗口。FFN 包含 320 个 routed experts 和 1 个 shared expert，每个 token 选择 8 个 routed experts。官方支持英语、韩语和日语。

| Benchmark | Score | 方向 |
|---|---:|---|
| SWE-bench Verified | 70.4 | Agentic coding |
| LiveCodeBench v6 | 92.4 | 代码 |
| IFBench | 80.0 | 指令遵循 |
| MMLU-Pro | 86.2 | 知识与推理 |
| GPQA-Diamond | 86.3 | 知识与推理 |
| Ko-GDPval | 86.8 | 韩语办公 Agent；项目方自建评测 |

技术报告还报告 Solar Open 2 在 APEX-Agents 套件中领先同规模开放权重对比模型。Ko-GDPval 属于 Upstage 自建的交付物型办公任务评测，不应与独立公共榜单等同看待。BF16 推荐使用 4 张 NVIDIA H200；官方量化版本可缩减到 2 张 H200。Upstage Solar License 允许商业使用和衍生模型开发，但对衍生模型名称、归属标识和许可证附带方式另有要求。

来源：[模型卡](https://huggingface.co/upstage/Solar-Open2-250B) · [技术报告](https://arxiv.org/abs/2607.20062) · [发布文章](https://www.upstage.ai/blog/en/solar-open-2)

### Macaron-V1

Mind Lab 发布的 Mixture-of-LoRA（MoL）Agent 模型系列。旗舰版 Macaron-V1-Venti 在冻结的 744B GLM-5.2 基座上配置 4 个约 1B 参数的 LoRA specialists，分别负责对话与指令遵循、通用 Agent、代码和生成式 UI，总规模约 748B。Macaron-V1-Tall 面向本地部署，使用 35B Qwen 3.6 基座和 4 个约 3.7B 的 LoRA specialists，总规模约 50B。运行时先由 L0 Chat 选择 specialist，后续推理和工具调用留在选中的 LoRA 上下文中；不同 specialist 通过简短总结交换已完成工作。

以下成绩均来自项目方发布图表，对应 Venti，不代表 Tall：

| Benchmark | Score | 方向 |
|---|---:|---|
| Macaron ChatBench | 58.3 | 长程对话诚实性；项目方自建评测 |
| Macaron LivingBench | 64.0 | 跨周个人生活 Agent；项目方自建评测 |
| VitaBench | 60.0 | 个人生活 Agent |
| PinchBench | 94.0 | Agent |
| ClawGym | 77.7 | Agent |
| SWE Verified | 85.6 | Agentic coding |
| TerminalBench 2.1 | 87.6 | 终端任务 |
| DeepSWE | 58.4 | 代码 |
| SWE Atlas QnA | 49.5 | 代码库问答 |
| UI4ABench | 87.8 | 生成式 UI |

模型与 harness 一并设计：UI4A 负责生成可交互界面，REPL harness 使用持久 Python namespace 组合和复用已验证工具，Harness Context Protocol（HCP）统一训练与服务阶段的 Agent 配置。LongStraw 用 resident state 和 response replay 降低长上下文强化学习的内存压力；项目方报告其可在 32×H20 上完成 GLM-5.2 的 2.1M-token 训练。Venti、Coding-Venti 和 Tall 均已在 Hugging Face Collection 发布开放权重。当前研究页未明确给出统一的模型许可证名称，实际使用应以各模型仓库中的许可证文件和基座模型条款为准。

来源：[研究页面](https://macaron.im/mindlab/research/introducing-macaron-v1) · [模型集合](https://huggingface.co/collections/mindlab-research/macaron-v1) · [Venti 权重](https://huggingface.co/mindlab-research/Macaron-V1-Venti) · [Tall 权重](https://huggingface.co/mindlab-research/Macaron-V1-Tall)

### Holo3.1

H Company 发布的 Computer Use VLM 家族，基于 Qwen 3.5 系列，覆盖 Web、桌面和移动端 GUI。模型提供 0.8B、4B、9B 和 35B-A3B 四种规格，同时支持结构化 JSON 输出和原生 function calling。35B-A3B 另有 BF16、FP8、NVFP4 与 Q4 GGUF 权重，面向云端、工作站和消费级设备上的本地部署。

以下结果对应 35B-A3B：

| Benchmark | Score | 说明 |
|---|---:|---|
| Overall Performance | 78.3% | 项目方组合指标；包含公共和内部评测 |
| OSWorld | 80.0% | H Company 的内部 benchmark implementation |
| AndroidWorld | 79.3% | 移动端操作 |
| ScreenSpot-Pro | 71.5% | UI grounding |
| OSWorld-G | 78.8% | UI grounding |
| H Corporate — E-Commerce | 97.8% | 项目方内部评测 |
| H Corporate — Business Software | 90.1% | 项目方内部评测 |
| H Corporate — Collaboration | 75.3% | 项目方内部评测 |
| H Corporate — Multi-Apps | 65.5% | 项目方内部评测 |

官方的 Overall Performance 先对四项 H Corporate 内部任务取平均，再与 OSWorld、AndroidWorld、ScreenSpot-Pro 和 OSWorld-G 一起求均值，因此不是独立榜单成绩。量化方面，项目方报告 FP8 与 NVFP4 的 OSWorld 分数相同，较 BF16 低约 2 分；DGX Spark 上 NVFP4 W4A16 的总 token throughput 是 FP8 的 1.41 倍、BF16 的 1.74 倍。结合 harness 优化后，平均操作步骤耗时从 6.8 秒降至 3.3 秒。

来源：[发布页面](https://hcompany.ai/holo3.1) · [模型集合](https://huggingface.co/collections/Hcompany/holo31) · [35B-A3B 模型卡](https://huggingface.co/Hcompany/Holo-3.1-35B-A3B)

### Nanbeige4.2-3B

南北阁发布的中英双语小型 Agent 模型，基于 Nanbeige4.2-3B-Base，模型卡标注约 4B 总参数、3B non-embedding 参数和 262,144-token 上下文。模型采用 Looped Transformer，通过重复使用 Transformer 层增加有效计算深度，而不按循环次数增加参数量；架构还包含 LoopSplit、带 depth attention 的 mHC 和拼接式 n-gram embedding。

训练分为监督微调和强化学习。监督数据同时来自真实工具集成与大规模环境合成，并通过测试执行和 rubric 评估筛选轨迹；强化学习同时使用结果奖励和过程奖励。模型支持 XML 与 JSON 两种工具调用格式，其中模型卡优先推荐 XML。`preserve_thinking=true` 适用于多轮工具调用、办公和代码 Agent；普通聊天与问答则建议关闭。

| Benchmark | Score | 评测配置摘要 |
|---|---:|---|
| GDPval rubrics | 74.3 | 办公与协作任务；项目方自建 scaffold |
| Agent-IF-Oneday | 67.5 | 项目方报告 |
| Pinch-Bench-V2 | 74.7 | 项目方报告 |
| Claw-Gym | 65.0 | 项目方报告 |
| Claw-Eval pass | 52.2 | 项目方报告 |
| MCP-Atlas | 57.8 | 项目方报告 |
| SWE-bench Verified | 63.6 | OpenHands scaffold |
| SWE-bench Pro | 46.9 | SWE-agent scaffold |
| Terminal-Bench 2.0 | 44.1 | Terminus 2 scaffold |
| DeepResearch Bench II | 33.4 | OpenClaw 本地个人助理评测 |
| ResearchRubrics | 44.8 | OpenClaw 本地个人助理评测 |

上述成绩均为项目方模型卡报告。主评测表统一启用 thinking mode，并设置 `preserve_thinking=true`；不同 scaffold 下的数字不宜直接横向比较。官方给出 Transformers、SGLang、vLLM、llama.cpp、Ollama 和 GGUF 等部署方式。

来源：[模型卡](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) · [基础模型](https://huggingface.co/Nanbeige/Nanbeige4.2-3B-Base)

### KAT-Coder-V2.5-Dev

Kwaipilot 发布的中英双语 Agentic Coding 模型，基于 Qwen3.6-35B-A3B 继续训练，总参数 35B、每个 token 激活约 3B 参数，原生上下文长度为 262,144 tokens。开放版本只包含语言模型权重，不含视觉塔或其他多模态组件，因此实际运行是纯文本模型。官方支持 thinking、non-thinking、历史 thinking trace 保留和结构化工具调用，并提供 SGLang、vLLM、KTransformers 与 Transformers 的部署方法。

模型先使用 127K 条样本进行监督微调，再进入强化学习。RL 训练采用 rollout 与训练 token 一致性、截断重要性采样、经过检查的 sandbox 和 verifier，以及基于 harness 执行反馈的分层奖励。针对 Qwen3.6 在训练中出现的大量并行工具调用、失败调用、空工具块和重复输出，项目方又加入了专门惩罚；模型卡报告异常工具标签比例从 9.34% 降至 0.28%，单轮连续重复从 0.34% 降至 0。

| Benchmark | Score | 评测配置摘要 |
|---|---:|---|
| SWE-bench Verified | 69.40 | Claude Code 2.1.195；pass@1；256K |
| SWE-bench Multilingual | 63.00 | Claude Code 2.1.195；pass@1；256K |
| SWE-bench Pro | 45.96 | Claude Code 2.1.195；pass@1；256K |
| Terminal-Bench 2.1 | 41.02 | Terminus-2 与 Claude Code 平均；单项 32.60 / 49.44 |
| PinchBench | 93.43 | OpenClaw 2026.3.13；pass@1；256K |
| SciCode | 44.20 | pass@1；256K |
| KAT-Code-Bench | 46.21 | Claude Code 2.1.195；pass@1；项目方评测 |

表中成绩均由项目方下载公开权重后，在自建的统一流水线中复测；每个模型通常只运行一次，不是独立第三方复现。SWE-bench 系列和 KAT-Code-Bench 使用 `temperature=1.0`、`top_p=0.95`，Terminal-Bench 2.1 使用 `temperature=0.7`、`top_p=1.0`。原生 256K 之外可使用 YaRN 扩展上下文，但扩展后的效果不等同于原生长上下文能力。

来源：[模型卡](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) · [技术报告](https://arxiv.org/abs/2607.05471)

### QUEST

Ohio State University NLP Group 发布的通用 Deep Research Agent 系列，覆盖 2B、4B、9B、30B 和 35B 多种规模。旗舰 QUEST-35B-RL 基于 Qwen3.5-35B-A3B，依次经过 mid-training、监督微调和强化学习。项目不仅提供模型权重，还公开训练数据、数据生成流程、推理与评测代码以及训练脚本；代码仓库采用 MIT License，QUEST-35B-RL 模型采用 Apache-2.0。

QUEST 用 rubric tree 表示每项研究任务的事实、约束、引用、完整性和可读性要求，并据此生成无需人工标注的可验证训练任务。长程研究过程中，context condenser 会把历史整理为结构化状态，区分可信事实、待验证线索和不可信内容，模型随后从压缩状态继续搜索。SFT 使用通过 rubric 筛选的完整工具调用轨迹；RL 同时使用任务完成奖励和引用事实核查奖励，降低无依据引用。

公开 checkpoint 的规模和训练阶段如下。QUEST-4B 的 Hugging Face 仓库显示实际约 5B 参数，QUEST-30B 系列显示约 31B；表中保留项目名称，同时单列实际规模。

| Checkpoint | 实际规模 | 基座/结构 | 训练阶段 |
|---|---:|---|---|
| [QUEST-2B](https://huggingface.co/osunlp/QUEST-2B) | 2B | Qwen3.5 dense | SFT |
| [QUEST-4B](https://huggingface.co/osunlp/QUEST-4B) | 5B | Qwen3.5 dense | SFT |
| [QUEST-9B](https://huggingface.co/osunlp/QUEST-9B) | 9B | Qwen3.5 dense | SFT |
| [QUEST-30B-SFT](https://huggingface.co/osunlp/QUEST-30B-SFT) | 31B-A3B | Qwen3-30B-A3B MoE | SFT；未发布评测 |
| [QUEST-30B-MT+SFT](https://huggingface.co/osunlp/QUEST-30B-MT-Plus-SFT) | 31B-A3B | Qwen3-30B-A3B MoE | MT + SFT；未发布评测 |
| [QUEST-30B-RL](https://huggingface.co/osunlp/QUEST-30B-RL) | 31B-A3B | Qwen3-30B-A3B MoE | MT + SFT + RL |
| [QUEST-35B-SFT](https://huggingface.co/osunlp/QUEST-35B-SFT) | 35B-A3B | Qwen3.5-35B-A3B MoE | SFT |
| [QUEST-35B-MT+SFT](https://huggingface.co/osunlp/QUEST-35B-MT-Plus-SFT) | 35B-A3B | Qwen3.5-35B-A3B MoE | MT + SFT |
| [QUEST-35B-RL](https://huggingface.co/osunlp/QUEST-35B-RL) | 35B-A3B | Qwen3.5-35B-A3B MoE | MT + SFT + RL |

各模型卡公布的跨规模结果如下。BC、M2W2、HLE、DRB、BC+、GAIA 和 LRB 使用 avg@3；WS 使用 Item F1 avg@4。

| Checkpoint | BC | M2W2 | HLE | DRB | BC+ | WS | GAIA | LRB |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| QUEST-2B SFT | 28.0 | 8.8 | 30.3 | 21.0 | 52.6 | 40.9 | 72.8 | 57.4 |
| QUEST-4B SFT | 40.0 | 24.3 | 36.2 | 22.0 | 52.1 | 55.0 | 77.7 | 62.1 |
| QUEST-9B SFT | 45.4 | 24.4 | 36.9 | 32.6 | 55.6 | 58.5 | 78.6 | 63.5 |
| QUEST-30B RL | 37.0 | 28.6 | 24.6 | 45.3 | 48.2 | 54.2 | 69.0 | 74.1 |
| QUEST-35B SFT | 45.1 | 26.5 | 39.49 | 36.35 | 57.9 | 61.1 | 83.5 | 64.69 |
| QUEST-35B MT+SFT | 45.5 | 29.9 | 39.74 | 39.72 | 58.6 | 62.5 | 83.17 | 65.47 |
| QUEST-35B RL | 45.5 | 30.7 | 37.9 | 48.2 | 61.0 | 64.5 | 80.8 | 68.2 |

缩写：BC = BrowseComp，M2W2 = Mind2Web 2，DRB = DeepResearch Bench，BC+ = BrowseComp-Plus，WS = WideSearch，LRB = LiveResearchBench。小模型只经过 SFT；30B 和 35B RL 模型增加了 MT 与 RL，因此上表既反映参数规模差异，也包含训练阶段差异。RL 明显改善 DRB、LRB 等开放式报告任务，但 35B 的 HLE 和 GAIA 分数低于 MT+SFT，符合项目方对 objective tasks 优先使用 MT+SFT checkpoint 的建议。

训练数据也已公开：

| 阶段 | 数据类型 | Tasks | Trajectories | Sessions |
|---|---|---:|---:|---:|
| MT | Context Summarization | 309,346 | — | — |
| MT | Relevant Info Extraction | 1,052,663 | — | — |
| SFT | Objective | 5,070 | 19,435 | 39,861 |
| SFT | Open-ended | 1,958 | 4,485 | 11,903 |
| RL | Objective | 864 | — | — |
| RL | Open-ended | 269 | — | — |

约 8K 指的是 SFT 与 RL 的合成研究任务规模，不包含两项 MT 辅助任务。上述成绩来自各 checkpoint 的官方模型卡和论文，尚未由本仓库独立复现。

来源：[代码仓库](https://github.com/OSU-NLP-Group/QUEST) · [项目主页](https://osu-nlp-group.github.io/QUEST/) · [QUEST-2B](https://huggingface.co/osunlp/QUEST-2B) · [QUEST-4B](https://huggingface.co/osunlp/QUEST-4B) · [QUEST-9B](https://huggingface.co/osunlp/QUEST-9B) · [QUEST-30B-RL](https://huggingface.co/osunlp/QUEST-30B-RL) · [QUEST-35B-RL](https://huggingface.co/osunlp/QUEST-35B-RL) · [论文](https://arxiv.org/abs/2605.24218)

## 收录原则

- 优先收录开放权重、开源代码或提供可复现实验材料的 Agent 模型。
- 每个成绩需要给出 benchmark 名称、数值、来源 URL 和核对日期。
- 项目方自报、第三方榜单和本仓库复现结果分开标记。
- 不把不同 harness、scaffold、上下文长度或采样设置下的结果当作严格同条件排名。
- 模型许可证与本仓库内容许可证相互独立，使用模型前请阅读原项目条款。

## 数据

`data/agents.json` 保存适合程序读取的模型信息。后续可以据此生成网页、筛选表或定期检查榜单变化。

最后核对：2026-07-24。

## License

本仓库的整理文字与数据采用 [MIT License](LICENSE)。模型、代码和论文仍受各自许可证约束。
