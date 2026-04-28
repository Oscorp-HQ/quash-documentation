# Using @slug in Prompts

Once a validation has a prompt action enabled, you can call it inline inside any task prompt by typing `@`. The validation runs at exactly the point in the sequence where you place it — not before, not after. Order matters.

### How to insert a validation

Type `@` in any task prompt input. A dropdown appears listing all validations that have prompt actions enabled, showing their slug and description. Select the one you want. The `@slug` is inserted at the cursor position.

You can also type the slug directly — `@verify-order-created` — without using the dropdown.

### How execution works

When Mahoraga reaches an `@slug` reference in a task prompt, it pauses UI interaction, triggers the validation, waits for the result, and then continues with the next instruction.

This means placement is everything. A `@slug` after a UI action verifies the state after that action. A `@slug` before an action verifies the state before it.

**Example — verifying an order was created after checkout:**

```
Open the app and log in using the Standard User credentials.
Add the first product to the cart.
Proceed to checkout and complete the purchase.
@verify-order-created
Verify the order confirmation screen shows the correct order number.
```

Here, `@verify-order-created` runs immediately after the purchase is completed — checking the backend state before the agent continues to verify the confirmation screen. If the backend check fails, Mahoraga notes it in the report and continues (unless the validation is marked as required, in which case the run stops).

### Prompt action vs. task settings

You have two ways to attach a validation to a task:

**`@slug` in the prompt** — the validation runs at that specific moment in the task sequence. Use when timing matters — you need to check state immediately after a specific action, not at the start or end of the run.

**Task Settings** — open a task, go to Settings, and add validations. Choose when they run: before execution (verify initial state), after execution (verify final state), or both. Use when you always want a validation to run for this task, regardless of where in the prompt flow it logically belongs.

Both methods can be used together. A task can have validations in settings (run at start and end) and `@slug` references mid-prompt (run at a specific step).

### Passing parameters to validations

If a validation is configured with parameters, pass values to them inline using `key=value` syntax after the slug.

```
@check-user-profile user_id=12345
@verify-order-status order_id=ORD-789012 expected_status=completed
```

Parameters let a single validation work across many different test scenarios without creating separate validations for each one.

### Reading validation results in reports

Every validation that runs during a task appears in the [Execution Report](../../execution-reports/report-dashboard.md) under Observations. The report shows:

* Which validation ran and when
* The full API request that was made
* The response received
* Which assertions passed or failed
* Any variables extracted

If a validation marked as **required** fails, the report shows it as a definitive test failure — even if the UI steps all completed successfully. A passing UI with a failing backend validation is a failing test.

If a validation marked as **optional** fails, it appears as a warning in Observations — noted for visibility but not counted as a run failure.

### Common patterns

**Verify state after creation:**

```
Fill in the registration form and submit.
@confirm-user-registered
Verify the welcome screen appears.
```

**Verify state was not changed:**

```
Navigate to the product detail page.
@check-inventory-count
Tap Back without adding to cart.
@check-inventory-count
Verify the inventory count is unchanged.
```

**Extract and use an ID:**

```
Complete the checkout flow.
@get-latest-order-id
Navigate to Order History and verify the order with id {{order_id}} is listed.
```

**Check before and after:**

```
@check-cart-empty
Add three items to the cart.
@verify-cart-count expected_count=3
Proceed to checkout.
```
