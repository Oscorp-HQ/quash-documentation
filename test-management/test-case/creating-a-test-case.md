# Creating a Test Case

There are two ways to create test cases in Quash: manually using the **+ New Test Case** panel, or by generating them in Test Studio and saving them to the library. Manual creation gives you full control over every field. Test Studio is faster when you need to create many test cases at once.

### Manual creation

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>



1. Click **Test Cases** in the left navigation panel.
2. Click **+ New Test Case** in the top right. A panel slides in from the right with all fields empty.
3. Fill in the fields (see below).
4. Click **Create**.

The test case is saved to the library immediately and is available to add to suites.

### Fields

#### Name

The title of the test case. It appears in the library list, in suite views, and in execution reports. A good name makes it obvious what the test covers without having to open it.

**Good:** "Login with invalid password shows error message" **Poor:** "Login test"

The name should describe what is being tested and what the expected outcome is — specific enough that anyone on the team understands it at a glance.

#### Instruction

The prompt Mahoraga follows when this test case runs. Write it the same way you would write a task prompt — describe the steps in order, name UI elements explicitly, and be specific about what to tap, scroll, or navigate to.

**Good instruction:**

```
Open the app and navigate to the login screen.
Enter an invalid email address in the Email field.
Enter any password in the Password field.
Tap the Sign In button.
Verify an error message appears below the email field.
```

**Poor instruction:**

```
Try to log in with bad credentials and check the error.
```

The clearer the instruction, the more consistently Mahoraga executes it. Vague instructions lead to inconsistent results.

#### Expected Result

What the app should look like at the end of a successful run. This is your pass condition — the benchmark Mahoraga and anyone reviewing the report use to determine if the test passed.

Be explicit about the end state: what should be visible on screen, what should have changed, what the app should have done.

**Good:** "An error message reading 'Invalid email address' appears below the email field. The user remains on the login screen." **Poor:** "Error message shows."

### Details

#### Platform

Choose **Android**, **iOS**, or **Both**. Selecting Both means the instruction is written to work across platforms without needing separate versions. If the interaction differs significantly between platforms, create separate test cases.

#### Priority

| Priority     | When to use                                                                               |
| ------------ | ----------------------------------------------------------------------------------------- |
| **Critical** | Core functionality that blocks a release if broken — login, checkout, data loss scenarios |
| **High**     | Important features users rely on daily — search, notifications, profile editing           |
| **Medium**   | Features that matter but are not release blockers                                         |
| **Low**      | Edge cases, rarely used features, cosmetic issues                                         |

#### Type

| Type           | What it tests                                             |
| -------------- | --------------------------------------------------------- |
| **Functional** | A specific feature works as intended                      |
| **Smoke**      | A quick pass confirming core app functionality is working |
| **Regression** | Nothing previously working has broken                     |
| **E2E**        | A full user journey across multiple screens               |
| **Custom**     | Anything that does not fit the above                      |

#### Tags

Freeform labels for grouping and filtering. A test case can have as many tags as needed. Tags make it easy to build targeted suites and find related test cases quickly.

Common tagging approaches:

* By feature: `login`, `checkout`, `profile`, `search`
* By journey: `onboarding`, `purchase-flow`
* By test type: `happy-path`, `error-handling`, `edge-case`
* By release: `sprint-23`, `v2.1`

### Creating test cases from Test Studio

If you need to create many test cases at once, Test Studio is faster. Prompt Recipe with what you want to test, review the generated cases in the Tests panel, and save them to the library in bulk using **Save to Test Cases**.

[→ Saving Generated Tests](../../test-studio/saving-generated-tests.md)
