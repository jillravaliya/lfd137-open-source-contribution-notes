# LFD137 — Open Source Contribution Notes

![Topics](https://img.shields.io/badge/Topics-06-000000?style=for-the-badge&logo=github&logoColor=white&labelColor=grey)
![Focus](https://img.shields.io/badge/Focus-Open%20Source-EE4444?style=for-the-badge&logo=opensourceinitiative&logoColor=white&labelColor=grey)
![Status](https://img.shields.io/badge/Status-In%20Progress-F5A623?style=for-the-badge&logo=buffer&logoColor=white&labelColor=grey)
![License](https://img.shields.io/badge/License-CC--BY--SA--4.0-1D96E8?style=for-the-badge&logo=creativecommons&logoColor=white&labelColor=grey)

> Notes built while going through LFD137 — rewritten around what actually matters for any developer contributing to open source.

---

## Purpose

LFD137 is a Linux Foundation course on open source contribution in the finance industry. The finance-specific regulatory content is niche. The open source knowledge underneath it is not.

This repository extracts and expands everything that matters universally:

- **How open source actually works** (the history, the politics, the governance)
- **What licenses actually do** (not definitions, real consequences)
- **How supply chains get attacked** (Log4Shell, dependency confusion, typosquatting)
- **What contribution looks like at scale** (OSPO, CLA, DCO, scanning)
- **Why export controls apply to code** (PGP history, crypto as munition, sanctions)
- **Why antitrust touches open source** (Linux Foundation lawyers exist for a reason)

Finance appears where it is useful context. It is not the subject.

---

## Repository Structure

### **[01-how-open-source-actually-works/](./01-how-open-source-actually-works/README.md)** 

> The real story behind open source — where it came from, how communities govern, and how companies fake it.

**Covers:**
- Stallman, Xerox printer, MIT AI Lab 1980
- The four freedoms and copyleft logic
- FSF vs OSI split — pragmatists vs idealists
- BDFL, foundation model, Python PEP process
- Openwashing — Llama 2, Terraform BSL switch
- FINOS — why competitors need neutral ground
- Full history (Unix → BSD → Linux → legal wars) → [unix-to-linux/](./01-how-open-source-actually-works/unix-to-linux/README.md)

---

### **[02-licenses-the-complete-picture/](./02-licenses-the-complete-picture/README.md)**
> What licenses actually do — the traps, the obligations, the real cost of choosing wrong.

**Covers:**
- Copyright by default — the GitHub trap
- MIT, Apache 2.0, GPL v2, LGPL, AGPL
- Patent grant — why MIT and Apache 2.0 are not the same
- GPL viral clause — what actually triggers it
- AGPL — the SaaS loophole and when it triggers
- CLA vs DCO — Schedule A problem, kernel choice
- SSPL and BSL — not open source, what OSI said

---

### **[03-supply-chain-security/](./03-supply-chain-security/README.md)** 🚧
> How open source dependencies become attack vectors — and what to do about it.

**Covers:**
- What a software supply chain is
- Log4Shell — JNDI injection, transitive dependency problem
- Dependency confusion, typosquatting, RepoJacking, PR sneaking
- SBOM — EO 14028, EU CRA, SPDX vs CycloneDX
- OSSF Scorecard and dependency evaluation
- Left-pad incident and approved repository architecture

---

### **[04-contribution-process-reality/](./04-contribution-process-reality/README.md)** 🚧
> What contribution approval looks like inside a large organisation.

**Covers:**
- What an OSPO is and what it actually does
- OSPO maturity levels — Reactive to Leading
- 6-stage contribution approval workflow
- Data leakage scanning — secrets, PII, git history
- CLA mechanics — what signing actually transfers
- How Goldman open-sourced Legend
- Conflicts of interest in contribution

---

### **[05-export-controls-and-sanctions.md/](./05-export-controls-and-sanctions.md)** 🚧
> Why cryptographic code is legally a weapon — and what that means for a developer.

**Covers:**
- Why code is treated as a physical export
- PGP story — Zimmermann, 1991, criminal investigation
- EAR and ITAR — ECCN 5E002, standard vs non-standard crypto
- Kernel crypto subsystem and compliance
- Tornado Cash — the code itself was sanctioned
- GitHub Iran incident, North Korean developers in open source

---

### **[06-antitrust-in-open-source/](./06-antitrust-in-open-source/README.md)** 🚧
> Why Google, Microsoft, and Meta contribute to the same kernel — and where the line is.

**Covers:**
- Why antitrust applies to open source
- Linux Foundation antitrust policy
- De facto standard risk — early contributor advantage
- Collaboration vs coordination — where the line is
- FDC3 and OpenMAMA — who shaped the standard

---

### **[linux-kernel-contribution/](./linux-kernel-contribution/README.md)** 🚧
> How Linux kernel contribution actually works — patches, maintainers, mailing lists.

**Covers:**
- Maintainer hierarchy — how patches reach Linus
- Mailing list culture — why there is no GitHub PR
- Patch lifecycle — commit format, git send-email, review
- DCO in practice — what Signed-off-by means legally
- Stable vs mainline — the difference
- Review culture — why harsh review is normal

---

## Context

- These notes were built alongside **[lfd103-linux-kernel-notes](https://github.com/jillravaliya/lfd103-linux-kernel-notes)** — which goes deep on how Linux actually works at the hardware level.
- LFD137 is the layer above: what happens when you want to contribute back to the ecosystem that runs everything.
- Topics are organized by concept rather than course order, with each file providing both depth (how it works) and context (why it matters).

---

## Learning Approach

> **Start with foundations, build incrementally:**

The files are designed to be read sequentially or referenced for specific topics. Each one dives deep into a single area with clear explanations of both mechanisms and reasoning.

**Philosophy:**
- Understand the why before the how
- Learn from real incidents, not hypothetical scenarios
- See the full picture — from license text to legal consequence
- Finance is context, not the subject

---

## What's Not Included

This repository does **not** cover:
- Bank communication regulations (WhatsApp fines, SEC Rule 17a-4)
- AML and anti-money laundering in open source
- Financial institution-specific OSPO structures
- Cross-border data transfer regulations

Focus is on **open source knowledge** that applies regardless of industry.

---

## License

- Documentation released under CC-BY-SA-4.0.

---

## Author

> Built by **Jill Ravaliya** while going through LFD137 and expanding what the course touches briefly.

**Focus Areas:**
- Open source ecosystem and contribution workflows
- Linux kernel development and internals
- Systems programming
- Supply chain security

**Currently Exploring:**
- Linux kernel contribution process
- Open source licensing and governance
- Upstream contribution workflows

---

## Connect With Me

I'm actively learning and building in the **open source** and **systems programming** space.

- **Email:** jillahir9999@gmail.com
- **LinkedIn:** [linkedin.com/in/jill-ravaliya-684a98264](https://linkedin.com/in/jill-ravaliya-684a98264)
- **GitHub:** [github.com/jillravaliya](https://github.com/jillravaliya)

**Open to:**
- Open source contribution discussions
- Kernel development collaboration
- Systems programming conversations
- Feedback on these notes

---

### ⭐ Star this repository if these notes help you understand open source contribution better.

---

> **Navigate to individual files for the full deep dives. Each one goes significantly further than the course material.**

<div align="center">

<img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=18&pause=1000&color=60A5FA&center=true&vCenter=true&width=600&lines=Open+Source+Is+Not+Just+a+License;It+Is+a+Legal+and+Political+System;Understanding+It+Changes+How+You+Contribute;Built+While+Learning+in+Public" alt="Typing SVG" />

</div>
