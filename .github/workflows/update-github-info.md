---
name: update-github-info
description: Refresh site/content/github-info.md from GitHub Blog and Changelog sources + Keep Mona's GitHub Info page current with recent GitHub Blog and Changelog stories, proposed via pull request for review
emoji: 📰
on:
  schedule:
    - cron: "0 8 * * *"
  workflow_dispatch:
permissions:
  contents: read
strict: true
network:
  allowed:
    - defaults
    - github.com
    - github.blog
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    title-prefix: "[update-github-info] "
    labels: [automation, content]
    draft: true
    allowed-files:
      - "site/content/github-info.md"
---

# Update GitHub Info

## Task

1. Read [notes/mona-notes.md](../../notes/mona-notes.md) for Mona's editorial
   guidance on tone, sourcing, and review process.
2. Fetch `https://github.blog/latest/` and `https://github.blog/changelog/` to
   find recent, notable GitHub Blog posts and Changelog entries.
3. Update `site/content/github-info.md` to reflect the most relevant recent
   stories, following Mona's notes:
   - Keep summaries short and practical.
   - Prefer updates that help developers learn GitHub faster.
   - Mention the source (GitHub Blog or GitHub Changelog) for each update.
   - Preserve the existing structure and sections of the file where it still
     makes sense; only edit what needs updating.
4. Open a pull request with the change so Mona can review it before it goes
   live.

## Safe Outputs

- Use `create-pull-request` to propose the updated `site/content/github-info.md`.
- If nothing in `site/content/github-info.md` needs to change after reviewing
  both sources, call `noop` with a short reason instead of opening a pull
  request.
