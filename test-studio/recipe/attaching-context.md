# Attaching Context

The quality of the tests Recipe generates is directly proportional to the context it has before it starts. A prompt with no context produces generic steps that could describe any app. The same prompt backed by your Figma designs, your PRD, your GitHub branch, and your Jira ticket produces tests that reference your actual screens, your documented acceptance criteria, and your real API contracts.

Attaching context is the single highest-leverage thing you can do before sending your first prompt in a recipe.

### Two ways to attach context

Every recipe has two attachment controls at the bottom of the prompt area.

**The `+` button** — opens a dropdown for structured sources: your connected app, a GitHub repository branch, a Figma design, or a Jira issue. These are live connections — Recipe reads directly from the source.

**The paperclip icon (📎)** — opens a file picker for documents: PRDs, spec sheets, feature briefs, or any written requirements in `.pdf` or `.doc` format.

Both can be used simultaneously. A well-prepared recipe session typically has an app selected, a GitHub branch chosen, a Figma file linked, and a PRD attached — all before the first prompt is sent.

> **Attach before your first prompt.** Recipe uses the context that is present at the time of each prompt. Attaching a document after you have already sent a prompt means it was not available for that generation. Set everything up first, then prompt.

### Your app

Selecting your app gives Recipe visibility into your app's structure — the screens that exist, the navigation flows, and the UI patterns Mahoraga has learned through [Guidance](../../getting-started/core-concepts/guidance.md).

**How to attach:**

1. Click the **+** button at the bottom of the prompt area.
2. Open the dropdown. Your connected apps are listed at the top.
3. Select the app you are testing.

The selected app name appears as a tag in the prompt area. Recipe now knows which app this recipe is for and can draw on everything configured in Apps — including Guidance.

If no apps appear in the dropdown, add one first in Apps→[ +Add app](../../apps/adding-an-app.md)

### GitHub repository branch

Connecting a GitHub branch gives Recipe access to your codebase — real API endpoints, real data models, real field names, real validation logic. Tests generated with a branch connected reference what your code actually does, not what the UI implies it does.

**How to attach:**

1. Click the **+** button.
2. Select your connected repository from the dropdown.
3. Choose the branch that matches what you are currently testing.

**Always select the right branch.** A test generated from `feature/checkout-v2` reflects that branch's endpoints and business logic — which may differ significantly from `main` or a production branch. If you are testing a feature in active development, use the feature branch.

If no repositories appear, connect one first in Apps → [Knowledge](/broken/pages/lwIhutjx60iZesnLnEto). Indexing takes 4–5 minutes on first connection.

### Figma designs

Attaching a Figma file gives Recipe access to your screen designs — component names, interaction states, error states, empty states, and any annotations your designer has written about intended behaviour. This is context that neither a codebase nor a PRD captures as clearly.

When Recipe has your Figma designs, it generates tests that:

* Reference actual component and button names as labelled in the design
* Cover states the designer explicitly accounted for — loading, empty, error, disabled
* Include edge cases visible in annotations that would not appear in a text description
* Match the exact copy used for error messages and confirmation text

**How Figma works in Quash**

Figma integration uses Figma's desktop MCP server — the agent explores your design file directly through Figma's own tooling. This means Figma must be open on your computer with MCP enabled before you attach a design.

**Before attaching:**

* Open the Figma desktop app
* Ensure MCP is enabled in Figma (check Figma → Preferences → Enable MCP server)
* Have the file you want to attach open

**How to attach:**

1. Click the **+** button at the bottom of the prompt area.
2. Select **Add Figma design** from the dropdown.
3. In the modal that appears, paste your Figma file URL (e.g. `figma.com/design/...`).
4. Click **Add**.

**Link to a specific frame where possible.** A URL pointing to a specific screen or component gives Recipe focused, precise context rather than an entire project file.

**Use the final handoff version.** Early-stage or exploratory Figma files with placeholder content produce less accurate tests than final designs. If your file has both WIP and final frames, link directly to the completed screens.

### Jira issues, epics, and sprints

Attaching a Jira source gives Recipe the documented requirements for the feature — user stories, acceptance criteria, bug descriptions, epics, and sprint context. Tests generated with Jira attached align directly with what was formally specified.

**Jira must be connected first**

Before you can attach a Jira source to a recipe, your Jira workspace must be connected in the Integrations section. If Jira is not connected when you click **Add Jira issue**, Quash shows a "Jira Not Connected" screen and directs you to Integrations.

To connect Jira: go to your profile → **Integrations** → locate Jira → click **Connect**.

**How to attach:**

1. Click the **+** button at the bottom of the prompt area.
2. Select **Add Jira issue** from the dropdown.
3. Search for or paste the issue ID, epic, or sprint you want to attach.
4. Click to confirm.

**What you can attach:**

* **Issues** — individual feature tickets with user stories and acceptance criteria
* **Epics** — for broader feature coverage across multiple tickets
* **Sprints** — to give Recipe context about the full scope of current work

**What Recipe reads from Jira:**

* User story description and acceptance criteria
* Bug reproduction steps (useful for generating regression tests)
* Linked issues and epic context
* Labels, priority, and any notes on the ticket

**Attach the most specific source available.** A specific feature ticket (MYAPP-1204) produces more targeted tests than an entire epic. If your work spans multiple tickets, attach the one most directly relevant to the tests you are generating in this session.

### PRDs and specification documents

Attaching a document gives Recipe access to written requirements, feature specifications, product briefs, or any other documentation that describes what you are building and why.

**Supported formats:** `.pdf` and `.doc`

**How to attach:**

1. Click the **paperclip icon (📎)** next to the prompt input.
2. Select your file from the file picker.

The document is uploaded and processed. Recipe reads it as context for all subsequent prompts in this session.

**What Recipe reads from documents:**

* Feature descriptions and user journeys
* Acceptance criteria and success metrics
* Edge cases and out-of-scope statements
* Error handling requirements
* Any explicit test scenarios described in the doc

**Attach before your first prompt.** Documents are processed at attachment time. If you attach a PRD after sending your first prompt, it was not available for that generation — you will need to re-prompt explicitly referencing the document.

**Be selective.** A focused 10-page feature spec produces better tests than a 200-page product requirements document. If you have a large PRD, consider attaching only the relevant section or creating a focused summary document for test generation purposes.

### Using multiple sources together

The most effective recipe sessions combine all available sources. Each one fills a gap the others cannot.

| Source         | What it adds                                                          |
| -------------- | --------------------------------------------------------------------- |
| App            | Screen names, navigation structure, Guidance-built knowledge          |
| GitHub branch  | Real API endpoints, field names, validation logic, business rules     |
| Figma          | Component names, interaction states, error states, design annotations |
| Jira           | Acceptance criteria, user stories, formal requirements                |
| PRD / document | Feature intent, edge cases, out-of-scope definitions                  |

They are not redundant — they are complementary. A codebase tells you what the app does. A Figma file tells you what it should look like. A PRD tells you why it exists and what counts as success.

**Example — full context setup for a checkout feature:**

```
+ App:      MyApp (Android)
+ Branch:   feature/checkout-v2
+ Figma:    Checkout Redesign — Final handoff
+ Jira:     MYAPP-1204 — New checkout flow
📎 Document: Checkout v2 PRD.pdf
```

With this setup, Recipe has everything it needs to generate tests that are specific to your app, aligned with your codebase, grounded in your designs, and traceable to your requirements — without you having to describe any of it in the prompt.

### The difference context makes

Without context, Recipe generates tests like this:

```
1. Open the app
2. Navigate to the login screen
3. Enter email and password
4. Tap the login button
5. Verify the user is logged in
```

With app selected, GitHub branch connected, and Figma attached:

```
1. Launch the app on the home screen
2. Tap "Sign In" in the top-right corner of the navigation bar
3. Enter a valid email address in the "Email Address" field
4. Enter the correct password in the "Password" field
5. Tap the "Continue" button
6. Verify the app navigates to the "Home" tab
7. Verify the greeting banner displays "Welcome back, [first name]"
8. Verify the user avatar in the top-right matches the profile photo
```

Same intent. Completely different specificity. The second version is directly executable without any additional interpretation. That difference comes entirely from context.

### Context and the session token limit

Every source you attach contributes to the session's token count. Attaching a large PRD, a full GitHub repository, and a multi-page Figma file all at once will push the context window higher. Quash auto-compacts at the 200k token limit, but you can use `/compact` manually before that point to keep the session sharp.

[→ Token management & /compact](../token-management.md)
