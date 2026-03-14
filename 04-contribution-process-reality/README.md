# Contribution Process Reality: What It Actually Looks Like at Scale

---

> Ever wondered why a developer at a large company cannot just fork a repo, fix a bug, and send a PR the same way an individual contributor does? Why some companies have entire teams whose job is to manage open source contributions? Why Goldman Sachs spent years preparing before releasing a single line of code?

**You're about to find out — and after this, you will understand why "just open source it" is never that simple inside a large organisation.**

---

## What's Inside This File

> We are exploring what open source contribution actually looks like when legal, compliance, and business risk enter the picture — the approval workflows, the scanning tools, the IP decisions, and the real story of what it took to open source Legend.

```
04-contribution-process-reality.md
│
├── Why Large Organisations Need a Process
│   ├── What an individual contributor risks
│   ├── What a company risks — IP, legal, regulatory
│   └── Why "just push it" is not an option
│
├── What an OSPO Is
│   ├── Definition and scope
│   ├── Not just financial institutions
│   └── What OSPO teams actually do day to day
│
├── OSPO Maturity Levels
│   └── Reactive → Participatory → Leading
│
├── The 6-Stage Contribution Approval Workflow
│   ├── Stage 1 — Business justification
│   ├── Stage 2 — Legal review
│   ├── Stage 3 — Code scanning
│   ├── Stage 4 — Security review
│   ├── Stage 5 — Approval and sign-off
│   └── Stage 6 — Ongoing maintenance commitment
│
├── Data Leakage Scanning
│   ├── What gets scanned and why
│   ├── The git history problem
│   └── Tools used in practice
│
├── CLA Mechanics in Practice
│   ├── What signing actually transfers
│   └── The relicensing risk
│
├── How Goldman Open-Sourced Legend
│   ├── What Legend is
│   ├── The preparation process
│   └── What they had to do before a single line shipped
│
└── Conflicts of Interest in Contribution
    ├── Where contribution crosses a line
    └── Real scenarios and how to handle them
```

---

## Why Large Organisations Need a Process

When an individual developer contributes to open source, the risks are personal and contained. They might contribute code their employer considers proprietary. They might sign a CLA that conflicts with their employment contract. They might accidentally expose something sensitive. These are real risks, but they are bounded.

When a company contributes, the stakes are different in every dimension.

```
What a company exposes when contributing code:
│
├── Intellectual property
│   └── Code may implement patented processes
│   └── Code may reveal proprietary algorithms
│   └── Code may give competitors insight into architecture
│
├── Legal liability
│   └── GPL-incompatible dependencies in the codebase
│   └── Code borrowed from other projects without a license
│   └── Third-party libraries with unclear provenance
│
├── Regulatory exposure
│   └── Cryptographic code subject to export controls
│   └── Data handling code with privacy implications
│   └── Financial logic subject to regulatory scrutiny
│
└── Business risk
    └── Revealing product roadmap through contribution history
    └── Committing to maintain code publicly forever
    └── Community expectations once code is open
```

The moment a company puts code into a public open source project, that code is permanently public. There is no taking it back. Git history is distributed — even if you remove a file, anyone who cloned the repository before you removed it still has it.

This permanence is why the process exists. The review happens before the code ships, because after it ships there is no review that matters.

---

## What an OSPO Is

An **Open Source Program Office** is the internal function responsible for managing an organisation's relationship with open source — both consuming it and contributing back.

The term was coined in the technology industry but the function exists in any large organisation that depends on open source software. That is now essentially every large organisation.

```
What an OSPO manages:
│
├── Inbound (consuming open source)
│   ├── License compliance for all dependencies
│   ├── Security review and approved package lists
│   ├── SBOM generation and maintenance
│   └── Tracking open source obligations
│
├── Outbound (contributing to open source)
│   ├── Contribution approval workflow
│   ├── CLA management
│   ├── Code scanning before release
│   └── Community engagement strategy
│
└── Internal (open source culture)
    ├── Developer education and training
    ├── Internal open source programs (InnerSource)
    ├── Metrics and reporting to leadership
    └── Policy development and enforcement
```

### Not Just Financial Institutions

OSPO functions exist across industries. Google has one of the largest — it manages contribution to thousands of projects and maintains internal tools for license compliance at scale. Microsoft has one. Meta has one. These are not compliance bureaucracies — they are the teams that make large-scale open source contribution possible.

In financial services the function is more heavily compliance-oriented because of regulatory requirements. But the core job is the same everywhere: make it possible for the organisation to participate in open source without creating legal, security, or business problems.

---

## OSPO Maturity Levels

OSPOs do not appear fully formed. They develop over time as an organisation's open source engagement deepens. The Linux Foundation has defined a maturity model that describes this progression:

```
OSPO Maturity Model:
│
├── Stage 0 — Ad Hoc
│   ├── No formal process
│   ├── Individual developers contributing on their own
│   ├── No visibility into what is being contributed
│   └── Risk: IP leakage, license violations, CLA problems
│
├── Stage 1 — Reactive
│   ├── Process exists but only triggered by problems
│   ├── Legal gets involved after something goes wrong
│   ├── Policies written but not enforced consistently
│   └── Risk: Still largely invisible, reactive not preventive
│
├── Stage 2 — Participatory
│   ├── Formal approval workflow in place
│   ├── OSPO team exists with dedicated staff
│   ├── License scanning in CI/CD pipeline
│   └── Contributing strategically, not just reactively
│
├── Stage 3 — Strategic
│   ├── Open source is part of technology strategy
│   ├── Contributing to projects the org depends on
│   ├── Participating in foundations (Linux Foundation, FINOS)
│   └── Measuring contribution impact and community health
│
└── Stage 4 — Leading
    ├── Initiating and donating projects to foundations
    ├── Holding leadership positions in key projects
    ├── Influencing open source policy at industry level
    └── Example: Goldman Sachs donating Legend to FINOS
```

Most large financial institutions sit at Stage 2 or 3. Reaching Stage 4 requires years of investment and genuine community engagement — it cannot be faked because the open source community will notice immediately if the engagement is not real.

---

## The 6-Stage Contribution Approval Workflow

This is what actually happens inside a large organisation before a developer's contribution reaches a public repository. The exact stages vary by organisation, but this represents the standard pattern across major institutions.

---

### Stage 1 — Business Justification

Before anything technical happens, the contribution needs a business reason.

```
Business justification questions:
│
├── Why are we contributing this?
│   ├── Reducing maintenance burden on internal fork?
│   ├── Building community around a standard we use?
│   ├── Recruiting signal to attract engineers?
│   └── Regulatory requirement or foundation commitment?
│
├── What are we giving away?
│   └── Features? Performance improvements?
│       Bug fixes? Infrastructure tooling?
│
├── What do we get back?
│   └── Community maintenance? Bug fixes from others?
│       Ecosystem growth? Standard adoption?
│
└── What is the ongoing commitment?
    └── Who maintains this after it ships?
        Is there budget and headcount for it?
```

Contributions that cannot answer these questions do not proceed. Open sourcing code without a maintenance plan is worse than not open sourcing it — abandoned open source projects damage the organisation's reputation in the community.

---

### Stage 2 — Legal Review

Legal review covers three areas: IP ownership, license compatibility, and CLA obligations.

```
Legal review covers:
│
├── IP ownership verification
│   ├── Was all code written by employees?
│   ├── Was any code written by contractors?
│   │   └── Do contractor agreements assign IP to company?
│   ├── Was any code copied from other projects?
│   │   └── What license was that code under?
│   └── Does the code implement any patented processes?
│
├── License compatibility
│   ├── What license will the contribution be under?
│   ├── Does it contain any GPL/LGPL/AGPL dependencies?
│   │   └── Does the target project's license allow that?
│   └── CLA compatibility with target project
│
└── CLA obligations
    ├── Does the target project require a CLA?
    ├── Has the company signed a CCLA with that project?
    └── Are contributing employees on the Schedule A?
```

IP ownership is the most time-consuming part. Code that has been in an internal repository for years may have contributions from contractors, employees who have since left, or code that was copied from internal tools built on external sources. Tracing every line's origin — called **code archaeology** — is one of the most labour-intensive parts of preparing a large open source release.

---

### Stage 3 — Code Scanning

After legal review, the code goes through automated scanning. No manual reviewer can catch everything. Scanners catch what humans miss.

```
What scanners look for:
│
├── Secrets and credentials
│   ├── API keys hardcoded in source files
│   ├── Passwords in configuration files
│   ├── Private keys or certificates
│   └── Internal service URLs and endpoints
│
├── PII (Personally Identifiable Information)
│   ├── Names, email addresses, phone numbers
│   ├── Account numbers or identifiers
│   └── Any data that could identify a real person
│
├── License violations
│   ├── GPL code in a project being released as MIT
│   ├── Code with no license header (ambiguous provenance)
│   └── Dependencies with incompatible licenses
│
└── Sensitive internal references
    ├── Internal system names and hostnames
    ├── Internal project codenames
    └── References to unreleased products or features
```

Tools used: **Trufflehog** and **Gitleaks** for secrets, **FOSSA** and **Black Duck** for license scanning, **git-filter-repo** for history cleaning.

---

### Stage 3b — The Git History Problem

Scanning the current state of the code is not enough. Git preserves every version of every file ever committed. A secret that was added in a commit three years ago and deleted the next day is still in the git history. Anyone who clones the repository gets that history.

```
The git history problem:
│
├── Developer commits config file with API key
│   └── Commit hash: a3f9b2c
│
├── Developer realises mistake
│   └── Deletes file in next commit
│   └── Commit hash: 7e1d4a8
│
├── Repository looks clean
│   └── No API key visible in current state
│
└── But git history contains both commits
    └── git show a3f9b2c -- config.json
        └── API key visible to anyone with repo access
```

Cleaning git history before open sourcing requires rewriting the entire commit graph — every commit that came after the sensitive commit must be rewritten. Tools: `git filter-repo`, BFG Repo Cleaner.

This is destructive and irreversible. The original commit hashes no longer exist after a history rewrite. Any existing clones or forks will have diverged history. For a project that has been in internal development for years, history cleaning is a significant engineering effort.

---

### Stage 4 — Security Review

The security review is distinct from code scanning. Scanning finds known patterns. Security review finds architectural problems.

```
Security review covers:
│
├── Does the code expose attack surface?
│   └── New APIs, new network interfaces, new parsers
│
├── Does the code handle untrusted input safely?
│   └── Injection risks, deserialization, path traversal
│
├── Does the code have cryptographic weaknesses?
│   └── Custom crypto, weak algorithms, key management
│
├── Does publishing reveal security-relevant details?
│   └── Internal network topology
│   └── Authentication mechanisms
│   └── Rate limiting or abuse prevention logic
│
└── Does the code have known CVEs in dependencies?
    └── Full dependency tree scan against CVE database
```

For financial institutions this stage may also involve the information security team reviewing whether contributing the code creates any regulatory reporting obligations.

---

### Stage 5 — Approval and Sign-off

After all reviews pass, formal approval is required before publication. The approvers depend on what is being contributed.

```
Typical sign-off chain:
│
├── OSPO team — process compliance confirmed
├── Legal — IP and license clearance confirmed
├── Security — no security concerns confirmed
├── Business owner — strategic justification confirmed
└── For significant releases:
    ├── CTO or VP Engineering sign-off
    └── Sometimes General Counsel sign-off
```

For small contributions — a bug fix, a documentation improvement — this chain can be lightweight. For a significant open source release like a new project or a large feature, this is a formal process with documented sign-offs that go into the organisation's legal records.

---

### Stage 6 — Ongoing Maintenance Commitment

The approval is not a one-time event. Contributing code creates ongoing obligations.

```
Post-release obligations:
│
├── Responding to community issues and PRs
│   └── Ignoring the community after releasing code
│       is worse than not releasing it
│
├── Patching security vulnerabilities
│   └── Once code is public, CVEs can be filed against it
│   └── Organisation is now responsible for patches
│
├── Keeping dependencies current
│   └── Outdated dependencies = security risk
│   └── Community will notice and lose confidence
│
└── Community governance participation
    └── If donated to a foundation, participating in
        project governance and technical steering
```

Organisations that release code and then disappear from the community are noticed. The open source community is small enough and connected enough that reputation matters. A company that does not follow through on its maintenance commitments will find its future contributions viewed with suspicion.

---

## Data Leakage Scanning — Going Deeper

The scanning stage deserves more depth because the failure modes are not obvious until you have seen them.

### Secrets in Code — Why It Keeps Happening

Hardcoded secrets in source code are one of the most common security failures, and they keep happening despite widespread awareness because of how development workflows actually work.

```
How secrets end up in code:
│
├── Local development shortcuts
│   └── Developer needs to test against real service
│   └── Hardcodes key to avoid credential management
│   └── Intends to remove it — forgets
│
├── Configuration as code patterns
│   └── Kubernetes manifests, Helm charts, CI config
│   └── Secrets mixed with configuration
│   └── Whole file committed including secrets
│
├── Copy-paste from internal documentation
│   └── Internal wiki shows example with real credentials
│   └── Developer copies example, keeps credentials
│
└── Historical accidents
    └── Secret committed, deleted, forgotten
    └── Still in git history
    └── Not caught until open source review — or after
```

Tools like **Trufflehog** scan every commit in git history, not just the current state. They use entropy analysis and pattern matching to find strings that look like secrets — high-entropy strings, strings that match known API key formats (AWS keys start with `AKIA`, GitHub tokens start with `ghp_`, etc.).

### PII in Code — The Less Obvious Problem

Developers do not usually think of PII as something that ends up in source code. It does.

```
How PII ends up in source code:
│
├── Test data that was never cleaned
│   └── Real names and emails used in unit tests
│   └── Real account numbers in test fixtures
│
├── Log statements that captured real data
│   └── Debug logging that included user identifiers
│   └── Error messages that echoed user input
│
├── Hardcoded examples in documentation
│   └── "Example: user@realdomain.com" using real person
│   └── Employee names in inline code comments
│
└── Database dumps used as test fixtures
    └── Anonymisation was planned but not done
    └── Real data in test database schema files
```

Once PII is in a public git repository it is effectively impossible to remove completely. The GDPR right to erasure becomes impossible to fulfil. This alone has blocked open source releases.

---

## CLA Mechanics in Practice

### What Signing Actually Transfers

Most developers who sign CLAs do not read them carefully. The standard CLA does not transfer copyright — it grants a license. But that license is broad enough to effectively give the project owner significant control.

```
What a typical CLA grants:
│
├── Copyright license
│   └── Perpetual, worldwide, non-exclusive license
│   └── To reproduce, modify, distribute your contribution
│
├── Patent license
│   └── To make, use, sell anything that implements
│       the patented processes in your contribution
│
├── Right to sublicense
│   └── Project can license your contribution to others
│   └── Under any terms the project chooses
│
└── Right to relicense
    └── Project can change the license of your contribution
    └── This is the most significant clause
```

### The Relicensing Risk

The right to relicense is the clause that matters most and is least understood.

```
Relicensing scenario:
│
├── You contribute to a project under Apache 2.0 CLA
├── CLA grants the project owner right to relicense
│
├── Project owner decides to go commercial
│   └── Changes license from Apache 2.0 to proprietary
│
├── Your contribution is now in a proprietary product
│   └── Licensed to others commercially
│   └── You receive nothing
│   └── You cannot prevent this
│
└── Real examples:
    ├── HashiCorp — BSL switch
    │   └── Years of community contributions
    │       now under a non-open license
    └── MongoDB — SSPL switch
        └── Same pattern
```

This is not hypothetical. When HashiCorp switched Terraform to BSL, every contributor who had signed the CLA had already granted HashiCorp the right to make exactly that change. The community could fork — and did, creating OpenTofu — but the original project could still take the new direction.

The DCO does not have this problem. A Signed-off-by line certifies that you contributed code you have the right to contribute under the project's current license. It does not grant the project owner any right to relicense. This is one reason why some contributors prefer projects that use DCO over CLA.

---

## How Goldman Sachs Open-Sourced Legend

Legend is a data management platform originally built internally at Goldman Sachs under the name Alloy. It was donated to FINOS in 2020 and became one of the most significant open source releases in financial services history.

The preparation process illustrates everything in this file in a single real case.

### What Legend Is

Legend is a platform for data modelling, data management, and data governance. It allows organisations to create formal models of their data — what a trade is, what a position is, what a risk metric means — in a way that can be shared, versioned, and executed across systems.

At Goldman it solved a specific problem: different systems used different definitions for the same concepts. A "trade" in the equities system was not quite the same as a "trade" in the fixed income system. Legend created a common language.

### The Preparation Process

Goldman spent approximately two years preparing Legend for open source release. The work fell into several categories:

```
Legend open source preparation:
│
├── Code archaeology
│   ├── Tracing the origin of every significant component
│   ├── Identifying code written by contractors
│   ├── Finding code copied from or inspired by other sources
│   └── Documenting IP ownership for every module
│
├── Dependency cleaning
│   ├── Removing all internal Goldman dependencies
│   ├── Replacing internal libraries with open alternatives
│   ├── Resolving license conflicts in dependency tree
│   └── Ensuring no proprietary third-party code remained
│
├── History sanitisation
│   ├── Scanning full git history for secrets
│   ├── Scanning for internal hostnames and endpoints
│   ├── Scanning for employee PII in commits and comments
│   └── Rewriting history where sensitive data was found
│
├── Security review
│   ├── Full external security audit
│   ├── Penetration testing of exposed interfaces
│   └── CVE scan of all dependencies
│
└── Community readiness
    ├── Documentation written for external audience
    ├── Contribution guidelines established
    ├── Governance model agreed with FINOS
    └── Dedicated maintainer team identified and committed
```

The internal codebase that became Legend had been built over years by hundreds of engineers. None of them were writing code intended for public release. Code had been written, copied, modified, and deleted without any thought for what would need to happen before it could be open sourced.

The two years of preparation were spent undoing the assumptions baked into every line of that code.

### What They Gained

After donation to FINOS, several other financial institutions — JPMorgan, Morgan Stanley, Deutsche Bank — began contributing to Legend. A platform that one bank built became an industry standard that the whole industry maintains.

This is the strategic case for open sourcing: the maintenance cost is shared across the entire industry. Goldman still uses Legend, still influences its direction, but no longer pays the full cost of maintaining it alone.

---

## Conflicts of Interest in Contribution

Contributing to open source while employed creates scenarios where personal interests, employer interests, and community interests can conflict. These situations are not always obvious when they arise.

---

### Scenario 1 — Contributing on Company Time to Unrelated Projects

```
Scenario:
├── Developer works at Bank A
├── Developer contributes to an open source project
│   unrelated to their work at Bank A
├── Developer does this during work hours
│
└── Problem:
    └── In most employment contracts, work done on
        company time using company resources belongs
        to the company
        └── Developer may have just donated Bank A's IP
            to an open source project without authorisation
```

The fix: contribute to personal projects on personal time using personal equipment. Or get explicit written permission from your employer for specific contributions.

---

### Scenario 2 — Shaping a Standard You Will Benefit From

```
Scenario:
├── Developer works at Company A
├── Developer becomes active contributor to
│   open source project that is becoming an industry standard
├── Developer shapes the API design of the project
│   in ways that align with Company A's internal architecture
│
└── Problem:
    └── Company A now has a structural advantage
        Their systems already work with the standard
        because they helped design it to match them
        Other companies must adapt to the standard
        └── Antitrust concern if done deliberately
            to disadvantage competitors
```

The Linux Foundation antitrust policy exists partly to address this. Contribution to standards-setting projects must be done in good faith for the benefit of the community, not to advantage a single participant.

---

### Scenario 3 — Contributing Fixes You Were Paid to Write

```
Scenario:
├── Company A uses open source Library B
├── Library B has a bug that affects Company A
├── Company A pays Developer to fix the bug
│   as part of their normal employment
│
└── Who owns the fix?
    ├── Developer wrote it — copyright default: developer
    ├── Company A paid for it — employment contract: company
    └── The fix was contributed to Library B — community
        └── All three have claims
        └── A CLA determines who wins
```

This is why corporate CLAs matter. The CCLA establishes that contributions made by employees in the course of employment are contributed with the employer's permission and under terms that make the contribution legally clean.

Without a CCLA, the company has a potential claim on the contribution even after it ships. That claim is unlikely to be pursued in most cases — but it creates a legal cloud over the contribution that can matter if the company is ever acquired or if there is ever a dispute.

---

## The Pattern Across All of This

Every stage of the contribution process is answering the same question: **what are we actually releasing, and have we thought through every consequence?**

```
What the process protects against:
│
├── IP leakage
│   └── Code archaeology + legal review
│
├── Secret exposure
│   └── Automated scanning + history cleaning
│
├── License violations
│   └── License scanning + legal review
│
├── Security vulnerabilities
│   └── Security review + CVE scanning
│
├── Community abandonment
│   └── Maintenance commitment + governance
│
└── Legal liability
    └── CLA management + sign-off chain
```

The process is not bureaucracy for its own sake. Every stage exists because something went wrong without it — somewhere, at some point, a company shipped code that had a secret in the history, or a license conflict in a dependency, or no plan for maintenance. The process is the accumulated institutional memory of every mistake that came before.

---

> **Now read the next file — because once your code is in a public repository, it may be subject to laws you have never thought about.**
> **Export controls apply to code — and the story starts with a man facing federal prison → [05-export-controls-and-sanctions.md](05-export-controls-and-sanctions.md)**
