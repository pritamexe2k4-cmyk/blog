---
title: "How this blog ships"
slug: how-logfile-ships
tags: ["pipeline"]
excerpt: "Desk in the app, markdown on GitHub, Editorial in Notion, figures in Drive. One pipeline. No fourth CMS."
featured: false
published: 2026-08-31
---

Logfile is the public blog. This post is the operator manual.

## Write

Open **Desk** (signed in). Title, slug, tags, excerpt, markdown body. Preview is the right column. Save a draft as many times as needed. Drafts are yours; they are not public.

You can also start from:

- GitHub `posts/*.md` with YAML frontmatter (canonical backup)
- A Google Doc in Drive `Knowledge Vault / Blogs`
- A row in Notion **Blogs → Editorial** with Status = Draft

## Ship

In Desk, hit **Publish**. The post is live at `/writing/<slug>`. Status in Editorial should move to Published. Copy the generated markdown into [`pritamexe2k4-cmyk/blog`](https://github.com/pritamexe2k4-cmyk/blog) under `posts/` — or hit **Pull GitHub** after you push, if you wrote in the repo first.

Frontmatter shape:

```md
---
title: Refuse or cite. Nothing in between.
slug: refuse-or-cite
tags: [rag, systems]
excerpt: Grounded ops Q&A is not a chatbot.
featured: false
published: 2026-08-31
---

Body in markdown. No HTML.
```

## Pull

Desk has two importers:

- **GitHub** — reads the public `blog` repo. Safe for anyone; it only upserts markdown that already has a slug.
- **Drive** — lists `Knowledge Vault / Blogs` via your connected Google account. Continue with Grok if the gate asks. Docs import as drafts, not live posts.

Notion is the calendar, not an importer. Keep the Editorial database in sync by hand or from Desk notes. Daily Journal stays private.

## What does not ship

- Gym lines, quotes, SQL drills, unless they are a real engineering note
- Anything that belongs in `corpus/personal/`
- Screenshots without a caption
- Posts that cannot point at a file or a repo

## RSS

`/feed.xml` is the feed. That is the only syndication for now.
