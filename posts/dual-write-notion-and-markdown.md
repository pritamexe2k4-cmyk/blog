---
title: "Dual-write: Notion is the editor, markdown is the corpus"
slug: dual-write-notion-and-markdown
tags: ["pipeline", "systems"]
excerpt: "Durable notes get written twice. Notion for the human. .md for the retriever. Photos stay in Drive. Public posts take a third path."
featured: true
published: 2026-08-31
---

From 31 Aug 2026, durable notes are written in Notion **and** as `.md` so Production RAG can ingest them.

This is not a sync product. It is a rule.

## The three streams

| Stream | Where it lives | Public? |
|---|---|---|
| Journal, gym, SQL, quotes | Notion + `corpus/personal/YYYY-MM-DD-topic.md` (gitignored) | No |
| Figures and photos | Drive Knowledge Vault; caption only in markdown | No |
| Public engineering posts | This site + GitHub `blog/posts/*.md` | Yes |

If a note does not have a destination in that table, it is a scratch file. Scratch files do not get infrastructure.

## Why two copies

Notion is the editor I will actually open. Markdown is what `ingest.py` can hash, chunk, and embed. One format cannot do both jobs without pretending.

The drop path for personal files is local:

```
corpus/personal/YYYY-MM-DD-topic.md
```

Not GitHub. Journals do not belong on a public remote. The public samples for the RAG showcase live in `corpus/ops/` and are safe to clone.

## Public writing is a different pipeline

Logfile (this site) is the public blog. The canonical files are:

1. Draft in Desk on this site, or a row in the Notion **Blogs → Editorial** database.
2. Body is markdown with a slug, tags, excerpt.
3. Ship from Desk. The post is live here.
4. Dual-write the same `.md` to [`pritamexe2k4-cmyk/blog`](https://github.com/pritamexe2k4-cmyk/blog) under `posts/`.
5. Optional Drive drop in `Knowledge Vault / Blogs` if there is a figure.

Desk can also pull public markdown from GitHub and import Google Docs from that Drive folder. Notion stays the calendar, not the renderer.

## Failure mode I am watching

Over-building the pipeline instead of writing the next note. The dual-write is three folders and a naming convention. If I add a fourth tool before the next `corpus/ops` file exists, that is activity, not progress.
