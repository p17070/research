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
| 1 | Agent Design Patterns | 0-1 | Framework docs only | **WHITE SPACE** |
| 2 | Agent Anti-Patterns | 0 | Practitioner knowledge | **WHITE SPACE** |
| 3 | Agent Performance Profiling | 3-5 (tangential) | 5+ commercial tools | **EMERGING** (industry-led) |
| 4 | Agent Refactoring | 0 | DSPy tangentially | **WHITE SPACE** |
| 5 | Agent Technical Debt | 0 (4+ for ML broadly) | Practitioner knowledge | **WHITE SPACE** |
| 6 | Agent Documentation Standards | 0 (3+ for models) | Model/system cards | **WHITE SPACE** |
| 7 | Agent Development Methodology | 0-1 | 2-3 blog posts | **WHITE SPACE** |
| 8 | Agent CI/CD | 2-3 (tangential) | 6+ commercial tools | **EMERGING** (industry-led) |
| 9 | Agent A/B Testing | 0 | Shadow mode in practice | **WHITE SPACE** |
| 10 | Agent Incident Response | 0 (3+ for AI broadly) | AI Incident Database | **WHITE SPACE** |
| 11 | Agent Capacity Planning | 0 (5+ for LLM serving) | Pricing/routing tools | **WHITE SPACE** |

---

## 1. Agent Design Patterns

**Status: WHITE SPACE (0-1 papers)**

### What Exists

No academic "Gang of Four" equivalent exists for LLM agent architectures. Patterns exist implicitly in frameworks and research papers but have never been formally cataloged, named, or evaluated as design patterns.

**Closest academic work:**
- **AgentSpec** (ICSE 2026) — specification language for agent behaviors; defines contracts, not patterns
- **GPTSwarm** (ICML 2024) — graph-based optimization of agent interactions; implicitly uses pipeline/DAG patterns
- **CAMEL** (NeurIPS 2023) — formalizes role-playing communication pattern between agents
- **DyLAN** (COLM 2024) — dynamic team formation pattern for multi-agent collaboration

**Framework-embedded patterns (no academic treatment):**

| Pattern | Description | Where It Lives | Papers as "Pattern" |
|---------|-------------|---------------|-------------------|
| ReAct Loop | Reason → Act → Observe cycle | Original paper → all frameworks | 1 (original only) |
| Reflexion | Self-critique and retry | Original paper → LangGraph | 1 (original only) |
| Supervisor | Central agent delegates to workers | LangGraph, AutoGen | 0 |
| Swarm | Decentralized peer agents | OpenAI Swarm, LangGraph | 0 |
| Router | Agent routes to specialized sub-agents | LangGraph, Semantic Kernel | 0 |
| Map-Reduce | Parallel processing with aggregation | LangGraph | 0 |
| Plan-and-Execute | Separate planning from execution | LangGraph, BabyAGI | 1-2 |
| Human-in-the-Loop Gate | Checkpoint requiring human approval | All frameworks | 0 |
| Memory-Augmented | Agent with persistent memory store | MemGPT, various | 1-2 |
| Guardian/Validator | Separate agent validates output | Industry practice | 0 |
| Self-Healing | Agent retries/recovers on failure | Industry practice | 0 |
| Tool-Use Pipeline | Sequential tool calling with verification | All frameworks | 0 |
| Debate/Adversarial | Agents argue to improve output | Research papers | 2-3 (not as "pattern") |
| Ensemble/Voting | Multiple agents vote on answer | Research papers | 2-3 (not as "pattern") |

### What's Missing

A formal pattern catalog would need to:
1. **Name and define** each pattern (intent, motivation, applicability, structure, participants, consequences)
2. **Classify** patterns by category (structural, behavioral, orchestration, safety)
3. **Provide selection guidance** — when to use which pattern and why
4. **Document trade-offs** — performance, cost, reliability implications
5. **Show composition rules** — which patterns combine well, which conflict
6. **Include empirical evaluation** — benchmarked comparisons across task types

### Forward Research Directions

1. **"Design Patterns for LLM Agents"** — A systematic catalog of 20-30 patterns with formal GoF-style structure. This is arguably the single highest-impact paper that could be written in this space.
2. **Pattern mining from frameworks** — Systematic extraction and comparison of patterns across LangGraph, CrewAI, AutoGen, Semantic Kernel, and others.
3. **Pattern composition theory** — Formal analysis of how patterns interact. Some combinations (e.g., Supervisor + Swarm) may be incompatible or create emergent behaviors.
4. **Empirical pattern evaluation** — Controlled experiments comparing patterns on standardized benchmarks (SWE-bench, WebArena, GAIA) to answer: which pattern works best for which task type?
5. **Pattern evolution** — How should patterns change as underlying LLM capabilities improve? ReAct may become unnecessary as models internalize reasoning.

---

## 2. Agent Anti-Patterns

**Status: WHITE SPACE (0 papers)**

### What Exists

No academic catalog of agent anti-patterns exists. However, failure analysis papers implicitly identify recurring failure modes that function as anti-patterns:

- **"Spark to Fire: Error Propagation in Multi-Agent Systems"** (Mar 2026) — documents cascading failure modes
- **"Agent Error Taxonomy"** — classifies error types but doesn't frame them as anti-patterns with refactoring guidance
- **MAST** — multi-agent stress testing reveals failure patterns under load

### Known Anti-Patterns (Practitioner Knowledge Only)

| Anti-Pattern | Description | Consequence | Detection Signal |
|-------------|-------------|-------------|-----------------|
| **Infinite Loop** | Agent repeats same action without progress | Resource waste, timeout | Same tool call repeated 3+ times |
| **Hallucination Cascade** | Agent acts on hallucinated info, causing downstream errors | Corrupted state, wrong outputs | Actions on non-existent entities |
| **Tool Abuse** | Agent calls tools unnecessarily or incorrectly | Cost explosion, errors | Tool calls with no effect on task |
| **Context Window Stuffing** | Agent fills context with irrelevant information | Quality degradation, cost | Context utilization vs. task relevance |
| **Premature Commitment** | Agent commits to plan without exploring alternatives | Suboptimal solutions | No branching in planning phase |
| **Over-Delegation** | Supervisor delegates everything, adds no value | Latency, cost, no quality control | Supervisor with 0 direct actions |
| **Echo Chamber** | Multiple agents reinforce each other's errors | Confident wrong answers | Unanimous agreement without verification |
| **Capability Overestimation** | Agent attempts tasks beyond its abilities | Failures, partial work | Task acceptance without capability check |
| **Retry Storm** | Agent retries failed actions without changing approach | Resource waste | Same error repeated with same strategy |
| **Gold Plating** | Agent over-elaborates or adds unnecessary features | Wasted effort, scope creep | Output complexity >> input complexity |
| **Monolithic Agent** | Single agent handles everything instead of decomposing | Fragility, context overflow | System prompt > 2000 tokens, 10+ tools |
| **Phantom Progress** | Agent reports progress but makes none (verbose reasoning, no action) | Time waste | High token output, low action count |

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

**Status: EMERGING (3-5 tangential papers, 5+ industry tools)**

This is one of two topics in Dimension 6 where industry has significantly outpaced academia.

### Academic Papers

1. **"Efficient Agents: A Systematic Multi-Agent Framework for Optimizing LLM Token Consumption"** (arXiv, 2025)
   - Proposes multi-agent framework specifically for reducing token consumption. Includes analysis of where tokens are spent across agent operations.

2. **"AgentTaxo: Benchmarking LLM Agent Systems with Comprehensive Task Taxonomy"** (2025)
   - Provides taxonomic analysis of agent task performance including efficiency metrics. Breaks down performance across task types.

3. **"SPAgent: Adaptive Task Decomposition and Model Selection for General-Purpose LLM Agents"** (2025)
   - Analyzes agent efficiency through adaptive model routing — using cheaper models for simpler sub-tasks. Implicitly profiles where complexity lives.

4. **"BATS: Budget-Aware Task Scheduling for Multi-Agent Systems"** (2025)
   - Models token consumption and latency across agent workflows. Provides profiling data for budget optimization.

5. **"TALE: Token-Aware LLM Evaluation"** (ACL 2025)
   - Evaluation framework that accounts for token consumption alongside task performance. First step toward efficiency-aware benchmarking.

### Industry Profiling Tools

| Tool | Focus | Key Capability |
|------|-------|---------------|
| **LangSmith** (LangChain) | Traces & evaluation | Detailed per-step token counts, latency, cost breakdown |
| **Helicone** | LLM proxy & analytics | Dashboards for cost, latency, token usage across all LLM calls |
| **AgentOps** | Agent observability | Session recording, cost tracking, behavioral monitoring |
| **Arize Phoenix** | Open-source observability | Trace visualization showing token consumption per agent step |
| **OpenLLMetry** (Traceloop) | OpenTelemetry for LLMs | Standardized telemetry using OpenTelemetry conventions |
| **W&B Weave** | Experiment tracking | Traces and evaluates LLM apps with cost tracking |

### What's Missing

- **No formal profiling methodology** — No equivalent of CPU/memory profiling discipline for agents
- **No standard efficiency metrics** — tokens-per-task? latency-per-decision? cost-per-successful-outcome? No consensus
- **No optimization strategies from profiles** — Industry tools show raw data but no analysis frameworks for acting on it
- **No academic benchmarking** of profiling tools themselves
- **No agent flamegraph equivalent** — Visual representation of where an agent spends its token/time budget

### Forward Research Directions

1. **Agent profiling methodology** — Formal framework: what to measure, how to measure, how to interpret (analogous to Brendan Gregg's systems performance methodology)
2. **Standard efficiency metrics** — Community consensus on agent efficiency measures, enabling cross-system comparison
3. **Profile-guided optimization** — Using profiling data to automatically optimize agent architectures (cache frequent tool calls, skip unnecessary reasoning steps, route to cheaper models)
4. **Agent flamegraphs** — Visual tools showing hierarchical token/time/cost consumption across agent execution trees
5. **Efficiency benchmarks** — Extend existing benchmarks (SWE-bench, WebArena) with efficiency tracks that penalize waste

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

**Status: WHITE SPACE for agents (4+ papers for ML broadly)**

### Foundational Work (ML, Not Agent-Specific)

1. **"Hidden Technical Debt in Machine Learning Systems"** (Google, NeurIPS 2015)
   - Authors: Sculley, Holt, Golovin et al.
   - The foundational paper. Identifies data dependencies, configuration debt, pipeline jungles, and the CACE principle ("Changing Anything Changes Everything"). Cited 4000+ times. Nearly every concept applies to agent systems but none has been validated in the agent context.

2. **"Challenges in Deploying Machine Learning: A Survey of Case Studies"** (Paleyes et al., NeurIPS 2022)
   - Reviews 50+ deployment case studies. Taxonomy of deployment challenges including data management, model management, and infrastructure debt.

3. **"Technical Debt in AI Systems: A Preliminary Taxonomy and Assessment"** (2024)
   - Extends Google's ML debt framework with additional categories. Still traditional ML focused.

4. **"Beyond the ML Model: Challenges for Deploying AI in Production"** (IEEE Software, 2024)
   - Gap between ML development and production, touching on maintenance burden.

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

### What's Missing

- **0 papers** on technical debt specific to LLM agent systems
- **No empirical studies** measuring debt accumulation in agent systems over time
- **No debt detection tools** for agent architectures
- **No debt quantification** — how to measure the "interest rate" on agent technical debt
- **No maintenance cost models** — what does it cost to maintain an agent system over 1, 2, 5 years?

### Forward Research Directions

1. **"Technical Debt in LLM Agent Systems"** — Empirical study of how agent systems accumulate debt, extending Google's 2015 framework
2. **Agent debt metrics** — Quantifiable measures: prompt complexity growth rate, tool utilization ratio, eval-production gap
3. **Debt detection tools** — Automated analysis of agent configurations to flag debt indicators
4. **Longitudinal case studies** — Track real agent systems over months/years to measure debt accumulation
5. **Model update impact analysis** — Quantify how LLM version changes propagate through agent systems (the CACE principle for agents)

---

## 6. Agent Documentation Standards

**Status: WHITE SPACE for agents (3+ papers for models)**

### Foundational Work (Models, Not Agents)

1. **"Model Cards for Model Reporting"** (Mitchell et al., FAT* 2019)
   - Proposes standardized ML model documentation: intended use, performance metrics, ethical considerations, limitations. Cited 2000+. The gold standard for AI documentation, but covers models, not agents.

2. **"Datasheets for Datasets"** (Gebru et al., CACM 2021)
   - Standardized dataset documentation analogous to electronics datasheets. Relevant because agents consume data.

3. **"System Cards for AI-Based Decision-Making"** (2022)
   - Extends model cards to system-level documentation. Closer to agents since agents are systems, not just models.

4. **Foundation Model Transparency Index** (Stanford HAI, 2023-2024)
   - Scores providers on 100 transparency indicators. Establishes what should be documented about AI systems.

### Industry Precedents

- **OpenAI System Cards** (GPT-4, GPT-4o) — document capabilities, limitations, safety evaluations
- **Anthropic Model Cards** (Claude) — document capabilities and safety properties
- **Google DeepMind** — various safety documentation efforts

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

### Forward Research Directions

1. **"Agent Cards: Documentation Standards for LLM Agent Systems"** — Propose and validate an agent-specific documentation standard
2. **Automated agent card generation** — Tools that introspect agent configurations and generate documentation
3. **Agent capability benchmarking** — Standardized tests that populate the "Capabilities" section of agent cards
4. **IEEE 3394 integration** — Align agent documentation with the emerging IEEE standard for agent interoperability

---

## 7. Agent Development Methodology

**Status: WHITE SPACE (0-1 papers)**

### What Exists

1. **"Software Engineering for AI-Based Systems: A Systematic Mapping Study"** (Martínez-Fernández et al., JSS 2020)
   - Systematic review of SE practices for AI broadly. Identifies gaps in requirements engineering, design, testing, and maintenance. Foundational but not agent-specific.

2. **AgentSpec** (ICSE 2026)
   - Specification language for monitoring agent behavior. Implies a methodology where specs are written before deployment, but doesn't propose a full methodology.

### Industry Methodology Proposals (Blog Posts, Not Papers)

1. **Anthropic's "Building Effective Agents"** (Dec 2024)
   - Key principle: start with augmented LLM patterns (retrieval, tool use) before escalating to autonomous agents. Proposes a maturity ladder.

2. **LangChain's development guides** (2025)
   - Informal methodology: start simple → add tools → add memory → add multi-agent. Incremental complexity.

3. **Microsoft AutoGen's design philosophy**
   - Conversational patterns as the basis for multi-agent design.

### What a Methodology Would Cover

A software engineering methodology for agents would need to address each SDLC phase:

| Phase | Traditional SE | Agent Equivalent | Status |
|-------|---------------|------------------|--------|
| **Requirements** | User stories, specs | Agent capability spec, task scope, safety requirements | No methodology |
| **Design** | Architecture diagrams, interfaces | Pattern selection, tool selection, prompt design, guardrail design | No methodology |
| **Implementation** | Coding, code review | Prompt engineering, tool integration, agent configuration, prompt review | No methodology |
| **Testing** | Unit/integration/e2e tests | Eval suites, red teaming, scenario testing, regression testing | Emerging (2025-2026) |
| **Deployment** | CI/CD, blue-green, canary | Agent deployment, shadow mode, canary agents | No methodology |
| **Monitoring** | APM, alerting, dashboards | Agent observability, SLA monitoring, behavior monitoring | Emerging (AgentSLA) |
| **Maintenance** | Bug fixes, updates, refactoring | Prompt updates, model migration, eval maintenance, debt paydown | No methodology |

### Forward Research Directions

1. **"Agent Development Lifecycle"** — Propose and validate an end-to-end methodology for building agent systems, from requirements through maintenance
2. **Agent requirements engineering** — How to specify what an agent should and shouldn't do (functional + safety requirements)
3. **Agent design review** — Structured review process for agent architectures before implementation
4. **Prompt review practices** — Code review equivalent for prompts and agent configurations
5. **Agent maturity model** — Levels of agent development maturity (ad-hoc → managed → optimizing), similar to CMMI

---

## 8. Agent CI/CD

**Status: EMERGING (2-3 tangential papers, 6+ industry tools)**

The second topic where industry has outpaced academia.

### Academic Papers

1. **"An Empirical Study of Testing Practices in Open Source AI Agent Frameworks"** (arXiv:2509.19185, Sept 2025)
   - First empirical baseline of testing practices across agent frameworks. Taxonomy of 10 testing patterns. Closest work to understanding how agents are tested in pipelines.

2. **"The Rise of Agentic Testing: Multi-Agent Systems for Robust Software Quality Assurance"** (arXiv:2601.02454, Jan 2026)
   - Proposes closed-loop multi-agent testing framework where agents test other agents. Implications for CI pipelines.

3. **"Towards Automated Functional Testing of LLM-Based Agents"** (Jan 2026)
   - Structural testing methodologies for agents that could integrate into CI pipelines.

### Industry CI/CD Tools

| Tool | Type | CI/CD Capability |
|------|------|-----------------|
| **promptfoo** | Open-source eval framework | CLI designed for CI pipelines; regression testing, red teaming |
| **Braintrust** | Eval platform | Logging, scoring, regression detection pre-deployment |
| **Patronus AI** | Eval + red-teaming | Automated guardrails and evaluation in deployment pipelines |
| **LangSmith** | Dev platform | Dataset management, experiment tracking, testing |
| **Arize Phoenix** | Open-source observability | Trace-based evaluation, pre-deployment testing |
| **AgentOps** | Agent observability | Session recording, regression flagging |

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

**Status: WHITE SPACE (0 papers)**

### What Exists

Zero dedicated papers on A/B testing for LLM agents. The closest work:

1. **"Chatbot Arena"** (Zheng et al., ICML 2024)
   - Open platform for evaluating LLMs through human preference using Elo-based ranking. Focused on chatbots, not agents, but establishes comparative evaluation methodology.

2. **"Judging LLM-as-a-Judge"** (Zheng et al., NeurIPS 2023)
   - Automated judge methodology for comparing LLM outputs. Prerequisite for scalable A/B testing of agents.

### Industry Practices (Undocumented)

- **Shadow mode** — Run new agent alongside old, compare outputs without user exposure
- **Canary deployments** — Route small percentage of traffic to new agent variant
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

**Status: WHITE SPACE for agents (3+ papers for AI broadly)**

### What Exists (AI Broadly, Not Agent-Specific)

1. **AI Incident Database** (McGregor, AAAI 2021)
   - URL: https://incidentdatabase.ai/
   - Catalogues 700+ real-world AI incidents. Not agent-specific but includes chatbot failures, autonomous system failures. Primary data source.

2. **OECD AI Incident Monitor** (2024)
   - Classifies AI incidents by type, severity, sector. Taxonomic framework applicable to agents.

3. **NIST AI Risk Management Framework** (AI 100-1, 2023)
   - General framework for managing AI risks including incident response guidelines. Not agent-specific.

4. **"Towards a Science of AI Agent Reliability"** (Princeton, Feb 2026)
   - Defines 12 reliability metrics across 4 dimensions. Closest work to establishing what constitutes an "agent incident."

### SRE → Agent Incident Response Mapping

| SRE Concept | Agent Equivalent | Academic Treatment |
|-------------|------------------|-------------------|
| **Runbook** | Agent failure playbook (loop detection, hallucination recovery, tool failure) | None |
| **Severity Levels** | P0: data loss/corruption; P1: agent stuck/looping; P2: poor quality output | None |
| **Post-Mortem** | Root cause: bad tool output? wrong plan? context overflow? model regression? | None |
| **Error Budget** | Acceptable failure rate before human takeover mandated | None |
| **Circuit Breaker** | Automatic agent shutdown on repeated failures | Practitioner blogs only |
| **Rollback** | Revert agent to previous version/config on failure | None (white space in Dim 1) |
| **Alerting Rules** | Thresholds for paging humans about agent behavior | None |
| **Blameless Culture** | Agent failures as learning opportunities, not blame targets | None |

### What's Missing

- **No incident taxonomy** for agent-specific failures (distinct from general AI incidents)
- **No severity classification** standard for agent incidents
- **No post-mortem methodology** adapted for agent failures
- **No error budget framework** for agent reliability
- **No runbook templates** for common agent failures (infinite loop, hallucination cascade, tool failure, context overflow)
- **No on-call practices** for agent operations teams

### Forward Research Directions

1. **Agent incident taxonomy** — Classify agent-specific incidents by type, root cause, severity, and remediation
2. **Agent post-mortem methodology** — Structured analysis framework for understanding why agents failed
3. **Error budgets for agents** — Formal framework for acceptable failure rates across different agent tasks
4. **Automated incident detection** — Real-time detection of agent anomalies that constitute incidents
5. **Agent SRE practices** — Adapt SRE discipline (error budgets, SLOs, toil reduction) for agent operations

---

## 11. Agent Capacity Planning

**Status: WHITE SPACE for agents (5+ papers for LLM serving)**

### What Exists (LLM Serving, Not Agent-Specific)

1. **"Astraea: Towards Fair and Efficient Learning-based Congestion Control for LLM Serving"** (2025)
   - Resource allocation for LLM serving. Proves scheduling is NP-hard for LLM workloads.

2. **Llumnix** (OSDI 2024)
   - Dynamic scheduling for LLM inference including preemptive scheduling and GPU migration.

3. **"Efficient Agents"** (2025)
   - Token consumption patterns across agent architectures. Foundational data for capacity planning.

4. **BudgetThinker** (2025)
   - Models computational budget allocation across reasoning steps.

5. **BATS** (2025)
   - Task scheduling under budget constraints for multi-agent systems. Includes token/compute cost models.

6. **SPAgent** (2025)
   - Adaptive model routing for cost/performance optimization.

### Industry Approaches

- **Inference cost calculators** — OpenAI, Anthropic, Google provide token-based pricing
- **LLM routers** — Martian, Portkey, LiteLLM route to cheaper models when possible
- **Auto-scaling engines** — vLLM, TGI, TensorRT-LLM provide scaling for LLM inference

### What Agent Capacity Planning Needs

| Planning Aspect | Description | Current State |
|----------------|-------------|---------------|
| **Token budget prediction** | Tokens needed for agent X on task type Y | Partial (BATS, BudgetThinker) |
| **Concurrency modeling** | How many agents can run simultaneously | No treatment |
| **Scaling laws for agents** | How quality/cost scales with resources | No treatment |
| **Burst capacity** | Handling demand spikes for agent workloads | No treatment |
| **Multi-model costing** | Cost prediction for agents using multiple models | Partial (SPAgent) |
| **Tool call overhead** | External API call costs in agent pipelines | No treatment |
| **Memory storage costs** | Long-term memory storage at scale | No treatment |
| **End-to-end cost prediction** | Total cost of agent task completion | No treatment |

### Forward Research Directions

1. **Agent scaling laws** — Empirical study of how agent quality, cost, and latency scale with compute (analogous to Kaplan/Chinchilla scaling laws for LLMs)
2. **Task-aware capacity models** — Predict resource needs based on task type, complexity, and agent architecture
3. **Multi-tenant capacity planning** — Resource allocation for shared agent infrastructure serving multiple users/orgs
4. **Agent workload characterization** — Empirical profiles of real agent workloads (burstiness, seasonality, task mix)
5. **Cost prediction models** — Given an agent config and task description, predict total cost before execution

---
---

## Cross-Cutting Analysis

### The Maturity Gap

Traditional software engineering has had **60+ years** to develop its practices. Agent engineering has had **~3 years** (since ChatGPT, Nov 2022). The gap is predictable — but the speed of agent adoption means we can't wait 60 years to close it.

| Discipline | Traditional SE Milestone | Year | Agent Equivalent | Year |
|-----------|------------------------|------|------------------|------|
| Design Patterns | GoF Book | 1994 | — | Not yet |
| Refactoring | Fowler's Book | 1999 | — | Not yet |
| CI/CD | Continuous Integration | 2000 | Industry tools only | 2024-2025 |
| DevOps/SRE | Google SRE Book | 2016 | — | Not yet |
| Technical Debt | Cunningham's metaphor | 1992 | — | Not yet |
| A/B Testing | Web experimentation | 2000 | — | Not yet |
| Incident Response | PagerDuty/SRE practices | 2010s | — | Not yet |

### Industry vs. Academia Divergence

A distinctive feature of Dimension 6 is the **industry-academia gap**:

- **Industry has tools** (LangSmith, AgentOps, Braintrust, promptfoo, Helicone) but **no theory**
- **Academia has neither** — it hasn't even started on most topics

This creates risks:
1. **Tools without foundations** — industry tools make implicit assumptions about what to measure and optimize, without theoretical justification
2. **No evaluation criteria** — how do we know which observability tool is better? No framework exists
3. **Fragmented standards** — each tool defines its own metrics, formats, and practices, leading to vendor lock-in

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

Based on impact and feasibility, these are the highest-priority papers that could be written:

| Priority | Paper | Why |
|----------|-------|-----|
| **1** | "Design Patterns for LLM Agent Systems" | Names and formalizes what practitioners already do; immediate practical value |
| **2** | "Technical Debt in LLM Agent Systems" | Empirical study extending Google's 2015 framework; high citation potential |
| **3** | "Agent Cards: Documentation Standards for Agentic AI" | Extends model cards; regulatory relevance (EU AI Act) |
| **4** | "Agent Smells: Anti-Patterns in LLM Agent Development" | Pairs with design patterns; direct practitioner value |
| **5** | "The Agent Development Lifecycle" | First comprehensive SE methodology for agents; fills the biggest process gap |
| **6** | "Agent CI/CD: Continuous Delivery for Agentic Systems" | Reference architecture; bridges industry practice and academic framework |
| **7** | "SRE for Agents: Incident Response and Reliability Engineering" | Adapts proven SRE discipline; immediate operational value |

