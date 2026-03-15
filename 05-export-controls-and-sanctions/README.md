# Export Controls and Sanctions: Why Code Is Legally a Weapon

---

> Ever wondered why a man who wrote an encryption program in 1991 faced federal criminal charges just for sharing it? Why GitHub blocked users in Iran, Syria, and Cuba? Why a smart contract on Ethereum was sanctioned by the US Treasury — not the people using it, the code itself? Why a developer contributing to the Linux kernel crypto subsystem might need to file paperwork with the US government?

**You're about to find out — and after this, you will understand why "it's just code" has never been a legal defence.**

---

## What's Inside This File

> We are exploring the intersection of open source software and national security law — the real history, the exact regulations, and what they mean for a developer who writes, contributes to, or distributes anything cryptographic.

```
05-export-controls-and-sanctions.md
│
├── Why Code Is Treated as a Physical Export
│   ├── The legal theory — munitions and dual-use goods
│   └── How software became subject to export law
│
├── The PGP Story — Where It Started
│   ├── Phil Zimmermann, 1991, the criminal investigation
│   ├── What actually happened and why it matters
│   └── How it changed export control law permanently
│
├── EAR and ITAR — The Two Regimes
│   ├── What each covers
│   ├── ECCN 5E002 — where most crypto software lives
│   ├── Standard vs non-standard crypto
│   └── What the mass market exemption covers
│
├── What Actually Applies to a Developer
│   ├── Contributing to kernel crypto subsystem
│   ├── What notification requirements exist
│   └── When to worry and when not to
│
├── Tornado Cash — When Code Itself Gets Sanctioned
│   ├── What Tornado Cash is
│   ├── What OFAC did and why it was unprecedented
│   └── What it means for open source developers
│
└── Sanctioned Contributors and Restricted Countries
    ├── CoreJS and Russia
    ├── GitHub Iran incident
    └── North Korean developers in open source
```

---

## Why Code Is Treated as a Physical Export

The legal framework for controlling what crosses international borders was built for physical goods — weapons, military equipment, dual-use technology. When cryptographic software appeared, governments faced a question: is this a product or is it information? Is distributing it internationally a sale of goods or freedom of speech?

The answer they settled on: it depends on the cryptographic strength, and strong crypto is a dual-use good that can be exported only under specific conditions.

### The Legal Theory

```
Export control theory applied to software:
│
├── Physical weapons are export-controlled
│   └── Cannot ship a missile to a sanctioned country
│
├── Technology that enables weapons is also controlled
│   └── Dual-use goods — civilian use, military application
│
├── Strong cryptography is dual-use
│   └── Civilian: securing communications and data
│   └── Military: hiding communications from surveillance
│
└── Therefore: distributing strong crypto internationally
    is a controlled export
    └── Subject to the same regime as physical munitions
```

This was not abstract theory. During the Cold War, strong cryptography was classified as a munition under the International Traffic in Arms Regulations (ITAR). Exporting it required a State Department license. The concern was real: if adversaries could encrypt with unbreakable ciphers, signals intelligence — interception and reading of communications — became impossible.

---

## The PGP Story — Where It Started

### 1991 — Phil Zimmermann Writes PGP

In 1991, Phil Zimmermann wrote **Pretty Good Privacy** — PGP — a program that allowed anyone to encrypt their email using public key cryptography. The encryption was strong enough that at the time it was effectively unbreakable with available computing power.

Zimmermann's motivation was political. The US Senate was considering legislation that would require backdoors in all encryption software — a mechanism for law enforcement to decrypt any communication. Zimmermann released PGP before the legislation passed, specifically to establish that strong encryption was already widely available and a backdoor requirement was unenforceable.

He posted PGP to Usenet newsgroups. From there it propagated internationally within days.

### The Criminal Investigation

```
PGP criminal investigation timeline:
│
├── 1991 — Zimmermann posts PGP to Usenet
│   └── PGP crosses international borders within days
│
├── 1993 — US Customs Service opens investigation
│   └── Allegation: unauthorised export of munitions
│   └── PGP used 128-bit RSA — classified as munition
│   └── Criminal charge potential: federal felony
│
├── 1993-1996 — Three year investigation
│   └── Zimmermann under federal investigation
│   └── Cannot be easily charged — did not personally
│       export it, someone else uploaded internationally
│   └── But Zimmermann made it available knowing
│       it would cross borders
│
└── January 1996 — Investigation dropped
    └── No charges filed
    └── Legal question remained unresolved
```

The investigation was dropped partly because of legal uncertainty about whether posting something to the internet — from which it could be downloaded internationally — constituted an "export." The law had been written for physical goods crossing physical borders. Digital distribution did not fit cleanly.

### Why It Changed Everything

The PGP case drew massive public attention to export control law as applied to software. Civil liberties organisations, cryptographers, and software developers organised against what they saw as an unconstitutional restriction on speech. Some protesters printed PGP's source code in books — which were clearly protected speech — and shipped the books internationally, making the legal inconsistency visible.

```
The export control absurdity made visible:
│
├── PGP source code as a file: EXPORT CONTROLLED
│   └── Criminal offence to send internationally
│
├── PGP source code printed in a book: NOT CONTROLLED
│   └── Books are protected speech
│   └── Can be shipped internationally freely
│
├── Someone could legally:
│   └── Buy the book in Europe
│   └── Type the code back in
│   └── Have working PGP
│
└── Same code: legal as paper, illegal as bits
    └── Obviously unworkable
```

By 1996 the US government began relaxing export control rules for cryptographic software. By 2000 the rules had been reformed significantly — strong encryption could be exported to most countries with a notification requirement rather than a license, with exceptions for embargoed countries and certain end uses.

---

## EAR and ITAR — The Two Regimes

Two separate regulatory regimes govern US export controls. Understanding which applies to software requires knowing what the software is and who it is for.

### ITAR — International Traffic in Arms Regulations

ITAR is administered by the State Department. It covers the United States Munitions List — items specifically designed for military use.

```
ITAR for software:
├── Covers: software specifically designed for
│   military or intelligence applications
├── Examples: weapons guidance software,
│   military comms encryption,
│   signals intelligence tools
├── Requirements: State Department license
│   for any international transfer
└── Most open source software: NOT under ITAR
    └── Unless specifically designed for military use
```

Most open source developers do not need to worry about ITAR. It applies to military-specific software, not general-purpose cryptographic tools.

### EAR — Export Administration Regulations

EAR is administered by the Commerce Department's Bureau of Industry and Security (BIS). It covers dual-use goods — items with both civilian and military applications.

Every product covered by EAR is assigned an **Export Control Classification Number (ECCN)**. Software with encryption functionality almost always falls under:

```
ECCN 5E002 — Information Security Software:
│
├── Covers: software implementing encryption
│   for confidentiality of information
│
├── Who it applies to:
│   └── Anyone exporting or re-exporting
│       such software from the US
│
├── What "export" means for software:
│   ├── Selling or transferring to foreign national
│   ├── Uploading to a public server abroad
│   └── Emailing source code internationally
│
└── Deemed export:
    └── Foreign national in the US receiving
        the software is also an "export"
```

### Standard vs Non-Standard Crypto

The key distinction for most open source developers is between standard and non-standard cryptographic algorithms.

```
Standard cryptography (lower controls):
├── Algorithms published and available publicly
├── Examples: AES, RSA, SHA-256, TLS, SSH
├── Available in: OpenSSL, libsodium, kernel crypto API
└── Treatment: eligible for License Exception ENC
    with notification to BIS — not a license

Non-standard cryptography (higher controls):
├── Custom or proprietary encryption algorithms
├── Modified versions of standard algorithms
├── Algorithms not publicly available
└── Treatment: may require BIS license
    └── Much higher bar to export
```

### The Mass Market Exemption

There is a specific exemption for mass market products — software generally available to the public that implements standard cryptographic algorithms. Most open source software qualifies.

```
Mass market exemption conditions:
├── Software is generally available to the public
├── Sold without restriction from stock
├── Encryption cannot be easily changed by the user
└── Effect: one-time notification to BIS
    └── Annual self-classification report
    └── No license required for most destinations
    └── Still restricted: Cuba, Iran, North Korea,
        Syria, Russia (certain uses), China (some)
```

---

## What Actually Applies to a Developer

The regulations sound broad. In practice, what does this mean for a developer contributing to open source?

### Contributing to the Linux Kernel Crypto Subsystem

The Linux kernel contains a cryptographic subsystem — `crypto/` in the kernel tree — that implements AES, SHA, RSA, and other standard algorithms. It is used by IPsec, dm-crypt, TLS, and dozens of kernel features.

```
Kernel crypto subsystem contribution:
│
├── You write a patch implementing a standard algorithm
│
├── You submit it to the kernel mailing list
│   └── Patch is publicly posted
│   └── Accessible internationally immediately
│
├── Is this an export?
│   └── Technically: yes
│
├── Does it require a license?
│   └── No — standard crypto, mass market exception
│
└── Does it require any action from you?
    └── No — The Linux Foundation files BIS notification
        on behalf of the project
        └── See: Documentation/admin-guide/README.rst
            "EXPORT CONTROLS" section
        └── Individual contributors: nothing required
            unless you are the project maintainer
            exporting commercially
```

### When You Actually Need to Worry

```
Situations requiring attention:
│
├── Starting a new project that implements cryptography
│   └── File a one-time BIS notification before
│       making it publicly available
│
├── Selling a product containing cryptographic software
│   └── Annual self-classification report required
│   └── Certain destinations may require license
│
├── Contributing custom or non-standard crypto
│   └── Not covered by mass market exception
│   └── May require BIS review before export
│
└── Working with a company in a restricted country
    └── Even open source contribution may be restricted
```

### When You Do Not Need to Worry

```
Situations not requiring action:
│
├── Contributing bug fixes or features to an existing
│   open source project with standard crypto
│   └── Project's existing classification covers it
│
├── Using cryptographic libraries in your application
│   └── You are using crypto — not exporting it
│
└── Contributing docs or non-crypto code
    to a project that contains crypto
    └── Your contribution is not crypto
```

---

## Tornado Cash — When Code Itself Gets Sanctioned

On August 8, 2022, the US Treasury Department's Office of Foreign Assets Control (OFAC) sanctioned Tornado Cash. This was unprecedented — not because of who was sanctioned, but because of **what** was sanctioned.

### What Tornado Cash Is

Tornado Cash is a cryptocurrency mixer — a smart contract on the Ethereum blockchain that allows users to deposit cryptocurrency and withdraw equivalent amounts to a different address, breaking the transaction trail. It is used for privacy. It is also used for money laundering. OFAC estimated it had been used to launder over $7 billion, including over $455 million stolen by the Lazarus Group — North Korean state-sponsored hackers.

### What OFAC Did

```
OFAC Tornado Cash action:
│
├── Added Tornado Cash to the SDN list
│   (Specially Designated Nationals and Blocked Persons)
│
├── What was sanctioned:
│   ├── The smart contract addresses on Ethereum
│   │   └── Immutable code on a blockchain
│   └── The organisation and associated individuals
│
├── Effect:
│   ├── US persons prohibited from interacting with it
│   ├── GitHub removed the Tornado Cash repository
│   ├── Circle froze USDC funds in the contracts
│   └── Infura and Alchemy blocked RPC access
│
└── What was unprecedented:
    └── The code itself — not just people — was sanctioned
        └── Immutable, autonomous smart contracts
            with no off switch
            added to a sanctions list
```

### The Legal Challenge

```
Legal argument against the sanction:
│
├── OFAC can sanction property
│   └── Property must be owned or controlled by someone
│
├── Immutable smart contracts:
│   ├── Cannot be modified
│   ├── Cannot be stopped
│   ├── Have no owner
│   └── Execute automatically based on code
│
├── Argument: immutable code is not "property"
│   in the legal sense — it cannot be owned
│
└── November 2024 — Fifth Circuit ruled for plaintiffs
    └── Immutable contracts cannot be sanctioned
        under IEEPA (the statute OFAC used)
    └── But: organisation and mutable contracts
        remain sanctioned
```

### What It Means for Open Source Developers

```
Implications for open source:
│
├── Writing code usable for sanctioned purposes
│   is not automatically a violation
│   └── Code itself is generally protected speech
│
├── Deploying code as a service used for
│   sanctioned purposes: different exposure
│   └── Operating a mixer ≠ writing one
│
└── Practical guidance:
    └── Building financial privacy tools,
        cryptocurrency infrastructure, or anything
        that could evade sanctions:
        get legal advice before deploying publicly
```

---

## Sanctioned Contributors and Restricted Countries

### CoreJS and Russia

CoreJS is one of the most downloaded JavaScript packages in the world — a polyfill library that allows modern JavaScript to run in older browsers. It is a transitive dependency in an enormous fraction of web applications.

```
CoreJS dependency reality:
│
├── Downloads: ~250 million per week at peak
├── Maintained by: one person, based in Russia
│
├── After February 2022 Russia invasion of Ukraine:
│   └── International payment processors blocked
│       └── GitHub Sponsors unavailable in Russia
│       └── PayPal withdrew from Russia
│
├── Question for organisations:
│   └── Does using CoreJS create sanctions exposure?
│
└── Answer: No
    └── Using open source maintained by someone
        in Russia is not a sanctions violation
        └── Sanctions restrict transactions
            not reading publicly available code
        └── Paying a maintainer in a sanctioned country
            through a financial transfer: different
            └── That is a transaction
```

---

### GitHub Iran Incident

In 2019, GitHub began restricting access for users in Iran, Syria, and Crimea, citing US export control and sanctions law.

```
GitHub Iran restriction (2019):
│
├── GitHub blocked or restricted:
│   ├── Users in Iran, Syria, Crimea
│   ├── GitHub Actions for restricted regions
│   ├── Private repository access
│   └── Some public repository access
│
├── Why:
│   └── US export regulations and OFAC sanctions
│   └── GitHub interpreted EAR as requiring restrictions
│   └── Legal risk of providing services to
│       sanctioned regions
│
├── Community reaction:
│   └── Significant backlash
│   └── Iranian developers had contributed to
│       major open source projects
│   └── Seen as contradicting open source principles
│
└── Partial resolution:
    └── GitHub obtained OFAC license to provide
        free services to developers in Iran
    └── Some restrictions remain for commercial features
    └── Lesson: platform risk is real for developers
        in restricted regions
```

---

### North Korean Developers in Open Source

The most operationally dangerous intersection of open source and sanctions involves North Korea. The Lazarus Group — North Korea's state-sponsored hacking organisation — has conducted extensive operations using social engineering against the cryptocurrency industry and software supply chain.

```
North Korean developer tactics in open source:
│
├── Social engineering maintainers
│   └── Building trust as contributors over months
│   └── Eventually requesting commit access or
│       elevated permissions
│
├── Fake identities
│   └── Complete GitHub profiles with history
│   └── Convincing LinkedIn profiles
│   └── Fake employment histories
│
├── Supply chain insertion
│   └── Contributing backdoored code to
│       cryptocurrency libraries
│   └── Targeting npm packages used by crypto wallets
│
├── Documented incidents:
│   ├── 2023 — 3CX supply chain attack
│   │   └── Traced to developer who installed
│   │       malicious npm package
│   └── Multiple npm packages with backdoors
│       targeting crypto wallets
│       attributed to Lazarus Group
│
└── Why this is a sanctions issue:
    └── Accepting contributions from North Korean nationals
        may violate OFAC sanctions
        regardless of whether you know
        └── "Willful blindness" is not a defence
```

### What to Do if You Suspect a Contributor

```
Red flags in a contributor:
├── Unusual focus on security-sensitive code paths
├── Requests for elevated access early in relationship
├── Profile with suspicious history patterns
├── Contributions adding unnecessary complexity
└── Pressure to merge quickly without full review

What to do:
├── Do not merge until thoroughly reviewed
├── Report to project security contact
└── Strong suspicion of North Korean origin:
    └── Report to FBI IC3 or CISA
        (US persons have reporting obligations)

What not to do:
├── Do not publicly accuse without evidence
├── Do not attempt to engage or expose yourself
└── Do not ignore it hoping it resolves
```

---

## The Pattern Across All of This

Export controls and sanctions in open source all reduce to the same tension: governments wrote laws for a world of physical goods and nation-state actors. Open source exists in a world where code is speech, borders are permeable to bits, and contributors are pseudonymous.

```
The core tension:
│
├── Export control law assumes:
│   ├── Goods have identifiable exporters
│   ├── Goods cross identifiable borders
│   └── Exporters can control distribution
│
├── Open source reality:
│   ├── Code posted publicly goes everywhere instantly
│   ├── Contributors are often pseudonymous
│   └── Distribution cannot be controlled once posted
│
└── The result:
    ├── Laws apply in theory
    ├── Enforcement is selective — big cases only
    │   └── Zimmermann, Tornado Cash, GitHub Iran
    └── Most developers never encounter enforcement
        but the legal exposure is real
```

What protects most open source developers most of the time is the mass market exemption, the public domain nature of their code, and the practical reality that enforcement concentrates on large-scale violations. But "most of the time" is not the same as "not applicable."

If you are working on cryptographic software, financial privacy tools, or anything that touches cryptocurrency infrastructure — understand the regulations before you deploy. The PGP story ended without charges. Not everyone has been that fortunate.

---

> **Now read the next file — because even within the open source community, competitors contributing to the same project raises questions that antitrust law was built to answer.**
> **Why Google, Microsoft, and Meta can work together legally → [06-antitrust-in-open-source.md](06-antitrust-in-open-source.md)**
