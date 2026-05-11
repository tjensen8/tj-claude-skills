---
name: biz-dev
description: >
  Structured business development skill for evaluating, iterating, and stress-testing
  a product idea from initial problem statement through to a viable, fundable business.
  Trigger when the user asks about business model, go-to-market, customer discovery,
  monetization, positioning, unit economics, competitive moat, or product-market fit.
  Also trigger on phrases like "is this a real business", "how do I sell this",
  "who is my customer", "what should I charge", "how do I grow this", or when the
  user wants to think through what to build next from a business perspective.
  Always apply a critical lens — challenge assumptions, distinguish validated facts
  from beliefs, and force prioritization of the hardest questions first.
compatibility:
  tools: []
---

# Business Development Framework

This skill structures business development conversations around a repeatable
methodology — from raw idea through validated, revenue-generating product. It is
opinionated. It challenges weak answers. It does not let you skip hard questions.

---

## Guiding Principles

**1. Distinguish facts from beliefs.**
Most early-stage business thinking is belief dressed as fact. Every answer gets
labeled: **(F) Fact** (validated by real evidence) or **(B) Belief** (plausible but
untested). The goal of each phase is to convert beliefs into facts cheaply.

**2. The hardest question first.**
The natural instinct is to answer easy questions (features, branding, tech stack)
before hard ones (who pays, how much, why you). This skill reverses that order. If
the hardest question has a fatal answer, the easy questions don't matter.

**3. One customer archetype at a time.**
"Everyone" is not a customer. Vague markets produce vague strategy. The skill
forces one specific buyer persona at a time until that archetype is proven or
eliminated.

**4. Push back on hand-wavy answers.**
An answer like "real estate agents would love this" is a belief. A good answer names
a specific person, describes what they do today instead of your product, and
explains why today's solution is painful enough to switch. If an answer doesn't
meet that bar, it gets challenged.

**5. Track the critical path.**
At every phase, the skill identifies the single riskiest assumption — the one that,
if wrong, kills the business. All effort should be focused on resolving that
assumption before moving forward.

---

## The Seven Phases

Work through these in order. Do not skip ahead. Each phase has a clear output
that must exist before moving to the next.

---

### Phase 1: Problem Framing

**Goal:** Articulate the problem with surgical precision. Most pitches describe
a solution, not a problem. This phase forces the problem to be stated independently
of any solution.

**Questions to answer:**
1. What specific situation creates the problem? (Trigger event — when does it occur?)
2. Who experiences it? (Role, context, frequency)
3. What do they do today instead? (The existing behavior you're displacing)
4. Why is today's solution painful? (Concrete cost — time, money, risk, embarrassment)
5. How often does this problem occur for one person? (Frequency drives LTV)

**Output:** A one-paragraph problem statement in this format:
> When [specific person] is [doing specific thing], they face [specific problem].
> Today they solve it by [current behavior], which costs them [concrete cost].
> This happens [frequency] and affects [how many people like them].

**Critical lens:** If the problem statement requires the customer to *realize* they
have a problem, that's a red flag. The best problems are ones customers are already
actively trying to solve (they're searching, spending, complaining).

---

### Phase 2: Customer Archetype

**Goal:** Define one specific buyer with enough precision to find 10 of them.

**Questions to answer:**
1. What is their job title or role?
2. What industry / company size / geography?
3. What does their day look like when this problem occurs?
4. Who else is involved in the decision to buy a solution? (Economic buyer vs. user)
5. What does a "win" look like for them — personally, not just professionally?
6. Where do they spend time online and in person? (Where you'll find them)

**Output:** A one-page customer profile. If you can't name 3 real people who match
this profile within 24 hours, the archetype is too vague.

**Critical lens:**
- If the buyer and the user are different people (e.g., agent buys, homebuyer uses),
  name both and be explicit about who controls the budget.
- If the archetype is defined by demographics instead of behavior, push back —
  "homebuyers aged 28–45" is not a useful archetype; "first-time buyers doing due
  diligence on a property purchase over $400k" is.

---

### Phase 3: Value Proposition

**Goal:** State precisely what outcome your product delivers, in the customer's
language, tied to what they care about.

**Questions to answer:**
1. What does the customer have after using your product that they didn't have before?
   (Outcome, not feature)
2. How do you measure that outcome? (Quantifiable if possible)
3. How much better is this than the current alternative? (10x better? 2x? Why?)
4. What would make a customer choose NOT to use your product even if it works?
   (Adoption blockers — trust, workflow change, cost, habit)

**Output:** A value proposition statement:
> [Product] helps [customer archetype] [achieve outcome] by [key mechanism],
> unlike [current alternative] which [pain point].

**Critical lens:**
- "Saves time" and "better insights" are not value propositions — they're
  categories. Push until there's a specific number or a named alternative.
- If the value proposition only works after the customer changes a habit, the
  adoption blocker analysis is mandatory.

---

### Phase 4: Business Model

**Goal:** Define how money flows — who pays, how much, how often, and what
it costs to deliver.

**Questions to answer:**
1. Who is the economic buyer? (Not who benefits — who writes the check?)
2. What is the pricing model? (Per use, subscription, seat license, API, rev share)
3. What is the price point, and what anchors it? (Comparable products, cost of
   alternative, value delivered, willingness to pay tests)
4. What does it cost to deliver one unit of value? (COGS per report, per user, per API call)
5. What does gross margin look like at scale? (Target: >60% for SaaS, >40% for
   data products)
6. What's the LTV / CAC ratio at your target price point? (Target: >3:1)

**Output:** A simple unit economics model:
```
Price per [unit]:         $___
COGS per [unit]:          $___
Gross margin:             ___%
Estimated CAC:            $___
LTV (price × retention):  $___
LTV:CAC ratio:            ___:1
```

**Critical lens:**
- If the business only works with enterprise customers (high ACV), the sales motion
  will be long and expensive — is that consistent with your resources?
- If gross margin is below 50%, the business is operationally constrained — growth
  requires more capital, not just more customers.
- "We'll figure out pricing later" is not acceptable past Phase 4. Price is a
  strategic signal, not a detail.

---

### Phase 5: Competitive Positioning

**Goal:** Define your defensible position — why customers choose you and why
that advantage is durable.

**Questions to answer:**
1. Who are the direct competitors? (Same buyer, same problem)
2. Who are the indirect competitors? (Different solution, same budget)
3. On what dimensions do you win? (Speed, accuracy, price, integration, brand, data coverage)
4. What is your moat — and how long until a competitor replicates it?
   (Data, network effects, switching costs, brand, proprietary tech, regulatory)
5. What would a well-funded competitor need to do to replicate what you've built?
   How long would it take?

**Output:** A 2x2 positioning map (axes TBD based on the specific market) and a
one-paragraph moat statement.

**Critical lens:**
- "First mover advantage" is rarely a moat — it's a head start. What makes the
  advantage compound over time?
- If the moat is "better product," that's a temporary advantage, not a structural
  one. Push for something that gets harder to replicate as you grow.
- Open data + LLM wrapper is replicable in weeks. The moat must come from
  something else — data breadth, relationships, brand, workflow integration,
  or proprietary enrichment.

---

### Phase 6: Go-to-Market

**Goal:** Define a specific, executable path to the first 10 paying customers
and the motion that scales from 10 to 100.

**Questions to answer:**
1. How do you find one customer who matches your archetype today?
   (Not "we'll run ads" — name a specific action in the next 7 days)
2. What is the sales motion? (Self-serve, low-touch, high-touch, channel partner)
3. What triggers a purchase? (What event causes someone to seek out this product?)
4. What is the onboarding path from awareness to first value? (Time-to-value)
5. What does retention look like — and what causes churn?
6. What's the scalable acquisition channel? (SEO, paid, referral, partnerships,
   content, product-led)

**Output:** A GTM narrative:
> Our first 10 customers will come from [specific source]. We'll reach them by
> [specific action]. The trigger that causes them to seek us out is [trigger event].
> We'll close them with [sales motion]. They'll churn if [churn reason], which we
> prevent by [retention mechanism]. At scale, acquisition is driven by [channel].

**Critical lens:**
- If the GTM requires educating the market before selling to it, the timeline and
  capital requirement multiplies significantly — flag this explicitly.
- "Word of mouth" is not a GTM. It's an outcome of having a great product. Push
  for the seeding strategy that generates the first referrals.
- If the first customer requires a complex procurement process, the "first 10"
  timeline will be 6–18 months, not weeks. Budget accordingly.

---

### Phase 7: Critical Path to Viable Product

**Goal:** Define the minimum product that can generate revenue, and the sequence
of work to get there — not the ideal product, the first dollar.

**Questions to answer:**
1. What is the minimum feature set that a paying customer would use today?
   (Not the full vision — the stripped version)
2. What does the current product lack to reach that bar?
3. What is the single highest-risk assumption that must be validated before
   building further? (The thing most likely to be wrong)
4. What is the cheapest way to test that assumption without building?
   (Landing page, manual concierge, mockup, interview)
5. What does the 6-month product roadmap look like, sequenced by revenue impact?

**Output:** A one-page roadmap:
```
Current state:     [What exists today]
Gap to first $:    [What's missing]
Riskiest assumption: [The one thing most likely to be wrong]
Cheapest test:     [How to validate without building]
Milestone 1 (M1): [First revenue event — date + what]
Milestone 2 (M2): [First retention signal — date + what]
Milestone 3 (M3): [First growth signal — date + what]
```

**Critical lens:**
- If the roadmap starts with infrastructure or polish instead of customer-facing
  value, challenge the ordering.
- "We need to build X before we can sell" is usually false. Most things can be
  faked or done manually for the first 10 customers.
- The riskiest assumption is almost never technical. It's almost always about
  customer behavior — will they pay, will they use it, will they come back.

---

## Session Behavior

### Starting a session

When this skill is invoked:
1. Ask which phase the user wants to work on, OR begin at Phase 1 if this is a
   first session.
2. **Read `biz-dev/business-review.md` in the current project repo first** (if it
   exists). This is the source of truth for where the analysis stands. Acknowledge
   what's already known and what phase is in progress before asking anything new.
3. State the riskiest open assumption before beginning any phase.

### Persisting analysis

After every session — or whenever a phase output is confirmed, a new fact is
validated, or a belief is added or resolved:

1. **Update `biz-dev/business-review.md`** in the current project repo with:
   - Progression tracker (mark phases complete/in-progress)
   - Any new **(F) Fact** entries with date and source
   - Any new or resolved **(B) Belief** entries
   - The completed phase output (problem statement, customer profile, etc.)
   - Updated riskiest open assumption
2. **Commit the file** with a message in the format:
   `[biz-dev] Phase N complete — <one-line summary of what was learned>`
   or for belief updates:
   `[biz-dev] Validate/invalidate assumption — <what changed>`
3. Do not wait for the user to ask to save — persist after every meaningful update.

This ensures business decisions are version-controlled alongside the code.

### During a session

- Ask one question at a time. Wait for an answer before asking the next.
- After each answer, label it **(F) Fact** or **(B) Belief** and explain why.
- If an answer is hand-wavy, challenge it directly:
  > "That's a belief right now. What would make it a fact? Can we test it
  > this week without building anything?"
- When a phase is complete, state the output explicitly and confirm it before
  moving on.
- Track the riskiest assumption at all times and surface it if it changes.

### Ending a session

Before closing:
1. State which phase was completed and what the output is.
2. State the single most important thing to do before the next session.
3. Identify any new beliefs that were surfaced and need validation.
4. If relevant, create Asana tasks for validation work (using asana-pm-workflow).

---

## Critical Challenge Rules

Apply these whenever an answer is given:

| If the answer says...              | Challenge with...                                      |
|------------------------------------|--------------------------------------------------------|
| "Everyone needs this"              | Who specifically loses money or time today without it? |
| "No real competitors"              | What do people do instead? That's your competitor.     |
| "We'll figure out pricing later"   | What would you charge tomorrow if you had to?          |
| "Word of mouth will drive growth"  | How do you get the first referral?                     |
| "The market is huge"               | How many reachable buyers match the archetype exactly? |
| "We just need to build X first"    | Can you sell it manually before building it?           |
| "Customers will love this feature" | Have you watched a customer try to use it?             |
| "We have a first-mover advantage"  | What compounds your advantage over time?               |

---

## Progression Tracker

Use this to track state across sessions:

```
Phase 1 — Problem Framing:       [ ] Not started  [ ] In progress  [x] Complete
Phase 2 — Customer Archetype:    [ ] Not started  [ ] In progress  [ ] Complete
Phase 3 — Value Proposition:     [ ] Not started  [ ] In progress  [ ] Complete
Phase 4 — Business Model:        [ ] Not started  [ ] In progress  [ ] Complete
Phase 5 — Competitive Positioning:[ ] Not started  [ ] In progress  [ ] Complete
Phase 6 — Go-to-Market:          [ ] Not started  [ ] In progress  [ ] Complete
Phase 7 — Critical Path:         [ ] Not started  [ ] In progress  [ ] Complete

Riskiest open assumption:
[State the single biggest belief that, if wrong, changes everything]

Validated facts (F):
- [List facts confirmed by evidence]

Outstanding beliefs (B):
- [List beliefs still needing validation]
```
