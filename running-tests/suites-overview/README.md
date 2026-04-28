# Suites Overview

## Suite Overview

A test suite is a named collection of test cases that run together as a unit. Instead of running tests one at a time, suites let you execute everything related to a feature, a flow, or a release cycle in a single run — with unified results and one report covering everything.

**To access Suites:** Click **Suites** in the left navigation panel.

### Why suites exist

Individual test cases are useful. Suites are how they become a testing strategy.

A suite for your login flow runs every authentication scenario in one go — valid credentials, invalid password, empty fields, forgotten password, account locked. A suite for your release process runs your smoke tests across every critical flow before anything ships. A regression suite runs everything that has ever broken, automatically, on every PR.

Suites are also where execution becomes efficient. Run the same set of tests across multiple devices simultaneously. Get one report with a clear pass rate instead of ten separate reports to interpret.

### The suite list

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

When you open Suites, every suite in your workspace appears as a card. Each card shows:

* Suite name
* Number of test cases it contains
* Last run date and result
* Pass rate from the most recent run as a progress bar
* **NEW** badge if the suite has never been run

Use the search bar to find a specific suite by name. Click **+ New Suite** to create one.

### Inside a suite

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Clicking a suite opens the detail view, split into two panels.

**Left panel — test case list** Every test case in the suite listed with its name and priority level. Use **+ Test Case** at the bottom to add new ones directly, or **Import** to pull from your [Test Cases library](../../test-management/test-case/about-the-test-cases-library.md).

**Right panel — suite summary**

* Total test case count with priority breakdown (Critical, High, Medium, Low)
* Pass rate from the last run
* Last run date and total duration
* Test type breakdown (Functional, Smoke, Regression, E2E)
* Current execution mode

### Execution modes

Every suite runs in one of two modes. This is the most important configuration decision for a suite — it determines whether test cases share state or run independently.

#### Sequential

Test cases run in order. Each case starts from the state left by the previous one.

**Use when:** Your cases form a connected flow where order matters. The classic example: create account → log in → complete profile → make a purchase. Each step depends on the previous one succeeding.

**What happens if a case fails:** By default, the suite continues to the next case. You can configure the suite to stop on first failure if a blocking step should halt everything downstream.

#### Isolated

Each test case runs independently with no shared state. Cases can run in parallel across multiple connected devices simultaneously.

**Use when:** Your cases are self-contained and do not depend on each other. Independent feature tests — search, notifications, profile editing — are all good candidates.

**Advantage:** Because cases are independent, Quash can distribute them across multiple devices at once. A 20-case isolated suite running on 4 devices takes roughly the time of 5 sequential cases.

#### Which to choose

If removing one test case from the suite would break the others — use Sequential. If any single case would still make sense running on its own — use Isolated.

When in doubt, Isolated is safer. You can always switch later.

### Suite groups

Within a suite, you can organise test cases into named groups. Groups are visual organisers — they do not affect execution order or mode.

Use groups to cluster related cases inside a large suite:

```
Suite: "Full Checkout Flow"
  Group: "Cart management"
    - Add item to cart
    - Remove item from cart
    - Update quantity
  Group: "Promo codes"
    - Apply valid promo code
    - Apply expired promo code
    - Apply already-used code
  Group: "Payment"
    - Complete purchase with card
    - Decline invalid card
```

### Running a suite

1. Open the suite.
2. Click **Run All**.
3. Select the device or devices to run on.
4. Confirm. The run begins immediately.

For **Isolated** suites with multiple devices connected, Quash distributes test cases across all selected devices automatically. You do not need to assign cases to devices manually.

The run appears in **Reports** as soon as it starts. Results update in real time as each case completes.

### Task Preview Panel

Before running the full suite, you can preview individual test cases in isolation using the Task Preview Panel.

1. Open the suite.
2. Click the **play icon** on any test case card.
3. The Task Preview Panel opens on the right with the device view loaded for that specific case.

Use preview when:

* Debugging a single case before running the full suite
* Validating setup or navigation steps after editing a test
* Checking whether a recently modified test behaves as expected

Preview does not affect suite state. It is for inspection only — changes made during preview do not carry into the suite run.

### Suite reports

Every suite run generates a single [Execution Report ](../../execution-reports/report-dashboard.md)covering all cases in the run. The report shows:

* Overall pass rate and verdict
* Per-case breakdown — which passed, which failed, which returned Partial Success
* Executive Summary covering the run as a whole
* Individual step-by-step detail accessible for each case
* Device recordings for every case

For suites with failures, start with the per-case breakdown to identify which cases failed, then drill into the individual case reports for root cause.
