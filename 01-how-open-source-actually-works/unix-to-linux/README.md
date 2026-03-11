# From Unix to Linux: The Complete History

---

> Ever wondered how we got from a research operating system in 1969 to Linux running 90% of the internet today? Why did AT&T give Unix away free and then suddenly start charging? Why did Apple build macOS on free code — completely legally? How did one lawsuit nearly kill BSD and accidentally make Linux dominant? Why did Oracle buy a company just to kill its open source project overnight?

**This is the full story — no shortcuts.**

---

## What's Inside This File

```
unix-to-linux/README.md
│
├── 1969 — Unix Born at Bell Labs
│   ├── Ken Thompson, Dennis Ritchie
│   ├── First portable OS written in C
│   └── Why universities got it free for a decade
│
├── 1979 — AT&T Changes Everything
│   ├── Antitrust consent decree expires
│   ├── Unix goes commercial overnight
│   └── The moment that made everything necessary
│
├── BSD — The University Response
│   ├── Berkeley modifies Unix for a decade
│   ├── TCP/IP, virtual memory, fast filesystem
│   └── The BSD license — maximally permissive
│
├── 1983 — GNU Project Starts
│   ├── Stallman's response to the closed world
│   ├── gcc, bash, glibc, make — everything except a kernel
│   └── Why Hurd never worked
│
├── 1991 — Linus Builds the Missing Piece
│   ├── Minix frustration and the famous announcement
│   ├── GPL relicensing — Stallman convinces Linus
│   └── GNU tools + Linux kernel = complete OS
│
├── 1992 — The BSD Lawsuit That Nearly Killed Everything
│   ├── AT&T vs University of California
│   ├── Two years of frozen development
│   └── How it accidentally made Linux dominant
│
├── 2000 — Apple Takes BSD and Closes It
│   ├── XNU kernel — BSD + Mach
│   ├── Completely legal under BSD license
│   └── The permissive license consequence
│
├── 2003 — SCO vs IBM and the Linux FUD Campaign
│   ├── The $1 billion lawsuit
│   ├── 1500 companies threatened
│   └── How the community fought back and won
│
├── 2010 — Oracle Buys Sun, Kills OpenSolaris Overnight
│   ├── Five years of community work erased in 6 months
│   ├── illumos fork, ZFS survives on Linux
│   └── Why single-company projects are fragile
│
└── 2010-2021 — Oracle vs Google and the API Wars
    ├── Can you copyright an API?
    ├── What was at stake for all of open source
    └── Supreme Court rules — Google wins, barely
```

---

## 1969 — Unix Born at Bell Labs

Ken Thompson and Dennis Ritchie created Unix in 1969 at AT&T Bell Labs. To understand why it mattered, you have to understand what computing looked like before it.

Before Unix, every computer manufacturer wrote their own operating system. IBM's OS worked only on IBM hardware. DEC's OS worked only on DEC hardware. Software was written for specific machines. Portability barely existed.

Unix changed this in two ways.

First, it was written in C — a language Ritchie had also created at Bell Labs. C compiled to machine code for different processors. The same C source could be recompiled for different hardware. Unix became the first OS that could be ported to new machines without rewriting from scratch.

Second, it was built around a small set of clean ideas that have survived 55 years:

```
Unix core philosophy:
│
├── Everything is a file
│   └── Devices, pipes, sockets — all accessed like files
│
├── Do one thing well
│   └── Small tools that compose together
│
├── Programs that work together
│   └── Pipes connect output of one to input of another
│
└── Text as universal interface
    └── Tools communicate through readable text streams
```

AT&T distributed Unix to universities throughout the 1970s for essentially free — source code included. Computer science departments built their entire curriculum around it. An entire generation of developers learned to program by reading Unix source code. The culture of reading and modifying system source code as normal practice started here.

---

## 1979 — AT&T Changes Everything

In 1956, AT&T had signed a consent decree with the US government as part of an antitrust settlement. The decree prohibited AT&T from entering the computer business commercially. This is why they could give Unix away freely — they legally could not sell it.

In 1979, that consent decree expired. AT&T moved immediately.

```
Before 1979:
└── Unix + full source code
    ├── Available to universities for ~$99 nominal fee
    ├── Modify it, study it, teach with it
    └── Source sharing assumed and expected

After 1979:
└── Unix becomes commercial product
    ├── Commercial licenses: $10,000 — $100,000+
    ├── Source code restricted
    ├── Modifications require AT&T permission
    └── Redistribution prohibited
```

Developers who had built careers on open access to Unix source code suddenly found that access taken away. The reaction came from two directions simultaneously — Berkeley and MIT — and both shaped everything that followed.

---

## BSD — The University Response

The University of California, Berkeley had been using and modifying Unix since 1974. By 1979 their version — the **Berkeley Software Distribution** — had diverged substantially from AT&T's original.

Berkeley had added things AT&T had not built:

```
BSD additions to Unix:
│
├── Virtual memory system
│   └── Programs larger than physical RAM could now run
│
├── TCP/IP networking stack
│   └── The literal foundation of the internet
│
├── Fast File System
│   └── Dramatically improved disk performance
│
├── vi text editor
├── csh shell
└── Dozens of other tools and improvements
```

The TCP/IP networking stack is worth pausing on. The internet as it exists today — HTTP, email, SSH, every protocol — runs on TCP/IP. That networking code was written at Berkeley, funded by DARPA for ARPANet. It was given away freely with BSD. Every device connected to the internet today uses code that descends from what Berkeley wrote and gave away.

The BSD license philosophy was the opposite of what Stallman was developing at MIT:

```
BSD License:
├── Use it for anything — commercial or not
├── Modify however you want
├── Distribute freely
├── Include in proprietary products
├── Ship binaries without releasing source
└── Just keep the copyright notice

What this enables:
├── Maximum adoption
├── Commercial products built on BSD
└── No obligation to share improvements back
```

This permissiveness had enormous consequences — both enabling wide adoption and allowing corporations to take BSD code and close it. Apple would demonstrate this most visibly decades later.

---

## 1983 — GNU Project Starts

Richard Stallman at MIT watched AT&T's commercialization of Unix and drew a different conclusion from the Berkeley developers. Berkeley responded by building their own open version. Stallman responded by building a movement.

By 1991, GNU had produced most of what was needed:

```
GNU tools produced by 1991:
│
├── gcc        — C compiler (still dominant today)
├── bash       — shell (default on most Linux systems)
├── glibc      — C standard library
├── make       — build automation
├── gdb        — debugger
├── emacs      — text editor
├── binutils   — assembler, linker, object tools
└── coreutils  — ls, cp, mv, cat, and 70+ basic tools

Missing:
└── Kernel — GNU Hurd was years behind schedule
    └── Architecturally ambitious, practically incomplete
```

Hurd was designed as a microkernel — architecturally clean, theoretically elegant, practically never finished. Stallman has acknowledged it was a mistake to pursue such an ambitious design. The GNU Project had built everything for a complete operating system except the one piece everything else depended on.

---

## 1991 — Linus Builds the Missing Piece

Linus Torvalds was a 21-year-old computer science student in Helsinki. He was using **Minix** — a small Unix-like OS created by professor Andrew Tanenbaum as a teaching tool. Minix was deliberately limited. When Linus wanted to add real features, Tanenbaum refused — educational simplicity was the design goal.

So Linus built his own kernel. His announcement on August 25, 1991:

> "I'm doing a (free) operating system (just a hobby, won't be big and professional like gnu) for 386(486) AT clones."

He released version 0.01 under a license that prohibited commercial use. Stallman reached out and persuaded Linus to relicense under the GPL. Linus agreed. Linux became GPL v2 — the decision that made it impossible for anyone to make Linux proprietary.

```
What Linus had:              What GNU had:
│                            │
├── Working kernel           ├── gcc compiler
├── Hardware support         ├── bash shell
├── Process management       ├── glibc
└── Basic filesystems        ├── make, gdb, coreutils
                             └── Everything except a kernel
                                      ↓
                          GNU tools + Linux kernel
                                      ↓
                          Complete free operating system
```

Tanenbaum publicly declared Linux "obsolete" in 1992 — monolithic kernels were architecturally inferior to microkernels. Linus disagreed directly and publicly. Linux continued growing. Minix remained a teaching tool. Linux runs the world.

---

## 1992 — The BSD Lawsuit That Nearly Killed Everything

In 1992, AT&T's Unix Systems Laboratories sued the University of California, Berkeley. The claim: BSD contained proprietary AT&T Unix code Berkeley had no right to distribute.

```
What was actually at stake:
│
├── BSD development frozen during litigation
├── Companies afraid to build on BSD
├── Legal uncertainty around all Unix-derived systems
│   └── Including Linux — design similarities even though
│       it shared no actual AT&T code
└── Chilling effect across the entire open source ecosystem
```

The lawsuit dragged for two years. BSD development slowed dramatically. Linux had no AT&T code — written from scratch. Linux became the safer choice. Two years of momentum shifted permanently.

The lawsuit settled in 1994. Berkeley removed 3 files from a distribution of about 18,000. The vast majority of BSD was clean. But the damage to BSD's momentum was permanent.

FreeBSD, NetBSD, and OpenBSD emerged as fully open derivatives — FreeBSD powers Netflix's CDN and parts of PlayStation OS, OpenBSD is the security-focused choice for infrastructure. But Linux had gained two years of enterprise momentum that BSD never fully recovered.

---

**The lesson:** document the provenance of every line of code. Legal ambiguity is a weapon corporations will use.

---

## 2000 — Apple Takes BSD and Closes It

When Apple needed to rebuild their aging operating system in the late 1990s, they acquired NeXT — Steve Jobs' company — which had built NeXTSTEP on the Mach microkernel and BSD Unix.

The result was **XNU** — the kernel running every Apple device today.

```
XNU kernel composition:
│
├── Mach microkernel (Carnegie Mellon)
│   └── Process management, IPC, virtual memory
│
├── BSD layer (University of California, Berkeley)
│   └── Networking, filesystem, POSIX compatibility
│
└── Apple's proprietary layers
    └── IOKit drivers, security subsystems, everything visible
```

This was **completely legal** under the BSD license.

```
BSD license permitted Apple to:
│
├── Take BSD networking code     → used in every Apple device
├── Take BSD filesystem code     → used in every Apple device
├── Modify without releasing     → done
├── Build proprietary products   → done
└── Never contribute back        → done

Result:
└── Billions of Apple devices run BSD-derived code
    Apple built a trillion-dollar company partly on free code
    BSD contributors had zero legal recourse
    The license they chose explicitly permitted all of it
```

**Permissive licenses give corporations freedoms that copyleft licenses do not.** Whether that is good or bad depends on what you think open source is for.

---

## 2003 — SCO Group vs IBM and the Linux FUD Campaign

In March 2003, the SCO Group filed a $1 billion lawsuit against IBM. Their claim: IBM had contributed proprietary Unix code SCO owned to the Linux kernel.

This was not a legal strategy. It was a **FUD campaign** — Fear, Uncertainty, and Doubt.

```
SCO's actual playbook:
│
├── File high-profile lawsuit against IBM
│   └── Headlines create fear
│
├── Send letters to 1,500+ large companies
│   ├── "Your Linux use may infringe our IP"
│   └── "License from us for $699 per server"
│
└── Create enough uncertainty that companies pay rather than fight

Who was funding SCO:
└── Microsoft invested $50M+ during this period
    └── Microsoft was losing server market to Linux
```

The community responded methodically. Volunteers and companies audited the Linux kernel line by line. IBM counterclaimed with 150+ patents. Novell produced documents proving they — not SCO — owned the Unix copyrights.

```
How it ended:
│
├── 2004 — Novell proves it owns Unix copyrights, not SCO
├── 2007 — Court rules SCO does not own Unix copyrights
├── 2007 — SCO files for bankruptcy
├── 2010 — SCO loses final appeals
└── Linux kernel audited — no AT&T code found anywhere
```

Linux adoption accelerated throughout. FUD did not stop adoption.

---

**The lesson:** legal attacks on open source are often about creating uncertainty, not winning in court. The defense is transparent code, clear provenance, and organizations willing to fight back.

---

## 2010 — Oracle Buys Sun, Kills OpenSolaris Overnight

Sun Microsystems had been one of the most open-source-friendly large companies. In 2005 they launched **OpenSolaris** — an open source version of their enterprise Solaris OS with genuinely innovative technology:

```
What OpenSolaris had:
│
├── ZFS — most advanced filesystem ever built
│   └── Checksumming, snapshots, compression, RAID-Z
│
├── DTrace — revolutionary system tracing
│   └── Debug production systems without restart
│
├── Zones — lightweight OS virtualization
└── SMF — service management framework
```

Five years of community contributions. A real ecosystem building.

Oracle acquired Sun in January 2010 for $7.4 billion.

```
Oracle's actions after acquisition:
│
├── Months 1-2:  OpenSolaris roadmap quietly dropped
├── Month 3:     Source code repository stopped updating
├── Month 4:     Community contributions rejected
├── Month 5:     Official announcement — discontinued
└── Month 6:     Last open source build released, repository closed

Time from acquisition to killing OpenSolaris:
└── 6 months
```

Five years of community work. Hundreds of contributors. All now serving a proprietary Oracle product.

The community forked into **illumos**. ZFS was ported to Linux and is now widely used as **ZFS on Linux** — Oracle's most innovative technology is more widely used on Linux than on Oracle's own platform. The irony is complete.

---

**The lesson:** a project living inside a single company is one acquisition away from death. No foundation, no independent governance, no protection.

---

## 2010-2021 — Oracle vs Google and the API Wars

Oracle also acquired Java when they bought Sun. Google had built Android using a clean-room reimplementation of Java APIs — they wrote new code compatible with Java's interface without using Sun's actual implementation.

Oracle sued Google in 2010. The claim: the **Java APIs themselves** were copyrightable.

```
What Oracle was claiming:
└── java.lang.String.substring(int start, int end)
    ├── The method name "substring"
    ├── The parameters (int start, int end)
    ├── The return type (String)
    └── The package structure (java.lang)
    → All of this = copyrightable creative expression
    → Google using this structure = copyright infringement

What was at stake if Oracle won:
│
├── Any Java-compatible reimplementation = infringement
├── Open source Java alternatives = infringement
├── POSIX compatibility layers = potentially infringement
├── Wine (Windows compatibility on Linux) = potentially infringement
└── Decades of open source compatibility work = undermined
```

The case ran through every level of the US court system over 11 years:

```
Court timeline:
│
├── 2010 — Oracle files suit ($8.8 billion claimed)
├── 2012 — District court: APIs not copyrightable → Google wins
├── 2014 — Federal Circuit reverses → Oracle wins
├── 2015 — Supreme Court declines to hear it
├── 2016 — Retrial on fair use → jury finds for Google
├── 2018 — Federal Circuit reverses again → Oracle wins
└── 2021 — Supreme Court: fair use → Google wins 6-2
```

Google won. The Supreme Court ruled Google's use was fair use. The court avoided fully resolving whether APIs are copyrightable — but the fair use ruling protected the broader practice of reimplementation.

Eleven years. Hundreds of millions in legal fees. A decade of uncertainty about something the community assumed was settled.

---

## Where This History Lands

Every major open source institution, practice, and defense mechanism today exists because of these fights:

```
AT&T commercializes Unix (1979)
        ↓
Stallman writes GPL to prevent it happening again
        ↓
BSD lawsuit (1992)
└── Lesson: document code provenance
    Legal ambiguity is a weapon
        ↓
Linux gains momentum from BSD uncertainty
        ↓
Apple takes BSD legally (2000)
└── Lesson: license choice determines what
    corporations can do with your work
        ↓
SCO FUD campaign (2003)
└── Lesson: fight back, audit everything,
    build organizations with resources to counter-sue
        ↓
Oracle kills OpenSolaris (2010)
└── Lesson: foundations matter
    Single-company projects are fragile
        ↓
Oracle vs Google (2021)
└── Lesson: API compatibility is defensible
    but defending it costs a decade
        ↓
Modern open source:
├── Independent foundations (Linux Foundation, Apache, CNCF)
├── Deliberate license strategies (GPL vs permissive)
├── Code provenance tracking (DCO, Signed-off-by, SBOM)
├── Legal defense organizations (SFC, EFF)
└── Community auditing practices
```

None of this was designed in advance. It was built in response to attacks. Each attack taught a lesson. Each lesson became a practice. Each practice became infrastructure.

That infrastructure is what you are using when you contribute to open source today.

---

> **Back to the main file → [../01-how-open-source-actually-works.md](../01-how-open-source-actually-works.md)**
