# Technical Setup Guide
## AI Ops Consultant + Meeting Tool Subscription

**Target:** Day 1 setup completable in one afternoon (under 4 hours)
**Stack:** JS/Python, Node.js, Claude API, GitHub, Stripe, Notion, Airtable

---

## Day 1 Checklist (Do Today, Before Any Outreach)

- [ ] Stripe account created and bank connected
- [ ] Invoice template saved and ready to send
- [ ] Contract template saved (1 page, plain English)
- [ ] Meeting summarizer subscription link live ($29/mo)
- [ ] GitHub private repo created for client work template
- [ ] Claude Code architecture template committed to that repo

**Estimated time: 3.5 hours**

---

## Part 1: Consulting Side

---

### 1. Client Intake System — `DAY_1`

**Goal:** Let someone go from "I'm interested" to a scoped project in 48 hours without chasing them.

**V1 setup (no website needed):**

1. Create a free [Calendly](https://calendly.com) account (free tier is enough)
2. Create one event type: **"AI Ops Discovery Call — 30 min"**
3. In the Calendly form, add these required questions before they can book:
   - "What tool is causing the most pain right now? (Notion / Airtable / Slack / Gmail / Other)"
   - "Roughly how many people on your team touch this process?"
   - "What does the manual version of this currently look like?"
   - "What's your rough timeline to get something in place?"
4. Set availability to exclude after 2:30pm (buffer before school pickup)
5. Copy your Calendly link — this is what you send in every outreach message

**That's your intake system.** No form builder, no CRM, no website needed.

When they book, Calendly emails you their answers. You read them before the call. You arrive ready to scope, not ask basic questions.

---

### 2. Proposal Template — `DAY_1`

Save this as `proposal_template.md` in a local folder. Fill in the `[BRACKETED]` fields per client.

```
---
PROPOSAL
[CLIENT NAME] x [YOUR NAME]
[DATE]
---

THE PROBLEM WE'RE SOLVING
[1-2 sentences describing the specific manual process that costs them time]
Example: "Your team is copying Slack standup messages into Notion manually every morning.
This takes ~20 minutes/day and falls through the cracks on Fridays."

WHAT I'LL BUILD
[Specific deliverable — be exact, not vague]
Example: "A Claude Code automation that reads your #standup Slack channel each morning,
extracts action items per person, and posts a formatted summary to your Notion project tracker."

WHAT'S INCLUDED
- Working script deployed in your environment
- Tested on your real data (minimum 5 live runs before handoff)
- 30-minute live handoff session (screen share, I walk you through it)
- Written setup doc so your team can restart it if needed
- 14 days of async support via email for bugs (not scope changes)

WHAT'S NOT INCLUDED
- Changes to the core workflow after final delivery
- Ongoing maintenance or monitoring
- API costs (you pay your own Claude/Slack/Notion API bills)

INVESTMENT
[TIER NAME]: $[AMOUNT]
Payment: 50% upfront, 50% on delivery
I accept Stripe (card) or ACH bank transfer

TIMELINE
Discovery confirmed: [DATE]
First working version for your review: [DATE — typically 5-7 business days from deposit]
Final delivery: [DATE — typically 3-5 business days after your feedback]

NEXT STEP
Reply "yes" to this email and I'll send the contract and invoice for the deposit.
---
```

**Pricing reference:**
- Starter ($500): Single workflow, one tool, straightforward prompt-in/output pattern
- Core ($2,700): 2-3 connected workflows, cross-tool (e.g. Slack → Notion), 1-2 weeks
- Premium ($5,400): Complex multi-step automation with conditionals, error handling, custom triggers

---

### 3. Contract Template — `DAY_1`

**Use [HelloSign free tier](https://www.hellosign.com) or just email with explicit written confirmation.**

For V1, a plain-text email agreement is legally binding in the US. Send this after they say yes to the proposal:

```
Subject: Project Agreement — [PROJECT NAME]

Hi [NAME],

Per our conversation, here's a quick written summary of what we've agreed to.
Reply "Confirmed" and I'll send the deposit invoice.

SCOPE: [Copy the "What I'll Build" section from the proposal]

PRICE: $[TOTAL] — $[50%] deposit due before work begins, $[50%] due on delivery

TIMELINE: First draft by [DATE], final delivery by [DATE]

OWNERSHIP: You own the code I write for you. I retain the right to use
non-confidential patterns and approaches in future work (not your data or business logic).

CHANGES: If the scope changes materially after we start, we'll agree in writing
on added cost and time before I proceed. Small adjustments included at my discretion.

BUGS VS SCOPE: If something I built doesn't work as described, I fix it free.
If you want something different than what was described, that's a new scope item.

PAYMENT: Late payment beyond 14 days pauses all work until resolved.

Does this reflect your understanding? Reply "Confirmed" to proceed.

— [YOUR NAME]
```

**When to upgrade:** Once you have 3+ clients, get a real contract via [Bonsai](https://www.hellobonsai.com) ($19/mo) or hire a freelance contract lawyer for a one-time $200 template.

---

### 4. Invoice and Payment System — `DAY_1`

**Use Stripe. Not Wave. Here's why:**

| | Stripe | Wave |
|---|---|---|
| Card processing fee | 2.9% + 30¢ | 2.9% + 60¢ (higher) |
| ACH bank transfer | 0.8% (capped $5) | Not available |
| Subscription billing | Native | Clunky |
| Professional appearance | Very high | Medium |
| Time to set up | 30 min | 30 min |

Wave is free accounting software. Use it to track income if you want. But send invoices and collect payment through Stripe.

**Stripe setup — exact steps:**

1. Go to [stripe.com](https://stripe.com) → Create account
2. Enter your legal name, address, SSN (last 4 for now, full later for payouts), bank account
3. In dashboard: **Products → Add Product**
   - Create "AI Ops Consulting Deposit" at $0 (you'll set the amount per invoice)
4. Go to **Billing → Invoices → Create Invoice**
   - Add customer (email is enough)
   - Add line item: "Project deposit — [project name]" at the agreed amount
   - Set payment method: Card + ACH
   - Send
5. For recurring (meeting tool): see Part 2 below

**For consulting, you'll create a new invoice per project. Takes 5 minutes each time.**

For accounting: use a free [Wave](https://www.waveapps.com) account to import Stripe transactions monthly and track income for taxes. Do not use Wave for invoicing.

---

### 5. Delivery Protocol — `WEEK_1`

**The handoff has three components. Every project gets all three.**

**a. Final code delivery**
- Push final code to a private GitHub repo
- Transfer ownership of the repo to the client's GitHub account OR
- Zip the folder and share via Google Drive link (simpler for non-technical clients)
- Include a `README.md` with: what it does, how to run it, what credentials it needs, what to do if it breaks

**b. Live handoff session (30 min via Loom or Zoom)**
- Screen share and run the automation on real data while they watch
- Walk through the README
- Answer their questions
- Record it — send them the recording after
- This session is included in all tiers

**c. 14-day async support window**
- Bugs (it doesn't do what the proposal said it would do) = you fix for free
- Scope changes (they want something new) = new project conversation
- Response time during support window: within 24 hours on weekdays
- After 14 days: email support is $150/hr, billed in 30-minute increments

---

### 6. Communication Protocol — `DAY_1`

**Set this expectation in every project kickoff email:**

```
My working hours are roughly 9am-2:30pm ET, Monday-Friday.
I respond to project emails within 24 hours on weekdays.
I don't work evenings or weekends — if something comes in Friday afternoon,
you'll hear back Monday morning.

For urgent questions during a project: email is best, I check it twice a day.
No Slack, no DMs, no text for project communication — keeps everything documented.

If you want to change something in scope after we've started:
just email me what you're thinking. I'll tell you within 24 hours if it's
covered in the current scope or if we need to talk about adding to it.
I'll never just do extra work and surprise you with a bill.
```

**Scope change process:**
1. Client emails request
2. You assess: is this a bug fix (your problem) or a scope change (their ask)?
3. If scope change: reply with "That's outside our current scope. I can add it for $[X] and [Y days]. Want to proceed?"
4. Get written "yes" before doing any work
5. Send a mini-invoice for the add-on before starting

---

## Part 2: Meeting Tool Subscription Product

---

### 1. Payment Layer — `DAY_1`

**Adding $29/mo Stripe subscription to your existing meeting summarizer script**

This is a gate, not an integration. The script doesn't talk to Stripe. Stripe just tells you who's paid.

**Step-by-step:**

**In Stripe dashboard:**
1. Go to **Products → Add Product**
   - Name: "Meeting Summarizer — Monthly"
   - Pricing: $29/month, recurring
   - Click Save
2. Go to **Payment Links → Create Payment Link**
   - Select the product you just created
   - Under "After payment": set to redirect to a confirmation page (use a free [Carrd](https://carrd.co) page or just a Google Doc link)
   - Copy the payment link — this is what you share with people
3. Go to **Settings → Customer Portal**
   - Enable it (this lets customers manage their own subscription and cancel)
   - Copy the portal link — include it in your welcome email

**That's the payment layer. It takes 15 minutes.**

When someone pays, Stripe emails you a notification. You manually add them to your user list (see next section) and send them the tool access.

---

### 2. User Management — `DAY_1`

**V1: Use a Notion database or Google Sheet. No code needed.**

Create a table with these columns:

| Column | Values |
|---|---|
| Name | Text |
| Email | Text |
| Stripe Customer ID | Copy from Stripe dashboard (looks like `cus_abc123`) |
| Status | Active / Cancelled / Past Due |
| Access Sent | Yes / No |
| Start Date | Date |
| Notes | Text |

**Your workflow when someone pays:**
1. Get Stripe email notification
2. Open your user table, add a row
3. Paste their Stripe customer ID from the Stripe notification email
4. Send them the welcome email with tool access (see next section)
5. Mark "Access Sent: Yes"

**Your workflow when someone cancels:**
1. Stripe emails you
2. Update status to "Cancelled" in your table
3. No further action needed — they already have the script, but you're no longer obligated to support it

**When to upgrade (OPTIONAL):** Once you have 10+ subscribers, set up a Stripe webhook to auto-update a database. Until then, manual is fine — you'll have fewer than 5 events per month.

---

### 3. Delivery Mechanism — `WEEK_1`

**How a paying user gets the tool:**

After someone pays, send them this email:

```
Subject: Your Meeting Summarizer Access

Hi [NAME],

Welcome — your subscription is active.

Here's how to get started:

1. Download the script: [link to private GitHub repo or Google Drive zip]
2. Setup guide: [link to a Google Doc with step-by-step instructions]
3. You'll need: a Claude API key (get one at console.anthropic.com — takes 5 min)

The setup doc covers everything. If something doesn't work after following it,
email me at [your email] and I'll help within 24 hours on weekdays.

To manage your subscription or cancel: [Stripe customer portal link]

— [YOUR NAME]
```

**What to include in the setup Google Doc:**
- System requirements (Node.js version, how to install it)
- How to add their Claude API key (environment variable setup)
- How to run the script on a transcript file
- What the output looks like (include an example)
- Common errors and how to fix them
- One sentence: "Your API costs are separate and typically run $0.10-$0.50/month at normal usage"

**V1 delivery is a zip file or private GitHub repo link.** That's it. No app, no login portal, no dashboard.

**When to upgrade (OPTIONAL):** Phase 3 (months 4-6), if you have 20+ subscribers, build a simple web UI with auth. Until then, this approach scales to 50 subscribers with zero maintenance.

---

### 4. Support Policy — `DAY_1`

Include this in your welcome email and anywhere you describe the product:

```
WHAT'S INCLUDED WITH YOUR SUBSCRIPTION
- The script itself and all future updates
- Setup help if you get stuck following the setup guide (email, 24hr response weekdays)
- Bug fixes if the script produces incorrect output

WHAT'S NOT INCLUDED
- Help with your Claude API account or billing (contact Anthropic support)
- Custom modifications to the script for your workflow
- Real-time support or phone/video calls
- Support for running the script on non-standard platforms or corporate IT setups

CANCELLATION
Cancel anytime from your customer portal: [link]
No refunds for partial months, but you can cancel before your next billing date.
```

**Hard limit on support time:** If a subscriber sends more than 3 emails in a month, that's a consulting client, not a product subscriber. Reply: "It sounds like you might benefit from a custom setup session — I offer those at $150/hr if you'd like to book time."

---

## Part 3: Claude Code Delivery Architecture

**Use this pattern for every single client build. Same structure every time.**

---

### The Standard Architecture Pattern — `WEEK_1`

Every automation you build has exactly four layers:

```
[TRIGGER] → [CONTEXT LOADER] → [CLAUDE CALL] → [OUTPUT HANDLER]
```

**Layer 1: Trigger**
How the automation starts. Options in order of simplicity:
- Manual (they run a script): simplest, fine for V1 of almost anything
- Scheduled (cron job via node-cron or GitHub Actions): for daily/weekly automations
- Event-driven (webhook from Slack, Airtable, Notion): for real-time triggers

Default to manual or scheduled for first delivery. Event-driven adds complexity — only use it if the client's use case truly requires it.

**Layer 2: Context Loader**
What gets fed to Claude. This is where most bugs live. Build it separately from the Claude call so you can test it independently.

```javascript
// context_loader.js — always a separate function
async function loadContext(sourceData) {
  return {
    rawInput: sourceData,          // the actual thing being processed
    metadata: {                    // structured facts about it
      timestamp: new Date().toISOString(),
      source: "notion_database",
      recordCount: sourceData.length
    },
    constraints: {                 // limits and rules
      outputFormat: "json",
      maxItems: 10,
      language: "English"
    }
  };
}
```

**Layer 3: The Claude Call — Exact System Prompt Structure**

Every system prompt has four sections in this exact order:

```
ROLE
You are an operations assistant for [CLIENT COMPANY NAME].
Your job is to [specific task in one sentence].
You have access to [list what data you're giving it].

RULES
- Always output valid JSON
- If a field is missing from the input, use null — never guess
- Do not add commentary outside the JSON structure
- [2-3 rules specific to their use case]

OUTPUT FORMAT
Return exactly this structure:
{
  "summary": "string — 2-3 sentences",
  "action_items": [
    { "owner": "string", "task": "string", "due_date": "string or null" }
  ],
  "flags": ["array of strings — only include if something needs human attention"]
}

EXAMPLES
Input: [paste a real example from their data]
Output: [paste the exact JSON you want back]
```

**Why this order matters:** Role first sets context before rules. Rules before format prevents the model from optimizing for format over accuracy. Examples last — after it knows the rules, a concrete example locks in the behavior.

**The actual API call:**

```javascript
// claude_call.js
const Anthropic = require("@anthropic-ai/sdk");

const client = new Anthropic(); // reads ANTHROPIC_API_KEY from env

async function runClaude(systemPrompt, userContent) {
  const response = await client.messages.create({
    model: "claude-opus-4-5",          // use opus for complex reasoning
    // model: "claude-haiku-3-5",      // use haiku for simple extraction (10x cheaper)
    max_tokens: 1024,
    system: systemPrompt,
    messages: [
      { role: "user", content: userContent }
    ]
  });

  const raw = response.content[0].text;

  // Always parse and validate before returning
  try {
    return JSON.parse(raw);
  } catch (e) {
    console.error("Claude returned non-JSON:", raw);
    throw new Error("Parse failed — check system prompt OUTPUT FORMAT section");
  }
}
```

**Layer 4: Output Handler**
What happens with Claude's response. Keep this completely separate from the Claude call.

```javascript
// output_handler.js
async function handleOutput(parsedResponse, destination) {
  // destination is "notion" | "airtable" | "slack" | "file"

  if (destination === "notion") {
    await pushToNotion(parsedResponse);       // your Notion API call
  } else if (destination === "slack") {
    await postToSlack(formatForSlack(parsedResponse));
  } else if (destination === "file") {
    await writeJsonFile(`output_${Date.now()}.json`, parsedResponse);
  }

  // Always log locally too
  console.log(`[${new Date().toISOString()}] Delivered to ${destination}:`, parsedResponse);
}
```

---

### Context Management — `WEEK_1`

**The core problem:** Claude has a context window. Large inputs = higher cost + potential errors.

**Your rule:** Never pass more than 6,000 tokens of raw data to Claude in a single call. If the input is larger, chunk it.

**Chunking pattern:**

```javascript
function chunkArray(arr, size) {
  const chunks = [];
  for (let i = 0; i < arr.length; i += size) {
    chunks.push(arr.slice(i, i + size));
  }
  return chunks;
}

async function processLargeInput(items) {
  const chunks = chunkArray(items, 20); // 20 records per call
  const results = [];

  for (const chunk of chunks) {
    const result = await runClaude(SYSTEM_PROMPT, JSON.stringify(chunk));
    results.push(...result.action_items); // merge arrays
    await new Promise(r => setTimeout(r, 500)); // rate limit buffer
  }

  return results;
}
```

**When to use caching (OPTIONAL, WEEK_1):**
If your system prompt is longer than 1,000 tokens and you're running the same prompt repeatedly (e.g., daily batch jobs), add `cache_control` to reduce costs. The `claude-api` skill covers this if you need the exact implementation.

---

### Cost Estimation Formula — `DAY_1`

**Know this before you scope any project.**

**Token counting rule of thumb:**
- 1 token ≈ 4 characters ≈ 0.75 words
- A typical Slack message: ~50 tokens
- A meeting transcript (60 min): ~8,000-15,000 tokens
- A Notion page: ~1,000-3,000 tokens
- Your system prompt: ~300-800 tokens

**Claude pricing (as of April 2026 — verify at anthropic.com/pricing):**
- claude-haiku-3-5: ~$1 per million input tokens, $5 per million output tokens
- claude-opus-4-5: ~$15 per million input tokens, $75 per million output tokens

**Cost formula per run:**

```
cost_per_run = (input_tokens × input_price) + (output_tokens × output_price)

Example — meeting summarizer, haiku:
  input:  10,000 tokens (transcript + system prompt)
  output: 500 tokens (summary JSON)
  cost = (10,000 × $0.000001) + (500 × $0.000005)
       = $0.01 + $0.0025
       = ~$0.013 per meeting

Monthly (20 meetings): $0.26/month — negligible
```

**For client projects, tell them:**
> "API costs for this automation will run approximately $[X]/month based on [N] runs at [Y] records each. You'll pay this directly to Anthropic — it's typically $5-30/month for most ops workflows."

**Default model selection:**
- Use **haiku** for: extraction, classification, formatting, simple summaries
- Use **opus** for: complex reasoning, multi-step analysis, anything requiring judgment calls
- Use **sonnet** when haiku gets things wrong but opus feels like overkill

**Budget flag:** If your estimate exceeds $50/month in API costs for the client, flag it explicitly in the proposal. Surprises kill trust.

---

### GitHub Repo Template Structure — `WEEK_1`

Create this once, copy it for every client project:

```
client-project-template/
├── README.md              ← setup instructions (fill in per client)
├── .env.example           ← list all env vars needed, no actual values
├── .gitignore             ← includes .env, node_modules, output/
├── package.json
├── src/
│   ├── index.js           ← entry point, wires all layers together
│   ├── context_loader.js  ← Layer 2
│   ├── claude_call.js     ← Layer 3
│   ├── output_handler.js  ← Layer 4
│   └── prompts/
│       └── system_prompt.txt  ← system prompt lives here, not in code
├── test/
│   ├── sample_input.json  ← real anonymized sample from client
│   └── expected_output.json
└── scripts/
    └── run.sh             ← one command to run the whole thing
```

**The rule:** If a new person can't get this running in 30 minutes following only the README, the README isn't done yet.

---

## Day 1 Time Budget

| Task | Time |
|---|---|
| Stripe account + bank connection | 30 min |
| Create consulting invoice in Stripe | 10 min |
| Create $29/mo subscription product + payment link in Stripe | 15 min |
| Save proposal template locally | 10 min |
| Save contract template locally | 10 min |
| Create user management table in Notion or Google Sheets | 15 min |
| Set up Calendly with intake questions | 20 min |
| Create GitHub repo with template structure | 30 min |
| Write welcome email draft for meeting tool subscribers | 15 min |
| Review cost estimation formula, test on meeting summarizer | 15 min |
| **Total** | **~3.5 hours** |

---

## Week 1 Checklist (Before First Delivery)

- [ ] GitHub template repo tested end-to-end on a dummy project
- [ ] Meeting summarizer cleaned up and packaged for delivery (zip + setup Google Doc)
- [ ] At least one test run of the delivery protocol (send yourself the welcome email)
- [ ] README template written and tested (can you follow your own instructions?)
- [ ] First client scoping call completed
- [ ] Proposal sent for first project

---

## Optional (Do Not Do Until You Have Revenue)

- [ ] Website or landing page (Carrd, $19/yr — only when you need it for cold outreach)
- [ ] Bonsai contract software ($19/mo — only after 3+ clients)
- [ ] Stripe webhook for automatic subscriber management (only after 10+ subscribers)
- [ ] Payment UI for meeting tool (only in Phase 3, months 4-6)
- [ ] LLC formation (worth doing around month 2-3 once income is consistent)
- [ ] Separate business bank account (open this same time as LLC)
- [ ] Prompt caching implementation (only if monthly Claude API bill exceeds $20)
