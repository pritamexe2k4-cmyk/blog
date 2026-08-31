---
title: "Refuse or cite. Nothing in between."
slug: refuse-or-cite
tags: ["rag", "systems"]
excerpt: "Grounded ops Q&A is not a chatbot. If the files do not say it, the system refuses. That is the whole product."
featured: true
published: 2026-08-31
---

I am building a retrieval service that answers only from files. If the files do not say it, it returns `not_in_corpus`. That sentence is the spec. Everything else is implementation.

The repo is [production-rag](https://github.com/pritamexe2k4-cmyk/production-rag). Design is locked. Code is not shipped yet. This note is the public version of that README, written so I cannot quietly widen the scope.

## The problem, without decoration

People ask questions against a pile of markdown. The system must cite a file or refuse. No invented facts. No "based on general knowledge." No softening a miss into a maybe.

A demo that always answers is a demo of fluency, not of retrieval.

## Pipeline

```
.md / .pdf
  → ingest            load → split → embed
  → Chroma            persist ./chroma

POST /query {question}
  → LangGraph         retrieve → generate | refuse
  → JSON              {answer, sources[], refused}
  → SQLite            queries.db (question, refused, latency_ms)
```

Slots I will not skip:

| Slot | Choice |
|---|---|
| Source | `corpus/ops/` (public samples) and `corpus/personal/` (local, gitignored) |
| Split | ~1000 tokens, ~200 overlap |
| Store | Chroma persist |
| Graph | retrieve → (hits?) generate : refuse |
| API | FastAPI `POST /ingest`, `POST /query` |
| Eval | `eval.json` — in-corpus + must-refuse |

## Why refuse is a feature

Faithfulness is not fluency. A correct refuse on a question the files do not answer is a passing test. A fluent paragraph with no source is a failure.

The first eval set is twenty questions: twelve answerable from `corpus/ops`, eight that must refuse. I will not add agents until the refuse set passes.

Chunk size is the first knob. After the first `/query` log, I change it once and measure miss rate again. Not five knobs. One.

## Personal corpus stays off GitHub

Notion is the editor. From 31 Aug 2026, durable notes also exist as `.md` so this service can ingest them.

- Drop personal files in `corpus/personal/` (not committed).
- Photos stay in Drive; only the caption is markdown.
- Daily journal, SQL notes, quotes, gym one-liners → `.md` with a date in the filename.

Public blog posts are a different stream. They live in [`pritamexe2k4-cmyk/blog`](https://github.com/pritamexe2k4-cmyk/blog) and on this site. Journals never become blog posts by accident.

## Showcase bar

A stranger can clone, ingest `corpus/ops`, hit `/query`, and see a refusal on a question the files do not answer. If that path is not true, the project is not shippable.

Papers I am actually reading, in order: Lewis et al. 2020 (why retrieve), DPR, Self-RAG, CRAG, then the 2024 survey. I am not collecting a bibliography for its own sake. Each paper has to change a slot in the table above or it does not go in the log.
