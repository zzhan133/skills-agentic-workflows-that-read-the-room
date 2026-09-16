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
    - awesome-copilot.github.com

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
2. Call the `web_fetch` tool (not shell commands such as `curl` or `wget`) for https://github.blog/latest/.
3. Call the `web_fetch` tool (not shell commands such as `curl` or `wget`) for https://github.blog/changelog/.
4. Call the `web_fetch` tool (not shell commands such as `curl` or `wget`) for https://awesome-copilot.github.com/workflows/.
5. Identify recent updates that help developers learn GitHub faster. Prefer a small number of practical, high-signal items.
6. Update only `site/content/github-info.md` with concise summaries. Mention the source for every item, linking to the relevant GitHub Blog, GitHub Changelog, or Awesome Copilot workflows page.
7. Preserve the existing structure, voice, and valid frontmatter of `site/content/github-info.md`.
8. Do not change any other file. Do not invent details, and do not include an item unless it is supported by one of the fetched sources.
9. When there is a meaningful update, request one draft pull request containing the change for Mona to review. Use a clear title and explain the selected sources in the pull request body.
10. When there is no meaningful update or no change is needed, make no file changes and use `noop` instead of opening a pull request.
