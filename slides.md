---
theme: default
colorSchema: dark
background: '#0a0a0b'
title: Agentic Development at UC San Diego
info: |
  ## Agentic Development at UC San Diego
  Internal ITS framework for citizen agentic development.
  Discussion deck — April 2026.
author: Brett Pollak · Workplace Technology Services
keywords: ucsd,tritonai,citizen-developer,agentic
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: slide-left
mdc: true
fonts:
  sans: 'Inter'
  mono: 'JetBrains Mono'
layout: cover
---

<div class="flex flex-col items-center justify-center h-full">
  <div class="text-sm text-emerald-400 font-mono tracking-wider uppercase mb-6 opacity-80">
    UCSD ITS · Internal Discussion · April 2026
  </div>
  <h1 class="!text-6xl !font-extrabold tracking-tight leading-none mb-6 bg-gradient-to-br from-white via-slate-200 to-emerald-300 bg-clip-text text-transparent">
    Agentic Development<br/>at UC San Diego
  </h1>
  <div class="text-xl text-slate-400 mt-2">
    A framework for citizen developers — what we're proposing, where we want your input
  </div>
  <div class="text-sm text-slate-500 mt-12 font-mono">
    Brett Pollak · Workplace Technology Services
  </div>
</div>

<!--
Friday meeting. Audience already oriented to agentic dev. Goal: socialize the framework we've converged on, not re-design it. Expect heavy discussion — we have 20–45 min and slides are just prompts.
-->

---
layout: default
class: flex flex-col justify-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">01 — The problem</div>

# The train is moving

<div class="grid grid-cols-2 gap-12 mt-10">

<div>

<div class="text-slate-300 text-2xl leading-relaxed">
Users are going to build these agents.
</div>
<div class="text-slate-400 text-xl leading-relaxed mt-4 italic">
"We can either drive it or have to later catch up." — Adam
</div>

</div>

<div class="border-l-2 border-emerald-500/50 pl-6 text-slate-400 space-y-3">

<div>**Deans** are hearing it from their staff.</div>
<div>**Cabinet** is hearing it from the deans.</div>
<div>**Researchers** are already doing it — with or without rails.</div>
<div>**Service owners** haven't yet decided how to respond.</div>

</div>

</div>

<div class="absolute bottom-12 left-12 right-12 text-sm text-slate-500 font-mono">
The question isn't <span class="text-slate-300">if</span>. It's <span class="text-emerald-400">with what rails</span>.
</div>

<!--
Adam's line captures the thesis. Hugo from today's dean meeting: 70–80% of his office's manual work is "handshake between system A and system B" — exactly what agents automate. Faculty Rajesh has students and wants a custom assistant. Analyst wants Cognos → Tableau → email automated. They will do this with or without us.
-->

---
layout: two-cols-header
class: flex flex-col
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">02 — The shape</div>

# Two tracks, same philosophy

<div class="text-slate-400 mt-2">Decoupled for now. Coordinated via architecture meetings. Converge when we've learned.</div>

::left::

<div class="mt-8 p-6 rounded-lg border border-slate-800 bg-slate-900/40">
  <div class="text-xs font-mono text-blue-400 uppercase tracking-wider mb-2">Formal · Tier 3</div>
  <div class="text-2xl font-semibold text-white mb-3">Enterprise agentic dev</div>
  <div class="text-slate-400 text-sm space-y-2">
    <div>Joey &amp; Mike on the HR stack</div>
    <div>Supabase + AWS, streamlined</div>
    <div>Developers trusted top-to-bottom</div>
    <div class="text-slate-500 mt-4 font-mono text-xs">~1–5 apps / year</div>
  </div>
</div>

::right::

<div class="mt-8 p-6 rounded-lg border border-emerald-700/50 bg-emerald-950/30">
  <div class="text-xs font-mono text-emerald-400 uppercase tracking-wider mb-2">Informal · Tiers 0–2</div>
  <div class="text-2xl font-semibold text-white mb-3">Citizen agentic dev</div>
  <div class="text-slate-400 text-sm space-y-2">
    <div>Faculty, staff, researchers, analysts</div>
    <div>Shared rails, scaled guardrails</div>
    <div>Trust earned via tier, not assumed</div>
    <div class="text-slate-500 mt-4 font-mono text-xs">~1,200+ attempts / year</div>
  </div>
</div>

<!--
Decision from today's meeting: these stay separate but coordinated. Joey/Mike attend our Tuesday sync. Don't burden enterprise with campus-wide guardrails; don't burden citizen with enterprise separation-of-duties. Shared anchor: a single "AGENTS.md for UC-compliant code" document co-authored across both tracks.
-->

---
layout: center
class: text-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-8">03 — The vision</div>

```mermaid {theme: 'dark', scale: 1.0}
flowchart LR
    U["👤<br/><b>User</b>"] --> CC["<b>Claude Code</b><br/>Codex · Onyx Craft"]
    CC -->|"push"| GH["<b>GitHub</b>"]
    GH ==>|"low friction"| ITS["<b>ITS Infra</b>"]
    ITS --> UCSD["<b>UCSD</b>"]
    ITS -.->|"logs · monitoring"| U

    classDef user fill:#052e16,stroke:#10b981,stroke-width:2px,color:#fff;
    classDef tool fill:#0c1220,stroke:#3b82f6,stroke-width:2px,color:#fff;
    classDef infra fill:#1a0b0b,stroke:#f59e0b,stroke-width:2px,color:#fff;
    class U user;
    class CC,GH tool;
    class ITS,UCSD infra;
    linkStyle 2 stroke:#10b981,stroke-width:3px;
```

<div class="mt-10 text-slate-400 text-lg max-w-3xl mx-auto">
One sentence: user's prompt &rarr; coding agent &rarr; GitHub &rarr; ITS deployment &rarr; UCSD users, with a <span class="text-emerald-400">monitoring loop back to the author</span>.
</div>

<div class="mt-6 text-slate-500 font-mono text-sm">
<span class="text-emerald-400">Low friction</span> is load-bearing. Everything else in this deck is how we keep that promise.
</div>

<!--
This is the elevator pitch. The "low friction" edge is the promise to the user. Every other slide answers: how do we keep it low-friction without burning the house down?
-->

---
layout: default
class: flex flex-col
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">04 — The tier model</div>

# From laptop to campus

<div class="text-slate-400 mt-2">The further up, the higher the data tier, the more review. The further down, the more invocations, the faster iteration.</div>

<div class="grid grid-cols-4 gap-3 mt-8 flex-1">

<div class="rounded-lg border border-lime-700/50 bg-lime-950/30 p-4 flex flex-col">
  <div class="text-xs font-mono text-lime-400 uppercase tracking-wider">Tier 0</div>
  <div class="text-xl font-semibold mt-2">Individual</div>
  <div class="text-xs text-slate-500 mt-1">Local · ~1,000+/y</div>
  <div class="text-sm text-slate-400 mt-4 space-y-1.5">
    <div>Own laptop / Jupyter</div>
    <div>Auto LLM + Onyx keys</div>
    <div>P1–P2 author's data</div>
    <div>No publishing</div>
  </div>
</div>

<div class="rounded-lg border border-blue-700/50 bg-blue-950/30 p-4 flex flex-col">
  <div class="text-xs font-mono text-blue-400 uppercase tracking-wider">Tier 1</div>
  <div class="text-xl font-semibold mt-2">Scattered</div>
  <div class="text-xs text-slate-500 mt-1">~200/y</div>
  <div class="text-sm text-slate-400 mt-4 space-y-1.5">
    <div>*.apps.ucsd.edu</div>
    <div>ITS-managed fork</div>
    <div>SPA + SQLite / Supabase</div>
    <div>Quarterly review</div>
  </div>
</div>

<div class="rounded-lg border border-amber-700/50 bg-amber-950/30 p-4 flex flex-col">
  <div class="text-xs font-mono text-amber-400 uppercase tracking-wider">Tier 2</div>
  <div class="text-xl font-semibold mt-2">Many users</div>
  <div class="text-xs text-slate-500 mt-1">~20/y</div>
  <div class="text-sm text-slate-400 mt-4 space-y-1.5">
    <div>*.tritonai.ucsd.edu</div>
    <div>AI team hands-on</div>
    <div>P3 gated</div>
    <div>Rapid ITS Dev</div>
  </div>
</div>

<div class="rounded-lg border border-red-800/50 bg-red-950/30 p-4 flex flex-col">
  <div class="text-xs font-mono text-red-400 uppercase tracking-wider">Tier 3</div>
  <div class="text-xl font-semibold mt-2">Enterprise</div>
  <div class="text-xs text-slate-500 mt-1">~1–5/y</div>
  <div class="text-sm text-slate-400 mt-4 space-y-1.5">
    <div>iPaaS patterns</div>
    <div>AWS hosted</div>
    <div>Full SoD</div>
    <div>Joey &amp; Mike</div>
  </div>
</div>

</div>

<div class="mt-8 text-xs text-slate-500 font-mono text-center">
graduate &uarr; &nbsp; or &nbsp; escalate &uarr; &nbsp; or &nbsp; migrate &uarr;
</div>

<!--
Tier 0 is new based on David Balderson's feedback — the on-ramp. Tier 3 is where enterprise lives (Joey/Mike HR stack) and is deliberately decoupled for v1. The lateral boundaries matter: crossing them triggers a risk/scope review. The vertical ones matter too: you can stay at your tier indefinitely.
-->

---
layout: default
class: flex flex-col
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">05 — The pipeline</div>

# Who owns what

```mermaid {theme: 'dark', scale: 0.85}
flowchart LR
    subgraph USER [" USER owns the code "]
        direction TB
        P["Prompt"] --> H["Harness"] --> TB["Local testbed"]
    end
    subgraph AI [" AI TEAM owns the promotion "]
        direction TB
        R["Intake +<br/>risk review"] --> F["ITS-managed<br/>fork"] --> B["Build via<br/>GitHub Actions"]
    end
    subgraph INFRA [" INFRA owns the runtime "]
        direction TB
        K["K8s namespace<br/>per app"] --> D["Data:<br/>APIs · MCP · files"]
    end

    USER --> AI --> INFRA
    INFRA -.->|"logs · stats · status"| USER

    classDef us fill:#052e16,stroke:#10b981,color:#fff;
    classDef ai fill:#0c1220,stroke:#3b82f6,color:#fff;
    classDef inf fill:#1a0b0b,stroke:#f59e0b,color:#fff;
    class USER us;
    class AI ai;
    class INFRA inf;
```

<div class="mt-8 text-slate-400 text-center text-sm max-w-4xl mx-auto">
Three swim-lanes. User never touches the build/deploy path. Infra never touches the code. The AI team is the bridge — enforcing review at the gate, automating everything that can be automated.
</div>

<!--
Answers the "who does what" question. User's repo lives in their org; when they want to ship, they fork up and we own it from there. The dotted line back is the observability promise — they see what's happening with their thing without having to ask.
-->

---
layout: default
class: flex flex-col
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">06 — Harness choices</div>

# Three on-ramps, same rails

<div class="grid grid-cols-3 gap-5 mt-10">

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-xs font-mono text-emerald-400 uppercase tracking-wider">Free tier</div>
  <div class="text-xl font-semibold mt-2">Open Code + OSS models</div>
  <div class="text-slate-400 text-sm mt-4 space-y-2">
    <div>&euro;0 out of pocket</div>
    <div>Chinese open-weight models (Matthew's testing: <span class="font-mono text-slate-200">minimax 2.5</span> works)</div>
    <div>UCSD-branded instructions</div>
    <div>Clear upgrade path</div>
  </div>
  <div class="mt-4 pt-4 border-t border-slate-800 text-xs text-slate-500 font-mono">Staff onboarding</div>
</div>

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-xs font-mono text-blue-400 uppercase tracking-wider">Guided</div>
  <div class="text-xl font-semibold mt-2">Onyx Craft</div>
  <div class="text-slate-400 text-sm mt-4 space-y-2">
    <div>Opinionated — we control the env</div>
    <div>Auto-config, auto-updates</div>
    <div>Next.js + consistent UI kit</div>
    <div>Dashboards, forms, internal tools</div>
  </div>
  <div class="mt-4 pt-4 border-t border-slate-800 text-xs text-slate-500 font-mono">Non-technical builders</div>
</div>

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-xs font-mono text-amber-400 uppercase tracking-wider">Power users</div>
  <div class="text-xl font-semibold mt-2">Claude Code · Codex</div>
  <div class="text-slate-400 text-sm mt-4 space-y-2">
    <div>Bring your own chartstring</div>
    <div>LiteLLM gateway access</div>
    <div>Full flexibility</div>
    <div>Researchers with grants</div>
  </div>
  <div class="mt-4 pt-4 border-t border-slate-800 text-xs text-slate-500 font-mono">Devs + researchers</div>
</div>

</div>

<div class="mt-8 text-slate-500 text-sm font-mono text-center">
We don't build our own. We ship a setup script that configures the existing harnesses with UCSD skills, <span class="text-slate-300">AGENTS.md</span>, and gateway credentials.
</div>

<!--
Explicit decision from today: no own Claude/Codex fork. Setup script + skills repo. Onyx Craft is the exception because we already own it. Each user lands in the right lane based on who they are and what they have.
-->

---
layout: default
class: flex flex-col justify-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">07 — Data access</div>

# The data principle

<div class="text-slate-400 mt-2 mb-8 max-w-3xl">
Users want to automate what they <span class="text-slate-200">already see</span> in browsers. Blocking agentic access doesn't prevent it — it just drives it underground.
</div>

<div class="flex items-stretch gap-4 mt-4">

<div class="flex-1 rounded-lg border-2 border-emerald-500/60 bg-emerald-950/40 p-5">
  <div class="flex items-center gap-2 mb-3">
    <div class="w-2 h-2 rounded-full bg-emerald-400"></div>
    <div class="text-xs font-mono text-emerald-400 uppercase tracking-wider">Preferred</div>
  </div>
  <div class="text-base font-semibold">Official API / MCP</div>
  <div class="text-slate-400 text-sm mt-2">via TritonAI gateway, vetted, rate-limited, logged.</div>
</div>

<div class="flex items-center text-slate-600 text-2xl">&rarr;</div>

<div class="flex-1 rounded-lg border-2 border-amber-500/40 bg-amber-950/30 p-5">
  <div class="flex items-center gap-2 mb-3">
    <div class="w-2 h-2 rounded-full bg-amber-400"></div>
    <div class="text-xs font-mono text-amber-400 uppercase tracking-wider">Acceptable</div>
  </div>
  <div class="text-base font-semibold">Personal token</div>
  <div class="text-slate-400 text-sm mt-2">Canvas, Jira, etc. Scoped to the user's own permissions.</div>
</div>

<div class="flex items-center text-slate-600 text-2xl">&rarr;</div>

<div class="flex-1 rounded-lg border-2 border-red-500/40 bg-red-950/30 p-5">
  <div class="flex items-center gap-2 mb-3">
    <div class="w-2 h-2 rounded-full bg-red-400"></div>
    <div class="text-xs font-mono text-red-400 uppercase tracking-wider">Tolerated</div>
  </div>
  <div class="text-base font-semibold">Playwright browser</div>
  <div class="text-slate-400 text-sm mt-2">Inside UCSD infra. Only until service owners ship an API.</div>
</div>

</div>

<div class="mt-10 p-5 rounded-lg border border-slate-800 bg-slate-900/40">
  <div class="text-slate-300 italic text-lg">
    "Safer to have the kids drinking at home than drinking out in the world."
  </div>
  <div class="text-slate-500 text-sm mt-2">— Adam</div>
</div>

<!--
The punchline: our job is to make the preferred path easier than the tolerated path. Most UCSD APIs today aren't "gold standard" — consumable outside the team that built them. We need to MCP-ify the catalog, and that requires service-owner partnership.
-->

---
layout: default
class: flex flex-col justify-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">08 — Review &amp; protections</div>

# What ITS takes on

<div class="grid grid-cols-2 gap-10 mt-10">

<div>
  <div class="text-xs font-mono text-slate-500 uppercase tracking-wider mb-3">Automated first pass</div>
  <div class="space-y-3 text-slate-300">
    <div class="flex gap-3"><span class="text-emerald-400 font-mono">01</span><span>Sonarqube + Claude Code agent reads the PR</span></div>
    <div class="flex gap-3"><span class="text-emerald-400 font-mono">02</span><span>Flags security holes, unusual architecture</span></div>
    <div class="flex gap-3"><span class="text-emerald-400 font-mono">03</span><span>Accessibility defaults baked into templates</span></div>
    <div class="flex gap-3"><span class="text-emerald-400 font-mono">04</span><span>Feedback directly in the PR, not email</span></div>
  </div>
</div>

<div>
  <div class="text-xs font-mono text-slate-500 uppercase tracking-wider mb-3">Manual second pass</div>
  <div class="space-y-3 text-slate-300">
    <div class="flex gap-3"><span class="text-amber-400 font-mono">01</span><span>Resource footprint (CPU, network)</span></div>
    <div class="flex gap-3"><span class="text-amber-400 font-mono">02</span><span>Data-access scope</span></div>
    <div class="flex gap-3"><span class="text-amber-400 font-mono">03</span><span>Operational / business risk</span></div>
    <div class="flex gap-3"><span class="text-amber-400 font-mono">04</span><span>Unit Acceptance of Risk (UISL)</span></div>
  </div>
</div>

</div>

<div class="mt-12 p-5 rounded-lg border border-slate-800 bg-slate-900/40">
  <div class="text-xs font-mono text-slate-500 uppercase tracking-wider mb-2">Default protections</div>
  <div class="flex flex-wrap gap-x-6 gap-y-2 text-slate-300 text-sm">
    <div>&#9679; SSO <span class="text-slate-500">or</span> VPN gate</div>
    <div>&#9679; Title II accessibility template</div>
    <div>&#9679; 1Password for secrets</div>
    <div>&#9679; Runtime env injection</div>
    <div>&#9679; P4 data blocked at the tier</div>
  </div>
</div>

<!--
We take the risk by hosting. That's why we review architecture + security, not bugs. Bugs belong to the user. First 10 apps, review is a meeting — we use those to inform the form questions, then automate.
-->

---
layout: default
class: flex flex-col justify-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">09 — Open question for you</div>

# Where should this NOT go?

<div class="text-slate-400 mt-2 text-lg max-w-4xl">
You're the ones who know where the landmines are. <span class="text-slate-200">Help us stake out the hazardous ground.</span>
</div>

<div class="grid grid-cols-2 gap-8 mt-12">

<div>
  <div class="text-xs font-mono text-red-400 uppercase tracking-wider mb-3">Our starting no-go list</div>
  <div class="space-y-2.5 text-slate-300">
    <div class="flex gap-3 items-start"><span class="text-red-400 mt-1">&#9679;</span><span>P4 regulated data (HIPAA, PCI, FERPA-restricted)</span></div>
    <div class="flex gap-3 items-start"><span class="text-red-400 mt-1">&#9679;</span><span>SOC 2 separation-of-duties audits</span></div>
    <div class="flex gap-3 items-start"><span class="text-red-400 mt-1">&#9679;</span><span>Payment processing</span></div>
    <div class="flex gap-3 items-start"><span class="text-red-400 mt-1">&#9679;</span><span>Credentialing, grades-of-record writes</span></div>
  </div>
</div>

<div>
  <div class="text-xs font-mono text-emerald-400 uppercase tracking-wider mb-3">Open for your input</div>
  <div class="space-y-2.5 text-slate-300">
    <div class="flex gap-3 items-start"><span class="text-emerald-400 mt-1">?</span><span>Systems that should exclude even <em>read</em> access?</span></div>
    <div class="flex gap-3 items-start"><span class="text-emerald-400 mt-1">?</span><span>Where does "occasional manual access" become dangerous at agent scale?</span></div>
    <div class="flex gap-3 items-start"><span class="text-emerald-400 mt-1">?</span><span>Which APIs should require elevated review regardless of tier?</span></div>
    <div class="flex gap-3 items-start"><span class="text-emerald-400 mt-1">?</span><span>What compliance regimes are we underestimating?</span></div>
  </div>
</div>

</div>

<!--
Sandra's framing: we win the room by asking them to stake out the hazardous areas from their expertise. This is the highest-leverage slide in the deck — real signal on where we might break something we don't realize we're touching.
-->

---
layout: default
class: flex flex-col justify-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">10 — Open question for you</div>

# Which APIs should we MCP-ify first?

<div class="text-slate-400 mt-2 text-lg max-w-4xl">
Most UCSD APIs aren't consumable outside the team that built them. Each one we turn into an MCP unlocks a class of agent use cases.
</div>

<div class="mt-10 grid grid-cols-2 gap-6">

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-5">
  <div class="text-xs font-mono text-slate-500 uppercase tracking-wider mb-3">Our starting priority</div>
  <div class="space-y-2 text-slate-300 text-sm">
    <div><span class="font-mono text-emerald-400 w-6 inline-block">01</span>WSO2 catalog (gateway for many)</div>
    <div><span class="font-mono text-emerald-400 w-6 inline-block">02</span>Microsoft Graph (email, calendar, files)</div>
    <div><span class="font-mono text-emerald-400 w-6 inline-block">03</span>Canvas (instructional data)</div>
    <div><span class="font-mono text-emerald-400 w-6 inline-block">04</span>OFC / Oracle Financials</div>
    <div><span class="font-mono text-emerald-400 w-6 inline-block">05</span>Quality Build</div>
    <div><span class="font-mono text-emerald-400 w-6 inline-block">06</span>Google / Gmail API</div>
  </div>
</div>

<div class="rounded-lg border border-emerald-700/30 bg-emerald-950/20 p-5">
  <div class="text-xs font-mono text-emerald-400 uppercase tracking-wider mb-3">Questions for the room</div>
  <div class="space-y-3 text-slate-300 text-sm">
    <div>Which of these unlocks the most for <em>your</em> team?</div>
    <div>What's missing from this list that you'd use tomorrow?</div>
    <div>Where are you seeing the most gorilla-automation today?</div>
    <div>Who's the service-owner we should loop in first?</div>
  </div>
</div>

</div>

<!--
Each MCP-ification is real engineering on the service-owner side. We get real signal here on prioritization. Also surfaces which service owners need a heads-up conversation before next steps.
-->

---
layout: default
class: flex flex-col justify-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-4">11 — The ask</div>

# Where you come in

<div class="text-slate-400 mt-2 mb-10 text-lg">
We're not asking you to approve this framework. We're asking you to help us sharpen it.
</div>

<div class="grid grid-cols-2 gap-6">

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-3xl font-mono text-emerald-400">01</div>
  <div class="text-lg font-semibold mt-3">Find the landmines</div>
  <div class="text-slate-400 text-sm mt-2">Things we haven't thought of. Where it breaks.</div>
</div>

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-3xl font-mono text-emerald-400">02</div>
  <div class="text-lg font-semibold mt-3">Point at the APIs</div>
  <div class="text-slate-400 text-sm mt-2">What your teams wish existed. What's blocking them today.</div>
</div>

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-3xl font-mono text-emerald-400">03</div>
  <div class="text-lg font-semibold mt-3">Take it to your teams</div>
  <div class="text-slate-400 text-sm mt-2">Bring back what you hear. We'll fold it in.</div>
</div>

<div class="rounded-lg border border-slate-800 bg-slate-900/40 p-6">
  <div class="text-3xl font-mono text-emerald-400">04</div>
  <div class="text-lg font-semibold mt-3">Co-author AGENTS.md</div>
  <div class="text-slate-400 text-sm mt-2">The UC-compliant-code document. One shared anchor.</div>
</div>

</div>

<div class="mt-10 text-slate-500 text-sm font-mono italic text-center">
Nothing here is cast in stone. Regular touch-points will reshape it.
</div>

<!--
Brett's close. Small ask, intentionally. Friday is Round 1 of a series. Design responsibility stays with the AI team. This audience contributes via feedback and socialization.
-->

---
layout: center
class: text-center
---

<div class="text-emerald-400 font-mono text-sm tracking-wider uppercase mb-8">Discussion</div>

<div class="text-6xl font-extrabold tracking-tight leading-none bg-gradient-to-br from-white via-slate-200 to-emerald-300 bg-clip-text text-transparent">
  Over to you.
</div>

<div class="mt-12 grid grid-cols-2 gap-4 max-w-3xl mx-auto text-left">
  <div class="p-4 rounded-lg border border-slate-800 bg-slate-900/40 text-sm text-slate-300">Where should citizen dev <strong class="text-emerald-400">not</strong> go?</div>
  <div class="p-4 rounded-lg border border-slate-800 bg-slate-900/40 text-sm text-slate-300">Which APIs to <strong class="text-emerald-400">MCP-ify</strong> first?</div>
  <div class="p-4 rounded-lg border border-slate-800 bg-slate-900/40 text-sm text-slate-300">What have we <strong class="text-emerald-400">not thought of</strong>?</div>
  <div class="p-4 rounded-lg border border-slate-800 bg-slate-900/40 text-sm text-slate-300">How do we keep the <strong class="text-emerald-400">enterprise track</strong> connected?</div>
</div>

<div class="mt-16 text-slate-500 text-xs font-mono">
brett@ucsd.edu &nbsp;·&nbsp; <a href="https://bpollak.github.io/citizen-dev-proposal">bpollak.github.io/citizen-dev-proposal</a>
</div>
