---
name: update-github-info
description: Keep the GitHub Info page current with concise, sourced GitHub Blog and Changelog updates.
on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read

engine: copilot

tools:
  edit:
  web-fetch:

network:
  allowed:
    - github.blog
    - github.com

safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Keep the GitHub Info page useful, concise, and ready for Mona to review.

## Instructions

1. Read `notes/mona-notes.md` before making any changes.
2. Use web-fetch to read https://github.blog/latest/.
3. Use web-fetch to read https://github.blog/changelog/.
4. Identify recent updates that help developers learn GitHub faster. Prefer a small number of practical, high-signal items.
5. Update only `site/content/github-info.md` with concise summaries. Mention the source for every item, linking to the relevant GitHub Blog or GitHub Changelog page.
6. Preserve the existing structure, voice, and valid frontmatter of `site/content/github-info.md`.
7. Do not change any other file. Do not invent details, and do not include an item unless it is supported by one of the fetched sources.
8. When there is a meaningful update, request one draft pull request containing the change for Mona to review. Use a clear title and explain the selected sources in the pull request body.
9. When there is no meaningful update or no change is needed, make no file changes and use `noop` instead of opening a pull request.
