# Brutus' Book — GitHub Pages (canonical home)

The public page for Brutus' Book (daily sports picks, graded in public),
served by GitHub Pages at **https://hoffman517.github.io/brutus-book/**

## What this repo is

The **canonical public home** of Brutus' Book since 2026-10-14
(Scott approved the flip that day and distributes this link). It
began as a mirror of the page that lived as a Muse artifact
(https://muse.ai/s/brutus-s-book-gxa6nxejxq0naq); that page is now
frozen as a signpost after its 2026-10-14 farewell build. The
content is a byte-faithful port of the same build — same HTML, same
assets, no redesign. Publishing never depends on a manual approval
step, and the page's live-score fetches work from this origin.

Source of truth (edited by the daily picks build):
`~/workspace/ts-spaces/brutus-s-book/index.html` + `assets/`
on the project VM. Do not edit this repo's `index.html` by hand —
the next publish overwrites it.

## How publishing works

`~/workspace/sports-betting/scripts/pages_publish.sh`:

1. Syncs `index.html` + `assets/` from the source of truth into this repo.
2. Injects the commented-out analytics placeholder (below) into the
   Pages copy only — the artifact is untouched.
3. Hash-compares against the last published state; commits and pushes
   **only when content changed** (an unchanged page is a no-op).
4. Prints one receipt line:
   `pages_publish ts=… repo=hoffman517/brutus-book hash=… changed=yes|no commit=… url=…`

The hourly line-movement-snapshots job runs the script as a ride-along
step, so grading updates reach the page without any approval tap.

## Rollback / restore

Every publish is one commit. To roll back: `git revert <commit>` (or
reset to the previous publish commit) and push — Pages redeploys in a
minute or two. The full history of the page is this repo's git log.

## Analytics (view tracking) — Scott's one step

View tracking is **not active**. The published `index.html` carries a
commented placeholder near the end of `<head>`:

```
<!-- ANALYTICS PLACEHOLDER (inactive): GoatCounter view tracking. …
<script data-goatcounter="https://SITE_CODE.goatcounter.com/count" async src="//gc.zgo.at/count.js"></script>
-->
```

To activate: create the free account at https://www.goatcounter.com
(Scott's signup — it must be his account), note the site code, replace
`SITE_CODE` in that snippet inside
`~/workspace/ts-spaces/brutus-s-book/index.html`'s published copy via
`scripts/pages_publish.sh` (or ask Brutus to wire the real code into the
publish script), and uncomment. GoatCounter is cookie-free and collects
only page views + referrers.

## Notes

- The private backup repo `hoffman517/brutus-book-backup` is unrelated
  to this site; nothing here is backed up *to* it and it is never
  published from.
- No secrets live in this repo. The GitHub token used for pushes stays
  on the project VM and is never committed.
