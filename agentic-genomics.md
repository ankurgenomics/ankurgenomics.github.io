---
layout: page
title: "Agentic Genomics -- Portfolio"
permalink: /agentic-genomics/
---

# Agentic Genomics

*Ankur Sharma, PhD -- Singapore*

Systems that connect genomic data to real-world decisions using agentic AI.

---

## Reviewer2

**Autonomous ACMG variant second reviewer -- LangGraph + FastMCP + MCP Server**

[![GitHub](https://img.shields.io/badge/GitHub-Reviewer2-blue)](https://github.com/ankurgenomics/Reviewer2)
[![Tests](https://img.shields.io/badge/tests-21%20passing-brightgreen)](https://github.com/ankurgenomics/Reviewer2/tree/main/tests)
[![CI](https://github.com/ankurgenomics/Reviewer2/actions/workflows/ci.yml/badge.svg)](https://github.com/ankurgenomics/Reviewer2/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/ankurgenomics/Reviewer2/blob/main/LICENSE)

Clinical variant classification uses a 28-criterion framework (ACMG/AMP 2015). Applying it consistently is hard -- trained analysts disagree on edge cases more than the field admits, and manual peer review does not scale. Reviewer2 automates the second review step.

Give it a variant and a proposed classification. It fetches the relevant evidence, applies the ACMG criteria deterministically, and tells you exactly where its call differs from yours -- with the specific evidence sentence grounding every criterion it fires. If the evidence is not there, the criterion does not fire. That constraint is enforced at the Pydantic model level, not by convention.

**Architecture:**
- `normalise` -- parses variant input, resolves gene and consequence
- `fetch_evidence` -- retrieves allele frequency, functional data, in-silico predictions via `EvidenceProvider` protocol (RAG-ready, swappable)
- `score_acmg` -- applies ACMG 2015 criteria deterministically in pure Python (no LLM in the scoring loop)
- `detect_conflicts` -- compares engine call to proposed call, gates on action band (act / monitor / do-not-act)

**What makes it different:**
- Pydantic v2 validators enforce evidence grounding at the model level -- the pipeline physically cannot fire a criterion without attaching evidence
- LLM is provider-agnostic: Ollama locally, Anthropic / OpenAI / Gemini as drop-ins
- Exposed as a FastMCP server so any agent that speaks Model Context Protocol can call it as a tool
- Evaluation runs against expert-panel ClinVar classifications the engine never sees; out-of-scope cases reported honestly

**Evaluation:** 86% action-band concordance on in-scope cases vs expert-panel ClinVar (ClinGen VCEP / 3-star)

```bash
git clone https://github.com/ankurgenomics/Reviewer2
cd Reviewer2 && uv sync
uv run reviewer2 demo                          # 3 live cases, no API key with Ollama
uv run python -m reviewer2.mcp_server          # start MCP server on stdio
```

**Repo:** [github.com/ankurgenomics/Reviewer2](https://github.com/ankurgenomics/Reviewer2)

---

## outbreak-agent

**Infectious disease triage with LangGraph -- built around MV Hondius / ANDV 2026**

[![GitHub](https://img.shields.io/badge/GitHub-outbreak--agent-blue)](https://github.com/ankurgenomics/outbreak-agent)
[![Tests](https://img.shields.io/badge/tests-33%20passed-brightgreen)](https://github.com/ankurgenomics/outbreak-agent/tree/main/tests)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://github.com/ankurgenomics/outbreak-agent/blob/main/LICENSE)

A 4-node LangGraph state machine that triages infectious disease outbreak cases --
combining genomic analysis, contact linkage, risk scoring, and a self-correcting
critic loop that re-evaluates when outputs are inconsistent.

**What it produces on every run -- no API key required:**

![outbreak-agent risk dashboard](/assets/img/ANDV-2026-001-risk-dashboard-2026-05-09.png)

*Risk scores across 4 outbreak scenarios (left), event timeline showing 48-72h human
analyst window vs under-2h agent window (centre), contact cluster growth on MV Hondius
(right).*

**Architecture:**
- `genomic_node` -- clade identification, mutation flags, genome completeness
- `linkage_node` -- contact cluster resolution, transmission mode inference
- `risk_node` -- composite score 0-100, tier: LOW / MEDIUM / HIGH / CRITICAL
- `critic_node` -- consistency audit, loops back up to 3x if flags raised

**MV Hondius result:** CRITICAL (98/100) -- approved by critic in 1 loop, under 2 seconds.

**Blog post:** [When an AI Agent Boards a Cruise Ship: Hantavirus, LangGraph, and the Future of Outbreak Triage](https://ankurgenomics.github.io/2026/05/09/hantavirus-cruise-ship-agentic-ai.html)

**Repo:** [github.com/ankurgenomics/outbreak-agent](https://github.com/ankurgenomics/outbreak-agent)

```bash
git clone https://github.com/ankurgenomics/outbreak-agent
cd outbreak-agent
pip install -r requirements.txt
python demo.py --case hondius
```

---

## GenomicsCopilot (agentic-genomics)

**Reasoning-traceable variant interpretation -- LangGraph + Claude API**

[![GitHub](https://img.shields.io/badge/GitHub-agentic--genomics-blue)](https://github.com/ankurgenomics/agentic-genomics)

7-node LangGraph multi-agent pipeline: VCF ingest → gnomAD/ClinVar annotation →
frequency filtering → HPO phenotype scoring → ACMG-lite classification → LLM synthesis
→ LLM critic for fact-checking. Every call produces a full audit trail.

- Streamlit UI + Typer CLI
- 51 tests, 81% coverage, CI/CD via GitHub Actions
- MCP-compatible architecture; vector store-ready RAG design
- Stack: LangGraph, Claude/Anthropic API, Pydantic v2, pysam, Streamlit

```bash
pip install agentic-genomics
genomics-copilot analyze variants.vcf --phenotypes HPO:0001250
```

**Repo:** [github.com/ankurgenomics/agentic-genomics](https://github.com/ankurgenomics/agentic-genomics)

---

## genomics-skills

**Agent-callable skill library -- 8 production genomics tools**

[![GitHub](https://img.shields.io/badge/GitHub-genomics--skills-blue)](https://github.com/ankurgenomics/genomics-skills)

Modular library of 8 production Python skills, each agent-discoverable with a SKILL.md
contract, CLI entrypoint, and deterministic outputs (TSV + PNG/SVG).

Skills: TCGA pan-cancer expression (9,479 real samples) · Kaplan-Meier / Cox PH survival
· GO/KEGG enrichment · PubMed NLP digest · Protein variant mapping · 3D structure viewer
· Volcano plots

LLM-powered routing via Claude Haiku maps natural-language queries to the right skill.

**Repo:** [github.com/ankurgenomics/genomics-skills](https://github.com/ankurgenomics/genomics-skills)

---

## gwas_nf

**Genome-wide association study pipeline -- Nextflow DSL2**

[![GitHub](https://img.shields.io/badge/GitHub-gwas__nf-blue)](https://github.com/ankurgenomics/gwas_nf)

Production Nextflow pipeline for GWAS analysis. Handles QC, population stratification,
association testing, and result visualisation. Designed for AWS Batch and HPC
environments.

**Repo:** [github.com/ankurgenomics/gwas_nf](https://github.com/ankurgenomics/gwas_nf)

---

## Writing

[When an AI Agent Boards a Cruise Ship: Hantavirus, LangGraph, and the Future of Outbreak Triage](https://ankurgenomics.github.io/2026/05/09/hantavirus-cruise-ship-agentic-ai.html)
-- Full write-up: biology, architecture, critic loop, and design decisions behind `outbreak-agent`.

---

## Contact

- LinkedIn: [linkedin.com/in/ankurit](https://linkedin.com/in/ankurit)
- GitHub: [github.com/ankurgenomics](https://github.com/ankurgenomics)
- Email: [ankurs103@gmail.com](mailto:ankurs103@gmail.com)
