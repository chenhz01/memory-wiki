# memory-wiki

**The file-layer wiki for your agent's markdown memory.** Your agent remembers in scattered `.md` files. Give those files an index, a search, and a health check — without a database, a server, or a single dependency.

Agent memory tools keep racing toward vector stores and hosted services. But most agents (and most people) keep memory where it already works: **plain markdown files**. memory-wiki is the missing file layer — it treats your memory folder like code: indexed, searchable, and linted.

> Inspired by the persistent-wiki pattern (see [nashsu/llm_wiki](https://github.com/nashsu/llm_wiki)); this is an independent, dependency-free implementation. Pairs with [skill-spec](https://github.com/chenhz01/skill-spec) — specs for your agent's skills, a wiki for its memory.

## What it does

| Command | Effect |
|---|---|
| `ingest` | Absorb markdown files as entries (auto-dated if undated, slugified, never overwrites without `--force`) |
| `index` | Rebuild `index.md` — one table: title, date, first line, linked |
| `query` | Keyword search across entries, ranked by hit count, with context lines |
| `lint` | Health check: orphans not in the index, missing dates, duplicate titles, overlong files, broken relative links |
| `log` | Append-only operation log (`log.md`) — what entered the wiki and when |

## Install (60 seconds)

Single file. Zero dependencies. No server, no database, no network calls — your memory never leaves your disk.

```bash
git clone https://github.com/chenhz01/memory-wiki.git
python memory-wiki/tools/memory_wiki.py ingest my-notes.md --wiki ./wiki
python memory-wiki/tools/memory_wiki.py query "pricing" --wiki ./wiki
python memory-wiki/tools/memory_wiki.py lint --wiki ./wiki
```

`lint` exits `1` on FAIL-level rot (orphans, duplicate titles) — wire it into CI or a periodic check.

## Why lint your memory

Memory rots quietly: an entry gets renamed and its link dies; two logs share a title and search becomes ambiguous; a daily log grows past 400 lines and stops being scannable. None of that crashes anything — which is exactly why nobody notices. `lint` makes the rot a named, visible state.

## Honest boundary

This is keyword ranking, not semantic search — it finds the words you wrote, not the ideas you meant. It is a file-layer tool: if you need embeddings, add them on top; this layer stays useful underneath.

## Authorship

Produced through human-AI collaboration: the tool was drafted by an AI coding agent and reviewed, edited, and approved by a human maintainer. Shipped only after its own acceptance run (ingest → index → query → lint, including a deliberately rotted fixture) behaved as specified.

## License

MIT — use it, fork it, wire it into your agent's routine. Attribution appreciated, not required.

<a href="https://github.com/chenhz01/memory-wiki">canary: CANARY-ZS-MW-20260916-9B4D77C2</a>
