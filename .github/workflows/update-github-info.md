---
name: update-github-info
description: Refresh the GitHub Info page with practical updates from official GitHub sources.
strict: true
model: gpt-5.4
engine:
  id: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
tools:
  edit: true
  web-fetch: {}
  github:
    mode: local
    toolsets: [repos]
    allowed:
      - get_file_contents
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Follow these instructions exactly:

1. Read `notes/mona-notes.md` and the current `site/content/github-info.md` using the GitHub repository API `get_file_contents` tool.
2. Use the GitHub Blog by web-fetching `https://github.blog/latest/`.
3. Use the GitHub Changelog by web-fetching `https://github.blog/changelog/`.
4. Use Awesome Copilot workflows by web-fetching `https://awesome-copilot.github.com/workflows/`.
5. Update `site/content/github-info.md` with the useful, supported findings.

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Select only recent, useful updates that fit Mona's editorial angle. Keep the writing short and practical, focus on helping developers learn GitHub faster, and cite the original GitHub Blog or GitHub Changelog URL for every update. Preserve the existing page structure and edit only `site/content/github-info.md`.

Use the configured `create-pull-request` safe output to open one ready-for-review pull request for Mona. Include a concise title and body that summarize the changes and link to the source articles. Do not write directly to the default branch. Call `noop` with a short reason when the sources contain no meaningful new information or there is insufficient evidence for a trustworthy update.
