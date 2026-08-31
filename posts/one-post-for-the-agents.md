---
title: "One POST for the agents"
slug: one-post-for-the-agents
tags: ["agents", "systems"]
excerpt: "Ingest an event, call tools, write structured results. The rest of the stack should hit one endpoint, not a mesh of chat windows."
featured: true
published: 2026-08-30
---

Multi-agent work dies when every agent is a conversation. I want a backend: ingest an event, call tools and APIs, write structured results. One POST the rest of the stack can hit.

The repo is [agentic-ops](https://github.com/pritamexe2k4-cmyk/agentic-ops). Status: created; implementation in progress. Stack is Python, FastAPI, LangGraph, Pydantic.

## Intended surface

```
POST /run
  payload in → graph → structured agent result out
```

That is the whole public API until something forces a second route. Logs, traces, and tool adapters live behind it.

## What this is not

It is not a chat UI. It is not a swarm of personas arguing in Slack. It is not an excuse to skip [production-rag](https://github.com/pritamexe2k4-cmyk/production-rag). Retrieval that cites or refuses is a separate service. Agents that call tools are a separate service. Wiring them later is a POST from one to the other, not a rewrite.

## Contract I will keep

- Input is a typed payload, not free text with hidden defaults.
- Output is a Pydantic model: status, artifacts, tool calls, error.
- Every tool has a timeout and a recorded result, including failure.
- The graph is small. Retrieve-or-act branches are explicit.

If a run cannot be replayed from the request body and the tool log, it is not an ops backend. It is a demo.

## Why one endpoint

The rest of my stack is boring on purpose: a resume in LaTeX, a journal in Notion, a RAG corpus as markdown. Those things should call `POST /run` the same way they would call any other internal API. If the agents need a special client, I overbuilt the interface.
