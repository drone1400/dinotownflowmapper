# DinoTown Flowmapper

The whole tool is `index.html` (single file, no build), named that way so GitHub Pages serves it
at the site root. `README.md` is the user guide.

## Branches

- Work happens on `develop`. Commit changes there, not on `master`.
- `master` only gets release versions: when a version is ready, merge `develop` into `master`,
  with `APP_VERSION` in the HTML bumped and a matching entry in the README changelog.
- Changes that don't touch the tool (README, CLAUDE.md, hosting/CI files) can go to `master`
  without a version bump.

## Releasing

1. On `develop`: bump `APP_VERSION` in `index.html` and add a README changelog entry.
2. Merge `develop` into `master` and push `master`. GitHub Pages redeploys by itself.
3. Tag that `master` commit `v<APP_VERSION>` (e.g. `v3`) and push the tag.
   `.github/workflows/release.yml` checks that the tag is on `master` and matches
   `APP_VERSION`, then publishes a GitHub Release with `DinoTown_Flowmapper_v<N>.zip`
   (the tool renamed to `DinoTown_Flowmapper.html`, plus `README.md` and `LICENSE`).
4. If `index.html` changed, republish the Claude artifact (below).

## GitHub Pages

https://drone1400.github.io/dinotownflowmapper/ serves `master` from the repo root (Settings →
Pages → Deploy from a branch). It redeploys by itself on every push to `master`; no workflow
needed. `.nojekyll` turns off Jekyll so the files are served as they are.

## Claude artifact

https://claude.ai/artifact/RR5HYoB6kA8FT5PMNd6qi1 is a second hosted copy of the tool, linked
from the README. It does not update by itself and should always show the latest release.

Republish it only after a release has been committed to `master`, and only if `index.html`
changed in that release, using the `master` version of the file. Never publish from `develop`.

1. Artifact `read` the URL (needed before overwriting it in a new session).
2. Artifact `publish` with `file_path: index.html` (with `master` checked out) and `url` set to
   the link above. Leave out `icon` and `capabilities`: the page needs its existing `downloads`
   capability (`window.claude.use('downloads')`) for the zip and scene exports.
3. Check that the version badge in the header matches the released `APP_VERSION` and that
   "Download Source pack (.zip)" still downloads.

Only the artifact's owner can publish to it.
