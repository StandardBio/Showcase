# Showcase — Spatial Proteomic Highlights

A public landing page that showcases Standard BioTools **Imaging Mass Cytometry
(IMC) / spatial proteomic** image stories. Each card links to a self-contained
[Minerva](https://github.com/labsyspharm/minerva-story) narrative export for a
tissue/disease example (HER2 breast adenocarcinoma, clear cell RCC,
glioblastoma, mouse embryo, …).

**Live site:** https://standardbio.github.io/Showcase/

## How it works

- `index.html` is a hand-written **Tailwind** (CDN) page — no build step. It
  renders a responsive grid of cards; each card is an `<a>` linking to a
  per-story folder and styled with a background image.
- Each story lives in its own top-level folder (e.g. `HER2/`, `ccRCC/`,
  `Glioblastoma/`) containing a Minerva export (its own `index.html` + assets).
- Card background images live in `image_backgrounds/`.

```
Showcase/
├── index.html              landing page (Tailwind CDN, the card grid)
├── image_backgrounds/      card background thumbnails
├── HER2/  ccRCC/  Glioblastoma/  MouseEmbryo/  …   per-story Minerva exports
├── *.png, site.webmanifest favicons / PWA manifest
└── .gitignore
```

## Add a new story

1. Drop the Minerva export into a new top-level folder (e.g. `Melanoma/`).
2. Add its background image to `image_backgrounds/`.
3. Add one `<a>` card to the grid in `index.html` (copy an existing card; point
   `href` at the folder and `background-image` at the new thumbnail).
4. Commit to `draft`; publish via cherry-pick to `main` (see below).

## Branching workflow

Work happens on the **`draft`** branch. **`main` is the published branch** —
GitHub Pages serves it directly (deploy-from-branch, `main` / root), so pushing
to `main` is the deploy step and only happens by deliberate cherry-pick.

```bash
git checkout draft                      # do all work here; pushing draft does NOT deploy
# … edit, commit, push to draft …

git checkout main && git pull           # publish:
git cherry-pick <sha> [<sha> …]         #   pick the ready commits
git push origin main                    #   ← this goes live
git checkout draft                      # back to work
```

New laptop / new session: `git pull` then `git checkout draft`.

> **`CLAUDE.md` is never published.** It lives only on `draft` as internal
> working context, kept off the public repo. Cherry-picks to `main` carry the
> README and site content — never `CLAUDE.md`.

> **Pages source:** deploy-from-branch (`main` / root). **Do not** switch it to
> "GitHub Actions" — there is no build, and the static files are served as-is.

## Local preview

No tooling needed — open `index.html` in a browser. (Per-story Minerva folders
also open directly.)

## Audience

This site is **public**. Confirm every story and image is cleared for public
release before publishing to `main`.
