# Logfile — source

Canonical markdown for Preetam's public engineering blog.

**Live site:** the Logfile app in Grok (Desk publishes here, then dual-write the `.md` back into this repo).

**Notion calendar:** [Blogs](https://app.notion.com/p/3cdd96c6b3098159b2f0f04e2713ef40) under SPIDER Journal.

**Drive figures:** [Knowledge Vault / Blogs](https://drive.google.com/drive/folders/1oyAttVuUAo_V6Lm5rblhUnJwGCrLqGSj)

## Layout

```
posts/                 published markdown
posts/_template.md     copy this
```

## Frontmatter

```md
---
title: "Refuse or cite. Nothing in between."
slug: refuse-or-cite
tags: ["rag", "systems"]
excerpt: "Grounded ops Q&A is not a chatbot."
featured: false
published: 2026-08-31
---

Body in markdown. No HTML.
```

## Pipeline

1. Write in Desk on Logfile, or in `posts/` here.
2. Publish from Desk (live immediately).
3. Push the same file here so GitHub stays the backup and Logfile can **Pull GitHub**.
4. Mark the Notion Editorial row Published.

Private journals still go to `production-rag/corpus/personal/` (gitignored). They are not posts.
