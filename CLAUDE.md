# CLAUDE.md — Showcase

Instructions for Claude sessions working in this repository.

## Project identity

**Showcase ("Spatial Proteomic Highlights")** — a **public** GitHub Pages site
that presents Standard BioTools IMC / spatial-proteomic image stories. It is a
hand-written Tailwind (CDN) landing page (`index.html`) linking to per-tissue
[Minerva](https://github.com/labsyspharm/minerva-story) narrative exports, one
per top-level folder.

## How to make the common change (add a story card)

1. New Minerva export → new top-level folder (e.g. `Melanoma/`).
2. Background image → `image_backgrounds/`.
3. Add one `<a>` card to the grid in `index.html` (copy an existing card; set
   `href` to the folder and the inline `background-image` to the new thumbnail).
   Commented-out `<a>` blocks for not-yet-published tissues already exist —
   uncomment rather than rewrite when bringing one online.

That's the whole job — there is **no build step**.

## Deploy behavior

- **Hosting:** GitHub Pages, **deploy-from-branch** (`main` / root). Static files
  served as-is.
- A push to `main` goes live in ~1 min. Verify on https://standardbio.github.io/Showcase/
- ⚠️ **Do NOT switch the Pages source to "GitHub Actions."** There is no build;
  changing it breaks deployment.

## Branching workflow

Work on **`draft`**; **`main` is publish-only** (pushing it deploys). Publish by
cherry-picking ready commits to `main`:

```bash
git checkout main && git pull
git cherry-pick <sha> [<sha> …]
git push origin main        # ← deploy step; confirm with the user first
git checkout draft
```

Start a session with `git pull` then `git checkout draft`.

**`CLAUDE.md` is `draft`-only — never publish it to `main`.** It's internal
working context, kept off the public repo. Keep `CLAUDE.md` edits in their own
commits (don't bundle with README/content) so they're never swept into a
cherry-pick. To publish the README by itself:

```bash
git checkout main && git pull
git checkout draft -- README.md
git commit -m "docs: publish README" && git push origin main
git checkout draft
```

## Commit conventions

- One logical change per commit; short imperative subject (≤72 chars).
- Co-author Claude when it helped:
  `Co-Authored-By: Claude Opus 4.8 (1M context) <noreply@anthropic.com>`

## Audience / release rules

**Public site.** Confirm every story and image is cleared for public release
before anything reaches `main`.

## Tone

Default to concise. This is content editing, not multi-step engineering. Skip
preambles and trailing summaries.
