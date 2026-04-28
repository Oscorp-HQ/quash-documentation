# Recipe

A recipe is a Test Studio session. Each recipe holds a complete conversation with the Megumi agent — your prompts, the agent's responses, and every test case generated in that session. It is a persistent workspace for a specific feature or flow. Close it and come back a week later — everything is exactly where you left it.

### What a recipe contains

Every recipe stores:

* The full conversation history between you and the agent
* Every test case generated in the session, with names, priorities, and descriptions
* The configuration settings used (coverage depth, scope, platform)
* All attached context — documents, connected app, repository branch, Figma designs
* Session memory, so the agent knows what was discussed and can build on it

When you reopen a recipe, the agent loads everything. You can say "change test 3 to High priority" or "add a negative case to the login test" and it knows exactly what you mean.

### Creating a recipe

**Step 1.** Click **Test Studio** in the left navigation panel.

**Step 2.** Click **+ New** in the top right. A new recipe opens with the prompt input in the center.

**Step 3 (recommended).** Click **CONFIG** on the right edge and set your preferences before prompting — coverage depth, scope, platform, and priority levels. If you are unsure, leave the defaults. You can change them mid-session.

**Step 4 (recommended).** Click the **+** button at the bottom of the prompt area to attach context:

* Select your connected app from the dropdown
* Choose a GitHub repository branch
* Add a Figma design link
* Add a Jira issue

The more context you attach before the first prompt, the more specific and accurate the generated tests will be. Attaching a PRD or design doc before prompting makes a significant difference — tests grounded in your actual spec need far fewer corrections.

**Step 5 (optional).** Click the **paperclip icon** to attach a document — a PRD, spec sheet, or feature doc in `.pdf` or `.doc` format. Do this before sending your first prompt.

**Step 6.** Type what you want to test in the prompt input and press **Enter** or click **Send**.

**Step 7.** Quash responds in the conversation. If it needs clarification, it will ask — answer directly or pick a suggestion. Once it has enough context, it generates test cases and explains what it built.

**Step 8.** Click **TESTS** on the right edge to open the Tests panel. Review what was generated. Select the tests you want, then click **Save to Test Cases** or **+ Add to Suite**.

**Step 9.** Keep prompting in the same input to add more tests, adjust priorities, or refine what was generated. The agent holds the full session in memory.

### The recipe list

When you open Test Studio, you see all your saved recipes as a grid of cards. Each card shows:

* Recipe name
* Coverage depth setting used
* Number of test cases generated
* Last updated timestamp

Click any card to reopen it and continue where you left off.

### Naming recipes

A recipe name should make it obvious what feature or flow it covers without having to open it. Be specific.

| Good names                              | Poor names           |
| --------------------------------------- | -------------------- |
| "Login & Authentication — v2 release"   | "Login tests"        |
| "Checkout flow — promo code edge cases" | "Checkout"           |
| "Onboarding — Android Q3 sprint"        | "Onboarding tests 2" |
| "Profile photo upload & crop"           | "Profile"            |

### When to create a new recipe vs. continue an existing one

**Create a new recipe when:**

* You are testing a different feature or product area
* You are starting a new sprint or release cycle
* The scope has changed significantly (e.g., switching from smoke to comprehensive)
* The scenarios are unrelated to anything in existing recipes

**Continue an existing recipe when:**

* You are adding more tests to the same feature
* You are refining or adjusting previously generated tests
* You are building out edge cases for existing scenarios
* You are adjusting priorities or test details

The key signal: if removing one recipe's context would make the new tests meaningless, continue. If the new work stands completely on its own, create a new recipe.

### The Tests panel

Click **TESTS** on the right edge of the screen to open the Tests panel.

As the agent generates test cases, they appear here as individual cards. Each card shows:

* **Priority indicator** — colour-coded dot (red = Critical, orange = High, yellow = Medium, gray = Low)
* **Test name** — short, descriptive title
* **Description** — a brief explanation of what the test covers
* **Counter** — total number of test cases in the current session (e.g., "Tests (8)")

#### Selecting and saving tests

| Action                     | How                                          |
| -------------------------- | -------------------------------------------- |
| Select individual tests    | Click the checkbox on a card                 |
| Select all                 | Click **Select all** at the top of the panel |
| Save to Test Cases library | Select tests → click **Save to Test Cases**  |
| Add directly to a suite    | Select tests → click **+ Add to Suite**      |
| Deselect without saving    | Click **Clear**                              |

### Refining tests mid-session

You do not need to save and start over if the first output isn't right. Stay in the same recipe and keep prompting:

* `"Add a test for the forgot password flow"`
* `"Change the first three tests to Critical priority"`
* `"Add more validation steps to the checkout test"`
* `"Remove the duplicate login test"`
* `"Make the instructions more specific — name the UI elements"`

The agent updates the Tests panel as it makes changes. Session memory means it always knows what you are referring to.

### Organising recipes

* Use one recipe per feature area — do not mix unrelated features in a single session
* Archive old or completed recipes to keep the list clean
* Group recipes by feature, sprint, or release for easier navigation
* Share recipes with teammates — they can see the full conversation and generated tests
