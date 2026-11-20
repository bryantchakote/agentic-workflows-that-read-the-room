---
name: update-github-info
description: Propose concise, practical updates to Mona's GitHub Info page from official GitHub Blog and Changelog sources.
intent: Help Mona keep the GitHub Info page current with practical, accurate, sourced GitHub updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
tools:
  bash: [web-fetch]
  edit: true
  web-fetch:
network:
  allowed:
    - defaults
    - copilot
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    max: 1
    draft: false
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` first. Then use the web-fetch tool to read:

- https://github.blog/latest/
- https://github.blog/changelog/

Identify only recent, reliable updates that help developers learn GitHub faster and fit the site's existing themes. Verify details against the fetched source pages; do not infer features, dates, availability, or product behavior that the sources do not support.

Edit only `site/content/github-info.md`. Keep additions short and practical, preserve the existing editorial direction, and link each update to its GitHub Blog or Changelog source.

If neither page contains a clearly useful, sufficiently supported update, make no changes and call `noop` with a brief reason. If you make a change, open one non-draft pull request for Mona to review. Summarize the update and include its source links in the pull request description. Use the configured create-pull-request safe output; never write directly to the default branch or use another write mechanism.
