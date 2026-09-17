# EU AI Act & Open Source — A Living Compliance Guide

> **Not legal advice.** A collaboratively maintained summary of how the [EU AI Act](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng) (Regulation 2024/1689) affects open-source AI projects. Covers exemptions, obligations, community debates, compliance tooling, and a practical action checklist.

---

## 🕒 Key Dates

| Date | What Happens |
|------|-------------|
| **1 Aug 2024** | AI Act enters into force |
| **2 Feb 2025** | Prohibited practices (Art. 5) apply |
| **2 Aug 2025** | GPAI model obligations (Chapter V) apply |
| **2 Aug 2026** | Transparency obligations (Art. 50), GPAI Code of Practice, most provisions apply |
| **27 Jul 2026** | Digital Omnibus on AI enters into force (deadline extensions) |
| **2 Dec 2027** | Annex III high-risk obligations apply (extended by Omnibus) |
| **2 Aug 2028** | Annex I high-risk obligations apply (extended by Omnibus) |

---

## ⚖️ The Two Open-Source Carve-Outs (And What They Don't Cover)

The AI Act has **two independent** open-source provisions. They are narrower than most people assume.

### Carve-Out 1: Article 2(12) — General OSS Exemption

```
"This Regulation does not apply to AI systems released under free and 
open-source licences, unless they are placed on the market or put into 
service as high-risk AI systems or as an AI system that falls under 
Article 5 or 50."
```

**What it means:** If your OSS AI system is *not* high-risk, *not* prohibited, and *not* subject to transparency obligations — you're largely out of scope. But that's a narrow set of systems. Most generative AI systems trigger Article 50 transparency rules, which apply regardless of licence.

### Carve-Out 2: Article 53(2) — GPAI Model OSS Carve-Out

Providers of qualifying open-source GPAI models are exempt from:
- **Art. 53(1)(a)** — Technical documentation for the AI Office
- **Art. 53(1)(b)** — Downstream provider documentation (Annex XII)

**But you STILL must:**
- ✅ **Art. 53(1)(c)** — Maintain a copyright compliance policy (respect text-and-data-mining opt-outs under the EU Copyright Directive)
- ✅ **Art. 53(1)(d)** — Publish a "sufficiently detailed summary" of training data using the [AI Office template](https://digital-strategy.ec.europa.eu/en/library/explanatory-notice-and-template-public-summary-training-content-general-purpose-ai-models)

**And the carve-out vanishes if:**
- Your model has **systemic risk** (training compute > 10²⁵ FLOPs, or designated by the Commission)

### What Counts as "Free and Open-Source"?

Recital 102 says the licence must allow users to **run, copy, distribute, study, change, and improve** the model. Attribution (e.g., Apache 2.0 notice) and copyleft terms (GPL-family) are fine. But:

- **Weights-only releases** with no architecture/usage info → do **not** qualify for Art. 53(2)
- **Licences with use restrictions** (e.g., no commercial use, no competitor use) → likely do **not** qualify
- **Research-only or non-commercial licences** → unlikely to qualify
- **Monetised models** (paid support, platform fees, personal-data monetisation) → excluded per Recital 103

> ⚠️ **Meta's Llama, Stability AI's models, and others with custom "open" licences** sit in a grey zone. The AI Office has not yet published definitive guidance on whether these qualify.

---

## 🎯 What This Means for Your OSS Project

### If you release a non-GPAI tool (library, framework, CLI, MLOps tool)
→ **Likely not directly regulated.** The AI Act targets AI *systems* and GPAI *models*, not general-purpose software tools. If your tool doesn't infer from inputs to generate outputs, it's probably out of scope.

### If you release an open-source GPAI model (LLM, image generator, etc.)

| Your situation | Your obligations |
|---------------|-----------------|
| Below 10²⁵ FLOPs, full OSS licence, weights + architecture + usage info public | Copyright policy + training-data summary only |
| Below 10²⁵ FLOPs, but weights-only release | Full Art. 53(1)(a)-(d) (no carve-out) |
| Above 10²⁵ FLOPs (systemic risk) | Full obligations: evaluation, adversarial testing, incident reporting, cybersecurity, copyright, data summary |
| Any GPAI model, any licence | Copyright policy + training-data summary ALWAYS apply |

### If you deploy an AI system (chatbot, SaaS, Gradio app, etc.)

| Risk level | Obligations |
|-----------|------------|
| **Minimal risk** (spam filter, video game AI) | No AI Act obligations |
| **Limited / Transparency risk** (chatbot, image generator) | Disclose AI interaction, mark synthetic content (Art. 50) — applies from Aug 2026 |
| **High risk** (CV screening, credit scoring, biometrics, critical infrastructure, law enforcement, etc.) | Full stack: risk management (Art. 9), data governance (Art. 10), technical docs (Art. 11), logging (Art. 12), transparency to deployers (Art. 13), human oversight (Art. 14), accuracy/robustness (Art. 15), conformity assessment (Art. 43) |
| **Prohibited** (social scoring, real-time remote biometric ID, subliminal manipulation) | Banned outright — applies since Feb 2025 |

> 🔑 **The downstream rule:** Even if you use a fully-exempt open-source model, *your* AI system is classified by what *it* does, not by what model it runs on. If your chatbot is used for CV screening (Annex III), you're the provider of a high-risk system.

---

## 🗣️ Community Debates & Policy Flashpoints

### 1. The "Open-Washing" Fight
A major tension: companies release models under restrictive "open" licences (e.g., Llama's acceptable-use policy, research-only terms) and claim OSS status. The [Open Source Initiative (OSI)](https://opensource.org/) released its [Open Source AI Definition](https://opensource.org/deepdive/drafts/open-source-ai-definition) in October 2024, requiring full freedoms including use for any purpose. The EU AI Act does not reference this definition, leaving a regulatory gap.

### 2. The GPAI Code of Practice Battle
- The **GPAI Code of Practice** was published **10 July 2025** after a multi-stakeholder process with ~1,000 participants
- **Early drafts** mandated acceptable-use policies that would have conflicted with OSS principle #6 (no discrimination against fields of endeavor)
- **OSI intervened** with a coalition letter; the **third draft (March 2025)** made AUPs optional and exempted open-source AI from downstream-use prohibitions
- The Code remains **voluntary** but will heavily influence future harmonised standards

### 3. GitHub's Position
GitHub has been the leading voice for OSS in Brussels since 2021:
- **CEO Thomas Dohmke** addressed policymakers calling for a developer exemption
- **CLO Shelley McKinley** argued the Act "strikes the right balance" but warned that without the OSS exemption, "developers would pull back on upstream contributions"
- GitHub co-authored a position paper with Creative Commons, EleutherAI, Hugging Face, LAION, and Open Future

### 4. The Digital Omnibus (2026)
Adopted mid-2026 (Regulation 1744/2026), the Omnibus:
- Extended Annex III high-risk deadlines to Dec 2027
- Extended Annex I high-risk deadlines to Aug 2028
- Added new Article 5 prohibitions (e.g., non-consensual AI-generated intimate content)
- Raised SME thresholds to 750 employees
- Did **not** change the OSS carve-outs substantively

### 5. The Transparency Paradox
Open Future noted in December 2023 that the current compromise creates a paradox: open-source GPAI models can actually get away with **less** transparency than proprietary ones (exempt from technical docs and downstream info), which was described as a "Frankenstein-like approach."

### 6. Copyright — The Sleeping Giant
Article 53(1)(c) applies to **all** GPAI providers, OSS included. If a rights-holder has expressed a text-and-data-mining opt-out under the EU Copyright Directive, your model must not have been trained on that content. This is potentially the most disruptive requirement for OSS models trained on web-scale data.

---

## 🛠️ Compliance Toolkit for OSS Projects

### Documentation (you probably already do some of this)
- **[Hugging Face Model Cards](https://huggingface.co/docs/hub/en/model-cards)** — Standardised model documentation; maps well to Annex IV requirements
- **[Model Card Toolkit (Google)](https://github.com/tensorflow/model-card-toolkit)** — Automate model card generation
- **[AI FactSheets 360 (IBM)](https://aifs360.res.ibm.com/)** — Comprehensive factsheets

### Transparency & Watermarking
- **[Gradio Watermarking](https://huggingface.co/spaces/gradio/watermark)** — Built-in tools for marking AI-generated content
- **[AI Disclosure Kit](https://disclosekit.com)** — Generates Article 50 disclosure templates

### Risk Classification & Compliance
- **[EU AI Act Compliance Checker (FLI)](https://artificialintelligenceact.eu/assessment/eu-ai-act-compliance-checker/)** — Free tool to determine if your system falls under AI Act obligations
- **[EU AI Act Compliance Checker (EC Official)](https://ai-act-service-desk.ec.europa.eu/en/eu-ai-act-compliance-checker)** — Official beta tool from the Commission
- **[Opencomplai](https://github.com/Opencomplai/opencomplai)** — Code-first AI compliance engine; integrates into CI/CD
- **[VerifyWise](https://github.com/verifywise-ai/verifywise)** — OSS AI governance platform supporting EU AI Act, ISO 42001, NIST AI RMF
- **[EuConform](https://github.com/Hiepler/EuConform)** — Risk classification, bias detection, Annex IV PDF reports — 100% offline

### Training-Data Summary
- **[AI Office Template](https://digital-strategy.ec.europa.eu/en/library/explanatory-notice-and-template-public-summary-training-content-general-purpose-ai-models)** — Mandatory template for Art. 53(1)(d)

### Copyright Compliance
- **[Hugging Face Opt-Out Support](https://huggingface.co/blog/eu-ai-act-for-oss-developers#copyright)** — Tools for respecting TDM opt-outs

### MCP / Agent Tools
- **[MCP EU AI Act Scanner](https://github.com/ark-forge/mcp-eu-ai-act)** — Scans codebases for compliance gaps
- **[Microsoft Agent Governance Toolkit](https://github.com/microsoft/agent-governance-toolkit)** — Runtime governance for autonomous agents with EU AI Act mappings

---

## 📋 Quick Self-Assessment Checklist

- [ ] **Is my project an "AI system"?** (Does it infer from inputs to generate outputs?)
- [ ] **Is my project a "GPAI model"?** (Trained on large data, significant generality, wide range of tasks?)
- [ ] **Am I using a genuinely free & open-source licence?** (Apache 2.0, MIT, GPL-family — not restricted-use custom licences)
- [ ] **Do I publish weights, architecture info, AND usage info?** (All three needed for Art. 53(2) carve-out)
- [ ] **Is my model above 10²⁵ FLOPs?** (If yes, full obligations regardless of licence)
- [ ] **Do I have a copyright compliance policy?** (Required for ALL GPAI providers, OSS or not)
- [ ] **Have I published a training-data summary?** (Using the AI Office template)
- [ ] **Does my deployed system interact with end users?** (If yes, Art. 50 transparency applies)
- [ ] **Does my system fall into an Annex III high-risk category?** (Employment, credit, biometrics, law enforcement, critical infrastructure, etc.)
- [ ] **Have I checked if my system is prohibited under Art. 5?** (Social scoring, real-time biometric ID, manipulation, etc.)

---

## 📚 Key Resources

### Official
- [Full AI Act Text (EUR-Lex)](https://eur-lex.europa.eu/eli/reg/2024/1689/oj/eng)
- [EU AI Office](https://digital-strategy.ec.europa.eu/en/policies/ai-office)
- [GPAI Code of Practice (Final)](https://code-of-practice.ai/)
- [AI Act Single Information Platform](https://ai-act-service-desk.ec.europa.eu/en)
- [Guidelines on GPAI Provider Obligations](https://digital-strategy.ec.europa.eu/en/policies/guidelines-gpai-providers)

### Expert Analysis
- [EU AI Act & Open Source: What's Exempt and What Isn't (euai-act.com)](https://www.euai-act.com/articles/open-source-ai-eu-ai-act)
- [Open-Source AI: Where the Exemptions Stop (Confir)](https://confir.eu/eu-ai-act/open-source-models)
- [Open Source Developers Guide (Hugging Face)](https://huggingface.co/blog/eu-ai-act-for-oss-developers)
- [What OSS Developers Need to Know (Linux Foundation Europe)](https://linuxfoundation.eu/newsroom/ai-act-explainer)
- [AI Act and Open Source Observatory (Open Future)](https://openfuture.eu/observatory/aia-open-source/)
- [Ensuring Open Source AI Thrives (OSI)](https://opensource.org/blog/ensuring-open-source-ai-thrives-under-the-eus-new-ai-rules)

### Community & News
- [The EU AI Act Newsletter (Risto Uuk / FLI)](https://artificialintelligenceact.substack.com/) — Biweekly, most detailed implementation updates
- [Awesome EU AI Act (GitHub)](https://github.com/GenAI-Gurus/awesome-eu-ai-act) — Curated tools, templates, and guides
- [AI Act Explorer (FLI)](https://artificialintelligenceact.eu/ai-act-explorer/) — Interactive browsing of the full regulation
- [Digital Omnibus Tracker](https://agentliability.eu/tools/omnibus-tracker/) — Provision-by-provision tracker of Omnibus changes

---

## 🤝 Contributing

This is a **living document**. The regulatory landscape is evolving rapidly. Contributions are welcome:

1. **Corrections & updates** — If a deadline has changed or new guidance has been published
2. **New tools** — Add compliance tools useful for OSS projects
3. **Case studies** — How your OSS project is handling compliance
4. **Translations** — Help make this guide accessible in more languages
5. **Policy analysis** — Links to new expert takes, court decisions, or enforcement actions

Please open a PR or issue. See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## ⚠️ Disclaimer

This guide is for **informational purposes only** and does not constitute legal advice. The EU AI Act is complex, evolving, and subject to interpretation by courts and regulators. Consult qualified legal counsel for your specific situation.

---

## 📄 License

[CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/) — Dedicated to the public domain. Use freely, no attribution required (though appreciated).