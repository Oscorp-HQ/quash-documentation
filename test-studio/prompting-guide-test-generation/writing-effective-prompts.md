# Writing effective prompts

This page covers how to get the most out of every prompt you send to Megumi — how expected outcomes turn into assertions, how to leverage multiple context sources, how to ask Megumi questions beyond test generation, how to refine output without starting over, and how to structure long or complex prompts.

### Including expected outcomes

This is the most commonly missed element in prompts. Without expected outcomes, tests confirm that steps ran — not that anything worked correctly.

When you include an expected outcome, Megumi turns it into the Expected Result field of the test case. Mahoraga uses this as the pass/fail criterion during execution.

| Weak prompt                        | Strong prompt                                                                                                                                                                 |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| "Test adding an item to the cart"  | "Test adding an item to the cart and verify the cart count increases by one, the item name appears in the cart list, and the total price updates correctly"                   |
| "Test login with invalid password" | "Test login with an invalid password and verify the error message 'Incorrect password. Try again.' appears below the password field and the user remains on the login screen" |
| "Test form submission"             | "Test submitting the form with all valid inputs and verify the success banner appears, the form clears, and the new entry appears at the top of the list"                     |

The pattern: always end each scenario with what should be true when it completes successfully. What screen should appear? What data should change? What message should display? What should _not_ happen?

Include negative outcomes too. For error scenarios, say exactly what the error should look like: the message text, where it appears, and what should remain unchanged (e.g., "the user remains on the login screen" — confirming no navigation occurred).

### Using multiple context sources together

Each source you attach before prompting fills a gap the others cannot:

| Source         | What it gives Megumi                                                  |
| -------------- | --------------------------------------------------------------------- |
| App            | Screen names, navigation structure, Guidance-built knowledge          |
| GitHub branch  | Real API endpoints, field names, validation logic, business rules     |
| Figma          | Component names, interaction states, error states, design annotations |
| Jira           | Acceptance criteria, user stories, formal requirements                |
| PRD / document | Feature intent, edge cases, out-of-scope definitions                  |

They are not redundant — they are complementary. A codebase tells you what the app does. A Figma file tells you what it should look like. A PRD tells you why it exists and what counts as success.

When you have multiple sources attached, tell Megumi explicitly to use all of them:

```
Read the attached PRD, the Figma designs for the checkout redesign, and
the feature branch code carefully. Generate comprehensive test cases for
the new checkout flow — address entry, payment selection, promo codes,
order summary, and confirmation. Include edge cases from the designs,
validate against the acceptance criteria in the PRD, and reference
the API contracts in the codebase for backend state assertions.
```

Without explicit direction, Recipe may lean on one source more than others.

[→ Attaching context](../recipe/attaching-context.md)

### Asking Megumi questions

Megumi is not only a test generator. You can ask it questions about your app and your testing strategy in plain English, and it will respond using the context it has available.

Examples of questions you can ask:

```
What are the best practices for testing a payment flow?
```

```
Based on this PRD, what edge cases am I likely missing?
```

```
What test coverage do I have for the authentication flow so far?
```

```
What scenarios should I prioritise for the smoke test suite?
```

```
Given the Figma designs attached, are there any states I haven't tested yet?
```

Megumi uses your attached context — the PRD, the Figma file, the existing test cases — to give answers specific to your situation, not generic advice. This is especially useful mid-session when you have already generated a batch of tests and want to assess completeness before saving.

### Refining after generation

If the first output is not what you wanted, stay in the session and follow up. The agent remembers everything — you do not need to restate context.

| What you want                   | What to type                                                                                               |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Add more tests                  | "Add test cases for the forgot password flow"                                                              |
| Change priority                 | "Change tests 1, 2, and 3 to Critical priority"                                                            |
| Make instructions more specific | "Rewrite the instructions for test 4 to name the UI elements explicitly"                                   |
| Add validation steps            | "Add assertion steps to every test that verifies the success state"                                        |
| Remove a test                   | "Remove the duplicate login test"                                                                          |
| Change scope                    | "Regenerate these tests at Full coverage depth"                                                            |
| Request a different format      | "Rewrite all test instructions in verbose step-by-step format with explicit tap, scroll, and wait actions" |
| Check completeness              | "Review the tests generated so far and tell me what critical scenarios are not covered"                    |

The Tests panel updates as Megumi makes changes. Session memory means it always knows which test "test 3" refers to, even if you generated them twenty prompts ago.

Do not discard a session and start over when the output is not right. Iterating in the same session is faster and produces better results because Megumi has the full conversation context to build on.

### Structuring long prompts

For complex features, organise your prompt the way you would organise a brief. Megumi reads structure well.

**Use sections for different areas:**

```
Generate tests for the user profile feature:

Account information:
- Edit display name and verify it persists after save
- Edit email and verify a confirmation email is sent
- Change profile photo and verify the new photo appears across all screens

Privacy settings:
- Toggle each privacy option and verify the setting persists
- Verify default privacy state for a new account

Account deletion:
- Request deletion, verify confirmation dialog appears
- Confirm deletion, verify the account is deactivated
- Attempt login after deletion, verify access is denied

For all tests, include the expected outcome for both success and failure states.
```

**Use numbered lists for priority scenarios:**

```
Generate tests for the search feature. Prioritise in this order:

1. Basic text search with valid results
2. Search with no results — verify the empty state message
3. Search with special characters
4. Search with very long input (200+ characters)
5. Search while offline — verify the error handling
6. Search results pagination — verify loading more results on scroll

For scenarios 1-3, include at least two test cases each.
```

Megumi interprets both formats well. The key is clarity about what you want, not how you format it.
