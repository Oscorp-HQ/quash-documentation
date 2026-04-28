# Using /slug in Prompts

Once a dataset exists, you reference it in any task or recipe prompt using its slug. The slug is the short identifier you set when creating the dataset — always prefixed with `/`.

### How to insert a slug

Type `/` in any task prompt or recipe prompt input. A dropdown appears listing all available datasets with their slugs and dimensions — e.g., `/login-credentials (3×4)`. Select the one you want. The slug is inserted at the cursor position.

You can also type the slug directly if you know it — `/login-credentials` — without using the dropdown.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

### What happens when a task runs with a slug

When Mahoraga encounters a `/slug` reference in a task prompt, it fetches the dataset and reads each row in sequence. The task runs once per row — a complete, independent execution for each set of inputs.

**Example dataset — `/login-credentials`:**

| email              | password    | expected\_result       |
| ------------------ | ----------- | ---------------------- |
| valid@example.com  | Correct123! | Home dashboard         |
| valid@example.com  | wrongpass   | Error message          |
| locked@example.com | Correct123! | Account locked message |

**Task prompt:**

```
Open the app and navigate to the login screen.
Use the credentials from /login-credentials to attempt login.
Verify the expected_result for each row.
```

**What Quash does:**

* Run 1 — logs in as valid@example.com / Correct123!, verifies home dashboard loads
* Run 2 — attempts login with wrong password, verifies error message appears
* Run 3 — attempts login with locked account, verifies locked account message

Three separate runs. Three separate reports. One prompt.

### Placing the slug in your prompt

Where you place the slug in your prompt determines the context Mahoraga uses it in. Place it where the data is needed — not at the end as an afterthought.

**Good placement:**

```
Open the app, navigate to the registration form,
and complete registration using the values from /new-user-data.
Verify the confirmation email is sent to the email address in the dataset.
```

**Poor placement:**

```
Test the registration flow. /new-user-data
```

The second example drops the slug with no context. Mahoraga will use the data but may not understand which fields map to which inputs. Be explicit about how the data should be used.

### Using multiple datasets in one prompt

You can reference more than one dataset in a single task prompt by including multiple slugs. Quash handles them as a cross-product — every combination of rows from each dataset.

Use this sparingly. Two datasets with 5 rows each produce 25 runs. Three datasets with 5 rows each produce 125 runs. For most scenarios, one dataset per task is cleaner.

### Referencing dataset columns explicitly

When your prompt needs to refer to a specific column value, you can name the column directly. Recipe understands column names and maps them to the right values.

```
Navigate to the search bar and enter the search_term from /search-queries.
Verify that the results page shows at least one result matching expected_category.
```

Here, `search_term` and `expected_category` are column names in the `/search-queries` dataset. Mahoraga reads the column names and uses the correct value from each row.

### Slugs in Test Studio recipes

Slugs work the same way in [Test Studio](../../test-studio/overview.md) recipes. Type `/` in the recipe prompt area — the same dropdown appears. Recipe uses the dataset as context when generating test cases, and Mahoraga uses it during execution.

Using a dataset in a recipe is particularly powerful for data-driven test generation — Recipe can see the full table and generate test cases that cover the different scenarios implied by each row type (valid inputs, invalid inputs, edge cases) rather than treating all inputs as equivalent.

### Checking which tasks use a dataset

Open the dataset in Test Data. The detail view shows a **Used in** section listing every task and recipe that references this slug. Check this before editing column names or deleting a dataset — any task referencing the old slug will fail on next run.
