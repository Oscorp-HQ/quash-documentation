# Report Dashboard

Every task and suite you run on Quash generates an execution report automatically. As soon as a run finishes, the report is ready — no setup required. The Reports section is where all of these live, giving you a complete history of what was run, what happened, and how it went.

Click **Reports** in the left navigation panel to open it.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Report Dashboard

When you open Execution Reports, you will see a summary of all test activity at the top. The dashboard displays:

* **Total Runs** – The number of test runs executed.
* **Completed** – The number of runs that finished successfully or with results.
* **Failed** – The number of runs that encountered errors or did not pass.
* **Success Rate** – The percentage of passed runs against total runs.

This gives you a quick snapshot of overall test health before diving into individual reports.

### The Reports List

The main view lists all reports in reverse chronological order. Each entry shows the prompt that was run, the device it ran on, when it completed, and the final result. Suite runs carry a **SUITE** badge.

Every report has one of three outcomes:

* **Pass** — The task completed and all steps executed as expected.
* **Failed** — The task did not complete successfully.
* **Partial Success** — The task completed some steps but could not finish — usually because of something outside Quash's control, such as a CAPTCHA or a mandatory manual step.

Use the filters at the top to switch between Tasks, Suites, or All, and to filter by result. The search bar finds specific runs by prompt text.
