# Glossary

#### Agent

An AI-powered automation module that performs a specific role in the testing workflow. Quash has two agents: Megumi (test generation) and Mahoraga (test execution). They operate sequentially — Recipe produces the plan, Mahoraga carries it out.

[Megumi & Mahoraga](../getting-started/core-concepts/megumi-and-mahoraga.md)

#### APK

The Android application package file format. In Quash, you upload an APK to the Builds tab of your App to define which version of your application Mahoraga runs tests against.

[→ Builds](/broken/pages/yam3tMsYgsIZ4OsfFpQk)

#### **Apps Manager**&#x20;

The dashboard in Quash that displays all registered apps as cards. Used to switch between apps and access each app's Overview, Builds, and Knowledge configuration.\
[Apps Manager](../apps/apps-manager/)

#### Backend Validation

A configured API call that runs during a test to verify that backend state matches what you expect — not just what is visible on screen. Defined once in the Validations section, then referenced in task prompts using `@slug` syntax. Can be set to run before execution, after execution, or both.

[ Backend Validation](../running-tests/backend-validations/)

#### Builds

The tab inside an App where you upload APK versions of your application. Only one build is active at a time — the active build is what Mahoraga installs and tests against. Every uploaded build is stored in the history so you can switch between versions or compare test results across releases.

[→ Builds](/broken/pages/yam3tMsYgsIZ4OsfFpQk)

#### **Bundle ID**&#x20;

The equivalent unique identifier for an iOS application, in the same reverse domain format as a package name.

#### **Environment tag**&#x20;

A label applied to an uploaded build in the Builds tab to indicate its testing context. Options are dev, stage, prod, or custom. Used to identify what environment a test report was generated against.

#### Guidance

The knowledge the Recipe agent builds for itself through repeated testing. Not configured by you — accumulated automatically as Mahoraga runs tests on your app. Starts empty. Grows with every session. Stores screen maps, learned flows, UI patterns, permanent vs temporary states, and edge cases encountered in previous runs. Editable from **Apps → Knowledge tab**.

[→ Guidance](../getting-started/core-concepts/guidance.md)

#### Knowledge Tab

The tab inside an App that houses two things: the connected GitHub repository and the Guidance profile. Together these give Recipe the deepest possible understanding of how the app actually works — the codebase from GitHub, and the observed behaviour from Guidance.

[→ Knowledge](/broken/pages/lwIhutjx60iZesnLnEto)

#### Mahoraga

The execution agent. Runs on your Android device or emulator, interacts with the UI, executes test case instructions, captures screenshots, records the session, and reports results back to Quash. Installs automatically on connected devices. Uses Android's accessibility APIs to detect and interact with UI elements.

[Megumi & Mahoraga](../getting-started/core-concepts/megumi-and-mahoraga.md)

#### Memory

The system that manages context across all Quash sessions. Operates in three layers: Apps context (configured by you, workspace-wide), Recipe Memory (per-session conversation history), and Guidance (agent-built knowledge, per app). None of the three layers ever resets — they are cumulative.

[→ Memory](../getting-started/core-concepts/memory.md)

#### **Megumi**&#x20;

The test generation agent inside Test Studio. Takes context — your app, your GitHub branch, a Figma file, a PRD, a Jira ticket, or a plain English prompt — and generates structured, executable test cases. Purpose-built for QA test generation. Works conversationally inside a Recipe session — follow-up prompts build on the previous context within the same Recipe.&#x20;

[→ Megumi & Mahoraga](../getting-started/core-concepts/megumi-and-mahoraga.md)

#### Recipe

A test generation session inside Test Studio. Each Recipe is a named, persistent workspace where you prompt Megumi to generate test cases. Recipes retain their full conversation history and generated tests indefinitely — reopening a Recipe picks up exactly where you left off. → Test Studio

[→ Megumi & Mahoraga](../getting-started/core-concepts/megumi-and-mahoraga.md)

#### Recipe Memory

The second layer of Memory. Everything discussed and generated inside a specific Recipe session — prompts, responses, generated tests, and refinements. Persists indefinitely. Loads automatically when you reopen a recipe. Scoped to its own recipe — does not carry over to other sessions.

[→ Memory](../getting-started/core-concepts/memory.md)

#### **Rerun**&#x20;

A subsequent execution of a task that has already completed successfully at least once. On a rerun, Mahoraga follows the stored path from the previous successful run instead of reasoning through the flow from scratch, resulting in significantly faster execution.

[→ Rerun](../running-tests/task-overview/rerun.md)

#### Slug

A short reference identifier used to call a Dataset or Backend Validation inside a task prompt. Dataset slugs start with `/` (e.g., `/login-credentials`). Validation slugs start with `@` (e.g., `@get_products`). Typing `/` or `@` in a prompt input opens a dropdown of available items.

→ [Test Data](../test-management/test-data-overview/) · [Backend Validations](../running-tests/backend-validations/)

#### Suite

[See Test Suite.](../running-tests/suites-overview/)

#### **Stored path**&#x20;

A structured record of a completed task run — the screens navigated, decisions made, and actions taken. Mahoraga stores this after the first successful run and uses it to execute reruns faster. It is not a recording of coordinates or selectors; it is a description of the flow's intent and context at each step.

#### **Self-healing**

&#x20;The ability of Mahoraga to detect a mismatch between the current screen state and the stored path during a rerun, switch back into reasoning mode to resolve the deviation, continue the test, and update the stored path with the new information. This prevents minor UI changes from causing test failures.

#### @slug

The syntax for referencing a Backend Validation inside a task or recipe prompt. Typing `@` in the prompt input opens a dropdown of available validations. The validation runs at exactly the point in the prompt sequence where you place it.

[→ Backend Validations](../running-tests/backend-validations/)

#### /slug

The syntax for referencing a Test Data dataset inside a task or recipe prompt. Typing `/` in the prompt input opens a dropdown of available datasets with their slugs and sizes. The agent fetches the dataset and runs the task once per row.

[→ Test Data](../test-management/test-data-overview/)

#### Task

A single plain English instruction you give to Mahoraga for ad-hoc execution. The fastest way to test something without setting up a full suite. Run immediately on any connected device. Every task run generates an Execution Report.

[→ Tasks](../running-tests/task-overview/)

#### Test Case

The fundamental building block of testing in Quash. Defines a single test scenario with three core fields: a **Name** (what it tests), an **Instruction** (what Mahoraga should do), and an **Expected Result** (the pass condition). Stored in the Test Cases library and added to Suites for execution. Can be created manually, generated via Test Studio, or imported.

[→ Test Cases](../test-management/test-case/)

#### Test Cases Library

The central repository where all test cases in a workspace are stored. Every test case created manually or saved from Test Studio lives here. Searchable and filterable by source, priority, type, and tag. Test cases in the library can be added to any number of suites and reused across projects and sprints.

[→ About the Library](../test-management/test-case/about-the-test-cases-library.md)

#### Test Data

A section in Quash (and a tab within each App) where structured datasets are stored and managed. Datasets are tables of input values — credentials, form data, product details — referenced in task prompts via `/slug`. When a task references a dataset with multiple rows, Quash runs the task once per row automatically.

[Test Data Overview](../test-management/test-data-overview/)

#### Test Scope

A CONFIG panel setting that determines the type of tests Recipe generates. **Feature** targets one piece of functionality in isolation. **Flow** traces a user through a multi-step journey. **Integration** validates how different parts of the app work together.

[→ Configuration](../test-studio/configuration-in-test-studio.md)

#### Test Studio

The AI-powered test generation section in Quash. Where you work with the Recipe agent to generate test cases from plain English, attached documents, Figma designs, GitHub branches, and Jira tickets. Organised into sessions called Recipes. Accessible from the left navigation panel.

[→ What is Test Studio?](../test-studio/overview.md)

#### Test Suite

A named collection of test cases grouped to run as a unit. Two execution modes: Sequential (cases share state, run in order) and Isolated (cases are independent, can run in parallel). Every suite run generates an Execution Report.

[→ Suites](../running-tests/suites-overview/)

#### Tests Panel

The right-side panel in Test Studio, opened by clicking **TESTS** on the screen edge. Shows all test cases generated in the current session as cards with priority indicators, names, and descriptions. From here you select tests and either save them to the Test Cases library or add them directly to a Suite.

[→ Recipes](../test-studio/recipe/)

#### Tokens

The unit of measurement for how much context the Recipe agent is actively processing in a session. Every prompt, response, attached document, and generated test case consumes tokens. Quash retains only what is actively needed. In long sessions, use the `/compact` command to compress conversation history and free up token budget.

[→ Tokens & /compact](../getting-started/core-concepts/tokens-and-compact.md)

#### Type (Test Case)

A classification field on every Test Case describing what kind of test it is. Options: **Functional** (a specific feature works as intended), **Smoke** (core app is working), **Regression** (nothing previously working has broken), **E2E** (full user journey across multiple screens), **Custom** (anything that doesn't fit the above).

[→ Test Cases](../test-management/test-case/)

#### **UDID**

Unique Device Identifier. A 25-character string that uniquely identifies an Apple device. Required when registering an iPhone with an Apple Developer account for testing.

#### Validations

In Test Studio: a CONFIG panel setting that adds assertion steps to generated tests — verifying the expected outcome occurred, not just that the steps ran. Three types: Visual (what is on screen), Functional (did the feature behave correctly), Data (are the values correct).

In Backend Validations: a separately configured API call that verifies backend state during a test run.

→ [Configuration](../test-studio/configuration-in-test-studio.md) · [Backend Validations](../running-tests/backend-validations/)

#### Workspace

The top-level organisational unit in Quash, shared by a team. Contains all apps, devices, test cases, suites, reports, and settings. Every team member with access to the workspace can see and contribute to shared resources — recipes, test case libraries, credentials, and reports.

[→ Platform Overview](../getting-started/platform-overview.md)

#### **WDA (WebDriverAgent)**&#x20;

A framework used by Quash to communicate with and control a physical iPhone during test execution. Installed automatically on connection. A WDA install error indicates the framework could not be deployed to the device, usually due to a missing iOS component in Xcode or incorrect team access.

### /compact

A command typed directly into the Recipe prompt input that compresses the full conversation history into a condensed form. Preserves essential context — what was tested, what tests were generated, what decisions were made — while freeing up significant token budget so a long session can continue without losing context.

[→ Tokens & /compact](../getting-started/core-concepts/tokens-and-compact.md)

###
