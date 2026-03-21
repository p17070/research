# Deep Dive: Agent Engineering Practices (Dimension 6)

**Research Date:** March 2026
**Parent Document:** `llm-orchestration-missing.md`
**Scope:** Comprehensive analysis of all 11 sub-topics within Dimension 6

---

## Executive Summary

Dimension 6 — Agent Engineering Practices — is the **most uniformly empty dimension** in the entire gap analysis. Of 11 sub-topics, **10 have zero dedicated academic papers** for LLM-based agents. This is not a collection of scattered gaps; it represents a **systematic absence** of software engineering discipline applied to agent development.

The agent field is where software engineering was before the 1968 NATO Conference that coined "software engineering" as a term. We have working systems, growing adoption, and no engineering discipline to sustain them.

**Key finding:** While academic coverage is near-zero, a parallel **industry tooling ecosystem** has emerged (LangSmith, AgentOps, Braintrust, Helicone, promptfoo) that provides practical solutions without theoretical foundations. This creates a fragile situation: tools exist but without the conceptual frameworks to evaluate, compare, or improve them.

---

## Coverage Summary

| # | Topic | Academic Papers | Industry Coverage | Status |
|---|-------|----------------|-------------------|--------|
| 1 | Agent Design Patterns | 1 catalog + adjacent | Framework docs + major industry guides | **EMERGING** (revised up) |
| 2 | Agent Anti-Patterns | 2-3 failure taxonomies | Practitioner knowledge + OWASP ASI | **EMERGING** (revised up) |
| 3 | Agent Performance Profiling | 7+ (AgentTaxo, AgentDiet, OPTIMA, TokenOps, TALE) | 5+ commercial tools | **ESTABLISHED** (revised up) |
| 4 | Agent Refactoring | 0 (agents-as-refactoring-tools exist, not refactoring agents) | DSPy tangentially | **WHITE SPACE** |
| 5 | Agent Technical Debt | 2-3 (PromptDebt, Context Rot, SATD study) | IBM Agentic Drift, Portkey | **EMERGING** (revised up) |
| 6 | Agent Documentation Standards | 1-2 (Agent Cards MICAI 2025, MIT AI Agent Index) | Google A2A Agent Cards | **EMERGING** (revised up) |
| 7 | Agent Development Methodology | 3-5 (ADLC, Promptware Eng., Spec-Driven Dev.) | Sierra, Microsoft, blog posts | **EMERGING** (revised up) |
| 8 | Agent CI/CD | 3-5 (AI-augmented pipelines, LangSmith CI/CD) | 8+ commercial tools | **EMERGING** (revised up) |
| 9 | Agent A/B Testing | 1 (AgentA/B, April 2025) | Langfuse, Dynatrace | **MINIMAL** (revised up) |
| 10 | Agent Incident Response | 1-2 (CoSAI framework, OWASP guide) | AI Incident Database, notable failures | **EMERGING** (revised up) |
| 11 | Agent Capacity Planning | 3-5 (HERMES, BATS, TALE, FinOps) | Routing/pricing tools | **EMERGING** (revised up) |

---

## 1. Agent Design Patterns

**Status: EMERGING (revised upward from initial assessment)**

### What Exists

The initial gap analysis rated this as "0-1 papers." Deeper search reveals **one dedicated pattern catalog** and several adjacent papers, though coverage remains thin relative to the number of patterns in practice.

**Dedicated pattern catalog:**
- **"Agent Design Pattern Catalogue"** (Lu et al., CSIRO, Journal of Systems and Software Vol 220, 2024; arXiv:2405.10467) — **18 formalized patterns** with context, forces, and trade-offs. The closest thing to a "Gang of Four" for agents. Published in a software engineering journal.

**Adjacent academic work:**
- **"Design Patterns for Securing LLM Agents against Prompt Injections"** (arXiv:2506.08837, 2025) — **6 security-specific patterns**: Tool Feedback Prevention, Advance Planning, Dual LLM, Map-Reduce isolation, Constrained Decoding, Guardrails
- **"Why Do Multi-Agent LLM Systems Fail?"** (arXiv:2503.13657, Cemri et al., 2025) — 14 failure modes categorized; implicitly defines anti-patterns
- **"Taxonomy of Failure Mode in Agentic AI Systems" (MASFT)** (Microsoft, 2024) — Systematic failure taxonomy
- **AgentSpec** (ICSE 2026) — specification language for agent behaviors; defines contracts, not patterns
- **GPTSwarm** (ICML 2024) — graph-based optimization of agent interactions
- **CAMEL** (NeurIPS 2023) — formalizes role-playing communication pattern
- **DyLAN** (COLM 2024) — dynamic team formation pattern
- **"System Architecture for Agentic LLMs"** (Tianjun Zhang, UC Berkeley PhD thesis, 2025) — covers training, deployment, safety architectures
- **AgenticSE Workshop** (ASE 2025, Seoul) — First international workshop on Autonomous Agents in Software Engineering

**Major industry pattern guides:**
- **Anthropic** — prompt chaining, routing, parallelization, orchestrator-worker, evaluator-optimizer
- **Google Cloud Architecture Center** — 8 essential multi-agent patterns
- **Microsoft Azure Architecture** — event-driven patterns, state management
- **Confluent** — 4 event-driven multi-agent patterns

### Comprehensive Pattern Taxonomy

**A. Reasoning & Execution Patterns**

| Pattern | Description | Academic Source | Industry Adoption |
|---------|-------------|---------------|-------------------|
| ReAct | Reason → Act → Observe cycle | Original paper (2022) | All frameworks |
| Reflexion | Self-critique + retry with memory | Original paper (2023) | LangGraph, others |
| ReWOO | Plan upfront, execute without re-calling LLM | arXiv:2305.18323 | IBM, PromptLayer |
| Tree-of-Thoughts | Explore multiple reasoning paths simultaneously | Original paper (2023) | Research use |
| Chain-of-Thought | Step-by-step reasoning before answering | Original paper (2022) | All frameworks |
| PreAct | Prediction step before planning | ACL 2025 (COLING) | Early |
| Plan-and-Execute | Separate planning from execution | 1-2 papers | LangGraph, BabyAGI |
| Self-Consistency | Generate multiple paths, vote on best | Original paper (2022) | Research use |

**B. Multi-Agent Orchestration Patterns**

| Pattern | Description | Academic Source | Industry Adoption |
|---------|-------------|---------------|-------------------|
| Supervisor/Orchestrator | Central agent delegates to workers | Lu et al. catalog | LangGraph, AutoGen |
| Sequential Pipeline | Output of agent N → input of agent N+1 | Lu et al. catalog | Swarms, AWS |
| Debate/Council | Agents argue, judge synthesizes | 2-3 papers | Swarms, MongoDB |
| Peer-to-Peer Mesh | Direct agent communication via message bus | 0 papers | Confluent, InfoWorld |
| Event-Driven | Agents react to event streams (Kafka) | 0 papers | Confluent, Azure |
| Hierarchical/Tree | Multi-level delegation (strategy → tactics → execution) | 0 papers | Confluent |
| Swarm | Decentralized, independent specialized agents | 0 papers | OpenAI Swarm, Swarms.ai |
| Chain-of-Agents | Sequential chunk processing for long context | Google (NeurIPS 2024) | Google Research |
| Evaluator-Optimizer | Generator + evaluator in loop | Anthropic blog | LangGraph |
| Routing | Classify input, direct to specialist | Anthropic blog | LangGraph, Semantic Kernel |
| Parallelization | Execute independent tasks concurrently | Anthropic blog | All frameworks |
| Map-Reduce | Parallel processing with aggregation | 0 as named pattern | LangGraph |

**C. Memory & State Patterns**

| Pattern | Description | Academic Source | Industry Adoption |
|---------|-------------|---------------|-------------------|
| Memory-Augmented Agent | Persistent memory store (episodic/semantic) | MemGPT (1-2 papers) | AWS Bedrock, MongoDB |
| Context Window Management | Three-tier: short-term, long-term, external | 0 papers | All frameworks |
| Token Caching | Reuse cached tokens (75% cheaper) | 0 papers | Provider APIs |
| Immutable Event Log | Permanent event record as source of truth | 0 papers | Confluent (Kafka) |
| External State Persistence | Durable state for long-running tasks | 0 papers | Azure, Redis |
| Context Compression | Smart summaries to cut token usage 40-50% | 0 papers | Industry practice |

**D. Safety & Security Patterns**

| Pattern | Description | Academic Source | Industry Adoption |
|---------|-------------|---------------|-------------------|
| Tool Feedback Prevention | Agent can't see tool outputs (immune to injection) | arXiv:2506.08837 | Research |
| Advance Planning | Plan tool calls before exposure to untrusted content | arXiv:2506.08837 | Research |
| Dual LLM | Privileged LLM coordinates quarantined LLM | arXiv:2506.08837 | Research |
| Guardian/Validator | Separate agent validates output | 0 papers | Industry practice |
| Human-in-the-Loop Gate | Checkpoint requiring human approval | 0 as pattern | All frameworks |
| Constrained Decoding | Enforce output format/content constraints | arXiv:2506.08837 | Guardrails frameworks |

**E. Modular Architecture Patterns**

| Pattern | Description | Academic Source | Industry Adoption |
|---------|-------------|---------------|-------------------|
| Agent Skills | Modular capability packages with lazy loading | arXiv:2602.12430 | Anthropic, Microsoft |
| Skills-as-Filesystem | Skills as directories with instructions + code | 0 papers | Anthropic Claude |
| Prompt Chaining | Sequential prompts, output → input | Anthropic blog | All frameworks |
| Self-Healing | Agent retries/recovers on failure | 0 papers | Industry practice |

### What's Missing

Lu et al.'s catalog (18 patterns) is a strong start but gaps remain:

1. **Selection guidance** — When to use which pattern? No decision framework exists. Practitioners rely on intuition.
2. **Composition rules** — Which patterns combine well? Supervisor + Reflexion? Swarm + Event-Driven? No formal analysis.
3. **Empirical evaluation** — No controlled experiments comparing patterns on standardized benchmarks. Which pattern works best for which task type?
4. **Cost/performance trade-offs** — Each pattern has different token, latency, and reliability profiles. No systematic comparison.
5. **Evolution guidance** — How should patterns change as LLMs improve? ReAct may become unnecessary as models internalize reasoning.
6. **Framework-agnostic specification** — Patterns are described in framework-specific terms. No universal pattern language.
7. **Many patterns remain unformalized** — ~20 patterns in the taxonomy above have 0 academic papers treating them as named patterns (event-driven, context compression, token caching, self-healing, etc.)

### Forward Research Directions

1. **Pattern selection framework** — Decision tree or flowchart: given task characteristics (complexity, safety requirements, latency budget, cost constraints), which pattern(s) to use?
2. **Empirical pattern evaluation** — Controlled experiments comparing patterns on SWE-bench, WebArena, GAIA. Answer: which pattern works best for which task type, and at what cost?
3. **Pattern composition theory** — Formal analysis of pattern interactions. Some combinations may be incompatible (Supervisor + Swarm?) or create emergent behaviors.
4. **Pattern mining from frameworks** — Systematic extraction and comparison across LangGraph, CrewAI, AutoGen, Semantic Kernel.
5. **Pattern evolution** — How should patterns change as LLM capabilities improve? Longitudinal study.
6. **Cost-aware pattern design** — Patterns optimized for token efficiency (ReWOO's 5x improvement over ReAct suggests this is tractable).

---

## 2. Agent Anti-Patterns

**Status: EMERGING (revised upward — 2-3 papers with failure taxonomies)**

### What Exists

Two significant failure taxonomy papers now exist, though neither frames findings as a formal "anti-pattern catalog" with detection/remediation guidance:

- **"Why Do Multi-Agent LLM Systems Fail?"** (arXiv:2503.13657, Cemri et al., 2025) — **14 failure modes** categorized. Key finding: **79% of multi-agent system failures originate from specification and coordination issues**, not technical implementation.
- **"Taxonomy of Failure Mode in Agentic AI Systems" (MASFT)** (Microsoft, 2024) — Systematic failure taxonomy covering system design flaws, inter-agent misalignment, and task verification failures.
- **"Spark to Fire: Error Propagation in Multi-Agent Systems"** (Mar 2026) — Documents cascading failure modes and amplification through feedback loops.
- **OWASP Agentic Security Initiative (ASI)** — Emerging threat catalog including ASI08 (Cascading Failures).

### Comprehensive Anti-Pattern Catalog

**A. Architectural Anti-Patterns**

| Anti-Pattern | Description | Evidence | Detection Signal |
|-------------|-------------|----------|-----------------|
| **Over-Engineering** | Complex multi-agent setup for simple problem | 41-86.7% of MAS fail in production (MASFT) | Multi-agent where single agent suffices |
| **Agent Sprawl** | Dozens of micro-agents with overlapping scope | Industry reports | Recursive logic, unintended interactions |
| **Monolithic Agent** | Single agent handles everything | Practitioner knowledge | System prompt >2000 tokens, 10+ tools |
| **Circular Dependencies** | Agents create deadlock patterns | arXiv:2503.13657 | Token consumption without progress |

**B. Specification & Prompt Anti-Patterns**

| Anti-Pattern | Description | Evidence | Detection Signal |
|-------------|-------------|----------|-----------------|
| **Specification Ambiguity** | Vague instructions agent can't interpret | 79% of MAS failures (Cemri et al.) | Agents exploring all interpretations |
| **Overloaded Prompts** | Too many tasks in single prompt | Practitioner knowledge | Missed tasks, quality degradation |
| **Instruction Layering** | Accumulated patches to system prompt | Practitioner knowledge | Prompt fragility on edge cases |
| **Metadata-Based Instructions** | Using API names instead of semantic descriptions | Elements.cloud | Agent can't map instructions to actions |
| **Prompt Overfitting** | Prompt too rigid, fails on variations | Prompt engineering research | High benchmark score, low real-world quality |

**C. Failure Cascade Anti-Patterns**

| Anti-Pattern | Description | Evidence | Detection Signal |
|-------------|-------------|----------|-----------------|
| **Hallucination Cascade** | Hallucinated info propagates downstream | MASFT, "Spark to Fire" | Actions on non-existent entities |
| **Infinite Loop** | Same action repeated without progress | Widely observed | Same tool call 3+ times |
| **Retry Storm** | Retries without changing approach | Industry observation | Same error with same strategy |
| **Tool Abuse** | Unnecessary or incorrect tool calls | Benchmark observations | Tool calls with no task effect |
| **Echo Chamber** | Agents reinforce each other's errors | Multi-agent research | Unanimous agreement without verification |

**D. State & Resource Anti-Patterns**

| Anti-Pattern | Description | Evidence | Detection Signal |
|-------------|-------------|----------|-----------------|
| **State Sync Failure** | Race conditions in shared state | Production reports | Duplicate operations, lost updates |
| **Context Window Stuffing** | Irrelevant information fills context | Practitioner knowledge | Relevance ratio drops below threshold |
| **Cost Explosion** | Unmonitored token waste | 40-70% savings possible | Retry loops, redundant context passing |
| **In-Memory Overload** | No external persistence for long tasks | Architecture guides | Data loss on interruption |

**E. Process Anti-Patterns**

| Anti-Pattern | Description | Evidence | Detection Signal |
|-------------|-------------|----------|-----------------|
| **Premature Commitment** | Agent commits to plan without exploring | Planning research | No branching in planning phase |
| **Over-Delegation** | Supervisor delegates everything | Multi-agent observation | Supervisor with 0 direct actions |
| **Capability Overestimation** | Agent attempts tasks beyond ability | Related to metacognition gap | Acceptance without capability check |
| **Gold Plating** | Over-elaboration beyond requirements | Coding agent observation | Output complexity >> input complexity |
| **Phantom Progress** | Verbose reasoning, no action | Industry observation | High token output, low action count |
| **Reactive Monitoring** | Log-based instead of structured tracing | Observability research | Can't trace errors to specific step |

### What's Missing

1. **Formal anti-pattern catalog** — Named, documented with detection heuristics and refactoring guidance (like Fowler's "code smells" + refactoring pairs)
2. **Automated detection** — Static analysis of agent configurations or runtime analysis of agent traces to flag anti-patterns
3. **Empirical prevalence data** — How common is each anti-pattern? Which frameworks are more susceptible?
4. **Refactoring guidance** — For each anti-pattern, what's the recommended fix? (e.g., Infinite Loop → add step counter + backtracking)

### Forward Research Directions

1. **"Agent Smells: A Catalog of Anti-Patterns in LLM Agent Systems"** — Systematic catalog with detection and remediation
2. **Anti-pattern mining from traces** — Analyze execution traces from agent benchmarks (SWE-bench, WebArena) to identify recurring failure patterns
3. **Anti-pattern detection tools** — Linters for agent configurations, runtime monitors for behavioral anti-patterns
4. **Anti-pattern/pattern duality** — Map each anti-pattern to the design pattern that prevents it

---

## 3. Agent Performance Profiling

**Status: ESTABLISHED (revised upward — 7+ papers, 5+ industry tools)**

This topic has significantly more academic coverage than initially assessed. A wave of 2025 papers addresses token profiling, trajectory optimization, and cost-aware evaluation.

### Academic Papers

1. **"AgentTaxo: Dissecting and Benchmarking Token Distribution of LLM Multi-Agent Systems"** (ICLR 2025 Workshop on Foundation Models in the Wild, Mar 2025; arXiv)
   - **First systematic benchmark for token distribution in multi-agent systems.** Categorizes agent roles (Planner, Reasoner, Verifier) and identifies a "communication tax" from duplicated tokens. Key finding: **input tokens outnumber output 2:1 to 3:1; verification phases consume up to 72% of tokens.** Analyzes MetaGPT, CAMEL, AgentVerse.

2. **"AgentDiet: Improving the Efficiency of LLM Agent Systems through Trajectory Reduction"** (arXiv:2509.23586, Sept 2025)
   - Demonstrates that **useless, redundant, and expired information is widespread in agent trajectories.** Designs automatic waste removal from multi-turn histories, reducing token consumption without degrading performance.

3. **"OPTIMA: Optimizing Effectiveness and Efficiency for LLM-Based Multi-Agent Systems"** (ACL 2025 Findings)
   - Iterative generate-rank-select-train paradigm with a reward function balancing task performance against efficiency.

4. **"TokenOps: A Compiler-Style Architecture for Token Optimization"** (2025)
   - Treats LLMs as programmable compute layers with a compiler-style approach. **Achieves 40-46% token reduction without loss of task fidelity.**

5. **"Efficient Agents: Building Effective Agents While Reducing Cost"** (arXiv:2508.02694, 2025)
   - Introduces **cost-of-pass metric** (dollars-per-successful-task-completion) rather than raw accuracy. Evaluates agents on both accuracy and token-based cost.

6. **"TokenPowerBench: Benchmarking the Power Consumption of LLM Inference"** (arXiv:2512.03024, Dec 2025)
   - First open-source framework coupling phase-aware power telemetry with token-level normalization. Profiles 15+ LLMs across batch size, context length, and quantization.

7. **"TALE: Token-Budget-Aware LLM Reasoning"** (ACL 2025 Findings)
   - Estimates reasonable token budgets per reasoning step to balance accuracy with consumption.

8. **"SPAgent: Adaptive Task Decomposition and Model Selection"** (2025)
   - Agent efficiency through adaptive model routing — cheaper models for simpler sub-tasks.

9. **"BATS: Budget-Aware Task Scheduling for Multi-Agent Systems"** (2025)
   - Token consumption and latency models across agent workflows.

### Industry Profiling Tools

| Tool | Focus | Key Capability |
|------|-------|---------------|
| **LangSmith** (LangChain) | Traces & evaluation | Detailed per-step token counts, latency, cost breakdown |
| **Helicone** | LLM proxy & analytics | Dashboards for cost, latency, token usage across all LLM calls |
| **AgentOps** | Agent observability | Session recording, cost tracking, behavioral monitoring |
| **Arize Phoenix** | Open-source observability | Trace visualization showing token consumption per agent step |
| **OpenLLMetry** (Traceloop) | OpenTelemetry for LLMs | Standardized telemetry using OpenTelemetry conventions |
| **W&B Weave** | Experiment tracking | Traces and evaluates LLM apps with cost tracking |

### Key Finding: The "Communication Tax"

AgentTaxo, AgentDiet, and OPTIMA collectively reveal that **multi-agent systems waste 40-70% of tokens** on:
- Redundant context passing between agents
- Verification overhead (up to 72% of total tokens)
- Expired/stale information in conversation histories
- Duplicated instructions across agent roles

The **cost-of-pass metric** (Efficient Agents) is emerging as the standard: dollars-per-successful-task-completion, not raw accuracy.

### What's Missing

- **No formal profiling methodology** — No equivalent of Brendan Gregg's systems performance methodology for agents
- **No agent flamegraph equivalent** — Visual representation of token/time/cost consumption across execution trees
- **No profile-guided optimization** — Tools show waste but don't automatically fix it (AgentDiet is a start)
- **No standard efficiency benchmarks** — Existing benchmarks (SWE-bench, WebArena) don't have efficiency tracks

### Forward Research Directions

1. **Agent flamegraphs** — Visual tools showing hierarchical token/time/cost consumption, enabling "hot spot" identification like CPU flamegraphs
2. **Profile-guided optimization** — Extend AgentDiet/TokenOps to automatically restructure agent architectures based on profiling data
3. **Efficiency-augmented benchmarks** — Add efficiency tracks to SWE-bench, WebArena, GAIA that penalize token waste
4. **Communication tax reduction** — Protocols for inter-agent communication that minimize token duplication (the 2:1-3:1 input:output ratio suggests massive waste in context passing)
5. **Real-time profiling** — Live dashboards that show token budget burn rate and predict whether budget will be exceeded before task completion

---

## 4. Agent Refactoring

**Status: WHITE SPACE (0 papers)**

### What Exists

Zero dedicated papers on refactoring agent systems. The closest related work:

- **DSPy** (Stanford, 2023) — Compiles declarative LM programs into optimized prompts. This is effectively automated prompt refactoring, but not framed as such.
- Papers on **LLM agents doing code refactoring** exist (agents as refactoring tools), but none address refactoring the agents themselves.

### Refactoring Catalog: Traditional → Agent Equivalents

No academic work proposes these mappings. Drawing from Fowler (1999):

| Traditional Refactoring | Agent Equivalent | Description |
|------------------------|------------------|-------------|
| Extract Method | **Extract Sub-Agent** | Break monolithic agent into specialized sub-agents |
| Inline Method | **Merge Agent Steps** | Combine over-decomposed agents back into one |
| Extract Class | **Decompose Monolithic Agent** | Split agent with too many responsibilities |
| Move Method | **Reassign Tool** | Move a tool from one agent to another in multi-agent setup |
| Replace Conditional with Polymorphism | **Replace Router with Specialized Agents** | Instead of one agent with if/else logic, use typed agents |
| Introduce Parameter Object | **Structured Context Object** | Replace ad-hoc context passing with typed schema |
| Replace Magic Number with Constant | **Replace Hardcoded Prompt with Template** | Parameterize prompt components |
| Extract Interface | **Define Agent Contract** | Formalize agent input/output schema |
| Replace Inheritance with Delegation | **Replace Monolithic Prompt with Tool Calls** | Move logic from prompt into tools |

### What's Missing

1. **Formal refactoring catalog** — Named agent refactorings with preconditions, mechanics, and postconditions
2. **Behavior preservation guarantees** — How to verify an agent behaves identically after refactoring (the fundamental requirement of refactoring)
3. **Automated refactoring tools** — IDE/tooling support for agent refactoring operations
4. **Smell-to-refactoring mapping** — Which anti-pattern triggers which refactoring?
5. **Refactoring safety** — Risk assessment for agent refactorings (which are safe? which might change behavior?)

### Forward Research Directions

1. **"Refactoring LLM Agent Systems"** — Catalog of 15-20 agent refactorings with formal structure
2. **Behavioral equivalence testing** — Methods to verify agent behavior is preserved post-refactoring (statistical equivalence testing on benchmark suites)
3. **DSPy as refactoring engine** — Extend DSPy's compilation approach to full agent architectures, not just prompts
4. **Refactoring economics** — When is refactoring worth the cost? Token savings vs. refactoring effort

---

## 5. Agent Technical Debt

**Status: EMERGING (revised upward — 2-3 LLM/agent-specific papers + foundational ML work)**

### LLM/Agent-Specific Technical Debt (NEW)

1. **"PromptDebt: A Comprehensive Study of Technical Debt Across LLM Projects"** (arXiv:2509.20497, Sept 2025)
   - **First paper to taxonomize prompt-related technical debt.** Introduces "prompt smells" (missing templates, hardcoded values, long/unclear instructions, poorly managed document inputs) and "prompt requirement smells." These fragile prompts are difficult to maintain and degrade output quality.

2. **"Self-Admitted Technical Debt in LLM Software: An Empirical Comparison with ML and Non-ML Software"** (arXiv:2601.06266, Jan 2026)
   - **First empirical study of self-admitted technical debt (SATD) in the LLM era.** Key finding: LLM-based systems exhibit fundamentally different SATD patterns from traditional ML or non-ML software. The median time to first SATD in ML repos increased from 10 days to 441 days between 2021-2025.

3. **"Context Rot"** (Chroma Research, 2025)
   - URL: https://research.trychroma.com/context-rot
   - Systematic study testing 18 frontier models showing **every model exhibits performance degradation as input length increases**, well before hitting context window limits. Three mechanisms: lost-in-the-middle effect, attention dilution (quadratic), distractor interference.

4. **"Agentic Drift"** (IBM Think, 2025)
   - Identifies "agentic drift" as a key risk where agent performance silently degrades as models update, training data shifts, or business contexts change. Proposes "intent-driven testing."

5. **"RAG-MCP: Mitigating Prompt Bloat in LLM Tool Selection"** (arXiv:2505.03275, May 2025)
   - Tool metadata consumes significant tokens. Proposes dynamic retrieval of relevant tools per query rather than global registration.

### Foundational Work (ML, Not Agent-Specific)

6. **"Hidden Technical Debt in Machine Learning Systems"** (Google, NeurIPS 2015)
   - The seminal paper. Identifies data dependencies, configuration debt, pipeline jungles, and the CACE principle. Cited 4000+.

7. **"How AI-Generated Code Accelerates Technical Debt"** (LeadDev, citing Google DORA Report 2024)
   - DORA found 25% increase in AI usage quickens code reviews but results in 7.2% decrease in delivery stability. GitClear tracked 8x increase in duplicated code blocks in 2024.

### Agent-Specific Debt Types (No Academic Treatment)

| Debt Type | Description | Traditional Equivalent | Severity |
|-----------|-------------|----------------------|----------|
| **Prompt Rot** | Prompts degrade as model behavior shifts across versions | Configuration debt | High — silent quality degradation |
| **Tool Sprawl** | Growing number of tools with overlapping functionality | Dependency debt | Medium — cost and confusion |
| **Context Window Bloat** | System prompts grow unbounded with accumulated instructions | Code bloat | High — quality degradation at limits |
| **Evaluation Drift** | Eval criteria diverge from actual user needs over time | Test debt | High — false confidence |
| **Memory Accumulation** | Agent memory stores grow with stale/contradictory entries | Data debt | Medium — wrong context retrieval |
| **Instruction Layering** | Accumulated patches to system prompts for edge cases | Lava layer anti-pattern | High — prompt fragility |
| **Provider Lock-in** | Deep integration with specific LLM provider APIs | Vendor lock-in | Medium — migration cost |
| **Benchmark Overfitting** | Optimizing for benchmarks rather than real-world performance | Teaching to the test | High — production failures |
| **Guardrail Accretion** | Safety rules accumulate without pruning or testing | Security debt | Medium — false sense of safety |
| **Implicit Coupling** | Agent behavior depends on undocumented model quirks | Hidden dependencies | Critical — breaks on model update |

### Key Finding: Debt Is Shifting from Data to Prompts

The original Sculley et al. (2015) framework identified data dependencies as the primary debt source. For LLM agents, **debt is shifting to prompts and context**:
- **PromptDebt** identifies new debt categories (prompt smells, template fragility) absent from the original taxonomy
- **Context Rot** shows that outputs degrade even when prompts are well-crafted, due to attention mechanics
- **Agentic Drift** shows that model updates silently break agent behavior (the CACE principle accelerated)
- **Tool Sprawl** creates a new dependency management problem with overlapping, redundant capabilities

### What's Still Missing

- **No longitudinal empirical studies** measuring debt accumulation in agent systems over 6+ months
- **No debt detection tools** — PromptDebt identifies smells but doesn't automate detection
- **No debt quantification framework** — how to measure the "interest rate" on agent technical debt
- **No maintenance cost models** — what does it cost to maintain an agent system over 1, 2, 5 years?
- **No integration of all debt types** — prompt debt, context rot, agentic drift, and tool sprawl are studied separately

### Forward Research Directions

1. **Unified agent debt taxonomy** — Integrate PromptDebt, Context Rot, Agentic Drift, and Tool Sprawl into a single framework extending Sculley et al.
2. **Automated debt detection** — Linters for prompt smells, context rot indicators, tool utilization analysis
3. **Longitudinal case studies** — Track real agent systems over months/years to measure debt accumulation rates
4. **Model update impact analysis** — Quantify how LLM version changes cascade through agent systems
5. **Debt paydown economics** — When is it worth refactoring prompts vs. accepting degradation?

---

## 6. Agent Documentation Standards

**Status: EMERGING (revised upward — agent-specific documentation standards now exist)**

### Agent-Specific Documentation (NEW)

1. **"Agent Cards: A Documentation Standard for Operational AI Agents"** (MICAI 2025, Springer)
   - URL: https://link.springer.com/chapter/10.1007/978-3-032-17933-3_25
   - **Proposes "Agent Cards" as a structured documentation artifact analogous to Model Cards but designed for operational agents.** Captures roles, memory taxonomy, tool integrations, communication protocols, monitoring hooks, governance scope, and evaluation metrics. Enables transparency, comparability, and auditability.

2. **"The 2025 AI Agent Index"** (MIT CSAIL, arXiv:2602.17753, Feb 2026)
   - URL: https://aiagentindex.mit.edu/
   - **Documents 30 prominent AI agents across 1,350 verified data fields.** Key finding: **only 4/30 agents provide agent-specific system cards** (ChatGPT Agent, OpenAI Codex, Claude Code, Gemini 2.5). **87% lack safety cards.** 25/30 disclose no internal safety results; 23/30 have no third-party testing.

3. **Google Agent2Agent (A2A) Protocol — Agent Cards**
   - Machine-readable JSON documents at `/.well-known/agent-card.json` describing identity, capabilities, and skills. Based on JSON-RPC 2.0. Enables cross-organization agent discovery and communication.

4. **Oracle Open Agent Specification**
   - Standardized representation for portability, reusability, and extensibility across AI agent platforms.

5. **"A Survey of AI Agent Protocols"** (arXiv:2504.16736, April 2025)
   - Identifies absence of standardized protocols as a critical bottleneck hindering interoperability.

### Foundational Work (Models)

6. **"Model Cards for Model Reporting"** (Mitchell et al., FAT* 2019) — Gold standard for ML documentation. Cited 2000+.
7. **"Datasheets for Datasets"** (Gebru et al., CACM 2021)
8. **Foundation Model Transparency Index** (Stanford HAI, 2023-2024) — 100 transparency indicators.

### Industry Precedents

- **OpenAI System Cards** (GPT-4, GPT-4o) — 100+ external red teamers across 45 languages
- **Anthropic System Cards** — Published for every Claude generation; 99.78% harmless response rate for Opus 4.5
- **Open Model Card Project** (openmodelcard.org) — Community standardized JSON format

### What an "Agent Card" Would Need

| Category | Contents | Model Card Equivalent |
|----------|----------|---------------------|
| **Identity** | Name, version, provider, base model, deployment context | Yes |
| **Capabilities** | What tasks the agent can perform, with expected quality levels | Partially |
| **Tool Access** | Tools/APIs the agent can call, with scope and permissions | **No equivalent** |
| **Action Space** | What real-world actions the agent can take | **No equivalent** |
| **Limitations** | Known failure modes, task types it shouldn't attempt | Yes |
| **Safety Properties** | Guardrails, content policies, action constraints | Partially |
| **Performance Envelope** | Expected latency, cost per task, token consumption | **No equivalent** |
| **Data Handling** | What data the agent accesses, stores, or transmits | **No equivalent** |
| **Human Oversight** | Required human-in-the-loop checkpoints | **No equivalent** |
| **Versioning** | Change history, compatibility notes, migration guides | Partially |
| **Incident History** | Known incidents and mitigations | **No equivalent** |
| **Composition Rules** | How this agent interacts with other agents | **No equivalent** |

### Key Finding: 87% of Agents Lack Safety Documentation

The MIT AI Agent Index reveals a stark documentation crisis: only 4 of 30 major agents have agent-specific system cards. This is despite model cards being established practice since 2019. The gap is not about the absence of standards — Agent Cards (MICAI 2025) and A2A Agent Cards exist — but about adoption.

### What's Still Missing

- **No consensus standard** — Agent Cards (MICAI), A2A Agent Cards (Google), Oracle Agent Spec, and AgentSpec (ICSE 2026) are competing proposals with no convergence
- **No adoption incentive** — 87% of agents lack documentation, suggesting standards alone are insufficient
- **No automated generation** — Agent cards must be manually authored; no tools introspect configurations to generate them
- **No agent capability benchmarking** — Standardized tests to populate the "Capabilities" section don't exist

### Forward Research Directions

1. **Standard convergence** — Harmonize Agent Cards (MICAI), A2A Agent Cards (Google), Oracle Agent Spec, and IEEE 3394 into a unified standard
2. **Automated agent card generation** — Tools that introspect agent configurations and generate documentation
3. **Documentation compliance metrics** — Extend MIT AI Agent Index methodology to track adoption over time
4. **Regulatory alignment** — Align agent documentation with EU AI Act requirements for high-risk AI systems

---

## 7. Agent Development Methodology

**Status: EMERGING (revised upward — 3-5 papers/frameworks)**

### What Exists

**Dedicated methodology proposals:**

1. **"The Agent Development Life Cycle (ADLC)"** (Sierra AI, Zack Reneau-Wedeen, July 2025)
   - URL: https://sierra.ai/blog/agent-development-life-cycle
   - **The most mature articulation of how agent development differs from traditional software.** Replaces the SDLC for agent systems. Traditional software is deterministic and rule-based; agents are non-deterministic and goal-based. The ADLC follows the same arc (scope → build → test → release → run) but shifts what teams engineer: outcomes shaped by instructions, context, tool responses, permissions, and live state. Introduces the "agent engineer" role. Built from experience shipping agents for Sonos, WeightWatchers, SiriusXM serving millions monthly.

2. **"Promptware Engineering: Software Engineering for Prompt-Enabled Systems"** (arXiv:2503.02400, March 2025)
   - Treats prompt development with SE rigor. Key finding: **only 21.9% of prompt changes are documented** in real-world projects, often resulting in logical inconsistencies. Proposes full lifecycle: prompt requirements engineering, design, implementation, testing, debugging, and evolution.

3. **"An AI-Led SDLC: Spec-Driven Development"** (Microsoft, Feb 2025)
   - Introduces **Spec-Driven Development (SDD)** where architectural decisions, business logic, and intent are captured and versioned as first-class artifacts. GitHub released the open-source Spec Kit tool.

4. **"The Prompt Report: A Systematic Survey of Prompt Engineering Techniques"** (arXiv:2406.06608, June 2024, updated Feb 2025)
   - Establishes a structured taxonomy of 33 vocabulary terms, 58 prompting techniques, and 40 techniques for other modalities.

**Broader SE-for-AI work:**

5. **"Software Engineering for AI-Based Systems: A Systematic Mapping Study"** (Martínez-Fernández et al., JSS 2020)
   - Systematic review of SE practices for AI broadly.

6. **"LLM-Based Multi-Agent Systems for SE: Literature Review, Vision and the Road Ahead"** (arXiv:2404.04834, 2024)
   - Organizes LLM multi-agent applications across SDLC stages. Covers ChatDev, MetaGPT, AgileCoder.

7. **AgentSpec** (ICSE 2026) — Specification language for agent behavior monitoring.

**Industry methodology proposals:**

8. **Anthropic's "Building Effective Agents"** (Dec 2024) — Start with augmented LLM patterns before autonomous agents.
9. **LangChain's guides** (2025) — Simple → tools → memory → multi-agent.
10. **Microsoft AutoGen** — Conversational patterns as design basis.

### ADLC vs. SDLC: How Agent Development Differs

Sierra's ADLC identifies the fundamental shifts:

| Phase | Traditional SDLC | Agent ADLC (Sierra) | Key Difference |
|-------|-----------------|---------------------|----------------|
| **Scope** | User stories, specs | Agent capability spec + safety boundaries | "Code" includes English-language prompts |
| **Build** | Coding, code review | Prompt engineering, tool integration, prompt review | Non-deterministic outputs |
| **Test** | Unit/integration/e2e | Eval suites, red teaming, LLM-as-judge | Assertions → statistical thresholds |
| **Release** | CI/CD, blue-green | Quality-gated deployment, canary agents | Model upgrades invalidate prior work |
| **Run** | APM, alerting | Agent observability, SLA monitoring | Must monitor semantic quality, not just uptime |

**Promptware Engineering** adds that only 21.9% of prompt changes are documented — suggesting the field needs prompt versioning and review practices comparable to code review.

**Spec-Driven Development** (Microsoft) complements ADLC by making specifications first-class versioned artifacts, addressing the documentation gap.

### What's Still Missing

1. **Agent requirements engineering** — How to formally specify what an agent should and shouldn't do (ADLC acknowledges the scope phase but doesn't formalize it)
2. **Agent design review** — Structured review process for agent architectures before implementation
3. **Prompt review practices** — Code review equivalent for prompts (Promptware Engineering identifies the problem but doesn't propose a review process)
4. **Agent maturity model** — Levels of development maturity (ad-hoc → managed → optimizing), similar to CMMI
5. **Empirical validation** — ADLC is based on Sierra's experience; no independent validation across diverse organizations

### Forward Research Directions

1. **Empirical validation of ADLC** — Apply Sierra's lifecycle across diverse organizations and agent types; measure outcomes
2. **Agent requirements engineering** — Formal specification methods for agent capabilities, constraints, and safety boundaries
3. **Prompt review methodology** — Structured review process with checklists, analogous to code review (addressing the 21.9% documentation rate)
4. **Agent maturity model** — Organizational capability levels for agent development
5. **Methodology comparison** — Empirical comparison of ADLC vs. SDD vs. ad-hoc approaches

---

## 8. Agent CI/CD

**Status: EMERGING (2-3 tangential papers, 6+ industry tools)**

The second topic where industry has outpaced academia.

### Academic Papers

1. **"AI-Augmented CI/CD Pipelines: From Code Commit to Production"** (arXiv:2508.11867, 2025)
   - Explores how AI can augment traditional CI/CD pipelines end-to-end from commit to production, including automated testing and deployment stages.

2. **"An Empirical Study of Testing Practices in Open Source AI Agent Frameworks"** (arXiv:2509.19185, Sept 2025)
   - First empirical baseline of testing practices across agent frameworks. Taxonomy of 10 testing patterns.

3. **"The Rise of Agentic Testing: Multi-Agent Systems for Robust Software Quality Assurance"** (arXiv:2601.02454, Jan 2026)
   - Closed-loop multi-agent testing framework where agents test other agents.

4. **"Towards Automated Functional Testing of LLM-Based Agents"** (Jan 2026)
   - Structural testing methodologies for agents integrable into CI pipelines.

### Industry CI/CD Tools

| Tool | Type | CI/CD Capability | Pricing |
|------|------|-----------------|---------|
| **promptfoo** | Open-source eval | CLI for CI; regression testing, red teaming. Native GitHub Actions | Free |
| **DeepEval** | Pytest integration | Agent-specific metrics: Task Completion, Plan Quality, Step Efficiency (LLM-as-judge) | Free tier |
| **Evidently AI** | GitHub Action | Downloads test prompts, runs agent, evaluates via LLM judges, fails CI if tests fail | Free tier |
| **Braintrust** | Eval platform | Side-by-side prompt comparison, regression detection. Posts results to PRs | Paid |
| **LangSmith** | Dev platform | Full CI/CD pipeline with LangGraph: unit/integration/e2e tests, quality-gated releases | $39/user/mo |
| **Arize Phoenix** | Open-source observability | Path evaluations, convergence evaluations, session-level evaluations | Free |
| **Patronus AI** | Eval + red-teaming | Automated guardrails and evaluation in deployment pipelines | Paid |
| **AgentOps** | Agent observability | Session recording, cost optimization, regression flagging | Free tier |

### Key Insight: LLM-as-Judge Is the Dominant Paradigm

The core challenge is **non-determinism**: LLM outputs are subjective and context-dependent, so traditional assertion-based tests fail. The field has converged on **LLM-as-a-Judge scoring with quantitative thresholds** as pass/fail gates, combined with regression detection against baseline datasets.

### What's Missing

- **No formal model** of "deployment readiness" for agents — what must pass before an agent ships?
- **No standard release criteria** — equivalent of code coverage thresholds for agent quality
- **No rollback model** — how to safely revert an agent deployment
- **No staging environment paradigm** — how to test agents in realistic but safe environments
- **No pipeline architecture** — standard CI/CD pipeline stages for agent systems (build → eval → red-team → stage → deploy → monitor)

### Forward Research Directions

1. **Agent deployment readiness framework** — Define what "ready to deploy" means for agents (eval pass rates, safety checks, regression thresholds)
2. **Agent CI/CD pipeline architecture** — Reference architecture for continuous delivery of agent systems
3. **Evaluation-as-code** — Standardized, version-controlled evaluation suites that run in CI (promptfoo is closest)
4. **Agent staging environments** — Sandboxed environments that simulate production for pre-deployment testing
5. **Continuous red teaming** — Automated adversarial testing integrated into deployment pipelines

---

## 9. Agent A/B Testing

**Status: MINIMAL (revised upward — 1 dedicated paper)**

### What Exists

1. **"AgentA/B: Automated and Scalable Web A/B Testing with Interactive LLM Agents"** (Lu et al., arXiv:2504.09723, April 2025)
   - Uses LLM-based autonomous agents with diverse personas to **simulate user interactions on live webpages**, replacing or augmenting real user traffic. Enables persona-driven agents that navigate dynamic pages and execute multi-step interactions (search, click, filter, purchase) to produce early behavioral signals before committing real traffic. **This is about using agents to perform A/B testing, not A/B testing of agents themselves** — but the methodology is transferable.

2. **"Evaluation and Benchmarking of LLM Agents: A Survey"** (Mohammadi et al., ACM SIGKDD 2025, Toronto; arXiv:2507.21504)
   - Two-dimensional taxonomy: evaluation objectives (behavior, capabilities, reliability, safety) × evaluation process (interaction modes, datasets, metrics, tooling). Highlights enterprise challenges: role-based access, reliability guarantees, long-horizon interactions.

3. **"Chatbot Arena"** (Zheng et al., ICML 2024) — Elo-based ranking through head-to-head battles. Chatbot-focused but methodology is transferable.

4. **"Judging LLM-as-a-Judge"** (Zheng et al., NeurIPS 2023) — Automated judge methodology, prerequisite for scalable A/B testing.

### Industry Tools

- **Langfuse** — Supports canary-style prompt deployments by labeling prompt versions (prod-a, prod-b) to split traffic
- **Dynatrace** — End-to-end telemetry across full chain (UI → services → agents → model gateways → GPU) with standardized tracing for A/B testing and canary deployments
- **Shadow mode** — Run new agent alongside old, compare outputs without user exposure
- **Feature flags** — Toggle agent capabilities on/off for subsets of users

### Why Agent A/B Testing Is Harder Than Web A/B Testing

| Challenge | Web A/B Testing | Agent A/B Testing |
|-----------|----------------|-------------------|
| **Metric definition** | Click rates, conversions | Task completion? Cost? Safety? User satisfaction? No consensus |
| **Session length** | Single page view | Multi-step interaction, potentially hours |
| **Side effects** | Minimal (UI changes) | Agent actions affect real systems (files, APIs, databases) |
| **Non-stationarity** | Environment is stable | Agent environment changes during testing |
| **Sample size** | Millions of pageviews | Hundreds of agent sessions (expensive) |
| **Evaluation cost** | Automated | May require human judgment per session |
| **Rollback** | Instant (serve old page) | Agent may have taken irreversible actions |

### Forward Research Directions

1. **Statistical frameworks for agent A/B testing** — Sample size calculation, significance testing, metrics selection for multi-step agent interactions
2. **Agent comparison metrics** — Standardized metrics for head-to-head agent comparison (composite of quality, cost, safety, latency)
3. **Interleaving methods** — Adapt search engine interleaving techniques for agent comparison (run both agents, merge actions)
4. **Counterfactual evaluation** — Offline A/B testing using logged agent traces (what would agent B have done?)
5. **Multi-armed bandit for agents** — Adaptive traffic allocation to agent variants based on ongoing performance

---

## 10. Agent Incident Response

**Status: EMERGING (revised upward — frameworks and playbooks now exist)**

### Incident Response Frameworks (NEW)

1. **CoSAI AI Incident Response Framework v1.0** (Coalition for Secure AI, Nov 2025)
   - URL: https://www.coalitionforsecureai.org/defending-ai-systems-a-new-framework-for-incident-response-in-the-age-of-intelligent-technology/
   - **Open-source framework specifically addressing agentic AI failures.** Includes playbooks with detection methods, triage criteria, containment steps, and recovery procedures for **five common AI architecture patterns** (from basic LLM apps to complex agentic RAG systems). Immediately usable by security operations teams.

2. **OWASP GenAI Incident Response Guide** (2025)
   - Aligns with NIST, ISO, and OWASP Top 10 for LLM Applications. Stresses cross-functional collaboration (security, legal, compliance, data science). Identifies key challenges: absence of AI-focused monitoring, difficulty validating outputs at scale, accountability gaps across multi-vendor chains.

3. **America's AI Action Plan** (White House, July 2025)
   - Directs federal agencies to partner with private sector on AI incident response standards and update CISA's playbook to cover AI system failures.

### Incident Databases

4. **AI Incident Database (AIID)** — 1,200+ reports. Stanford AI Index 2025: incidents surged from 149 (2023) to 233 (2024), a **56.4% increase**.
5. **MIT AI Incident Tracker** — Tracks incidents 2015-2025 using MIT AI Risk Repository taxonomies.

### Notable Agent Failures in Production

| Incident | What Happened | Impact | Response |
|----------|--------------|--------|----------|
| **Replit Agent Data Deletion** (July 2025) | Agent deleted 1,206 executive records despite all-caps code freeze instruction | Data loss, AIID #1152 | Implemented "planning-only mode" requiring confirmation for destructive ops |
| **Runaway API Costs** | Research agent entered recursive loop | $47,000 in API calls over 11 days | Detection system added |
| **Unauthorized Infra Destruction** | Agent executed `terraform destroy` on production | Production outage | Missing state file was root cause |
| **Unauthorized Purchases** (Feb 2025) | Agent asked to check egg prices instead purchased eggs | Unauthorized transaction | Consent framework gaps |

### SRE Practices Adapted for Agents (NEW)

6. **"AI Reliability Engineering (AIRE)"** (Solo.io, 2025)
   - Defines AIRE as embedding AI agents into platform engineering workflows (GitOps, CI/CD, IaC). Agents observe architecture, correlate events, access tribal knowledge.

7. **"Human-Centred AI for SRE"** (InfoQ, Jan 2026)
   - Multi-agent AI working alongside on-call engineers. Narrowing search space while leaving judgment to humans.

8. **AWS Multi-Agent SRE Architecture** (AWS, 2025)
   - Four specialized agents (DB Ops, Payment, Network, etc.) under supervisor agent, each trained on domain-specific runbooks.

### What's Still Missing

- **No agent-specific incident taxonomy** — CoSAI covers architecture patterns but doesn't classify agent failure types
- **No post-mortem methodology** adapted specifically for agent failures (root cause: bad tool output? wrong plan? context overflow? model regression?)
- **No error budget framework** — What's the acceptable agent failure rate before mandating human takeover?
- **No automated root cause analysis** — Observability tools show traces but don't automatically attribute failures

### Forward Research Directions

1. **Agent incident taxonomy** — Classify agent-specific incidents by type (data corruption, unauthorized action, infinite loop, hallucination cascade) with severity levels
2. **Agent post-mortem methodology** — Structured framework extending CoSAI with root cause categories specific to agent failures
3. **Error budgets for agents** — Formal framework defining acceptable failure rates across task types
4. **Automated incident detection** — Real-time behavioral anomaly detection triggering circuit breakers
5. **Agent SRE handbook** — Comprehensive guide adapting Google SRE principles for agent operations

---

## 11. Agent Capacity Planning

**Status: EMERGING (revised upward — cost management becoming first-class concern)**

### Academic Papers

1. **"Understanding and Optimizing Multi-Stage AI Inference Pipelines" (HERMES)** (MIT CSAIL, 2025)
   - Enables nine distinct routing strategies with a modular router API for multi-stage inference. Global coordinator orchestrates execution across clients for efficient capacity management.

2. **"Budget-Aware Tool-Use Enables Effective Agent Scaling" (BATS)** (arXiv:2511.17006, Nov 2025)
   - Extends test-time scaling to tool-augmented agents under budget constraints. Introduces AgentTTS (optimizing LLM size and sampling under FLOPs budgets) and **SLIM (periodic summarization for managing context growth in long-horizon agents).**

3. **"Token-Budget-Aware LLM Reasoning" (TALE)** (ACL 2025 Findings)
   - Dynamically adjusts reasoning token counts based on problem complexity. Reduces costs with slight performance loss.

4. **Astraea** (2025) — Proves LLM scheduling is NP-hard. Fair resource allocation.
5. **Llumnix** (OSDI 2024) — Dynamic scheduling with preemptive GPU migration.
6. **BudgetThinker** (2025) — Computational budget allocation across reasoning steps.
7. **SPAgent** (2025) — Adaptive model routing for cost/performance optimization.

### Industry Cost Data

8. **"The Hidden Costs of Agentic AI"** (Galileo AI, 2025)
   - Gartner predicts **40%+ of agentic AI projects will fail to reach production by 2027** due to cost/complexity. 53% of AI teams experience costs exceeding forecasts by 40%+. Hybrid architectures can reduce spend by 30-50%.

9. **"FinOps in the Age of AI"** (Finout, 2025)
   - Production cost forecasting: inference from complex prompts can drive daily expenses to **$3,000-$6,000 per 10,000 user sessions.**

10. **LLM Pricing Trends** (Stanford AI Index 2025)
    - Inference costs for GPT-3.5-class models fell **280-fold** between 2020-2024. H100 cloud prices dropped from $7-8/hr to $1.49-3.90/hr.

### Industry Approaches

- **Intelligent routing** — HERMES, Martian, Portkey, LiteLLM, Requesty route queries to cheapest capable model
- **OpenTelemetry** — Converging as industry standard for agent telemetry (opentelemetry.io/blog/2025/ai-agent-observability)
- **Datadog LLM Observability** — End-to-end tracing with cost attribution
- **Auto-scaling** — vLLM, TGI, TensorRT-LLM for inference workloads

### What's Still Missing

| Planning Aspect | Description | Current State |
|----------------|-------------|---------------|
| **End-to-end cost prediction** | Total cost before execution starts | No treatment |
| **Concurrency modeling** | How many agents can run simultaneously | No treatment |
| **Scaling laws for agents** | How quality/cost scales with resources | No treatment |
| **Burst capacity** | Handling demand spikes | No treatment |
| **Agent workload characterization** | Empirical profiles (burstiness, seasonality) | No treatment |
| **Token budget prediction** | Tokens needed for agent X on task type Y | Partial (BATS, TALE) |
| **Multi-model costing** | Cost for agents using multiple models | Partial (SPAgent, HERMES) |

### Forward Research Directions

1. **Agent scaling laws** — How do quality, cost, and latency scale with compute? (analogous to Kaplan/Chinchilla laws)
2. **Pre-execution cost prediction** — Given agent config + task description, predict total cost before running
3. **Agent workload characterization** — Empirical profiles of real production workloads
4. **FinOps for agents** — Comprehensive cost management discipline, extending traditional FinOps
5. **Multi-tenant capacity planning** — Resource allocation for shared agent infrastructure

---
---

## Cross-Cutting Analysis

### The Maturity Gap

Traditional software engineering has had **60+ years** to develop its practices. Agent engineering has had **~3 years** (since ChatGPT, Nov 2022). The gap is narrowing faster than expected — 2025 saw significant progress.

| Discipline | Traditional SE Milestone | Year | Agent Equivalent | Year |
|-----------|------------------------|------|------------------|------|
| Design Patterns | GoF Book | 1994 | Lu et al. catalog (18 patterns) | 2024 |
| Development Lifecycle | Waterfall/Agile | 1970/2001 | Sierra ADLC | 2025 |
| CI/CD | Continuous Integration | 2000 | LangSmith/promptfoo pipelines | 2024-2025 |
| Performance Profiling | gprof/flamegraphs | 1982/2011 | AgentTaxo/AgentDiet | 2025 |
| Refactoring | Fowler's Book | 1999 | — | Not yet |
| DevOps/SRE | Google SRE Book | 2016 | CoSAI framework, AIRE | 2025 |
| Technical Debt | Cunningham's metaphor | 1992 | PromptDebt, Context Rot | 2025 |
| Documentation | IEEE standards | Various | Agent Cards (MICAI), A2A | 2025 |
| A/B Testing | Web experimentation | 2000 | AgentA/B (limited) | 2025 |
| Incident Response | PagerDuty/SRE practices | 2010s | CoSAI, OWASP GenAI IR | 2025 |

### Cross-Cutting Themes From Research

1. **Non-determinism is the fundamental challenge** — Every topic grapples with variable LLM outputs breaking traditional SE assumptions. CI/CD converges on LLM-as-Judge with statistical thresholds rather than assertions.

2. **The "communication tax"** — AgentTaxo, AgentDiet, and OPTIMA collectively show multi-agent systems waste 40-70% of tokens on redundant context, verification overhead, and expired information. This is the single largest efficiency opportunity.

3. **Convergence with microservices patterns** — Agent architecture follows the same trajectory as distributed systems: monolithic → decomposed, with patterns (orchestrator-worker, generator-critic) mapping directly to established patterns.

4. **ADLC as successor to SDLC** — Sierra's Agent Development Life Cycle represents the most mature articulation of how agent engineering differs from traditional software engineering.

5. **79% of multi-agent failures are specification failures** (Cemri et al.) — The biggest agent engineering problem is not technical but methodological: unclear specifications, not buggy code.

### Industry vs. Academia Divergence

The gap has **narrowed significantly since the initial assessment** but remains for specific topics:

| Area | Industry | Academia | Gap |
|------|----------|----------|-----|
| **Profiling** | 5+ commercial tools | 7+ papers (AgentTaxo, TokenOps, etc.) | **Closing** |
| **CI/CD** | 8+ tools (promptfoo, DeepEval, etc.) | 3-5 papers | **Narrowing** |
| **Methodology** | ADLC (Sierra), SDD (Microsoft) | Promptware Engineering paper | **Narrowing** |
| **Design Patterns** | All major clouds have guides | Lu et al. catalog | **Narrowing** |
| **Technical Debt** | IBM Agentic Drift, Portkey | PromptDebt, Context Rot papers | **Narrowing** |
| **Documentation** | A2A Agent Cards, Oracle Spec | Agent Cards (MICAI), MIT Index | **Narrowing** |
| **Incident Response** | CoSAI framework, OWASP guide | Notable failure cases documented | **Narrowing** |
| **Refactoring** | DSPy tangentially | 0 papers on refactoring agents | **Wide** |

### The "DevOps for Agents" Opportunity

The largest research opportunity in Dimension 6 is the **"DevOps for Agents"** paradigm — a unified engineering discipline covering the full lifecycle of agent systems. This would be the agent equivalent of the DevOps movement that transformed traditional software engineering in the 2010s.

A research agenda for "Agent DevOps" would need:

1. **Agent Design Patterns** (Section 1) — what to build
2. **Agent Anti-Patterns** (Section 2) — what not to build
3. **Agent Development Methodology** (Section 7) — how to build it
4. **Agent CI/CD** (Section 8) — how to ship it
5. **Agent Performance Profiling** (Section 3) — how to optimize it
6. **Agent A/B Testing** (Section 9) — how to compare variants
7. **Agent Monitoring & Incident Response** (Section 10) — how to operate it
8. **Agent Capacity Planning** (Section 11) — how to scale it
9. **Agent Technical Debt** (Section 5) — how to maintain it
10. **Agent Documentation** (Section 6) — how to communicate about it
11. **Agent Refactoring** (Section 4) — how to improve it

### Priority Research Papers

Based on impact and feasibility, these are the highest-priority papers that could **still** be written (accounting for what now exists):

| Priority | Paper | Why | What Exists Already |
|----------|-------|-----|-------------------|
| **1** | "Refactoring LLM Agent Systems" | The only topic with truly 0 coverage; direct practitioner value | Nothing — complete white space |
| **2** | "Unified Agent Technical Debt Taxonomy" | Integrate PromptDebt + Context Rot + Agentic Drift + Tool Sprawl | Separate papers exist; no integration |
| **3** | "Agent Pattern Selection Framework" | Decision guidance: which pattern for which task? | Lu et al. catalog exists but no selection guidance |
| **4** | "Agent CI/CD Reference Architecture" | Bridge industry tools (promptfoo, DeepEval) with academic framework | Tools exist; no architecture framework |
| **5** | "Agent A/B Testing: Statistical Frameworks" | Sample size, metrics, significance for multi-step agents | AgentA/B exists but for testing websites, not testing agents |
| **6** | "Agent Scaling Laws" | How quality/cost scale with compute for agents | BATS/TALE exist for token budgets; no scaling laws |
| **7** | "Empirical ADLC Validation" | Validate Sierra's lifecycle across diverse organizations | ADLC proposed; no independent validation |

