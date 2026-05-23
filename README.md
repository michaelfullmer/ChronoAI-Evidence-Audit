# ChronoAI Evidence Audit Tool

**Verifies sourcing. Not truth. Unsourced = unverifiable.**

A standalone, open-source tool for classifying factual claims in any text — AI-generated responses, academic excerpts, relay transcripts, news articles, or anything else. Built on research conducted at ChronoAI Solutions into AI fabrication mechanics and epistemic drift.

> *"The tool doesn't verify truth. It verifies sourcing. The standard is consistent regardless of accuracy — an unsourced claim is an unverifiable claim, whether it came from a machine or a human."*

---

## Why This Exists

AI systems generate text that looks authoritative whether or not the underlying claims are real. The fabrication isn't intentional — it's architectural. Models trained on authoritative text learn to produce authoritative-sounding output, including statistics, citations, and empirical claims that don't exist.

The danger isn't the individual fabrication. It's the citation chain:

```
Document A (AI-assisted) → includes fabricated statistic
Document B → cites Document A as a source  
Document C → treats it as established knowledge
```

By Document C, the fabrication has inherited the credibility of everything around it. There's no flag. There's no seam.

This tool creates a mandatory checkpoint between AI output and acceptance — surfacing what is sourced and what isn't before fabricated claims enter the record.

---

## Features

- **Multi-provider support** — works with Groq (free tier), OpenAI, or any OpenAI-compatible API
- **Single block mode** — audit any text passage, AI response, or article excerpt
- **Relay transcript mode** — audit multi-speaker conversations with per-speaker classification
- **Three claim types** — Technical, Performance Narrative, Opinion — each with appropriate risk levels
- **High-risk first sorting** — unsourced performance metrics surface immediately
- **Export** — download full audit report as plain text
- **No backend required** — runs entirely in the browser with your own API key
- **No data collection** — your key and content go directly to your chosen provider, nowhere else

---

## Quick Start

**Option 1 — Run directly in browser (no install)**

1. Download `evidence_audit.html`
2. Open it in any browser
3. Get a free Groq API key at [console.groq.com](https://console.groq.com)
4. Paste your key in the configuration panel
5. Paste any text and click **RUN AUDIT**

**Option 2 — Host it yourself**

Drop `evidence_audit.html` on any static host (GitHub Pages, Netlify, your own server). No build process, no dependencies, no backend.

**Option 3 — Server proxy (for Anthropic)**

Anthropic's API blocks direct browser calls due to CORS. If you want to use Claude models, deploy the server proxy version. See [`/server-proxy`](/server-proxy) for the Node.js Express endpoint — same pattern as NexusAI.

---

## Provider Setup

| Provider | Cost | Setup | CORS |
|----------|------|-------|------|
| **Groq** | Free tier available | [console.groq.com](https://console.groq.com) | ✅ Works directly |
| **OpenAI** | Pay per use | [platform.openai.com](https://platform.openai.com) | ✅ Works directly |
| **Anthropic** | Pay per use | [console.anthropic.com](https://console.anthropic.com) | ⚠️ Requires server proxy |

Groq's free tier is fast enough for audit tasks and costs nothing. Start there.

---

## Claim Classification

| Type | Description | Risk if Unsourced |
|------|-------------|-------------------|
| **PERFORMANCE_NARRATIVE** | Metrics, percentages, benchmarks, session counts, improvement figures, comparative results | 🔴 HIGH |
| **TECHNICAL** | Code behavior, system architecture, verifiable technical assertions | 🟡 MEDIUM |
| **OPINION** | Interpretation, framing, editorial judgment | 🟢 LOW |

**Sourcing rule:** Vague phrases like *"studies show," "experts agree," "research indicates"* are not sources. They get flagged.

---

## Relay Transcript Mode

Switch to **Relay Transcript** mode to audit multi-speaker conversations. The tool parses `SPEAKER NAME: message` format automatically.

Label each speaker as AI, Human, or Unknown before running. The audit applies the same sourcing standards to every speaker — human claims get audited the same as AI claims. This matters because:

- AI fabrication is unintentional and architectural
- Human fabrication can be intentional and targeted  
- The detection mechanism shouldn't care about intent

Example format:
```
INSTANCE A: Here's what I'm thinking about this problem...
INSTANCE B: That's an interesting framing. Studies show that...
HUMAN: I read that 91% accuracy has been achieved on these benchmarks...
```

---

## The Research Behind This

This tool emerged from a specific finding in ChronoAI's relay drift experiments:

In a two-instance AI relay, the framed instance (with an epistemic grounding prompt) caught a fabricated 3-qubit circuit claim immediately. But fabricated performance metrics — *"87% improvement across 2,400 sessions over 30 days"* — slipped through and were accepted as publication-worthy. No source was requested.

**The asymmetry:** Technical facts get checked against prior discussion. Plausible performance narratives get accepted and amplified.

The Evidence Audit Tool addresses the second half of that failure. It doesn't verify truth — it surfaces what's unsourced, consistently, regardless of how authoritative it sounds.

Full research documentation:
- [ChronoAI Unified Framework](https://chronoaisolutions.com) — three-pillar AI safety architecture
- [Relay Experiment Tool](https://github.com/michaelfullmer/ChronoAI-Relay-Experiment) — run the drift experiments yourself
- [MemoryBridge](https://github.com/michaelfullmer/Memory-Bridge) — AI memory file builder

---

## File Structure

```
ChronoAI-Evidence-Audit/
├── evidence_audit.html     # Complete standalone tool — single file, no dependencies
├── README.md               # This file
└── server-proxy/
    └── audit_proxy.js      # Node.js Express endpoint for Anthropic (CORS workaround)
```

---

## Built By

**Michael Fullmer** — Founder, ChronoAI Solutions  
Self-taught developer. Went from zero coding knowledge to a live production environment with 15+ deployed applications in 8 weeks. Works construction during the day, builds technology at night.

- [chronoaisolutions.com](https://chronoaisolutions.com)
- [github.com/michaelfullmer](https://github.com/michaelfullmer)
- [MemoryBridge](https://github.com/michaelfullmer/Memory-Bridge)

---
## Citation

If you use this tool or reference this research, please cite:

Fullmer, Michael. "Context as a Safety Mechanism: A Unified Framework for 
Quantum Context Routing, Relay Drift Experiments, and Evidence Audit Systems 
in AI Safety." ChronoAI Solutions, May 2026.

ORCID: 0009-0009-6926-3240  
GitHub: https://github.com/michaelfullmer/ChronoAI-Evidence-Audit  
Preprint DOI: https://doi.org/10.5281/zenodo.20351307

## License

MIT — use it, fork it, build on it. Credit appreciated, not required.

If this tool helps you catch something that would have slipped through, that's the whole point.
