# Supaboard documentation

This repository contains the Mintlify documentation for Supaboard. The site uses the Almond theme and is organized around user tasks.

## Preview and validate

Install the [Mintlify CLI](https://www.mintlify.com/docs/installation) if it is not already available:

```sh
npm install -g mint
```

From this directory:

```sh
mint dev
```

The preview runs at [localhost:3000](http://localhost:3000). Before submitting changes, run:

```sh
mint validate
mint broken-links
```

Check the affected pages in the browser at desktop and phone widths, in light and dark themes. Verify navigation, contents links, tables, code blocks, and any moved URLs. Build validation uses Mintlify's local preview cache and may need filesystem access outside this repository.

## Content layout

| Folder | Content |
| --- | --- |
| `getting-started/` | Quickstart and product concepts |
| `analyst/` | Questions, prompts, answers, chats, and Slack/Claude integrations |
| `projects/` | Organizing work in projects |
| `artifacts/` | Artifact library, reports, and presentations |
| `dashboards/` | Dashboards, widgets, filters, exploration, and embedding |
| `datasites/` | Datasites, custom domains, and variables |
| `sheets/` | Spreadsheet creation, imports, editing, analysis, and storage |
| `automations/` | Workflow automation and scheduled reporting |
| `data-sources/` | Data sources, connector setup, and network security |
| `query-bench/` | Query editing and SQL guidance |
| `agents/` | Agent configuration and MCP tools |
| `workspace/` | Workspace administration and white labeling |
| `release-notes/` | Release index and dated entries under `YYYY/MM-DD.mdx` |
| `maintenance/` | Source evidence for editors; not part of the documentation navigation |
| `snippets/`, `images/`, `icons/` | Shared content and assets |

`index.mdx` is the documentation homepage and the only root-level article. Feature entry pages use `overview.mdx`. Keep related guides under their feature folder and add them to the corresponding group in `docs.json`. The Documentation tab follows tasks; Release notes has its own navigation, newest first.

## Page conventions

- Use the exact app label when describing a control. Explain product terms in plain language.
- Start a new guide with its purpose and prerequisites, then steps, the expected result, and relevant next steps.
- Set a descriptive `title` and `description`. Use `sidebarTitle` when a shorter navigation label helps.
- The frontmatter title provides the page's H1. Start body sections at `##` and keep heading levels in order.
- Use the standard article layout so the table of contents is available. `mode: "wide"` is reserved for the homepage and release-note index.
- Use native Mintlify components. Keep tables and code scrollable within the article on small screens.
- Use root-relative links without `.mdx`, such as `/dashboards/overview#filters`. Import shared snippets from `/snippets/` and reference assets from their shared root folders.
- Keep historical release notes tied to what was available at the time. Correct unsupported claims or dates against production merge evidence, and retain existing URLs and heading IDs.

## Screenshots and how-to guides

Keep task walkthroughs beside their feature reference; dashboard walkthroughs live in `dashboards/how-to/`. Link from the overview and place them together in native navigation.

Store app screenshots in `images/guides/`. Use a descriptive filename, useful alt text, and a caption explaining the control or result. Capture a settled UI from an authorized example workspace. Do not include credentials or present unsaved drafts as completed work. Screenshots are examples, not authoritative current balances, network allow-lists, or plan pricing.

Document plan allowance as a percentage and extra credits as a dollar balance. Do not explain credit calculations.

## Release notes

`release-notes/overview.mdx` is a native Mintlify `Update` timeline. Dated articles contain the details; navigation groups them by year and month, newest first. A date is the end of a roundup's coverage period, which is stated on the article. It is not a claim that every change deployed that day.

Write for people using Supaboard: lead with what they can do or what now works better. Use **New**, **Improved**, and **Fixed** sections only when they contain changes. Put any required user action above those sections and flag it in the timeline. Keep summaries short and link to the current guide for instructions. Use a descriptive headline and a short date as `sidebarTitle`. Each timeline update has an explicit RSS title and description.

Before adding or correcting an entry:

1. Check the remote `production` head in both source repositories, then inspect their first-parent production merges and the changes introduced by each merge. Exclude changes that exist only on development or staging. Check both app and backend readiness for features that need both.
2. Review the source changes, not just PR titles. Announce user-visible behavior; leave out refactors, deployment plumbing, credentials, and unsupported speed or accuracy claims. Hidden or disabled features are not generally available.
3. Record the roundup window, production PR or merge links, supporting commits for each item, and the reviewed heads in `maintenance/release-notes-sources.json`. Keep these implementation references out of public release prose. The ledger's `introduced_by` field identifies the production merge that first contains a supporting commit.
4. Preserve dated article paths, redirects, and legacy heading IDs when rewriting. Older roundup cutoffs may fall after the last merge they cover; do not assign a feature to a roundup before its production merge.
5. Update the timeline and month navigation, run both Mintlify checks, and review the index and affected notes on desktop and phone widths. Check article links, native update filters, and any action-required notice.

Production merges establish source availability, not successful deployment or runtime acceptance. The current evidence covers April 1–October 12, 2026. The supplied backend history begins April 25, so earlier backend claims cannot be verified from it. The ledger records this limitation and the exact reviewed heads.

Editorial references: [Mintlify's five changelog principles](https://www.mintlify.com/blog/five-changelog-principles-from-best-developer-brands) and [how to write release notes](https://www.mintlify.com/library/how-to-write-release-notes).

## Moving pages safely

Moving an MDX file changes its public URL. In the same change:

1. Update `docs.json` navigation and every internal link to the canonical destination.
2. Add a permanent redirect in `docs.json` from the old public path directly to the new one. Avoid chains and loops.
3. Keep old heading IDs when rewriting sections. Use an explicit `<span id="old-heading" />` beside the replacement content when necessary. Redirect sources cannot match URL fragments.
4. Run both validation commands and visit the old URL, including any bookmarked fragment, in the local preview.

Retain legacy redirects so links from the app, search engines, and shared messages keep working. The current local preview responds with HTTP 307 even for redirects configured with `permanent: true`; confirm permanent status codes on a deployed preview before production rollout.

## Publishing

The repository is connected to Mintlify. Pushing to the deployment branch can publish changes automatically. Review the local preview and follow the repository's publishing workflow before pushing.
