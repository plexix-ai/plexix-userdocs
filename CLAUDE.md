# plexix-userdocs

User documentation for Alder (working product name), built and hosted on [Mintlify](https://mintlify.com). Alder lets law firms, accounting firms and other professional services firms govern the AI agents they use: policies, permissions, review and an audit trail in one console. The reader is someone at a firm who runs or uses Alder: a CIO, their IT and security team, or a reviewer. Plexix sells software and does not provide legal or accounting services; never write anything that implies otherwise.

The Plexix-wide rules in `~/src/plexix/CLAUDE.md` apply here too (PRs only, `bmersereau` account, no secrets, no client material).

## Before any Mintlify task

Run `mint instructions <topic>` (or `npx mint@latest instructions <topic>`). It prints current Mintlify guidance and wins over anything you remember. Topics: `write`, `write components`, `configure`, `configure navigation`, `configure settings`, `publish`, `troubleshoot`. Never guess a `mint` command or flag; run `mint <command> --help`.

## Layout

- `docs.json`: site config and navigation. Schema: https://mintlify.com/docs.json. A page that is not in `navigation` is still built and reachable by URL; `hidden: true` is not access control.
- `*.mdx`: pages, YAML frontmatter plus MDX. The file path is the URL (`guides/policies.mdx` is `/guides/policies`).
- `snippets/`: reusable content. Write a fact once and import it instead of copying it.
- `images/`, `logo/`, `favicon.svg`: static assets.
- `.mintignore`: files Mintlify must not publish (drafts, `CLAUDE.md`, `AGENTS.md`).
- Instructions for AI tools that read the published docs go in `markdown.instructions` in `docs.json`, not in a page. Instructions for the Mintlify agent go in `.mintlify/AGENTS.md`.

## Commands

Run from the folder that holds `docs.json`.

```sh
mint dev --no-open     # preview at http://localhost:3000 (run in the background, stop when done)
mint validate          # build check; fails on errors, prints warnings
mint broken-links      # internal link check
```

Before you say a change is done, `mint validate` and `mint broken-links` are clean and you have looked at the changed page in `mint dev`. Say what you checked.

## Content model (Diátaxis)

Every page is one of four types. Do not mix them on one page.

| Type | Reader's need | Shape |
|---|---|---|
| Tutorial | Learn by doing, first time | One path, numbered `<Steps>`, a working result at the end |
| How-to guide | Get one task done | Title starts with a verb ("Approve an agent request"), prerequisites, steps, result |
| Reference | Look up a fact | Tables and fields, structured like the product, no advice |
| Explanation | Understand why | Prose, concepts and trade-offs, no steps |

Link between types instead of mixing them: a how-to links to the explanation, it doesn't contain it.

## Pages

- Frontmatter on every page: `title` (sentence case, under 60 characters) and `description` (one sentence, under 160 characters, used for SEO and search). Add `sidebarTitle` only when the title is too long for the nav.
- Add every new page to `navigation` in `docs.json`. When you move or rename a page, add a `redirects` entry for the old path.
- Internal links are root-relative (`/guides/policies`), never absolute URLs.
- Headings: one idea each, sentence case, no skipped levels. The page `title` is the H1; start body headings at `##`.
- Images need alt text that says what the image shows. Screenshots come from the fictional demo data only.
- Use Mintlify components only where they help: `<Steps>` for procedures, `<Note>`/`<Warning>` for things the reader must not miss (sparingly), `<Tabs>` for real alternatives, `<CardGroup>` for landing pages. Check `mint instructions write components` for syntax.

## Writing style

Follows the Google developer documentation style guide and Microsoft Writing Style Guide where this file is silent.

- Second person ("you"), active voice, present tense. One idea per sentence.
- Lead with what the reader can do, then how.
- Sentence case for headings and UI labels you write. Bold for UI elements the reader clicks: select **Policies** > **New policy**. Code formatting for file names, commands, paths, values and field names.
- Name UI elements exactly as the product shows them.
- No em dashes, exclamation marks, emoji, "simply", "just", "easy", "vendor", "revolutionary", "cutting-edge" or "supercharge".
- Define a term the first time a page uses it, or link to where it is defined.

## Facts and accuracy

- Never invent a feature, setting, limit, field, error message or screenshot. If you can't confirm it from `plexix_engineering` (PRDs, ADRs) or `plexix-platform` (source), mark it `TBD` and tell Beau.
- Anything not shipped yet is written as "designed to", or left out. Do not document roadmap items as present-tense features.
- Code samples and commands must have been run, or be marked `Not verified`.
- Example data is fictional: firm, matter, client and person names are invented. Nothing from a real firm or its clients.
- Security, compliance or certification claims (SOC 2, ISO 27001, encryption, data residency) need a source in `plexix_isms` or `plexix-infra`. Without one, leave the claim out.

## Changes

- Branch from `origin/main`, open a PR, squash merge after checks pass. Commit, push or merge only when Beau asks.
- Mintlify deploys `main` to production on merge. Check the PR preview deployment before merging.
- Keep PRs to one topic. Search existing pages before adding one; update a page rather than duplicating it.
