# Antitrust in Open Source: Why Competitors Can Build the Same Thing Together

---

> Ever wondered why the Linux Foundation has lawyers at every major technical meeting? Why Google, Microsoft, Meta, and Amazon can all contribute to the same kernel without the Department of Justice investigating? Why being an early contributor to an open source project that becomes a standard is not just a technical advantage — it is a structural market advantage that regulators watch? Why open source foundations write antitrust policies that developers are required to read before participating in governance?

**You're about to find out — and after this, you will understand why the most important conversations at open source foundations happen in rooms with lawyers present.**

---

## What's Inside This File

> We are exploring why antitrust law applies to open source collaboration — the legal theory, the real risks, and where the line is between legitimate collaboration and illegal coordination.

```
06-antitrust-in-open-source.md
│
├── Why Antitrust Applies to Open Source at All
│   ├── What antitrust law actually prohibits
│   ├── Why open source is not automatically exempt
│   └── The collaboration paradox
│
├── The Linux Foundation Antitrust Policy
│   ├── What it says and why it exists
│   ├── What is explicitly prohibited at meetings
│   └── Why developers have to read it before governance
│
├── De Facto Standard Risk
│   ├── What a de facto standard is
│   ├── Early contributor advantage — structural
│   └── When standard-setting becomes anticompetitive
│
├── Collaboration vs Coordination — Where the Line Is
│   ├── What legitimate collaboration looks like
│   ├── What illegal coordination looks like
│   └── The conversations you should never have
│
├── FDC3 — A Financial Services Example
│   ├── What FDC3 is
│   ├── Who shaped it and what that means
│   └── How it plays out in practice
│
└── OpenMAMA — When Standards Determine Markets
    ├── What OpenMAMA is
    ├── The structural advantage problem
    └── What regulators actually watch
```

---

## Why Antitrust Applies to Open Source at All

Most developers think of antitrust as something that applies to mergers, monopolies, and predatory pricing. The idea that writing code together with competitors could raise antitrust concerns seems abstract. It is not.

### What Antitrust Law Actually Prohibits

Antitrust law in the US is primarily governed by the Sherman Antitrust Act (1890) and the Clayton Act (1914). The core prohibitions:

```
Sherman Act core prohibitions:
│
├── Section 1: Contracts, combinations, or conspiracies
│   in restraint of trade
│   └── Two or more parties agreeing to do something
│       that restricts competition
│       └── Does not require formal agreement
│       └── A nod, an email, a conversation at a
│           conference can be enough
│
├── Section 2: Monopolisation or attempted monopolisation
│   └── Single company using market power to
│       exclude competitors
│
└── Both apply to open source when:
    ├── Competitors collaborate in ways that restrict
    │   competition between them
    └── Standards are set in ways that exclude
        or disadvantage specific competitors
```

The key word in Section 1 is "agreement." It does not need to be written. It does not need to be explicit. Two competitors sitting in a room at an open source foundation meeting, discussing pricing strategies — even casually — creates antitrust exposure for both companies. Courts have found violations based on conversations at industry events, shared lunches, and golf games.

### Why Open Source Is Not Automatically Exempt

Open source collaboration is not inherently anticompetitive. In fact, most open source collaboration is clearly pro-competitive — it enables smaller companies to use infrastructure they could not build alone, it creates interoperability, it drives down costs across an industry.

But open source collaboration happens between competitors. And when competitors collaborate, the antitrust framework applies regardless of the stated purpose.

```
Open source ≠ antitrust exemption:
│
├── Collaborating on a shared codebase: generally fine
│   └── Building common infrastructure together
│   └── Sharing maintenance costs
│   └── Creating interoperability
│
├── Using that collaboration to coordinate
│   on commercial behaviour: not fine
│   └── Agreeing to price similarly
│   └── Agreeing not to compete in certain areas
│   └── Excluding specific competitors from
│       the collaboration without legitimate reason
│
└── The line is not about the code
    └── It is about what conversations happen
        around the code
        └── And what market effects result
```

### The Collaboration Paradox

Open source creates a genuine paradox for antitrust analysis. The same collaboration that produces a shared kernel, a shared compiler, or a shared data format also creates a forum where competitors regularly interact. Those interactions are useful and necessary for the technical work. They are also exactly the kind of competitor contact that antitrust law monitors.

```
The paradox:
│
├── To build good shared infrastructure, you need:
│   └── Regular meetings between competing companies
│   └── Technical discussions that reveal roadmaps
│   └── Agreement on technical direction
│   └── Shared decision-making on standards
│
├── This looks similar to what antitrust prohibits:
│   └── Regular meetings between competitors
│   └── Information sharing about business plans
│   └── Agreement on market direction
│   └── Shared decision-making affecting market
│
└── The difference is intent and subject matter
    └── Technical collaboration: fine
    └── Commercial coordination disguised as
        technical collaboration: not fine
    └── The distinction is not always obvious
        in the moment
```

This is why antitrust counsel is present at major open source foundation meetings. Not because everyone is assumed to be acting in bad faith. Because the settings are genuinely ambiguous, and the cost of a mistake is severe.

---

## The Linux Foundation Antitrust Policy

The Linux Foundation Antitrust Policy is a document that participants in Linux Foundation projects are required to acknowledge. It is not bureaucratic box-checking. It reflects specific legal risks that have been identified by antitrust counsel as relevant to the activities of these projects.

### What It Says

```
Linux Foundation Antitrust Policy — core provisions:
│
├── What participants must NOT do at meetings:
│   ├── Discuss pricing, discounts, or terms of sale
│   ├── Discuss market share or market allocation
│   ├── Discuss bids on specific contracts
│   ├── Discuss whether to deal with specific
│   │   suppliers, customers, or competitors
│   └── Agree on anything that affects competition
│       between member companies
│
├── What participants CAN do:
│   ├── Discuss technical standards and specifications
│   ├── Collaborate on shared code and documentation
│   ├── Share publicly available information
│   ├── Discuss interoperability requirements
│   └── Make technical decisions by consensus
│
└── The bright line:
    └── Technical decisions about the code: permitted
        Commercial decisions affecting the market: not permitted
```

### Why Developers Have to Read It

Every person who participates in Linux Foundation technical governance — serving on technical steering committees, participating in special interest groups, attending working group meetings — is asked to acknowledge the antitrust policy.

This is not just legal protection for the Foundation. It is genuine risk management for the individuals involved.

```
Individual antitrust exposure:
│
├── Antitrust violations are not just company liability
│   └── Individuals can be personally liable
│   └── Criminal penalties include prison time
│       (up to 10 years under Sherman Act)
│
├── Developers serving on technical committees
│   are participating in competitor coordination
│   └── Even if the coordination is about code
│   └── If the conversation drifts to commercial topics
│       personal exposure is real
│
└── The policy protects individuals by:
    ├── Making clear what conversations are off-limits
    ├── Giving them a basis to stop problematic discussions
    └── Documenting that proper procedures were followed
        if a challenge ever arises
```

---

## De Facto Standard Risk

A de facto standard is a technical specification that becomes the dominant approach in a market not through formal standardisation processes but through widespread adoption. Open source projects become de facto standards when adoption reaches a point where not being compatible with them is a market disadvantage.

Linux is a de facto standard for server operating systems. Kubernetes is a de facto standard for container orchestration. OpenSSL was a de facto standard for TLS implementation.

### Early Contributor Advantage — Structural Not Accidental

When an open source project is becoming a standard, the companies that contributed earliest have structural advantages that persist long after the standard is established.

```
Early contributor structural advantages:
│
├── Technical familiarity
│   └── Deep knowledge of internals, edge cases, gotchas
│   └── Takes years for competitors to develop
│
├── Influence over design
│   └── Early architectural decisions shape everything
│   └── Decisions made before others joined
│       already constrain future choices
│
├── Maintainer positions
│   └── Early contributors often become maintainers
│   └── Maintainers have merge authority
│   └── Merge authority = influence over what ships
│
├── Community relationships
│   └── Trust built over years of participation
│   └── Newcomers start with zero credibility
│
└── Internal alignment
    └── Internal systems built on deep knowledge
        of the standard as it was being designed
    └── Competitors must adapt to the standard
        you helped design to fit your architecture
```

This advantage is not inherently anticompetitive. Being early and building expertise is how markets work. The problem arises when the advantage is deliberately engineered — when companies participate in open source standards specifically to shape them in ways that disadvantage competitors, rather than to build the best shared infrastructure.

### When Standard-Setting Becomes Anticompetitive

```
Anticompetitive standard-setting patterns:
│
├── Designing specifications around your patents
│   └── Then licensing those patents on terms that
│       competitors cannot meet
│   └── FRAND (Fair, Reasonable, Non-Discriminatory)
│       licensing requirements exist for this reason
│
├── Shaping APIs to favour your implementation
│   └── "Standard" that happens to match your
│       internal architecture precisely
│   └── Competitors must build adapters
│       you already have native support
│
├── Excluding competitors from governance
│   └── Using procedural mechanisms to block
│       competitors from influencing design
│   └── Structuring participation requirements
│       that favour incumbents
│
└── Coordinating adoption pace
    └── Large companies agreeing informally to adopt
        the standard simultaneously
    └── Creates lock-in for the ecosystem
        before competitors can respond
```

The line between "we built this well and it became standard" and "we designed this to lock in the market" is not always clear from the outside. Regulators look at the totality of the behaviour over time.

---

## Collaboration vs Coordination — Where the Line Is

The practical question for any developer participating in open source governance is: what conversations are acceptable and what conversations are not?

### What Legitimate Collaboration Looks Like

```
Legitimate open source collaboration:
│
├── Technical discussions
│   ├── How should this API be structured?
│   ├── Which algorithm performs better for this use case?
│   ├── How do we handle backwards compatibility?
│   └── What should the security model be?
│
├── Roadmap discussions
│   ├── What features should the next release include?
│   ├── Which bugs are blocking adoption?
│   └── What does the community need in 12 months?
│       (community needs — not commercial roadmap)
│
├── Governance discussions
│   ├── How should we structure the TSC?
│   ├── What should the contribution process be?
│   └── How do we handle security disclosures?
│
└── All of the above: fine
    └── Subject to the content staying technical
    └── The moment it shifts to commercial strategy:
        stop the conversation
```

### What Illegal Coordination Looks Like

```
Illegal coordination — explicit examples:
│
├── "We should all price our support contracts
│   in the same range so customers don't play us off"
│   └── Price fixing — per se illegal
│
├── "Let's agree that Company A focuses on banking
│   and Company B focuses on insurance"
│   └── Market allocation — per se illegal
│
├── "We shouldn't certify Company C's implementation
│   because they're undercutting everyone on price"
│   └── Group boycott — per se illegal
│
└── "If we all delay adoption until Q3 it'll be
│   too late for the startup to get traction"
    └── Coordination to exclude competitor — illegal
```

### The Conversations You Should Never Have

The hardest cases are not explicit price-fixing discussions. They are the conversations that happen naturally in settings where technical and commercial people mix — the hallway at a conference, the dinner after a foundation meeting, the Slack channel that started as technical and drifted.

```
Conversations that create exposure:
│
├── "What are you charging for your implementation?"
│   └── Even asking — not agreeing — creates risk
│
├── "Are you going to support Company X's proposal?
│   We're not going to."
│   └── Coordinating votes on technical proposals
│       based on commercial relationships
│
├── "We're planning to launch in March —
│   when are you launching?"
│   └── Sharing launch timing with a competitor
│       is information that can constitute coordination
│
└── "Do you think we should all wait for
│   the standard to mature before competing?"
    └── Agreement to delay competition
        even framed technically
```

The safe response to any of these is to say clearly: "I don't think we should be discussing this here" and redirect to technical topics. Doing this visibly, in front of others, creates a record. Staying silent does not.

---

## FDC3 — A Financial Services Example

**Financial Desktop Connectivity and Collaboration** (FDC3) is an open standard maintained under FINOS that defines how financial desktop applications communicate with each other. It allows a trading application, a risk system, and a market data terminal to share context — passing a stock symbol from one to another so all applications update simultaneously.

### What FDC3 Is

Before FDC3, every financial desktop integration was custom. If a bank wanted Bloomberg, Refinitiv, and their internal trading system to talk to each other, they built a custom integration for each pair. Three applications means three integrations. Ten applications means forty-five integrations. The combinatorial explosion was a significant cost.

FDC3 creates a common language. Applications that implement FDC3 can communicate with any other FDC3-compliant application. One integration per application instead of one per pair.

```
FDC3 value proposition:
│
├── Without FDC3:
│   └── N applications = N*(N-1)/2 custom integrations
│       10 apps = 45 integrations
│       20 apps = 190 integrations
│
└── With FDC3:
    └── N applications = N implementations of one standard
        10 apps = 10 implementations
        20 apps = 20 implementations
```

### Who Shaped It and What That Means

FDC3 was initially developed by a small group of financial institutions and financial technology vendors before being donated to FINOS. The companies that participated in the initial design shaped the API decisions that all future participants would have to work within.

```
Standard-shaping advantage in FDC3:
│
├── Early participants defined:
│   ├── Context data formats (what a "Contact" looks like)
│   ├── Intent vocabulary (what actions applications advertise)
│   ├── Channel model (how context flows between apps)
│   └── App Directory specification
│
├── Companies that shaped these decisions:
│   └── Already have internal systems aligned to them
│   └── Their existing applications are FDC3-compliant
│       with minimal adaptation
│
├── Companies that joined later:
│   └── Must adapt existing systems to the standard
│   └── The standard was not designed for their architecture
│   └── Adaptation cost is real competitive disadvantage
│
└── This is structural advantage — not misconduct
    └── The early participants were not acting in bad faith
    └── They were building something genuinely useful
    └── The advantage is the natural consequence
        of being first
```

### The Antitrust Lens

The antitrust question is not whether early participants gained advantage. They did. The question is whether the governance structure going forward gives all participants fair ability to influence the standard.

```
FINOS governance protections:
│
├── Open governance — all members can propose changes
├── Transparent decision-making — votes are recorded
├── IP policy — contributions under Apache 2.0
│   └── No participant can assert patents against
│       compliant implementations
└── Antitrust policy — all participants acknowledge
    └── Commercial coordination is prohibited
```

The FINOS governance model is designed to prevent the structural advantage from hardening into anticompetitive lock-in. Whether it succeeds is an empirical question that plays out over years as the standard evolves and the market develops.

---

## OpenMAMA — When Standards Determine Markets

**Open Middleware Agnostic Messaging API** (OpenMAMA) is an open source abstraction layer for market data messaging in financial services. It allows applications to be written against a single API that can run on top of different underlying message buses — Solace, TIBCO, IBM MQ — without changing application code.

### The Structural Advantage Problem

OpenMAMA was contributed to the Linux Foundation by NYSE Technologies in 2011. NYSE Technologies built middleware products. OpenMAMA was the open source abstraction layer above those products.

```
OpenMAMA structural dynamic:
│
├── NYSE Technologies contributes OpenMAMA
│   └── Open source API for market data messaging
│
├── OpenMAMA supports multiple backends:
│   └── Including NYSE Technologies' own products
│   └── And competitor products
│
├── Banks adopt OpenMAMA as standard
│   └── Write their systems against OpenMAMA API
│
├── NYSE Technologies' products:
│   └── Deeply familiar with OpenMAMA internals
│   └── Tested against OpenMAMA continuously
│   └── Performance characteristics well understood
│
└── The question regulators ask:
    └── Does maintaining the standard give the
        contributor insight into competitors' usage?
    └── Do performance characteristics of the standard
        systematically favour the contributor's products?
    └── Are API decisions subtly shaped to make
        competing products harder to use?
```

These questions do not have simple answers. The motivations of companies that contribute to open source standards are usually genuinely mixed — there are real benefits to the ecosystem and there are real competitive benefits to the contributor. The antitrust analysis looks at outcomes, not motivations.

### What Regulators Actually Watch

```
Regulatory indicators that attract scrutiny:
│
├── Standard adoption that creates switching costs
│   └── Once the ecosystem builds on your standard,
│       switching to a competitor's approach costs
│       millions in adaptation
│
├── Governance that systematically favours incumbents
│   └── Participation requirements that small companies
│       or new entrants cannot meet
│
├── IP assertions against compliant implementations
│   └── Contributing to a standard and then asserting
│       patents against competitors who implement it
│   └── This is why FRAND licensing exists for standards
│
├── Timing coordination around standard releases
│   └── Large companies timing their product launches
│       to coincide with standard releases
│       in ways that exclude competitors
│
└── Exclusionary use of certification programs
    └── Compliance certification controlled by incumbents
    └── Used to exclude competitors on technical grounds
        that are not genuinely technical
```

The Linux Foundation, FINOS, Apache Software Foundation, and other major open source foundations have all developed IP policies and antitrust policies specifically in response to these concerns. They exist because without them, the foundations themselves could become liability exposure for member companies.

---

## The Pattern Across All of This

Antitrust in open source is not about the code. It is about what happens around the code — the conversations, the governance decisions, the standard-shaping, and the market effects that follow.

```
What keeps open source collaboration legal:
│
├── Clear separation of technical and commercial topics
│   └── Foundation meetings: technical
│   └── Commercial strategy: bilateral, not at meetings
│
├── Open governance
│   └── Any participant can propose changes
│   └── Decisions are transparent and recorded
│   └── No single participant can veto others
│
├── IP clarity
│   └── Contributions under open licenses
│   └── Patent grants for standard implementations
│   └── No assertion of patents against compliant code
│
├── Antitrust education
│   └── Participants know the rules
│   └── They know how to stop problematic conversations
│   └── There is a record that proper process was followed
│
└── Foundation oversight
    └── Legal counsel present at governance meetings
    └── Antitrust policy acknowledged by all participants
    └── Escalation path for concerns
```

The reason Google, Microsoft, Meta, and Amazon can all contribute to the Linux kernel without antitrust problems is not that antitrust does not apply. It is that the Linux Foundation has built governance structures, policies, and processes that keep the collaboration within the safe harbour. Remove those structures and the same collaboration becomes legally risky.

Any developer who participates in open source governance — serving on a technical steering committee, participating in a working group, helping to shape a standard — is operating in that space. Understanding why the rules exist makes it far easier to follow them.

---

> **These notes cover the legal and governance layer of open source. The technical layer — how the kernel actually processes contributions — is in the final file.**
> **How patches actually reach Linus → [linux-kernel-contribution/README.md](linux-kernel-contribution/README.md)**
