# Quash Documentation

Source for the [Quash](https://quashbugs.com) docs site, built with [Mintlify](https://mintlify.com).

## Branches

| Branch | Purpose |
|--------|---------|
| `mintlify-port` | **The production branch.** Mintlify deploys from this branch. All PRs should target this branch. |
| `main` | Legacy GitBook content synced via the GitBook GitHub integration. **Not used by Mintlify.** Do not treat this as the primary branch. |

When creating a new branch for changes, always branch from `mintlify-port`.

## Repo structure

```
docs.json          # Mintlify site config (navigation, theme, icons, branding)
index.mdx          # Homepage / introduction
images/            # Static assets (screenshots, icons, videos)
getting-started/   # Quickstart, platform overview, core concepts, FAQs
devices/           # Physical devices, emulators, simulators, cloud
apps/              # App setup, Apps Manager, credentials
test-studio/       # Recipe, prompting guides, configuration, collaboration
test-management/   # Test cases library, test data / datasets
running-tests/     # Tasks, suites, backend validations
execution-reports/ # Report dashboard, reading and sharing reports
integrations/      # Slack, Jira, Notion
reference/         # Troubleshooting, glossary, help & support
administration/    # Pricing
```

## Configuration

All site configuration lives in `docs.json`:

- **Theme:** `maple`
- **Appearance:** dark mode only (`strict: true`)
- **Icons:** Lucide library, icons on all top-level sidebar groups
- **Font:** Inter
- **Colors:** primary `#FFD233`, dark background `#0B1316`

Navigation is defined under `navigation.tabs[0].groups`. Groups can have:
- `"root"` — makes the group heading clickable, linking to an index page
- `"icon"` — Lucide icon name shown in the sidebar
- `"tag"` — badge label (e.g. "NEW", "BETA")

## Writing pages

- Pages are `.mdx` files with YAML frontmatter (`title`, `description`, etc.)
- Mintlify generates H1 from `title:` in frontmatter — **never add a manual `# H1` in the body**
- Use `##` for main sections, `###` for subsections. Don't skip levels.
- Internal links must be **absolute root-relative paths** (e.g. `/devices/overview`). Do not use relative paths (`../`).
- Image filenames must not contain spaces or parentheses — use kebab-case.
- HTML tags must be valid JSX (e.g. `<br />` not `<br>`).
- YouTube videos are embedded with `<iframe>` using the `/embed/` URL format.

## Local preview

```bash
npm i -g mint
mint dev
```

## Useful frontmatter properties

```yaml
---
title: "Page Title"
description: "Brief description for SEO and subtitle."
sidebarTitle: "Sidebar Name"    # Different name in sidebar vs page heading
icon: "lucide-icon-name"        # Icon next to page in sidebar
tag: "NEW"                      # Badge label in sidebar
deprecated: true                # Marks page as deprecated
---
```
