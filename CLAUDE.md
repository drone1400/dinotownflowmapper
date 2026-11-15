# DinoTown Flowmapper

The whole tool is `DinoTown_Flowmapper.html` (single file, no build). `README.md` is the user guide.

## Branches

- Work happens on `develop`. Commit changes there, not on `master`.
- `master` only gets release versions: when a version is ready, merge `develop` into `master`,
  with `APP_VERSION` in the HTML bumped and a matching entry in the README changelog.

## Hosted copy

https://claude.ai/artifact/RR5HYoB6kA8FT5PMNd6qi1 is the web-hosted copy of the tool, linked
from the README. It does not update by itself and should always show the latest release.

Republish it only after a release has been committed to `master`, using the `master` version
of the file. Never publish from `develop`.

1. Artifact `read` the URL (needed before overwriting it in a new session).
2. Artifact `publish` with `file_path: DinoTown_Flowmapper.html` (with `master` checked out)
   and `url` set to the link above. Leave out `icon` and `capabilities`: the page needs its
   existing `downloads` capability (`window.claude.use('downloads')`) for the zip and scene
   exports.
3. Check that the version badge in the header matches the released `APP_VERSION` and that
   "Download Source pack (.zip)" still downloads.

Only the artifact's owner can publish to it.
