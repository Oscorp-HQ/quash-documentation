# Creating Datasets

A dataset is a named table of input values. Each column is a type of input. Each row is one complete set of inputs for a single test run. You can create datasets manually by building the table directly in Quash, or import them from an existing file.

### Creating a dataset manually

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>



1. Click **Test Data** in the left navigation panel.
2. Click **+ New** in the top right. A blank dataset editor opens.
3. Click the title field at the top — it reads "Untitled Test Data" — and replace it with a descriptive name. Keep it specific: "Login credentials" or "Checkout promo codes" is better than "Dataset 1".
4. Check the **Slug** field just below the title. It is auto-generated from your title but you can edit it. Keep it short, lowercase, and hyphenated — e.g., `/login-credentials` or `/checkout-codes`. This is what you type in a prompt to reference this dataset.
5. Add an optional **Description** to note what the dataset is for or which tests use it. Useful for teammates who inherit your work.
6. Set up your columns. Click directly on **Column 1** and **Column 2** to rename them. Use the **+** button on the right edge of the header row to add more columns. Column names become the variable names Megumi and Mahoraga understand.
7. Fill in your rows. Each row is one complete set of inputs. Click a cell to edit it. Use **+ Add row** at the bottom to add more entries.
8. The dataset saves automatically. It appears in the library immediately with its name, slug, size, and a last-updated timestamp.

> The size indicator at the bottom left of the editor shows current dimensions — for example **3×5** for a three-column, five-row table.

### Naming columns well

Column names matter. They appear in your prompt context and help Mahoraga understand what each value represents.

| Good column names                        | Poor column names      |
| ---------------------------------------- | ---------------------- |
| `email`, `password`, `role`              | `col1`, `col2`, `col3` |
| `product_name`, `quantity`, `promo_code` | `a`, `b`, `c`          |
| `search_term`, `expected_result`         | `input`, `output`      |
| `username`, `account_type`               | `user`, `type`         |

Use underscores instead of spaces. Keep names lowercase. Make them self-explanatory — when you write a prompt referencing `/login-credentials`, both you and Recipe should immediately know what `email` and `password` mean.

### Editing an existing dataset

1. Click **Test Data** in the left navigation.
2. Click the dataset you want to update.
3. Edit cell values, rename column headers, add rows, remove rows, or add new columns directly in the editor.
4. Changes save automatically.

The updated data takes effect the next time any task or recipe referencing that slug runs. Existing reports are not retroactively updated — they reflect the data that was used at the time of the run.

### Deleting a dataset

Open the dataset and click the **⋯** menu in the top right. Select **Delete**. Confirm.

Deleting a dataset does not affect tasks or recipes that reference its slug — they will simply fail to find the dataset on the next run. Before deleting, search for the slug in your tasks and recipes and update or remove the reference.

### Dataset size limits

* Values are text only — no file uploads, no binary data
* Each cell supports up to 5,000 characters
* Maximum 200 rows per dataset
* Maximum 20 columns per dataset

For test scenarios requiring more than 200 rows, split into multiple datasets with descriptive slugs — `/login-credentials-valid`, `/login-credentials-invalid` — and reference them in separate tasks.
