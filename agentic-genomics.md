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

**Blog post:** [When an AI Agent Boards a Cruise Ship](https://ankurgenomics.github.io/2026/05/09/hantavirus-cruise-ship-agentic-ai.html)

**Repo:** [github.com/ankurgenomics/outbreak-agent](https://github.com/ankurgenomics/outbreak-agent)

```bash
git clone https://github.com/ankurgenomics/outbreak-agent
cd outbreak-agent
pip install -r requirements.txt
python demo.py --case hondius
```

---

## GenomicsCopilot

*In development -- agentic genomics platform connecting sequencing pipelines to
clinical decision support. Private modules available to institutional collaborators.*

Contact [ankurs103@gmail.com](mailto:ankurs103@gmail.com) with institutional affiliation.

---

## Contact

- LinkedIn: [linkedin.com/in/ankurit](https://linkedin.com/in/ankurit)
- GitHub: [github.com/ankurgenomics](https://github.com/ankurgenomics)
- Email: [ankurs103@gmail.com](mailto:ankurs103@gmail.com)
