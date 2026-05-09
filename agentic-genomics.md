---
layout: page
title: "Agentic Genomics -- Portfolio"
permalink: /agentic-genomics/
---

# Agentic Genomics

*Ankur Sharma, PhD -- Singapore*

Systems that connect genomic data to real-world decisions using agentic AI.

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
