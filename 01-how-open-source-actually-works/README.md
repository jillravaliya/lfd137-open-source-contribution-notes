# How Open Source Actually Works: The Real Story Behind the Movement


> Ever wondered why Linux is free? Why thousands of developers contribute to software they do not own? Why Google, Microsoft, and Meta all contribute to the same kernel — and nobody calls it a conspiracy?

**You're about to find out — starting from a broken printer in 1980.**

---

## What's Inside This File

> We are exploring how open source actually works — not the marketing version, the real version. Where it came from, why it split into two movements, how communities govern themselves without a boss, and what happens when companies pretend to be open without actually being open.

```
01-how-open-source-actually-works.md
│
├── The Printer — Stallman, Xerox 9700, MIT AI Lab 1980
│   ├── Why he could not get the source code
│   ├── The Carnegie Mellon NDA refusal
│   └── GNU Project 1983 → Manifesto 1985 → GPL 1989
│
├── What "Free Software" Actually Means
│   ├── Free as in freedom, not price
│   ├── The four freedoms (0, 1, 2, 3)
│   └── Copyleft — why it exists and how it works
│
├── Why OSI Split From FSF — Pragmatists vs Idealists
│   ├── Netscape 1998 — the moment that triggered the split
│   ├── Eric Raymond + Bruce Perens coin "open source"
│   ├── FSF moral argument vs OSI pragmatic argument
│   └── Why the split is still not resolved today
│
├── How Open Source Communities Govern Themselves
│   ├── BDFL model — Linus Torvalds, patch flow, earned authority
│   ├── Foundation model — Linux Foundation, Apache, Python
│   └── Committee model — Python PEP process step by step
│
├── What Openwashing Is
│   ├── Llama 2 — Meta's license restrictions exposed
│   └── Terraform BSL switch — HashiCorp, OpenTofu fork
│
├── Where Finance Appears — The FINOS Problem
│   └── Why competitors need neutral ground to collaborate
│
└── The Pattern — printer → GPL → Linux → internet
```

> Want the full history first — Unix, AT&T, BSD, the legal wars, Oracle, Apple, SCO?
> That story lives here → **[unix-to-linux/README.md](unix-to-linux/README.md)**

---

## What Is Open Source — The Real Idea

Most people learn the definition: source code that anyone can read, modify, and distribute. That is accurate but it misses the point entirely.

Open source is not a licensing strategy. It is not a business model. It started as a direct response to a specific moment where one developer realized that software had become something it was never supposed to be — private, locked, and controlled.

The full story of how we got from Bell Labs in 1969 to Linux running 90% of the internet today — Unix, AT&T turning proprietary, BSD, the BSD lawsuit, GNU, why Linus built a kernel, Apple taking BSD and closing it, SCO trying to sue Linux out of existence, Oracle killing OpenSolaris overnight, the API wars — that story is deep and worth knowing completely.

> **It lives here → [unix-to-linux/README.md](unix-to-linux/README.md)**
>
> Read it first if you want full context. Come back here for how open source works today.

---

## The Printer — Why Stallman Started Everything

In 1980, Richard Stallman was a programmer and hacker at the MIT Artificial Intelligence Lab. The lab had a Xerox 9700 laser printer. It was slow. Jobs would get stuck in the queue and nobody would know. The printer would sit jammed while everyone waited.

Stallman had a straightforward idea. He would modify the printer's software to send a notification when the printer jammed — so people could go fix it instead of waiting. He had done exactly this with an older printer at the lab. It took a few hours and worked perfectly.

But the Xerox 9700 was different.

Xerox had not provided the source code. The software that ran the printer was a compiled binary — you could run it, but you could not read it, modify it, or fix it. Stallman asked Xerox for the source code. Xerox refused. He then found out that a researcher at Carnegie Mellon had received the source code from Xerox — under a non-disclosure agreement. Stallman asked that researcher for a copy. The researcher refused. He was legally bound not to share it.

That refusal — one developer choosing a legal obligation to a corporation over helping a fellow developer — is what started the entire free software movement.

Stallman's reaction was not frustration at the inconvenience. It was moral outrage. He believed that withholding source code was a betrayal of the community that made software possible. In 1983 he announced the GNU Project. In 1985 he published the GNU Manifesto. In 1989 he released the first version of the GPL license.

The entire structure of what we now call open source grew from that printer.

---

## What "Free Software" Actually Means

Stallman made a distinction that still matters and still gets confused:

```
"Free software" means free as in freedom — not free as in price.
```

He defined four specific freedoms that every user of software should have:

```
Freedom 0 — Run the program for any purpose
            └── No restrictions on who can use it or how

Freedom 1 — Study how the program works
            └── Requires access to source code

Freedom 2 — Redistribute copies
            └── Help your neighbour, share what you have

Freedom 3 — Distribute modified versions
            └── Your improvements benefit everyone
```

This is not about cost. You can sell free software. The point is that users must have control over the software they use. A program you cannot read, modify, or share is a program that controls you — not one that you control.

This distinction explains why the GPL was written the way it was. The GPL has a condition called **copyleft**: if you distribute software that includes GPL code, you must also distribute the source code under the same terms.

The logic behind copyleft:

```
Someone gave you freedom
        ↓
You built something with it
        ↓
You cannot take that freedom away from
the people you pass it to
        ↓
Freedom must flow forward — not stop with you
```

Without copyleft, a company could take GPL code, add proprietary code on top, and ship a binary with no source. The freedoms would die at that company's door. Copyleft prevents that.

---

## Why OSI Split From FSF — Pragmatists vs Idealists

By the mid-1990s, the free software movement had produced real, serious software. GNU tools — gcc, bash, make, glibc — were running on servers everywhere. Linux had appeared in 1991. There was clearly something powerful happening.

But the FSF's moral framing was a problem for businesses. Companies wanted to use this software and contribute back, but they did not want to join a movement that called proprietary software ethically wrong. The language of freedom and obligation made corporate lawyers nervous.

In 1998, Netscape released the source code to their browser. This was a major moment — a real commercial company releasing real commercial software. Eric Raymond and Bruce Perens used that moment to launch something different.

They coined the term **open source** — deliberately dropping the word "free" and all its moral weight — and founded the **Open Source Initiative**.

The OSI argument was purely pragmatic:

> Open source produces better software. More eyes on the code means more bugs found. Transparent development means faster iteration. You do not need to believe in software freedom as a moral principle — you just need to recognize that open development works better.

Stallman hated this. He still does. His argument is that by removing the ethical foundation, you give companies an easy way to claim the benefits of open development — community trust, free contributions, ecosystem growth — while retaining control in ways that harm users.

Both sides were right about something real:

```
FSF / Stallman:                         OSI / Raymond:
────────────────────────────────────────────────────────────
Software freedom is a moral issue  vs  Open development is pragmatically better
GPL protects the commons           vs  Permissive licenses enable more adoption
Proprietary software harms users   vs  Proprietary software is a business choice
The movement needs principles      vs  The movement needs corporate participation
```

This split is not resolved. Every debate about whether a license is "really" open source, every argument about copyleft vs permissive licensing, every discussion about whether a company is genuinely contributing or just extracting — all of it traces back to this disagreement from 1998.

---

## How Open Source Communities Govern Themselves

One of the genuinely surprising things about open source is that large, complex, critical software gets built and maintained without a traditional management structure. Nobody at Linux has a manager telling them what to work on. Nobody at Python has a boss approving commits.

How does this actually work? There are three main models.

---

### The Benevolent Dictator For Life Model

Some projects have a single person with final authority over all decisions. The community contributes, debates, and proposes — but one person has the final word.

**Linus Torvalds** is the most well known example. He created Linux in 1991 and has maintained final authority over what enters the kernel ever since. The title BDFL is partly ironic but the authority is completely real.

Here is what that actually looks like in practice:

```
Patch submitted by contributor
        ↓
Reviewed by subsystem maintainer
        ↓
Accepted into subsystem tree
        ↓
Subsystem maintainer sends pull request to Linus
        ↓
Linus reviews and decides
        ↓
    ┌──────────┬──────────┐
  Merged    Rejected   Sent back
 into next  with       for
  release   reason    changes
```

Linus has rejected patches from major companies. He has reverted commits from senior maintainers. He has publicly and bluntly disagreed with contributors — and his decision stands. This works because he has demonstrated over 30+ years that his technical judgment is sound. The authority comes from earned trust, not a title.

The BDFL model fails when the dictator is unavailable, makes decisions the community strongly disagrees with, or when the project grows too large for one person to oversee. Python hit this in 2018 — Guido van Rossum stepped down after a contentious PEP decision, which led to a steering council.

---

### The Foundation Model

Larger projects that need corporate participation, legal infrastructure, and long-term sustainability move to a foundation structure.

The key insight is separating two things that should not be mixed:

```
Technical decisions
└── Stay with the people doing the technical work
    └── Maintainers, contributors, subsystem leads

Legal and financial decisions
└── Go through people who understand legal and financial reality
    └── Foundation board, lawyers, accountants
```

**The Linux Foundation** holds the Linux trademark, manages infrastructure, and employs developers — but does not control technical decisions. Those still go through maintainers and ultimately Linus.

**The Apache Software Foundation** hosts hundreds of projects, each with their own Project Management Committee. Decisions are made by consensus among active contributors.

**The Python Software Foundation** manages the language, package index, and community infrastructure while the steering council handles technical direction.

Without a foundation, a project has no legal identity. It cannot hold a trademark. It cannot accept donations cleanly. It cannot sign contracts. It cannot protect contributors from liability when someone sues over a bug. A foundation turns a loose community into something that can actually exist and operate in the real world.

---

### The Committee Model — Python's PEP Process

Python uses a structured proposal system for any significant change to the language. It is worth understanding because it shows how a community makes real technical decisions transparently without chaos.

```
STEP 1: Author writes the PEP
        ├── What problem does this solve?
        ├── What is the proposed solution?
        ├── What alternatives were considered?
        └── What are the backward compatibility implications?

STEP 2: Draft posted publicly
        ├── Community discusses on mailing list
        ├── Anyone can comment, criticise, propose changes
        └── Author updates PEP based on feedback

STEP 3: Decision
        ├── Language changes    → Steering Council decides
        ├── Informational PEPs  → Community consensus
        └── Process PEPs        → Steering Council decides

STEP 4: Outcome
        ├── Accepted   → Goes into next Python version
        ├── Rejected   → Documented with reasoning, stays public forever
        ├── Withdrawn  → Author pulls it back
        └── Deferred   → Good idea, wrong time
```

Every decision is documented. The reasoning is public. Anyone can propose. Authority is clear. Ten years later you can look up exactly why a decision was made, who argued what, and what alternatives were rejected. This is how a language used by tens of millions of people changes without breaking into chaos.

The Linux kernel uses a similar but less formal version. Significant changes go through an RFC (Request for Comments) process on the mailing list. Subsystem maintainers decide what enters their subsystem. Linus decides what enters mainline.

---

## What Openwashing Is

Openwashing is when a company uses the language and aesthetics of open source without providing the freedoms that open source is supposed to guarantee.

It matters for a specific reason: developers trust open source projects with their time, their contributions, and their infrastructure decisions. When that trust is manufactured — when a project looks open but is not — developers end up dependent on software they cannot actually control. They contribute work that benefits a company without the reciprocal obligation that makes open source sustainable.

---

### Llama 2 — Meta's "Open" Model

In 2023, Meta released Llama 2 with significant public statements about openness. The reality is more complicated.

```
Llama 2 license says:
├── Cannot use if product has 700M+ monthly active users
├── Cannot use to train other AI models without Meta's permission
├── Fine-tuned versions must carry the Llama 2 name
└── Meta can revoke your license if they decide you violated terms
```

The OSI definition requires that a license not restrict who can use the software or for what purpose. A license that says "you can use this unless you are too successful" is not open source. It is a proprietary license with a source code release attached.

Meta received enormous free development work and community trust while retaining control over the most commercially valuable uses. The OSI officially stated Llama 2 is not open source.

---

### HashiCorp and the Terraform BSL Switch

HashiCorp built Terraform — the dominant infrastructure-as-code tool — under the Mozilla Public License, a genuine open source license. The community built an enormous ecosystem over years: providers, modules, tutorials, consulting businesses, hosted services.

In August 2023, HashiCorp switched Terraform's license to the **Business Source License**. The BSL prohibits using the software to compete with HashiCorp commercially.

```
Before BSL:
└── Anyone can use, modify, distribute Terraform freely

After BSL:
└── Cannot use Terraform to build a product that
    competes with HashiCorp's commercial offerings

Who got hurt immediately:
├── Companies that built businesses on top of Terraform
├── Hosted Terraform services that now potentially violate the license
└── Contributors whose years of work now serves a proprietary product
```

The community forked the project immediately, creating **OpenTofu** under the Linux Foundation.

This is exactly what the FSF warned about. Because Terraform was not under a copyleft license, HashiCorp could change the terms unilaterally. A GPL license would have prevented this — relicensing would have required agreement from every contributor.

MongoDB, Elasticsearch, and Redis have all made the same move. The pattern is always identical:

```
Build community trust on open source
        ↓
Reach commercial maturity
        ↓
Switch to a license that protects revenue
        ↓
Keep the community contributions
Lose the obligations
```

---

## Where Finance Appears — The FINOS Problem

There is one specific problem the finance industry ran into that illustrates why neutral foundations matter — not as a bank story, but as a real governance problem.

Goldman Sachs and JPMorgan Chase both needed common financial data infrastructure. Both had engineers who could build it. But they are direct competitors. Their engineers cannot privately discuss technical problems — antitrust risk. They cannot share code directly — IP and regulatory risk.

Without a neutral foundation, the collaboration cannot happen at all.

**FINOS** — the Fintech Open Source Foundation — exists to solve exactly this. Competing companies contribute independently to shared projects under neutral governance. Neither company controls the project. Everything is public.

```
Without neutral foundation:

CompanyA engineer <——— direct communication ———> CompanyB engineer
                         (antitrust risk)
                         Collaboration never happens.

─────────────────────────────────────────────────────────────────────

With neutral foundation (FINOS / Apache / Linux Foundation):

CompanyA engineer ——> Foundation project <—— CompanyB engineer
                        (neutral ground)
                        Both contribute independently.
                        Everything public.
                        Collaboration happens safely.
```

This is not a finance-specific insight. The Linux Foundation exists for the same reason. Google, Microsoft, Amazon, and Meta all contribute to Linux. They compete in almost every market. The foundation model is what makes that legally and practically possible.

The finance case just makes it unusually visible because the regulatory constraints are so explicit.

---

## The Pattern That Runs Through All of This

Open source started as a moral position about software freedom. It became a pragmatic development methodology. It created governance models that let competitors collaborate. It produced the infrastructure that runs almost everything.

And it is constantly under pressure from companies that want the benefits — community, trust, free development work — without the obligations that make those benefits possible.

Understanding this is not background knowledge. It is the context for every licensing decision, every contribution process, every supply chain security problem in the files that follow.

```
The printer Xerox would not share the source code for
        ↓
Led Stallman to write the GPL
        ↓
The GPL is why Linux cannot be made proprietary
        ↓
Linux being non-proprietary is why it runs
90% of bank servers, every Android phone,
and most of the internet
        ↓
That is not a coincidence
That is the design working exactly as intended
```

---

> **Now read the next file — because once you understand what a license actually is, you will never look at an import statement the same way again.**
