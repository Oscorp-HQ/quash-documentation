# Pricing model docs update — design

**Date:** 2026-08-01
**Branch:** `docs/pricing-model-update`, branched from `mintlify-port` (the production branch per `README.md`). PR targets `mintlify-port`, not `main`.
**Source of truth:** the pricing model handoff brief (marketing site shipped; docs lagging).

## Goal

Bring the Mintlify docs in line with the new commercial model: executions replace test minutes, a four-tier Free/Solo/Team/Enterprise ladder replaces the five-tier Free-Trial/Starter/Growth/Pro/Enterprise ladder, and overage billing disappears entirely.

## Scope

One page rewritten, four leaked claims corrected, one glossary entry added.

| File | Change |
|---|---|
| `administration/how-quash-pricing-works.mdx` | Full rewrite |
| `devices/cloud-device.mdx` | 3 edits (lines 19, 23, 33) |
| `devices/overview.mdx` | 1 edit (line 70) |
| `getting-started/quickstart-guide.mdx` | 1 edit (line 85) |
| `reference/glossary.mdx` | Add "Execution" entry |
| `quash-mcp/overview.mdx` | 1 edit — plan availability (added 2026-08-01, see MCP amendment) |

`docs.json` needs no change — the nav entry `administration/how-quash-pricing-works` and its label are still correct.

## Explicitly out of scope

Verified as unrelated to Quash pricing; must not be swept:

- The Apple Developer Program `$99/year` in `devices/physical-ios-devices.mdx:6` and `getting-started/faqs.mdx:78`.
- The **Figma** "free or Starter plans" reference in `test-studio/recipe/attaching-context.mdx:64` — that is Figma's tier ladder, not Quash's.
- Credit-card payment examples in `test-studio/prompting-guide-test-generation/common-mistakes.mdx` — test fixtures, unrelated to billing.
- `test-studio/token-management.mdx`, `getting-started/core-concepts/tokens-and-compact.mdx`, and the glossary "Tokens" entry — these describe the agent's context-window budget, not billing. Confirmed by grep: no metering, charging, or quota language.
- All security and compliance content (encryption, residency, retention).
- All product capability docs (what the agent does, integrations, reporting, test paths).

## Part 1 — `administration/how-quash-pricing-works.mdx`

Full rewrite. Section order:

1. **Frontmatter** — `description` currently reads "Plans, test minutes, cloud sessions, overage, and what changes when you upgrade." Replace with a description built on plans, executions, and what counts.
2. **Opening** — lead on the site's framing: *"Write all the tests you want. Pay only when they run."*
3. **Plans at a glance** — the four-tier table (below).
4. **What counts as an execution** — its own prominent section, ahead of tier detail. This is the definition everything else depends on.
5. **No overage billing** — replaces the old `## Overage` section outright.
6. **Free plan** — replaces `## Free trial`.
7. **What each plan includes** — "adds over the previous tier" prose.
8. **Feature comparison** — seven tables, recolumned (below).
9. **Common questions** — rewritten around executions.
10. Closing link to `https://quashbugs.com/pricing` (retained).

### The hard rule

**Solo is the only published price.** Team and Enterprise must never show a number anywhere on the page — not a range, not a "starting at", not an implied per-seat figure. Describe them by size:

- Team — "for teams past ~150 executions/month, 3+ seats, or multiple apps"
- Enterprise — "private deployment, 1,500+ executions/month"

Where a cost reference is unavoidable, say "quoted" or link to `/pricing`.

### Plans at a glance

| | Free | Solo | Team | Enterprise |
|---|---|---|---|---|
| Price | $0 | $99/mo ($79/mo billed annually) | Quoted | Quoted |
| Test generation | Unlimited | Unlimited | Unlimited | Unlimited |
| Executions | 40 to start, then 5/month | 150/month | Provisioned | Provisioned |
| Apps | 1 | 1 | Multiple | Unlimited |
| Seats | 1 | 2 | Negotiated | Unlimited |
| Overage billing | None | None | None | None |
| Cloud devices | — | ✓ | ✓ | ✓ |
| Real device fleet | — | — | — | ✓ |
| Support | Community | Community | Onboarding + email | Dedicated CSM, custom SLA |

The brief's separate "Card required" and "Expiry" rows are folded into the Free plan prose as "No card, no expiry" rather than carried as table rows — as rows they are only meaningful for the Free column.

### What counts as an execution

State all three rules explicitly. This is the single most important definition on the page.

**One execution = one test run on a device.**

- Counts **wherever it runs** — local device, emulator, or Quash-hosted cloud. This reverses the old "local execution doesn't count" rule; the page must be unambiguous, because the old rule is what existing users believe. The reason to give: the cost is the agent reasoning about the app, not the device, and that is incurred identically on a local run.
- A test that **fails counts the same as one that passes.** Finding a failure is the product working.
- **Generation never counts.** Describing flows, generating test cases, refining prompts, editing suites, reading reports, inviting teammates — free on all plans including Free.

There is a fair-use rate limit on generation. It must **not** be documented as a number or presented as a quota.

### No overage billing

Replaces `## Overage` entirely. No plan bills overage. Use the site framing: *"No overage billing. If you outgrow Solo, we'll size a plan with you — you'll never get a surprise invoice."*

Deleted from the old page: `$0.20/min`, "Annual customers get 20% off overage rates", "Overage available" as a Starter bullet, and the two overage mentions in the free-trial section.

### Free plan

Replaces `## Free trial`. 40 executions to start, then 5/month. No credit card. **No expiry** — the 14-day trial is gone. Full platform access minus the tier-gated capabilities below.

### What each plan includes

- **Free** — unlimited test generation, local devices and emulators, prompt-to-execution testing, detailed execution reports, community support.
- **Solo** adds over Free: cloud devices, backend and API validation, full test suite management.
- **Team** adds over Solo: CI/CD integrations (GitHub Actions, GitLab, Bitbucket, Jenkins), issue-tracker integrations (Jira, Linear, GitHub Issues), webhooks and triggers, scheduled regression runs, hands-on onboarding, email support.
- **Enterprise** adds over Team: private VPC or on-prem deployment, custom data residency, SSO (SAML/OIDC), RBAC, SCIM provisioning, compliance documentation (SOC 2, ISO 27001, GDPR, DPDPA), dedicated real device fleet, dedicated CSM, custom SLA.

**Team must not read as enterprise-only.** Include the site's framing: *"Team is quoted to your actual setup — it starts wherever you are, and plenty of Team customers are small."* This framing exists to stop mid-market buyers self-selecting out; it is not optional decoration.

### Feature comparison — row allocation

All seven tables retained, recolumned from Starter/Growth/Pro/Enterprise to Free/Solo/Team/Enterprise. Note that Free is now a **column**, which it was not before (the old tables started at Starter).

**Test Execution**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Intent-driven test execution | ✓ | ✓ | ✓ | ✓ | unchanged |
| Local devices and emulators | ✓ | ✓ | ✓ | ✓ | unchanged |
| Cloud devices (Quash-hosted) | — | ✓ | ✓ | ✓ | brief: Solo adds cloud devices |
| Vision + reasoning models | ✓ | ✓ | ✓ | ✓ | unchanged |
| Adaptive execution | ✓ | ✓ | ✓ | ✓ | **judgment call** |
| Bring your own LLM API keys | — | — | — | ✓ | unchanged |

**Test Generation**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Natural language test generation | ✓ | ✓ | ✓ | ✓ | brief: unlimited on every plan |
| Codebase ingestion | ✓ | ✓ | ✓ | ✓ | **judgment call** |
| Figma ingestion | ✓ | ✓ | ✓ | ✓ | **judgment call** |

**Test Management**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Full test suite management | — | ✓ | ✓ | ✓ | brief: Solo adds suite management |
| Test paths (memory-driven reruns) | ✓ | ✓ | ✓ | ✓ | unchanged |
| Apps Manager and Knowledge | ✓ | ✓ | ✓ | ✓ | unchanged |
| Scheduled regression runs | — | — | ✓ | ✓ | brief: Team adds |

**Backend and API**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Backend response validation | — | ✓ | ✓ | ✓ | brief: Solo adds |
| API validation | — | ✓ | ✓ | ✓ | brief: Solo adds |
| Database validation | — | — | ✓ | ✓ | **judgment call** |

**Reporting and Analytics** — all three rows (detailed execution reports, AI-powered debugging insights, real-time usage tracking) stay ✓ across all tiers, unchanged from the old page. The Free column is new; all three apply to it.

**Integrations and Workflow**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Webhooks and triggers | — | — | ✓ | ✓ | brief: Team adds |
| CI/CD (GitHub Actions, GitLab, Bitbucket, Jenkins) | — | — | ✓ | ✓ | brief: Team adds |
| Issue tracker (Jira, Linear, GitHub Issues) | — | — | ✓ | ✓ | brief: Team adds |
| Agentic app monitoring | — | — | ✓ | ✓ | **judgment call** |

**Security and Administration**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Encryption in transit and at rest | ✓ | ✓ | ✓ | ✓ | unchanged |
| RBAC | — | — | — | ✓ | **user decision** — see below |
| SSO (SAML / OIDC) | — | — | — | ✓ | brief |
| SCIM provisioning | — | — | — | ✓ | brief |
| On-prem / self-hosted | — | — | — | ✓ | brief |
| Private VPC | — | — | — | ✓ | brief |
| Custom data residency | — | — | — | ✓ | brief |
| Compliance docs (SOC 2, ISO 27001, GDPR, DPDPA) | — | — | — | ✓ | brief |

**Support**

| Row | Free | Solo | Team | Ent | Source |
|---|---|---|---|---|---|
| Community support | ✓ | ✓ | ✓ | ✓ | brief |
| Email support | — | — | ✓ | ✓ | brief: Team adds email support |
| Hands-on onboarding | — | — | ✓ | ✓ | brief: Team adds |
| Implementation services | — | — | — | ✓ | unchanged |
| Dedicated CSM | — | — | — | ✓ | brief |
| Custom SLA | — | — | — | ✓ | brief |

**Rows deleted:** "Priority response (&lt;4 biz hours)" and "Full automation guarantee". Both are SLA-shaped promises the new model does not make; Enterprise's "custom SLA" covers the ground.

### Decisions on record

**RBAC and SSO both land at Enterprise only.** The brief places both at Enterprise but flags SSO as unverified ("an earlier internal design had SSO at a lower tier"). The current docs ship RBAC at the mid tier. User decision on 2026-08-01: follow the brief. Consequence to be aware of — an existing mid-tier customer reading the docs sees RBAC move out of reach.

**Six rows are judgment calls, not brief-derived facts.** Marked above. Rationale:

- *Adaptive execution* → all tiers. Gating a core agent behaviour contradicts the model's thesis that you are metered only on executions.
- *Codebase ingestion, Figma ingestion* → all tiers. The old Enterprise-only rows already contradict the rest of the docs: `apps/apps-manager/knowledge.mdx` gates codebase connection on nothing, and `test-studio/recipe/attaching-context.mdx:64` gates Figma on a paid **Figma** plan rather than a Quash tier. Caveat worth restating: "generation is unlimited" is a claim about metering, and extending it to input sources is an inference. These are the two rows most worth a second opinion before publish.
- *Database validation* → Team+. The brief names Solo's adds as "backend **and API** validation" — pointedly not database — and the old page gated it above the $99 tier.
- *Agentic app monitoring* → Team+. Absent from the brief; Team is now the second-highest tier as Pro was.

### Common questions

Rewrite the section around executions. Questions to carry:

- What counts as an execution? (restate the definition)
- Do local runs count? — **yes**, explicitly reversing the old rule
- Does a failed test count? — yes, same as a pass
- Does generating tests count? — no
- What happens when I run out of executions? — no overage; size up
- When should I move from Solo to Team? — the size-based framing, no number
- Can I add more apps?
- Cloud devices vs the real device fleet? — fleet is **Enterprise**, no longer a Pro add-on
- How does annual billing work? — Solo $99 → $79/mo. **Delete** the old Growth/Pro annual figures and the "20% off overage" clause.
- How does the Free plan work? — 40 then 5/month, no card, no expiry
- Can I bring my own LLM API keys? — Enterprise (retained)
- What is in Enterprise that I cannot get in Team? (was "…in Pro")
- I am a fintech or regulated company — which plan? — Enterprise (retained, update tier names)
- I am already on a custom plan — what happens? — **retained verbatim**, still true and more relevant than ever during a pricing migration

### Strings that must not survive

Verify by grep after the rewrite: `test minute`, `agent minute`, `cloud device minute`, `Starter`, `Growth`, `$399`, `$899`, `$319`, `$719`, `$0.20`, `overage` (except in the "no overage billing" construction), `14-day`, `14 days`, `100 test minutes`, `concurrent cloud session`, `free credits`, `credit balance`, `recharge`, `add-on on Pro`.

Two of these have legitimate survivors elsewhere in the repo, so scope the grep accordingly rather than sweeping blindly:

- `Starter` must still appear in `test-studio/recipe/attaching-context.mdx:64` — that is a **Figma** tier. Grep for it only within the five in-scope files.
- `$99` must still appear in `devices/physical-ios-devices.mdx:6` and `getting-started/faqs.mdx:78` — Apple Developer Program — alongside its legitimate new Solo uses.

`Pro` as a bare word also survives legitimately in unrelated contexts (`MacBook Pro`, `Gemini 2.5 Pro`, `Apple Developer Program`); only tier-name uses are in scope.

## Part 2 — leaked plan claims

Per user decision: **soften, don't delete.** Drop the numbers and per-tier framing, keep a true statement that cloud device capacity depends on plan. Users still need an answer for why they hit a queue.

| Location | Current | Change |
|---|---|---|
| `devices/cloud-device.mdx:19` | "Cloud device access and the number of concurrent sessions depend on your plan." | Cloud device capacity depends on your plan. Leave the 5-minute inactivity timeout untouched — it is a product behaviour, not a plan limit. |
| `devices/cloud-device.mdx:23` | "See How Quash Pricing Works for cloud session limits per plan." | Keep the link, drop the "limits per plan" promise. |
| `devices/cloud-device.mdx:33` | "…up to the concurrent session limit on your plan. If you need dedicated devices, the real device fleet is available as an add-on on Pro and included in Enterprise." | Drop the session-limit clause. **Real device fleet becomes Enterprise-only** — this is a factual error under the new model, not just phrasing. |
| `devices/overview.mdx:70` | "Available on all plans — concurrent session limits vary by tier" | Available on paid plans; capacity varies. Note: cloud devices are **not** on Free under the new model, so "all plans" is now wrong on two counts. |
| `getting-started/quickstart-guide.mdx:85` | "Cloud access and concurrent session limits depend on your plan." | Soften; **keep the queue explanation intact** — it is the user-visible behaviour. |

## Part 3 — glossary

Add an **Execution** entry to `reference/glossary.mdx`, positioned between "Environment tag" (line 39) and "Guidance" (line 43) to hold the file's rough alphabetical order. Follows the file's existing shape: `## Heading`, definition paragraph, then a `[→ link]` line pointing to `/administration/how-quash-pricing-works`.

Content: one test run on a device; counts on local, emulator, and cloud alike; failures count the same as passes; generation does not count.

No "test minute" entry exists in the glossary, so there is nothing to remove.

## Amendment — MCP availability (2026-08-01)

Added after the initial pass, on user report that MCP had been left out of the plan model entirely. **The MCP server is available on every plan, including Free.** It is not a paid upgrade. Plan limits still apply to what you do through it: agent-started tests count as executions like any other run, and plan-gated capabilities (cloud devices, for instance) stay gated when the request arrives over MCP.

Reflected in six places:

- **Plans at a glance** — new `MCP server` row, ✓ across all four tiers.
- **What counts as an execution** — the first rule broadened from "wherever it runs" to "wherever it runs, **and however you start it**", naming the Quash app, web console, and MCP as equivalent. This closes a gap the original draft left: a user could have read the execution definition as covering device type only, and assumed agent-driven runs were metered differently or not at all.
- **What each plan includes** — added to the Free bullet list, so it inherits up the ladder.
- **Integrations and Workflow** table — new row, ✓ across all tiers. It is the only row in that table not gated at Team, which is the correct and useful contrast.
- **Common questions** — new "Is the Quash MCP server available on my plan?" entry carrying both halves: free to connect, limits still apply.
- **Glossary** — the Execution entry now names how a run is started alongside where it runs.

Plus one edit outside the pricing page: `quash-mcp/overview.mdx` "Before you install" now says "A Quash account on any plan, including Free", linking to the pricing page. Someone evaluating MCP reads that page, not the pricing page.

## Deliberately not done

Per §5 of the brief, nothing on the pricing page asserts per-surface metering behaviour. The product spans three surfaces with different meters — platform already meters runs, while console and desktop were still on test minutes and migrating. The page stays surface-agnostic: it describes the published commercial model without claiming what any given surface displays in-product.

**Resolved 2026-08-01:** the user confirmed the surface metering gap is being closed within a day, so no migration note is needed. The surface-agnostic framing stands on its own merits and needs no follow-up.

## Open items to raise at handoff

Carried from §5 of the brief; none block this work, all are worth confirming before or shortly after publish:

1. Is test generation genuinely unmetered in console today? The old playground granted 3 free prompts per generation. The rewritten page asserts unmetered generation on every plan.
2. Is the 14-day trial expiry fully removed everywhere in-product? The page now states "no expiry".
3. Does any surface still bill overage? The page now states no overage on any plan.
4. SSO/RBAC at Enterprise — decided above, but the brief flags SSO's tier as genuinely uncertain.
5. The codebase/Figma ingestion rows, per the judgment-call note above.

## Verification

- `grep` for every string in "Strings that must not survive"; confirm only the sanctioned survivors remain.
- `grep -rn 'Team\|Enterprise'` across the pricing page for any adjacent currency figure — Solo must be the only priced tier.
- Confirm the out-of-scope files are untouched: `git diff --stat` should list exactly the five files in Scope.
- `mint dev` renders the pricing page without MDX errors; all tables well-formed; the `&#x20;`/`&lt;` escaping conventions in the existing files preserved.
- Internal links remain absolute root-relative per `README.md`.
