# Licenses: The Complete Picture

---

> Ever wondered why you cannot just copy code from GitHub into your project? Why some open source code is completely free to use in commercial products but other open source code will force you to open your entire codebase? Why MIT and Apache 2.0 look almost identical but one can get your company sued over a patent?

**You're about to find out — and after this, you will read every LICENSE file before touching a dependency.**

---

## What's Inside This File

> We are exploring what software licenses actually do — not the legal definitions, the real consequences. What each license permits, what it forbids, what trap doors it contains, and why the choice between them has ended careers and cost companies millions.

```
02-licenses-the-complete-picture.md
│
├── Why Licenses Exist At All
│   ├── What happens to code with no license
│   ├── Copyright by default — the trap most developers fall into
│   └── Why "I found it on GitHub" is not a legal defense
│
├── The License Spectrum
│   └── Permissive → Weak Copyleft → Strong Copyleft → Network Copyleft
│
├── MIT — The Simplest License
│   ├── What it actually says in plain language
│   ├── What it gives you
│   └── The one thing it does not give you — patent rights
│
├── Apache 2.0 — MIT With Patent Protection
│   ├── The explicit patent grant
│   ├── The patent retaliation clause
│   └── Why MIT vs Apache 2.0 is not just a formality
│
├── GPL v2 — What Copyleft Actually Means
│   ├── The viral clause — step by step
│   ├── What "distribution" means and what triggers it
│   └── Why the Linux kernel is GPL v2 and what that means for drivers
│
├── LGPL — The Middle Ground
│   ├── How it differs from GPL
│   ├── Dynamic vs static linking — why it matters
│   └── When to use it and when it is not enough
│
├── AGPL — Closing the SaaS Loophole
│   ├── The loophole GPL left open
│   ├── What network use means
│   └── When AGPL triggers — the distribution question in depth
│
├── License Compatibility — What Can Combine With What
│   ├── Why incompatible licenses are a real problem
│   └── Compatibility matrix
│
├── CLA vs DCO
│   ├── What a CLA is — ICLA, CCLA, Schedule A problem
│   ├── What a DCO is — the Signed-off-by line
│   └── Why the kernel uses DCO but most projects use CLA
│
└── Openwashing Licenses — The Ones That Look Open But Are Not
    ├── SSPL — MongoDB's answer to AWS
    └── BSL — HashiCorp's answer to competition
```

---

## Why Licenses Exist At All

Most developers treat license files as legal boilerplate — something to click through, something the lawyers worry about. That is a mistake that has caused companies to rewrite entire codebases, pay settlements, and in some cases shut down products.

To understand why licenses matter, you need to understand what exists without them.

### What Copyright Does By Default

The moment you write code, copyright law in almost every country gives you automatic, exclusive rights over that code. You do not need to register anything. You do not need to put a copyright notice anywhere. The code is yours and nobody can legally copy it, modify it, or distribute it without your explicit permission.

This means that code with no license is not free to use. It is the opposite:

```
Code with no license:
├── Copyright is held by the author automatically
├── No one has permission to use it
├── No one has permission to copy it
├── No one has permission to modify it
└── No one has permission to distribute it

"But it's on GitHub publicly" does not matter
└── Public visibility ≠ permission to use
    Public visibility = anyone can read it
    Permission to use = requires a license
```

This is the trap that catches developers constantly. Someone puts code on GitHub without a license. Another developer uses it in a product. Years later, the original author — or someone who bought the copyright — sends a cease and desist. The code was always copyrighted. The developer who used it had no license. They were infringing from day one.

A license is the author's explicit statement of what others are permitted to do with the code. Without it, the answer is: nothing.

---

### Why There Are So Many Licenses

Different authors want different things from sharing their code:

```
"Use it however you want, just credit me"
└── MIT, BSD licenses

"Use it however you want, but protect me from patent claims"
└── Apache 2.0

"Use it freely, but if you distribute it, share your changes too"
└── GPL

"Use it in your application, but keep the library itself open"
└── LGPL

"Use it freely, but if you run it as a service, share your changes"
└── AGPL

"Use it freely unless you are competing with us commercially"
└── BSL, SSPL — not actually open source
```

Every major license is an answer to a specific question about what "sharing freely" should actually mean and what obligations it should create.

---

## The License Spectrum

Before going deep on each license, it helps to see where they sit relative to each other:

```
PERMISSIVE                                              COPYLEFT
────────────────────────────────────────────────────────────────
MIT          Apache 2.0      MPL 2.0      LGPL      GPL v2/v3      AGPL
 │               │              │           │            │             │
 │               │              │           │            │             │
Most           Patent        File-level   Library     Full          Network
permissive     grant         copyleft     copyleft    copyleft      copyleft
 │               │              │           │            │             │
Anyone can     Same +         Modified     Use freely  Distribute =  Run as
do anything    patent         files must   but keep    share source  service =
               protection     stay open    lib open                  share source
```

The further right you go, the more obligations you take on when you use the code. The further left, the more freedom you have — but the less protection the original author has against their work being taken and closed.

---

## MIT — The Simplest License

The MIT license is 171 words. Here is what it actually says in plain language:

```
MIT License says:
├── You can use this code for anything
├── You can modify it however you want
├── You can distribute it
├── You can sell it
├── You can use it in proprietary software
├── You can sublicense it
└── Just keep the copyright notice and this license text
    in any copy you distribute
```

That is it. The only obligation is attribution — keep the copyright notice. Everything else is permitted.

MIT is the most widely used open source license precisely because of this simplicity. It asks almost nothing. For a developer who wants their code used widely, MIT creates the lowest possible barrier.

---

### The One Thing MIT Does Not Give You

MIT is silent on patents. This is not an oversight — it is a gap that matters.

When a company contributes code to an MIT-licensed project, they give you permission to use that specific code. They do not give you any rights to patents they hold that the code might implement.

```
Scenario — the MIT patent trap:
│
├── Company A contributes code to an MIT project
├── That code implements functionality covered by Company A's patent
├── You use the MIT project in your product
├── Company A sues you for patent infringement
│
└── Your defense: "But it was MIT licensed!"
    Their response: "MIT covers copyright, not patents.
                    We never gave you a patent license."
    Result: You lose.
```

This has happened. It is not hypothetical. The MIT license covers copyright. It says nothing about patents. In a world where large companies hold thousands of software patents, contributing code to an MIT project without explicitly granting patent rights creates a legal weapon that can be activated later.

This is exactly why Apache 2.0 was written.

---

## Apache 2.0 — MIT With Patent Protection

Apache 2.0 does almost everything MIT does — permissive, commercial use allowed, modification allowed, distribution allowed. But it adds two critical clauses.

### The Explicit Patent Grant

```
Apache 2.0 patent grant says:
└── Each contributor grants you a perpetual, worldwide,
    non-exclusive, royalty-free patent license to make,
    use, sell, and distribute the contribution and
    derivative works
```

In plain language: when someone contributes to an Apache 2.0 project, they automatically grant you rights to any patents their contribution implements. You cannot use Apache 2.0 code and then sue the users for patent infringement on that same code.

This closes the exact gap that MIT leaves open.

---

### The Patent Retaliation Clause

Apache 2.0 goes further. If you use Apache 2.0 software and then file a patent lawsuit claiming that the software infringes your patents:

```
Apache 2.0 patent retaliation:
│
├── You use software licensed under Apache 2.0
├── You file a patent lawsuit claiming that software
│   infringes your patents
└── Result: Your Apache 2.0 license terminates automatically
    └── You lose the right to use the software
        └── Effective deterrent against patent aggression
```

This clause creates a real cost for using Apache 2.0 software as a platform and then attacking it with patents. It does not prevent patent lawsuits — nothing can fully prevent them — but it makes them expensive in a new way.

---

### Why MIT vs Apache 2.0 Is Not Just a Formality

Most developers treat MIT and Apache 2.0 as interchangeable — "both are permissive, both allow commercial use, pick whichever." This is wrong in any context where patents are relevant.

```
Choose MIT when:
├── You want maximum simplicity
├── Patent risk is genuinely low
└── You want the widest possible adoption with zero friction

Choose Apache 2.0 when:
├── Your project is in a domain with active patent holders
├── You want to protect users from patent aggression
├── Large companies are likely contributors or users
└── You want the patent retaliation deterrent
```

The Apache Software Foundation requires all projects under their umbrella to use Apache 2.0 specifically because of the patent protection. The Linux kernel uses GPL v2 partly because of its copyleft protection. These are not arbitrary choices — they reflect specific legal strategies.

---

## GPL v2 — What Copyleft Actually Means

The GPL is the license that confuses and frightens developers most. It is also the most important license in open source history. The Linux kernel, Git, GCC, and thousands of critical tools are GPL v2.

### The Core Idea

The GPL's copyleft condition says: if you distribute software that includes GPL code, you must distribute the complete source code under the GPL.

This sounds simple. The complexity comes from what "distribute" means and what exactly triggers the obligation.

---

### What Distribution Means

```
Distribution under GPL means:
├── Giving someone a binary or source to keep
├── Selling software that includes GPL code
├── Shipping a product with GPL software inside
│   (routers, embedded systems, phones)
└── Making GPL software available for download

Distribution does NOT mean:
├── Running GPL software internally on your servers
├── Using GPL tools to build your product
│   (gcc compiles your code — that is not distribution)
└── Modifying GPL code only for internal use
```

This distinction is critical. A company can use GPL software internally — run it on their servers, use it in their development process — without triggering any obligation. The obligation only appears when they distribute something that contains GPL code to someone outside the organization.

---

### The Viral Clause — Step by Step

```
STEP 1: You take a GPL v2 project
        └── Example: a GPL v2 library

STEP 2: You modify it or incorporate it into your software
        └── You write code that links against it

STEP 3: You distribute the combined work
        └── Ship it to customers, release it publicly,
            include it in a product

STEP 4: The GPL obligation triggers
        ├── You must provide complete source code
        ├── Under the GPL v2 license
        ├── To everyone who receives the binary
        └── Including your modifications

STEP 5: Your modifications are now GPL v2
        └── Anyone who receives your product can get
            the full source code of everything GPL
```

This is why companies are cautious about GPL code in commercial products. It is not that GPL is hostile to business — many successful commercial products use GPL code. It is that once you distribute a product containing GPL code, you have taken on a real obligation that has legal teeth.

---

### Linux Kernel GPL v2 and Device Drivers

The Linux kernel is licensed under GPL v2 with a specific clarification: normal system calls from user-space programs do not create a GPL obligation. Your proprietary application that runs on Linux does not need to be GPL.

But kernel modules — code that runs inside the kernel itself — are a different matter:

```
Kernel driver licensing:
│
├── Open source driver (GPL v2)
│   ├── Full access to kernel internals
│   ├── Can use any kernel API
│   └── Source must be distributed
│
├── Proprietary driver (binary blob)
│   ├── Technically possible but heavily discouraged
│   ├── Limited to stable exported APIs only
│   ├── Kernel marks itself as "tainted"
│   └── Community will not help debug issues
│
└── What companies do in practice:
    ├── NVIDIA — historically shipped binary blobs
    │   └── Caused years of Linux compatibility problems
    │   └── Finally open sourced drivers in 2022
    └── Most hardware vendors — open source drivers
        └── Better support, better performance,
            community maintains them
```

NVIDIA's long refusal to open source their GPU drivers is a direct consequence of GPL v2. They wanted the performance benefits of kernel-level access without the source disclosure requirement. The result was years of poor Linux GPU support, constant breakage on kernel updates, and a hostile relationship with the Linux community. When they finally open sourced their drivers in 2022, support improved dramatically within months.

---

## LGPL — The Middle Ground

The GNU Lesser General Public License was created specifically to allow GPL-licensed libraries to be used in non-GPL software. Stallman initially called it the "Library GPL" and later renamed it "Lesser GPL" — he considered it a compromise, not an ideal.

---

### How It Differs From GPL

```
GPL says:
└── If you distribute software that incorporates
    this code, your whole work must be GPL

LGPL says:
└── If you distribute software that uses this library,
    you must keep the library itself open source
    BUT your application code can be proprietary
```

The key distinction is between incorporating code and using a library:

```
LGPL — the linking distinction:

Dynamic linking (LGPL allows proprietary application):
├── Your proprietary app
├── calls functions in
└── LGPL library (separate, dynamically loaded)
    └── Library stays LGPL, app stays proprietary ✓

Static linking (more complex, LGPL has conditions):
├── Your proprietary app
├── with LGPL library compiled directly in
└── Combined binary
    └── Must allow user to relink with modified library
        └── In practice: more complicated obligations
```

### When LGPL Is Used

LGPL is common for libraries that want wide adoption including in proprietary software, but want to ensure improvements to the library itself stay open:

- **glibc** — the GNU C library, LGPL so proprietary software can use it
- **Qt** — available under LGPL for certain uses
- **GTK** — LGPL, allows proprietary applications to use the GUI toolkit

If glibc were GPL, every proprietary application on Linux would need to be GPL to legally run. That would have killed commercial Linux adoption. LGPL solved this by keeping the library free while allowing proprietary applications to exist on top of it.

---

## AGPL — Closing the SaaS Loophole

The GPL has a gap. A company can take GPL software, modify it heavily, run it on their servers, and offer it as a web service — without ever distributing the software. Since they never distribute, the copyleft obligation never triggers. They get the benefits of GPL code without contributing anything back.

This gap became enormously important as web services replaced distributed software. By the mid-2000s, companies were building massive businesses on modified GPL software without ever sharing their improvements.

---

### The Loophole In Concrete Terms

```
GPL loophole — SaaS scenario:
│
├── Company takes GPL database software
├── Makes significant improvements
├── Runs it on their servers
├── Offers it as a cloud service to customers
│
├── Do they distribute the software? NO
│   └── Customers access it via web browser
│       They never receive a copy
│
├── Does GPL trigger? NO
│   └── GPL only triggers on distribution
│       Running a service is not distribution
│
└── Result: Company profits from GPL improvements
           Community gets nothing back
           License intended to prevent exactly this
```

### What AGPL Does

The **Affero GPL** — AGPL — adds one additional trigger to GPL's copyleft condition: network use.

```
AGPL adds:
└── If you run modified AGPL software and allow users
    to interact with it over a network, you must make
    the complete source code available to those users
    under the AGPL
```

Running AGPL software as a web service now triggers the same source disclosure obligation as distributing it.

---

### When AGPL Triggers — The Exact Condition

```
AGPL triggers when ALL of these are true:
├── You have modified the AGPL software
├── You are running it on a server
└── Users interact with it over a network

AGPL does NOT trigger when:
├── You run it internally with no external users
├── You use it unmodified (though good practice to disclose)
└── Users do not interact with it over a network
```

---

### Why This Matters for a Developer

AGPL is increasingly common for developer tools, databases, and infrastructure software because cloud providers kept taking GPL infrastructure software and offering it as managed services without contributing back:

```
The pattern AGPL was designed to stop:
│
├── MongoDB (originally AGPL)
│   └── AWS offered MongoDB as a managed service
│       └── AWS improved it, shared nothing
│       └── MongoDB eventually switched to SSPL
│
├── Elasticsearch (Apache 2.0)
│   └── AWS offered Elasticsearch as a managed service
│       └── AWS improved it, shared nothing
│       └── Elastic switched to SSPL
│
└── The AGPL was designed for exactly this scenario
    But companies switched to non-open licenses instead
    because AGPL alone was not sufficient deterrent
```

If you are evaluating a dependency and it is AGPL — especially a library or service component — you need to understand whether your use constitutes network interaction. If it does, your modifications must be open sourced under AGPL. Many companies have a blanket policy of not using AGPL dependencies in commercial products for exactly this reason.

---

## License Compatibility — What Can Combine With What

You cannot just mix any two open source licenses together. Different copyleft conditions can be incompatible — requiring contradictory things from you at the same time.

---

### Why Incompatibility Is a Real Problem

```
Incompatibility scenario:
│
├── Library A is GPL v2
│   └── "If you distribute, everything must be GPL v2"
│
├── Library B is Apache 2.0
│   └── "You can use this in anything, including GPL v3"
│       (Apache 2.0 is compatible with GPL v3 but not GPL v2)
│
├── You want to combine A and B into one program
│   └── GPL v2 says the whole thing must be GPL v2
│   └── But Apache 2.0 has patent clauses GPL v2 lacks
│   └── You cannot simultaneously satisfy both
│
└── Result: You cannot legally combine them
           Must choose one or find alternative
```

---

### Compatibility Matrix

```
                MIT    Apache   LGPL    GPL v2   GPL v3   AGPL
                       2.0
─────────────────────────────────────────────────────────────────
MIT              ✓       ✓       ✓        ✓        ✓        ✓
Apache 2.0       ✓       ✓       ✓        ✗        ✓        ✓
LGPL             ✓       ✓       ✓        ✓        ✓        ✓
GPL v2           ✓       ✗       ✓        ✓        ✗        ✗
GPL v3           ✓       ✓       ✓        ✗        ✓        ✓
AGPL             ✓       ✓       ✓        ✗        ✓        ✓

✓ = Can be combined into GPL/AGPL work
✗ = Incompatible — cannot legally combine
```

The most important incompatibility in practice: **Apache 2.0 and GPL v2 cannot be combined**. This is why the Linux kernel — GPL v2 — cannot incorporate Apache 2.0 licensed code directly. The patent clauses in Apache 2.0 impose requirements that GPL v2 does not, making them legally incompatible.

GPL v3 was partly written to fix this — it is compatible with Apache 2.0. But Linus Torvalds has explicitly refused to upgrade Linux to GPL v3, partly due to the added restrictions around hardware tivoization and partly because coordinating a license change across thousands of contributors is practically impossible without unanimous consent.

---

## CLA vs DCO — How You Actually Transfer Rights

When you contribute to an open source project, there is a legal question that most developers never think about: what exactly have you given the project? You wrote the code — you own the copyright. The project needs some rights to use and distribute it. How does that transfer happen?

There are two main mechanisms: the **Contributor License Agreement** and the **Developer Certificate of Origin**.

---

### What a CLA Is

A Contributor License Agreement is a legal contract you sign before your contributions can be accepted. It transfers certain rights from you to the project or its governing organization.

```
CLA — Individual (ICLA):
├── You sign as an individual
├── Grant the project a license to use your contributions
├── Usually grant patent rights too
├── Often allow the project to relicense your contributions
└── You retain copyright ownership

CLA — Corporate (CCLA):
├── Your employer signs on behalf of all employees
├── Covers all contributions made during employment
├── Employer grants rights to everything employees contribute
└── Employees may also need to sign individual CLAs
```

---

### The Schedule A Problem

The most painful part of the corporate CLA process is **Schedule A** — the list of employees whose contributions are covered. Every time a new employee joins and wants to contribute, they need to be added. When an employee leaves, technically they should be removed. Large companies with high turnover can have dozens of CLA maintenance events per year across multiple projects.

```
Schedule A maintenance reality:
│
├── New engineer hired → needs to be added to Schedule A
│   └── Legal review, signature, update filed with project
│
├── Engineer leaves → should be removed from Schedule A
│   └── Often forgotten, creates ambiguity
│
├── Engineer changes role → may affect coverage
│
└── Company with 10,000 engineers contributing to
    50 open source projects
    └── Schedule A maintenance is a real operational burden
```

---

### What a DCO Is

The **Developer Certificate of Origin** is a much simpler mechanism. Instead of signing a legal contract, you add a single line to every commit:

```
Signed-off-by: Your Name <your.email@example.com>
```

By adding this line, you are certifying — under the DCO — that:

```
DCO certification (what Signed-off-by means):
├── The contribution was created by you, OR
├── It is based on previous work with compatible license, OR
├── It was provided to you by someone who certified one of the above
└── You understand this contribution is public and may be
    incorporated into the project
```

No contract. No legal process. No Schedule A. Just a line in the commit message that creates a documented, traceable record of who contributed what and what they certified about their right to contribute it.

---

### Why the Kernel Uses DCO

The Linux kernel switched to DCO specifically because of the legal burden CLAs create for a project with thousands of contributors across hundreds of employers. Linus has been explicit: the kernel does not want a CLA because it would create a barrier to contribution and a maintenance nightmare.

```
Linux kernel chose DCO because:
├── Thousands of contributors worldwide
├── Hundreds of different employers
├── No single organization to hold CLA agreements
└── DCO creates legal clarity without legal friction

FINOS projects use CLA because:
├── Financial institutions need clear IP ownership records
├── Regulatory requirements around IP documentation
├── Fewer contributors, more institutional
└── Legal certainty worth the friction
```

The choice between CLA and DCO is not about which is more legally robust — both create legally meaningful records. It is about the tradeoff between legal certainty and contribution friction. High-volume community projects choose DCO. Projects with institutional contributors and regulatory requirements choose CLA.

---

## Openwashing Licenses — The Ones That Look Open But Are Not

Not every license that uses open source language is actually open source. Two licenses in particular have become common in the last decade and are frequently mistaken for genuine open source:

### SSPL — MongoDB's Answer to AWS

In 2018, MongoDB replaced the AGPL with their own **Server Side Public License**. The stated reason was that cloud providers — primarily AWS — were offering MongoDB as a managed service and not contributing back.

The SSPL goes further than AGPL. It requires that if you offer the software as a service, you must open source not just your modifications to the software, but everything used to offer the service — your monitoring tools, your provisioning systems, your management interfaces, everything in your stack.

```
SSPL requirement:
└── If you offer the software as a service,
    you must release under SSPL:
    ├── Your modifications to the software itself
    ├── All software used to run the service
    ├── All management and monitoring software
    ├── All provisioning and orchestration software
    └── Essentially your entire service stack
```

The OSI reviewed SSPL and rejected it as non-open-source. The requirement to open source your entire service stack goes far beyond any accepted open source definition. It is effectively a prohibition on commercial use as a service unless you are willing to open source your entire business.

---

### BSL — HashiCorp's Answer to Competition

The **Business Source License** takes a different approach. It is time-limited: software under BSL eventually converts to an open source license after a specified period (usually four years). But during the BSL period, commercial use that competes with the licensor is prohibited.

```
BSL structure:
├── During BSL period (typically 4 years):
│   ├── Can use for non-commercial purposes
│   ├── Can use for internal business operations
│   └── Cannot use to compete commercially with licensor
│
└── After BSL period:
    └── Converts to specified open source license
        (often GPL or Apache 2.0)
```

The OSI does not recognize BSL as open source. The restriction on competitive use violates the basic open source requirement that licenses not discriminate against fields of endeavor.

Both SSPL and BSL are legitimate business decisions — companies trying to prevent value extraction without contribution. But they are not open source. Treating them as open source when evaluating dependencies creates real legal risk.

---

## The Pattern Across All of This

Every license in this file is an answer to the same question: **what does it mean to share code freely, and what obligations does that create?**

```
MIT:        Share freely, just credit me
Apache 2.0: Share freely, credit me, and I protect you from patents
GPL:        Share freely, but keep it free downstream
LGPL:       Keep the library free, use it in anything
AGPL:       Keep it free even when running as a service
CLA:        Formal rights transfer with legal clarity
DCO:        Informal certification with documented trail
SSPL/BSL:   Not actually open source — commercial restrictions
```

The license a project chooses tells you something real about what the authors value, what risks they are protecting against, and what obligations you take on when you use their work.

Reading the LICENSE file before using a dependency is not paranoia. It is the minimum due diligence that protects you, your employer, and your users.

---

> **Now read the next file — because knowing which license a dependency uses is only useful if you know whether that dependency is actually safe to include at all.**
> **Supply chain attacks have nothing to do with licenses and everything to do with trust → [03-supply-chain-security.md](03-supply-chain-security.md)**
