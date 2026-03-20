# Academic Landscape: LLM Agent Orchestration & Agentic AI

**Research Date:** March 2026

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Foundational Reasoning Frameworks](#foundational-reasoning-frameworks)
3. [Agent Architectures & Planning](#agent-architectures--planning)
4. [Tool Use & Function Calling](#tool-use--function-calling)
5. [Multi-Agent Systems](#multi-agent-systems)
6. [Agent Communication & Coordination](#agent-communication--coordination)
7. [Orchestration Frameworks](#orchestration-frameworks)
8. [Memory & Retrieval-Augmented Generation](#memory--retrieval-augmented-generation)
9. [Evaluation & Benchmarks](#evaluation--benchmarks)
10. [Failure Analysis & Reliability](#failure-analysis--reliability)
11. [Safety & Alignment](#safety--alignment)
12. [Agent Optimization & Compilation](#agent-optimization--compilation)
13. [Frontier Research Topics](#frontier-research-topics)
14. [Gap Analysis & Open Problems](#gap-analysis--open-problems)
15. [Key Trends & Observations](#key-trends--observations)
16. [References](#references)

---

## Executive Summary

LLM-powered agent orchestration has evolved from simple prompt-response chains into complex multi-step, multi-agent systems capable of reasoning, tool use, planning, and collaboration. This document maps the complete academic landscape of the field as of March 2026, covering **150+ papers** across 14 research areas.

**The field is structured around five pillars:**

1. **Reasoning** — From Chain-of-Thought (2022) through ReAct (2022) to Adaptive Graph of Thoughts (2025), reasoning topologies have evolved from linear to tree to graph to adaptive structures
2. **Planning & Architecture** — Cognitive architectures (CoALA) and plan-execute separation (Plan-and-Act) provide theoretical and practical scaffolding
3. **Multi-Agent Collaboration** — Systems like AutoGen, MetaGPT, and ChatDev demonstrate that specialized agent teams outperform monolithic agents, though coordination costs and failure propagation remain unsolved
4. **Evaluation & Safety** — Benchmarks are proliferating (AgentBench, SWE-bench, tau-Bench) but face contamination; no agent scores above 60% on safety benchmarks
5. **Orchestration** — Moving from static role assignment toward RL-trained dynamic orchestrators and protocol-level standards (MCP, A2A, TEA)

**Key statistics from the literature:**
- 57.3% of organizations have agents in production (LangChain 2025-2026)
- Multi-agent orchestration achieves 100% actionable recommendations vs. 1.7% for single-agent (MyAntFarm.ai, 2025)
- Agent failure rates range from 41% to 86.7% across 7 frameworks (MAST study, 2025)
- Only 52% of teams have evals, vs. 89% with observability (LangChain)
- Google DeepMind (Dec 2025): Unstructured multi-agent networks amplify errors up to 17.2x

---

## Foundational Reasoning Frameworks

The reasoning capabilities of LLM agents have evolved through a clear progression of increasingly sophisticated "thought topologies."

### Chain-of-Thought (CoT)
- **Paper:** "Chain-of-Thought Prompting Elicits Reasoning in Large Language Models" — Wei et al. (Google Brain), [arXiv:2201.11903](https://arxiv.org/abs/2201.11903), NeurIPS 2022
- **Contribution:** Showed that generating intermediate reasoning steps dramatically improves LLM performance on complex tasks. 540B-parameter model with 8 CoT exemplars achieved SOTA on GSM8K, surpassing finetuned GPT-3 with a verifier.

### Self-Consistency
- **Paper:** "Self-Consistency Improves Chain of Thought Reasoning" — Wang, Wei et al., 2023
- **Contribution:** Samples multiple reasoning paths and selects the most frequent answer via majority voting, improving CoT reliability.

### Least-to-Most Prompting
- **Paper:** "Least-to-Most Prompting Enables Complex Reasoning" — Zhou et al., [arXiv:2205.10625](https://arxiv.org/abs/2205.10625), 2022
- **Contribution:** Two-stage decomposition: break complex problems into subproblems, then solve sequentially. Generalizes to problems harder than demonstrations.

### ReAct
- **Paper:** "ReAct: Synergizing Reasoning and Acting in Language Models" — Yao et al. (Princeton, Google Brain), [arXiv:2210.03629](https://arxiv.org/abs/2210.03629), ICLR 2023
- **Contribution:** **Foundational paper for agentic LLMs.** Interleaves reasoning traces (Thought) with task-specific actions (Action) and environment feedback (Observation). Improved performance on diverse language and decision-making tasks; significantly improved interpretability and trustworthiness.

### Tree of Thoughts (ToT)
- **Paper:** "Tree of Thoughts: Deliberate Problem Solving with Large Language Models" — Yao et al. (Princeton), [arXiv:2305.10601](https://arxiv.org/abs/2305.10601), NeurIPS 2023
- **Contribution:** Generalizes CoT into tree search over reasoning paths with exploration, lookahead, and backtracking. Game of 24: 74% success vs. 4% for GPT-4 with CoT.

### Graph of Thoughts (GoT)
- **Paper:** "Graph of Thoughts: Solving Elaborate Problems with Large Language Models" — Besta et al. (ETH Zurich), [arXiv:2308.09687](https://arxiv.org/abs/2308.09687), AAAI 2024
- **Contribution:** Models reasoning as an arbitrary graph enabling combination, distillation, and feedback loops. 62% quality improvement over ToT on sorting tasks while reducing costs by >31%.

### Adaptive Graph of Thoughts (AGoT)
- **Paper:** [arXiv:2502.05078](https://arxiv.org/abs/2502.05078), Feb 2025
- **Contribution:** Unifies chain, tree, and graph paradigms into a single adaptive framework that dynamically selects reasoning topology. Up to 46.2% improvement on GPQA scientific reasoning tasks.

### Reflexion
- **Paper:** "Reflexion: Language Agents with Verbal Reinforcement Learning" — Shinn et al., [arXiv:2303.11366](https://arxiv.org/abs/2303.11366), NeurIPS 2023
- **Contribution:** Reinforces agents through linguistic self-reflection stored in episodic memory rather than weight updates. 91% pass@1 on HumanEval (surpassing GPT-4's 80%).

### Taxonomy Paper
- **Paper:** "Demystifying Chains, Trees, and Graphs of Thoughts" — Besta et al., [arXiv:2401.14295](https://arxiv.org/abs/2401.14295), Jan 2024
- **Contribution:** Comprehensive taxonomy of "reasoning topologies" with a general blueprint for effective reasoning schemes.

---

## Agent Architectures & Planning

### Cognitive Architectures for Language Agents (CoALA)
- **Paper:** Sumers, Yao, Narasimhan, Griffiths, [arXiv:2309.02427](https://arxiv.org/abs/2309.02427), TMLR 2024
- **Contribution:** Formal cognitive architecture organizing agents along memory (working + long-term), action space (internal + external), and decision procedures (planning + execution loops). Recognizes LLMs as probabilistic production systems. Provides the theoretical scaffolding for the field.

### Plan-and-Act
- **Paper:** [arXiv:2503.09572](https://arxiv.org/abs/2503.09572), Mar 2025
- **Contribution:** Separates Planner (structured high-level plans) from Executor (environment-specific actions). SOTA 57.58% on WebArena-Lite; 81.36% on WebVoyager (text-only SOTA).

### GoalAct
- **Paper:** [arXiv:2504.16563](https://arxiv.org/abs/2504.16563), Apr 2025
- **Contribution:** Continuously updated global planning with hierarchical execution decomposed into skills. Average 12.22% success rate improvement.

### Understanding the Planning of LLM Agents
- **Paper:** [arXiv:2402.02716](https://arxiv.org/abs/2402.02716), Feb 2024
- **Contribution:** First systematic taxonomy of LLM-agent planning: Task Decomposition, Plan Selection, External Module, Reflection, and Memory.

### HuggingGPT
- **Paper:** [arXiv:2303.17580](https://arxiv.org/abs/2303.17580), Mar 2023
- **Contribution:** LLM as controller orchestrating hundreds of AI models across 24 task types via a 4-stage pipeline: task planning, model selection, task execution, response generation.

### TaskWeaver
- **Paper:** [arXiv:2311.17541](https://arxiv.org/abs/2311.17541), Nov 2023
- **Contribution:** Code-first framework with Planner and Code Interpreter roles; interprets requests via code snippets and orchestrates plugins as functions.

---

## Tool Use & Function Calling

### Toolformer
- **Paper:** Schick et al. (Meta), [arXiv:2302.04761](https://arxiv.org/abs/2302.04761), NeurIPS 2023
- **Contribution:** LMs learn in a self-supervised way to decide which APIs to call, when, with what arguments, and how to incorporate results. Competitive with much larger models.

### Tool Learning with Large Language Models: A Survey
- **Paper:** Qu et al., [arXiv:2405.17935](https://arxiv.org/abs/2405.17935), 2024
- **Contribution:** Organizes tool learning into four stages (Task Planning, Tool Selection, Tool Calling, Response Generation) with two paradigms (single vs. iterative invocation).

### ToolACE
- **Paper:** [arXiv:2409.00920](https://arxiv.org/abs/2409.00920), 2024
- **Contribution:** Automated agentic framework for generating diverse function-calling training data supporting parallel and dependent calls with nested parameters.

### Think-Augmented Function Calling
- **Paper:** [arXiv:2601.18282](https://arxiv.org/abs/2601.18282), Jan 2026
- **Contribution:** Improves LLM parameter accuracy in function calling through embedded reasoning steps.

---

## Multi-Agent Systems

### AutoGen
- **Paper:** Wu et al. (Microsoft Research), [arXiv:2308.08155](https://arxiv.org/abs/2308.08155), COLM 2024
- **Contribution:** Introduces "conversable agents" and "conversation programming" — agents customizable to use LLMs, human inputs, and tools in flexible conversation patterns. Leading open-source framework for agentic AI.

### MetaGPT
- **Paper:** Hong et al., [arXiv:2308.00352](https://arxiv.org/abs/2308.00352), ICLR 2024
- **Contribution:** Encodes Standardized Operating Procedures (SOPs) into multi-agent workflows with structured outputs. Assembly-line paradigm assigning specialized roles (Product Manager, Architect, Engineer) with shared message pool.

### ChatDev
- **Paper:** Qian et al., [arXiv:2307.07924](https://arxiv.org/abs/2307.07924), ACL 2024
- **Contribution:** Virtual software company mirroring waterfall model. Complete software development in <7 minutes at <$1 cost.

### CAMEL
- **Paper:** Li et al., [arXiv:2303.17760](https://arxiv.org/abs/2303.17760), NeurIPS 2023
- **Contribution:** Role-playing framework using inception prompting for autonomous agent cooperation. Identified challenges: conversation deviation, role flipping, termination conditions.

### Generative Agents (Smallville)
- **Paper:** Park et al. (Stanford), [arXiv:2304.03442](https://arxiv.org/abs/2304.03442), UIST 2023
- **Contribution:** 25 agents in sandbox form relationships, coordinate activities, and plan daily routines using memory stream, reflection, and planning architecture.

### Voyager
- **Paper:** Wang et al., [arXiv:2305.16291](https://arxiv.org/abs/2305.16291), TMLR
- **Contribution:** First LLM-powered lifelong learning agent in Minecraft. Automatic curriculum, growing skill library, iterative prompting. 3.3x more unique items, 15.3x faster milestones.

### Multi-Agent Debate
- **Paper:** Du et al., [arXiv:2305.14325](https://arxiv.org/abs/2305.14325), May 2023
- **Contribution:** Iterative multi-agent debate reduces hallucinations. **Caveat:** Subsequent 2025 studies found MAD often fails to justify computational overhead vs. simpler baselines.

### Debate Only When Necessary (DOWN)
- **Paper:** [arXiv:2504.05047](https://arxiv.org/abs/2504.05047), Apr 2025
- **Contribution:** Adaptive debate activation based on confidence scores. Up to 6x efficiency improvement while preserving accuracy.

### AgentSociety
- **Paper:** [arXiv:2502.08691](https://arxiv.org/abs/2502.08691), Feb 2025
- **Contribution:** Large-scale simulation with 10K+ agents and 5 million interactions for understanding human social behaviors.

### Multi-Agent Collaboration Mechanisms Survey
- **Paper:** [arXiv:2501.06322](https://arxiv.org/abs/2501.06322), Jan 2025
- **Contribution:** Comprehensive survey of collaboration modes: debate, negotiation, competition, and cooperation.

---

## Agent Communication & Coordination

### LACP: LLM Agent Communication Protocol
- **Paper:** [arXiv:2510.13821](https://arxiv.org/abs/2510.13821), Oct 2025
- **Contribution:** Three-layer protocol inspired by telecom engineering for secure, reliable, interoperable multi-agent communication. Addresses systemic deficiencies of current methods.

### ProtocolBench & ProtocolRouter
- **Paper:** "Which LLM Multi-Agent Protocol to Choose?", [arXiv:2510.17149](https://arxiv.org/abs/2510.17149), Oct 2025
- **Contribution:** Protocol-agnostic benchmark measuring task success, latency, overhead, and robustness. ProtocolRouter learns to select per-scenario protocols.

### Agora
- **Paper:** "A Scalable Communication Protocol for Networks of LLMs", [arXiv:2410.11905](https://arxiv.org/abs/2410.11905), Oct 2024
- **Contribution:** Scalable communication protocol leveraging natural language as the communication medium for LLM networks.

### A Survey of AI Agent Protocols
- **Paper:** [arXiv:2504.16736](https://arxiv.org/abs/2504.16736), Apr 2025
- **Contribution:** Maps the protocol landscape: MCP (Anthropic), A2A (Google), ANP (decentralized), ACP, and LACP. Highlights fragmentation as a critical deficiency.

### Dynamic Communication Topologies
- **Paper:** [arXiv:2510.07799](https://arxiv.org/abs/2510.07799), Oct 2025
- **Contribution:** Frames optimal multi-agent topology as a conditional graph generation problem using graph diffusion models.

### AgentsNet
- **Paper:** [arXiv:2507.08616](https://arxiv.org/abs/2507.08616), Jul 2025
- **Contribution:** Multi-agent benchmark scaling to 100 agents (vs. 2-5 in existing benchmarks) with robust message-passing protocol.

### The Conductor
- **Paper:** [arXiv:2512.04388](https://arxiv.org/abs/2512.04388), Dec 2025
- **Contribution:** Language model trained with RL to orchestrate agents via natural language. A 7B Conductor achieves SOTA on complex reasoning, outperforming more expensive multi-agent baselines.

### LLM-Coordination Benchmark
- **Paper:** [arXiv:2310.03903](https://arxiv.org/abs/2310.03903), 2023
- **Contribution:** LLMs excel in coordination relying on environmental variables but struggle with scenarios requiring consideration of partners' beliefs and intentions (ToM).

---

## Orchestration Frameworks

### Multi-Agent Collaboration via Evolving Orchestration
- **Paper:** [arXiv:2505.19591](https://arxiv.org/abs/2505.19591), May 2025
- **Contribution:** "Puppeteer" paradigm — centralized RL-trained orchestrator dynamically directs agents, adapting to evolving task states. Superior performance with reduced computational costs.

### AgentOrchestra (TEA Protocol)
- **Paper:** [arXiv:2506.12508](https://arxiv.org/abs/2506.12508), Jun 2025
- **Contribution:** Tool-Environment-Agent protocol — unified abstraction modeling environments, agents, and tools as first-class resources with explicit lifecycles and versioned interfaces.

### MyAntFarm.ai
- **Paper:** [arXiv:2511.15755](https://arxiv.org/abs/2511.15755), Nov 2025
- **Contribution:** 348 controlled trials showed multi-agent orchestration achieves 100% actionable recommendation rate vs. 1.7% single-agent; 80x improvement in action specificity.

### Difficulty-Aware Agent Orchestration (DAAO)
- **Paper:** [arXiv:2509.11079](https://arxiv.org/abs/2509.11079), Sep 2025
- **Contribution:** Adapts workflow complexity based on query difficulty with heterogeneous LLMs per operator.

### Agentic AI Frameworks Survey
- **Paper:** [arXiv:2508.10146](https://arxiv.org/abs/2508.10146), Aug 2025 (IEEE)
- **Contribution:** Comprehensive coverage of frameworks (AutoGen, LangGraph, CrewAI), protocols (MCP, ACP, A2A, ANP), and memory architectures.

---

## Memory & Retrieval-Augmented Generation

### A-MEM: Agentic Memory
- **Paper:** [arXiv:2502.12110](https://arxiv.org/abs/2502.12110), Feb 2025
- **Contribution:** Self-organizing memory following the Zettelkasten method — interconnected knowledge networks through dynamic indexing and linking.

### Agentic RAG Survey
- **Paper:** [arXiv:2501.09136](https://arxiv.org/abs/2501.09136), Jan 2025
- **Contribution:** Embeds autonomous agents into the RAG pipeline with agentic design patterns (reflection, planning, tool use, multi-agent collaboration).

### Memory for Autonomous LLM Agents
- **Paper:** [arXiv:2603.07670](https://arxiv.org/abs/2603.07670), Mar 2026
- **Contribution:** Longer context windows do **not** make external memory obsolete — modest context with targeted retrieval outperforms brute-force long context.

---

## Evaluation & Benchmarks

### AgentBench
- **Paper:** Liu et al. (Tsinghua), [arXiv:2308.03688](https://arxiv.org/abs/2308.03688), ICLR 2024
- **Contribution:** 8 distinct environments testing 29 LLMs. Significant gap between commercial and open-source models; poor long-term reasoning is the main obstacle.

### SWE-bench
- **Paper:** Jimenez, Yang et al. (Princeton), [arXiv:2310.06770](https://arxiv.org/abs/2310.06770), ICLR 2024 (Oral)
- **Contribution:** 2,294 real GitHub issues across 12 Python repos. Extensions: SWE-bench Verified (500 human-confirmed), SWE-Bench+ (revealed 32.67% "cheating" patches), SWE-bench Multilingual (9 languages).

### tau-Bench
- **Paper:** Yao et al., [arXiv:2406.12045](https://arxiv.org/abs/2406.12045), 2024
- **Contribution:** Benchmarks tool-agent-user interaction patterns in realistic domain settings.

### MultiAgentBench
- **Paper:** [arXiv:2503.01935](https://arxiv.org/abs/2503.01935), Mar 2025
- **Contribution:** Evaluates multi-agent systems across interactive scenarios with milestone-based KPIs for collaboration quality.

### Evaluation Survey (KDD 2025)
- **Paper:** [arXiv:2507.21504](https://arxiv.org/abs/2507.21504), Jul 2025
- **Contribution:** Two-dimensional taxonomy: evaluation objectives (behavior, capabilities, reliability, safety) × evaluation process (interaction modes, datasets, metrics, tooling).

### Other Notable Benchmarks
| Benchmark | Focus | Year |
|-----------|-------|------|
| ScienceAgentBench | Scientific data analysis | 2025 |
| CORE-Bench | Computational reproducibility | 2024 |
| PaperBench | Replicating AI research | 2025 |
| BrowserGym | Web agent research | 2025 |
| WebArena / VisualWebArena | Web navigation | 2023-2024 |
| AgentHarm | Measuring agent harmfulness | 2025 |
| AgentDojo | Prompt injection attacks | 2024 |
| T-Eval | Tool utilization | 2024 |
| HAL | Holistic Agent Leaderboard | 2025 |

---

## Failure Analysis & Reliability

### Why Do Multi-Agent LLM Systems Fail? (MASFT)
- **Paper:** Cemri et al., [arXiv:2503.13657](https://arxiv.org/abs/2503.13657), Mar 2025
- **Contribution:** Identified 14 distinct failure modes in 3 categories. First structured failure taxonomy. Improved role specification and orchestration are insufficient — more complex solutions needed.

### Who&When: Automated Failure Attribution
- **Paper:** Zhang et al., [arXiv:2505.00212](https://arxiv.org/abs/2505.00212), May 2025
- **Contribution:** Even giant reasoning models like DeepSeek-R1 fail catastrophically at automated failure attribution.

### AgenTracer
- **Paper:** OpenReview, 2025
- **Contribution:** Scalable data synthesis pipeline and lightweight failure attributor (AgenTracer-8B based on QWEN3-8B).

### Resilience with Faulty Agents
- **Paper:** OpenReview, 2025
- **Contribution:** Hierarchical structure exhibits superior resilience (lowest performance drop of 5.5%) when agents are faulty or malicious.

### Agentless
- **Paper:** [arXiv:2407.01489](https://arxiv.org/abs/2407.01489), Jul 2024
- **Contribution:** Questions whether complex agents are necessary — simple agentless approach achieves 32% on SWE-bench Lite at $0.70, outperforming all open-source agents at the time.

---

## Safety & Alignment

### Agent-SafetyBench
- **Paper:** Zhang et al., [arXiv:2412.14470](https://arxiv.org/abs/2412.14470), Dec 2024
- **Contribution:** 349 environments, 2,000 test cases, 8 safety risk categories, 10 failure modes. **No agent scores above 60%.** Two fundamental defects: lack of robustness and lack of risk awareness.

### AgentHarm
- **Paper:** ICLR 2025
- **Contribution:** 110 unique + 330 augmented harmful behaviors across 11 harm categories using 104 tools.

### Safety in Large Reasoning Models Survey
- **Paper:** [arXiv:2504.17704](https://arxiv.org/abs/2504.17704), Apr 2025
- **Contribution:** Unique attack surfaces in multi-step reasoning — attackers can exploit by forcing overthinking or short-cutting deliberation.

### VeriGuard: Formal Verification for Agent Safety
- **Paper:** [arXiv:2510.05156](https://arxiv.org/abs/2510.05156), Oct 2025
- **Contribution:** Dual-stage architecture: offline policy synthesis via Nagini static verifier + online runtime monitoring. **0.0% attack success rate.** Paradigm shift from reactive filtering to correct-by-construction safety.

### AgentSpec
- **Paper:** [arXiv:2503.18666](https://arxiv.org/abs/2503.18666), ICSE 2026
- **Contribution:** First framework for customizable runtime enforcement of safety constraints via DSL. Limitation: no trajectory-based safety analysis.

### Pro2Guard
- **Paper:** [arXiv:2508.00500](https://arxiv.org/abs/2508.00500), 2025
- **Contribution:** Proactive runtime enforcement via probabilistic model checking with PAC guarantees on probability of reaching unsafe states.

### Alignment & Safety Survey
- **Paper:** [arXiv:2507.19672](https://arxiv.org/abs/2507.19672), Jul 2025
- **Contribution:** Comprehensive coverage of safety mechanisms, training paradigms, and emerging challenges.

---

## Agent Optimization & Compilation

### DSPy
- **Paper:** Stanford, ICLR 2024, [dspy.ai](https://dspy.ai/)
- **Contribution:** The "compiler" paradigm — abstracts LM pipelines as computational graphs, optimizes prompts and weights via trace-based optimization. Optimizers: MIPROv2 (Bayesian), SIMBA (mini-batch), GEPA (evolutionary).

### AFlow
- **Paper:** ICLR 2025, [OpenReview](https://openreview.net/forum?id=z5uVAKwmjf)
- **Contribution:** Workflow optimization as MCTS search over code-represented workflows. 5.7% improvement over SOTA; smaller models outperform GPT-4o at 4.55% cost.

### WorkflowLLM
- **Paper:** ICLR 2025 submission
- **Contribution:** 106,763 workflow samples covering 1,503 APIs from 83 applications.

### EvoAgentX
- **Paper:** EMNLP 2025 Demo
- **Contribution:** Evolutionary optimization of agent workflows; MATH solve rate from 66% to 76%.

### Optimization Survey
- **Paper:** [arXiv:2503.12434](https://arxiv.org/abs/2503.12434), Mar 2025
- **Contribution:** Covers parameter-driven (fine-tuning, RL, hybrid) and parameter-free (prompt engineering, external knowledge) optimization strategies.

---

## Frontier Research Topics

### Neurosymbolic Agents
- Publications peaked at 236 in 2023 with exponential growth since 2020
- **Key result:** Neurosymbolic representations achieve 82.86% lower cross-entropy loss and 24.5x more problems solved vs. CoT ([arXiv:2502.01657](https://arxiv.org/abs/2502.01657))
- **SymBa:** Symbolic backward chaining with SLD-resolution, invoking LLMs only as needed
- **Gap:** Most work is on reasoning benchmarks, not deployed agentic settings

### World Models for Agents
- **WorldLLM:** Natural language hypotheses about transition regularities via Bayesian inference
- Industry-scale: Genie 3 (DeepMind), Cosmos (NVIDIA), GAIA-2 (Wayve)
- **Gap:** LLM-only world models for abstract task environments are underexplored

### Continual Learning Agents
- **Roadmap:** "Lifelong Learning of LLM-based Agents" ([arXiv:2501.07278](https://arxiv.org/abs/2501.07278)) — first systematic survey
- **FLEX:** Continuous evolution via forward learning from experience
- **mem-agent:** 4B LLM trained with RL to manage memory via tools
- **Gap:** Catastrophic forgetting and stability/plasticity balance in agent contexts

### Agent Operating Systems (AIOS)
- **AIOS:** [arXiv:2403.16971](https://arxiv.org/abs/2403.16971), COLM 2025 — OS kernel for agents with scheduling, context management, memory management, access control. Up to 2.1x faster execution
- **Cerebrum SDK:** NAACL 2025
- **Semantic File System:** ICLR 2025
- **Gap:** Essentially only one major project (AIOS from Rutgers). Multi-tenant scheduling, resource isolation, IPC are wide open.

### Theory of Mind in Agents
- GPT-4 performs at or above human level on ToM tasks, but performance drops with minor perturbations
- **Hypothetical Minds** (ICLR 2025): Cognitive architecture with ToM module for hypothesis generation about other agents' strategies
- **Gap:** Whether LLMs truly possess ToM or mimic it; risks of ToM for manipulation

### Causal Reasoning Agents
- **Causal Agent:** [arXiv:2408.06849](https://arxiv.org/abs/2408.06849) — LLM + causal tools via ReAct, >80% accuracy
- **LLM-CD:** 169.53% recall improvement in causal discovery (KDD 2025)
- **Gap:** Most work is on causal *discovery*, not causal *reasoning for action/intervention*

### Real-Time / Streaming Agents
- **StreamAgent** (ICLR 2026): Continuous perception with task-driven planning for streaming video QA
- **StreamingLLM** (ICLR 2024): Infinite sequence length via "attention sink"
- **Helium** (Mar 2025): Cost-based scheduling hiding dependency latency
- **Gap:** Streaming *inference* is studied; streaming *agents* with continuous perception-action loops are barely studied

---

## Gap Analysis & Open Problems

### Areas with Few or No Papers

| Gap Area | Status | Notes |
|----------|--------|-------|
| **Agent Generalization / OOD** | Very few papers | Only 1-2 papers study generalization to novel environments/partners |
| **Streaming / Real-Time Agents** | Very few papers | Most frameworks assume turn-based interaction, not continuous operation |
| **Agent Operating Systems** | Very few papers | Only AIOS (Rutgers). Scheduling, isolation, IPC are wide open |
| **True Agent Compilers** | Conceptual only | DSPy is closest, but spec-to-optimized-plan with guarantees doesn't exist |
| **Formal Verification of Agents** | Nascent (2025 only) | VeriGuard, AgentSpec, Pro2Guard all from 2025. Full trajectory verification remains open |
| **Causal Reasoning for Planning** | Underexplored | Using causal models for interventions during execution barely studied |
| **Grounding Beyond Embodiment** | Gap | Grounding in social/cultural/abstract domains unresolved |
| **Formally Verified Workflow Synthesis** | No papers found | Workflow synthesis + formal correctness guarantees unexplored |
| **Cross-Domain Agent Transfer** | No papers found | Transfer across entirely different domains without retraining not studied |
| **Agent-Native Programming Languages** | No papers found | Languages designed specifically for agent programs don't exist |

### Consensus Open Questions Across Major Surveys

From [arXiv:2503.23037](https://arxiv.org/abs/2503.23037), [arXiv:2503.21460](https://arxiv.org/abs/2503.21460), [arXiv:2601.12560](https://arxiv.org/abs/2601.12560), and [arXiv:2503.12434](https://arxiv.org/abs/2503.12434):

1. **Long-horizon planning reliability** — agents degrade rapidly on multi-step tasks
2. **Evaluation methodology** — beyond coarse pass/fail metrics toward process-level assessment
3. **Multi-agent safety** — collusion, cascade failures, error amplification (17.2x in unstructured networks)
4. **Pipeline-to-native shift** — from tool-augmented LLMs to agents as first-class computational entities
5. **Real-world deployment gap** — benchmark performance doesn't predict production reliability

---

## Key Trends & Observations

1. **Separation of planning and execution** is the dominant architectural pattern, with adaptive replanning as the key innovation (Plan-and-Act, GoalAct, DAAO)

2. **Reasoning topology evolution:** Linear chains (CoT) → Trees (ToT) → Graphs (GoT) → Adaptive structures (AGoT) that select topology at test time

3. **Multi-agent orchestration** is shifting from static role assignment toward RL-trained dynamic orchestrators and protocol standards (TEA, MCP, A2A)

4. **Tool use maturation:** From self-supervised learning (Toolformer) to structured function-calling with dedicated benchmarks (ToolACE, BFCL)

5. **Memory convergence:** Hybrid approaches combining working memory (context window), structured long-term storage (vector DBs, knowledge graphs), and agentic self-organization (A-MEM)

6. **Benchmark proliferation + contamination:** Benchmarks face overfitting (SWE-Bench+ revealed 32.67% cheating patches)

7. **Efficiency matters:** Simpler approaches can outperform complex multi-agent systems at fraction of cost (Agentless, DOWN)

8. **Safety is unsolved:** No agent exceeds 60% on safety benchmarks; formal verification is nascent but promising (VeriGuard: 0% attack success rate)

9. **The biggest white spaces** for new research: (1) real-time streaming agents, (2) formally verified end-to-end agent behavior, (3) agent generalization/transfer, (4) agent OS primitives, (5) causal reasoning for planning

---

## References

### Major Surveys (2023-2026)
- "Agentic Large Language Models" — [arXiv:2503.23037](https://arxiv.org/abs/2503.23037), Mar 2025
- "LLM Agent: Methodology, Applications, Challenges" — [arXiv:2503.21460](https://arxiv.org/abs/2503.21460), Mar 2025
- "Agentic AI: Architectures, Taxonomies, Evaluation" — [arXiv:2601.12560](https://arxiv.org/abs/2601.12560), Jan 2026
- "AI Agent Systems: Architectures, Applications, Evaluation" — [arXiv:2601.01743](https://arxiv.org/abs/2601.01743), Jan 2026
- "A Survey on LLM-based Autonomous Agents" — [arXiv:2308.11432](https://arxiv.org/abs/2308.11432), Aug 2023 (updated Mar 2025)
- "Agentic AI: A Comprehensive Survey" — [arXiv:2510.25445](https://arxiv.org/abs/2510.25445), Oct 2025
- "Survey on Optimization of LLM-based Agents" — [arXiv:2503.12434](https://arxiv.org/abs/2503.12434), Mar 2025
- "Evaluation and Benchmarking of LLM Agents" — [arXiv:2507.21504](https://arxiv.org/abs/2507.21504), KDD 2025
- "Multi-Agent Collaboration Mechanisms" — [arXiv:2501.06322](https://arxiv.org/abs/2501.06322), Jan 2025
- "A Survey of AI Agent Protocols" — [arXiv:2504.16736](https://arxiv.org/abs/2504.16736), Apr 2025

### Industry Reports
- LangChain "State of AI Agents" (2025-2026) — [langchain.com](https://www.langchain.com/state-of-agent-engineering)
- Partnership on AI "Prioritizing Real-Time Failure Detection in AI Agents" (2025)
