<!-- .slide: data-state="title-slide" -->
# Agentic Development at UC San Diego

### A Framework for Citizen Developers

<small>Internal ITS socialization — April 2026</small>
<small>Brett Pollak · Workplace Technology Services</small>

Note:
Agentic coding meeting, Apr 22. Attendees: Brett Pollak, Holland (Matthew), Munro (Shawn), Tilghman (Adam), Chalmers (Sandra). The Friday session is a socialization, not a design workshop — we share the framework we've converged on, and the room gives feedback that shapes the next iteration.

---

## Today's 30 minutes

1. **Why** — the wave that's already moving through campus
2. **What** — the framework we're proposing
3. **How** — the mechanics (intake, harness, deploy, data, review)
4. **Open questions** — where we want your input

<small>We're expecting a lot of discussion. Interrupt freely.</small>

Note:
Timebox: we blocked up to 45 min. Anticipate heavy discussion. I'll push through content quickly so we have room for dialogue on the last section.

---

<!-- .slide: data-background="#1a1a2e" data-color="#fff" -->

## Act 1 — Why

<small>The problem we're trying to solve</small>

---

## The train is moving

> Users are going to build these agents. We can either drive it or have to later catch up. — *Adam, today's meeting*

- Faculty, researchers, and staff are already asking for agentic tools
- Generic chatbots don't scale into administrative reality
- We're hearing from **deans, cabinet, and individual departments** asking for this
- The question isn't *if* — it's *with what rails*

Note:
Adam's line from the meeting captures the thesis in one sentence. Hugo's point from the dean's meeting today — most of his office's manual work is "handshake between systems A and B." That's exactly what agents automate.

---

## Two things happening in parallel

<div class="two-col">
<div>

### Enterprise Agentic Dev
- Joey & Mike on the HR stack
- Performance management, higher online, JD online, badge apps
- Supabase + AWS, streamlined stack
- **Formal** development — Tier 3

</div>
<div>

### Citizen Agentic Dev
- Individual users, scattered departments
- ~1,000+ attempts/year at Tier 0
- Local tooling → shared apps
- **Informal** development — Tiers 0–2

</div>
</div>

<small>Same philosophy. Different trust model. Different scale. Decouple for now, converge later.</small>

Note:
Decision from today's meeting: these two work streams are **decoupled** but **coordinated** via architecture/orchestration meetings. Joey/Mike attend our Tuesday sync. We don't burden their work with campus-wide guardrails; we don't burden ours with enterprise separation-of-duties constraints.

---

## What problem are we actually solving?

**Staff Hugo** has five systems to move data between. Today he does it by hand.

**Faculty Rajesh** wants to give his students a custom assistant. Today he can't.

**Analyst** wants to automate a weekly report from Cognos → Tableau → email. Today she copy-pastes.

<small>70–80% of citizen-dev use cases start with **"automate what I already do in a browser."**</small>

Note:
Sandra's framing from the meeting: before we jump to design, clarify the problem. These three personas map to Tiers 0-1 roughly. Every one of them is doing something they already have access to — just doing it manually. The agent isn't getting them new access; it's removing friction.

---

## The gorilla-automation risk

If we don't offer APIs, they'll use **Playwright in a browser**:
- Agent logs in as the human
- Scrapes whatever the human can see
- Downloads, copies, submits — at machine speed

> Safer to have the kids drinking at home than drinking out in the world. — *Adam*

<small>We can't prevent this. We can contain it — inside UCSD infra, with rate limits, quotas, and a plan.</small>

Note:
Two risks Adam highlighted: (1) a faculty member's "occasional access to student home addresses" becomes "bulk lookup of ALL addresses" once an agent is driving. (2) Service owners need to take responsibility — rate limiting, quotas, captcha, agent-detection. Our environment is the contained space; our environment has to *become* safer than the open web.

---

<!-- .slide: data-background="#1a1a2e" data-color="#fff" -->

## Act 2 — What

<small>The framework we're proposing</small>

---

## The simple picture

<div class="mermaid">
flowchart LR
    U[👤 User] -->|"writes intent"| CC[Claude Code / Codex / Onyx Craft]
    CC -->|"pushes code"| GH[GitHub]
    GH -->|"Low Friction"| ITS[ITS Infra]
    ITS -->|"serves"| UCSD[UCSD Users]
    ITS -.->|"Logs & Monitoring"| U

    classDef user fill:#fef9c3,stroke:#a16207,stroke-width:2px,color:#1a1a1a;
    classDef tool fill:#dbeafe,stroke:#1e40af,stroke-width:2px,color:#1a1a1a;
    classDef infra fill:#dcfce7,stroke:#15803d,stroke-width:2px,color:#1a1a1a;
    class U user;
    class CC,GH tool;
    class ITS,UCSD infra;
</div>

<small>One sentence: **user's prompt → coding agent → GitHub → ITS deployment → UCSD user** with a monitoring loop back to the author.</small>

Note:
This is the elevator pitch. Low friction is load-bearing — it's the promise we're making. Everything else in this deck is how we keep that promise without burning the house down.

---

## The tier model

<div class="mermaid">
flowchart TD
    T0["<b>Tier 0</b> · Individual<br/>Local tools · ~1000+/y<br/><small>P1/P2 author's own data</small>"]:::t0
    T1["<b>Tier 1</b> · Scattered users<br/>*.apps.ucsd.edu · ~200/y<br/><small>P2 shared</small>"]:::t1
    T2["<b>Tier 2</b> · Many users<br/>*.tritonai.ucsd.edu · ~20/y<br/><small>P3 gated</small>"]:::t2
    T3["<b>Tier 3</b> · Campus-wide<br/>Traditional enterprise · ~1–5/y<br/><small>P4 regulated</small>"]:::t3

    T0 -->|graduate| T1
    T1 -->|escalate| T2
    T2 -->|migrate| T3

    classDef t0 fill:#ecfccb,stroke:#365314,color:#1a1a1a;
    classDef t1 fill:#dbeafe,stroke:#1e40af,color:#1a1a1a;
    classDef t2 fill:#fde68a,stroke:#b45309,color:#1a1a1a;
    classDef t3 fill:#fecaca,stroke:#991b1b,color:#1a1a1a;
</div>

**Moving up:** more users, higher data tier, more review. **Moving down:** more invocations, less oversight, faster iteration.

Note:
Tier 0 is NEW — added based on David Balderson's feedback. It's the on-ramp: local sandbox, no publishing, just "let me learn." Tier 0→1 is the critical step where the risk/scope review kicks in. Each tier inherits the tier above it; you can graduate or escalate.

---

## Tier 0 — the on-ramp

**Who:** individual faculty, staff, or students experimenting

**Where it runs:** their own laptop / campus-managed Jupyter + Codex / Onyx Craft

**What we give them:**
- Auto-provisioned **TritonAI LLM API key**
- Auto-provisioned **TGPT Onyx API key**
- A **skills / AGENTS.md** repo they clone
- Prefab templates (vue.js/Next.js, Python/FastAPI)
- Catalog of **tested APIs and MCPs** they can call as themselves

**Cost:** $15/month free credits (self-hosted models) · pay-through for Claude/GPT

Note:
This tier is where 1000+/year of activity happens. 99% of it never leaves the laptop. That's a feature, not a bug. The $15 free credit comes from the existing TritonAI Developer API program — already live, already working.

---

## Tier 1 — sharing it

**Who:** a department with ~10–100 users who benefit

**Trigger:** "I want to share this."

**What happens:**
1. Fill out a **short intake form** (what does it do, what data, who uses it)
2. Repo is **forked into ITS-managed org**
3. Automated + manual review for architecture and security
4. Deploy target: **`*.apps.ucsd.edu`**
5. Recurring quarterly risk/scope review

**Tech stack v1:** SPA front-end · SQLite (or Supabase) · SSO or VPN gated

Note:
The AI team owns the fork, the build, and the deploy. The user owns the repo upstream. Data is SQLite-in-a-file for v1 — no DBA required, no backend service to run. Supabase becomes the auth front-end even when storage is sqlite. `*.apps.ucsd.edu` is the visible boundary: anything here has been through a review.

---

## Tier 2 — many users, higher data

**Who:** cross-department tools, P3-eligible data

**Difference from Tier 1:** AI team gets more involved, possible Rapid ITS Dev track

**Deploy targets:**
- `*.tritonai.ucsd.edu` (TritonAI-native)
- `*.ucsd.edu` (ITS rapid dev)

**Review cadence:** tighter; ITS owns pull request approval

**Examples:** department tools that draw from Canvas, OFC, UCPath data

Note:
Tier 2 is where the AI team's review effort concentrates. The question Adam raised — "who handles P3 code review? AI team?" — this is the answer: yes, at Tier 2. Tier 1 is automated + light-touch; Tier 2 is hands-on.

---

## Tier 3 — enterprise

**Who:** campus-wide, regulated data, P4

**Stack:** traditional enterprise dev, iPaaS patterns, full separation of duties

**Examples this week:** Joey & Mike's HR stack (performance management, JD online, higher online, badge apps)

<small>**This is the track that stays decoupled from citizen dev for now.** Same philosophy; different implementation. We converge when we learn what works.</small>

Note:
Key message here: Tier 3 is real, it's running, and it's deliberately a parallel track. Joey and Mike trust: we give them the master key to ITS. That doesn't scale to campus. That's why citizen dev has guardrails the enterprise track doesn't.

---

<!-- .slide: data-background="#1a1a2e" data-color="#fff" -->

## Act 3 — How

<small>The mechanics</small>

---

## The pipeline

<div class="mermaid">
flowchart LR
    subgraph user [" 👤 USER "]
        P["Prompt"]
        H["Harness<br/>(Claude Code · Codex · Onyx Craft · Open Code)"]
        TB["Local testbed<br/>(VS Code · Docker · Jupyter)"]
    end
    subgraph ai [" 🛠️ AI TEAM "]
        R["Intake &<br/>risk/scope review"]
        F["ITS-managed<br/>fork"]
        B["Build<br/>(GitHub Actions)"]
    end
    subgraph infra [" ☁️ INFRASTRUCTURE "]
        K["K8s namespace<br/>per app"]
        D["Data<br/>(APIs · MCP · RAG · files)"]
    end

    P --> H --> TB --> R --> F --> B --> K
    K --> D
    K -.->|"logs, stats"| user

    classDef userStyle fill:#fef9c3,stroke:#a16207,color:#1a1a1a;
    classDef aiStyle fill:#dbeafe,stroke:#1e40af,color:#1a1a1a;
    classDef infraStyle fill:#dcfce7,stroke:#15803d,color:#1a1a1a;
</div>

<small>Three swim-lanes: user owns the code, AI team owns the promotion, infra owns the runtime.</small>

Note:
This is the redrawn version of Adam's full-flow diagram. The three swim-lanes answer the question "who is responsible for what?" — user owns the repo; AI team owns the fork, build, deploy policy; infra owns the runtime environment.

---

## Harness choices — three lanes

<div class="three-col">
<div>

### Free tier
**Open Code + OSS models**
- $0 out of pocket
- UCSD-branded instructions
- Chinese open-weight models proven working in Matthew's testing
- Path to upgrade

</div>
<div>

### Guided (non-technical)
**Onyx Craft**
- Opinionated, we control the env
- Auto-config, auto-updates
- Next.js + consistent UI kit
- Best for dashboards, forms

</div>
<div>

### Power users
**Claude Code / Codex**
- Bring your own chartstring
- LiteLLM gateway access
- Full flexibility
- Researchers with funding

</div>
</div>

<small>Different users, different lanes, same rails underneath. We don't build our own harness.</small>

Note:
Explicit decision from today: **we don't build our own Claude Code / Codex clone**. We ship a setup script that configures the existing harnesses with UCSD skills, AGENTS.md, and API gateway creds. Onyx Craft is the exception because we own it already.

---

## Data access — three modes

<div class="mermaid">
flowchart LR
    A["🟢 <b>Preferred</b><br/>Official API / MCP<br/>via TritonAI gateway"] --- B["🟡 <b>Acceptable</b><br/>Personal token<br/>(Canvas, Jira)"] --- C["🔴 <b>Tolerated</b><br/>Playwright browser<br/>(inside UCSD infra)"]

    classDef a fill:#dcfce7,stroke:#15803d,color:#1a1a1a;
    classDef b fill:#fef3c7,stroke:#b45309,color:#1a1a1a;
    classDef c fill:#fee2e2,stroke:#991b1b,color:#1a1a1a;
    class A a;
    class B b;
    class C c;
</div>

**Principle:** users want to automate what they already do in browsers. If we don't MCPify the API catalog, they'll Playwright it.

**Service-owner partnership:** each system owner (OFC, Canvas, Quality Build) decides agent-access policy. ITS surfaces the request; service owner decides yes/no/rate-limit.

Note:
Matthew + Adam's key realization today: the data users want is data they already access. Blocking agentic access doesn't prevent it — it just drives it underground. Our job is to make the preferred path easier than the tolerated path. Today, most UCSD APIs aren't "gold standard" — we need to MCP-ify them over time.

---

## Review & deploy

**Automated first pass** (inspired by the contract-review agent)
- Sonarqube + Claude Code agent reads the PR
- Flags gaping security holes, unusual architecture, missing accessibility
- Provides feedback directly in the PR

**Manual second pass** (AI team)
- Resource footprint (CPU, memory, network)
- Data-access scope
- Operational/business risk (# users, $ saved, $ cost)
- Unit Acceptance of Risk (UISL)?

**Default protections:** SSO *or* VPN gate · accessibility template · 1Password for secrets · runtime env injection

Note:
We take the risk by hosting. That's why we review architecture + security, not bugs. Bugs belong to the user. Accessibility (Decorator pattern, a11y) gets baked into the templates so Title II isn't an afterthought.

---

## The common thread across all tiers

Even though citizen and enterprise tracks are decoupled, **one document is shared**:

> **"Agent instructions for UC-compliant code"**

- Written collaboratively by the AI team + Joey & Mike
- Loaded into every harness as `AGENTS.md`
- Covers: accessibility defaults, data handling, auth patterns, logging, error handling
- This is our anchor for eventual convergence

<small>One shared skills repo · two different build/deploy stacks · zero conflicts today.</small>

Note:
Shawn's framing from today: "the agent instructions on how to write UC-compliant code will be identical for both groups." This is the seed of convergence. Everything else can diverge; this document stays in sync. This also gives the enterprise team a useful artifact regardless of whether citizen dev scales.

---

<!-- .slide: data-background="#1a1a2e" data-color="#fff" -->

## Act 4 — Open questions

<small>Where we'd like your input</small>

---

## Where should this NOT go?

<small>Sandra's framing: validate the hazardous areas by asking the room.</small>

**Clear no-go zones (our starting assumption):**
- P4 regulated data (HIPAA, PCI, FERPA-restricted)
- Any system with SOC 2 separation-of-duties audit requirements
- Payment processing, credentialing, grades-of-record writes

**Open for your input:**
- Are there systems we should carve out even from *read* access?
- Where does "occasional manual access" become dangerous at agent scale?
- Which APIs should require elevated review regardless of tier?

Note:
This is the highest-value slide for the Friday audience. These are trusted technologists — they know where the landmines are. Sandra's idea: we win the room by asking them to stake out the hazardous ground from their expertise, not by telling them what's off-limits.

---

## Service-owner gaps — who's priority?

Most UCSD APIs **aren't consumable by teams outside the one that built them.**

**Candidates for MCP-ification (in rough priority):**
1. WSO2 catalog (gateway for many downstream)
2. Microsoft Graph (email, calendar, files)
3. Canvas (instructional data)
4. OFC / Oracle Financials
5. Quality Build
6. Google/Gmail API

**Question for the room:** which of these unlocks the most for your teams? What's missing from the list?

Note:
Each MCP-ification is real engineering work on the service-owner side. Prioritization matters. This slide gets us real signal from people who know where the bottlenecks are.

---

## What we're deferring (not solving today)

- **Cross-tier promotion** — Tier 1 → Tier 3 is explicitly out of scope for v1
- **Scalable backends** — SQLite is fine until it isn't; we'll know when
- **Full API catalog** — start with what we have, grow by demand
- **Automated compliance proofs** — SOC 2, Title II audit trails come as tooling matures
- **Enterprise convergence** — eventually, not now

<small>**Deliberate** deferrals. Each has a trigger that tells us when to revisit.</small>

Note:
This slide preempts the "but what about X?" questions. We're not pretending we've solved everything. We've explicitly chosen what to defer and we know what signals will tell us to circle back.

---

## What's next

**This week:**
- AI team + Dominic + Shawn finalize Tier 0/1 mechanics (1-hour working session)
- Talk to Joey & Mike ahead of Friday — align on decoupling message
- First pilot: Mike Holland's PDF Remediator → Tier 1 candidate

**Next 2–4 weeks:**
- Ship the Tier 0 setup script + skills repo
- Run the first 10 intake reviews as meetings (learn, then automate)
- Re-draw the intake form based on what we learn

**Next 6 months:**
- Steady state: 5–10 Tier 1 apps live
- MCP catalog expanding with service-owner partners
- Re-open the enterprise convergence conversation

Note:
Light on dates because we're avoiding commitment-by-calendar on a space that's evolving daily. The milestones that matter are: first pilot up, first 10 reviews done, then steady state.

---

## Where you come in

We're not asking you to approve this framework. We're asking you to:

1. **Help us find the landmines** we haven't thought of
2. **Point us at the APIs** your teams already wish existed
3. **Take this to your own teams** and bring back what you hear
4. **Co-author the "UC-compliant code" AGENTS.md** with the AI team

<small>Nothing here is cast in stone. The point of today is to start the conversation.</small>

Note:
Brett's close. The ask is small on purpose. This is Friday #1 of a series of touch-points; the design responsibility stays with the AI team. The group's contribution is *feedback and socialization* with their own teams.

---

<!-- .slide: data-background="#1a1a2e" data-color="#fff" -->

## Discussion

<div class="discussion-prompts">

- Where should citizen dev <strong>not</strong> be allowed?
- Which APIs should we MCP-ify first?
- What have we not thought of?
- How do we keep the enterprise track connected without slowing either side down?

</div>

<small>brett@ucsd.edu · this deck lives at <a href="https://bpollak.github.io/citizen-dev-proposal/">bpollak.github.io/citizen-dev-proposal</a></small>

Note:
Open floor. Let the discussion breathe. Capture anything surprising; the next iteration of the deck gets those as new slides or open-question slots.
