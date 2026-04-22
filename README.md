# Want an AI Clone in the Cloud That Never Sleeps? $0 to Host.

**A Clone with a Brain, Hands, and a Heart.**

Private codebase. Public README.

**Author:** Rajan Gupta · [rajangupta.ai](https://rajangupta.ai)

---

## The idea

A clone that works like a person — not a chatbot, not a script.

Three parts:

- **🧠 Brain.** A library of ~1,200 markdown files as memory (sqlite-vec + FTS5 for hybrid semantic + full-text search). ~120 skills as reusable expertise. Auto-memory that learns preferences across every conversation.
- **✋ Hands.** Signal for chat. OAuth into Gmail, Google Calendar, Google Drive. GCP Compute Engine for the always-on remote body. The hands are how the brain reaches into the world.
- **❤️ Heart.** A SOUL file for values, voice, and behavioral rules. A HEARTBEAT that fires scheduled tasks via launchd — morning brief, weekly review, inbox triage — while I sleep. Together they're what makes the clone *me*, not a generic assistant, and keep it alive 24/7.

Claude Code is the voice that binds the three.

No framework. No managed database. No cloud-only SaaS.

---

## Hosting — $0/month

The always-on remote body runs on **one GCP Compute Engine `e2-micro` instances** under Google's Always Free tier.

- **secondinstance** — us-central1-b — redundancy + experiments

Everything else is local: macOS for compute, launchd for scheduling, sqlite for state, markdown for memory. No vector DB subscriptions, no observability SaaS, no managed anything.

**Infrastructure bill: $0/month.** The only recurring cost is the Claude API itself.

---

## What it does on a normal day

- Reads and replies to Signal messages from a whitelisted chat.
- Saves every session as a dated markdown file in the library.
- Searches the library by meaning, not just keywords.
- Runs a planning team of rival experts — assembled on the fly — for non-trivial decisions.
- Sends/reads Gmail. Creates calendar events. Writes to Drive.
- Deploys and monitors the GCP Compute Engine instances.
- Fires heartbeats on schedule — morning brief, weekly review, system health.
- Publishes to the blog. Builds audiobooks. Watches the trading system.

---

## Architecture

```
       Signal / CLI / heartbeats (launchd)
                    │
                    ▼
              Claude Code
                (voice)
        │          │          │
        ▼          ▼          ▼
      Brain      Hands       Heart
    (memory +  (Signal,     (SOUL +
     library + Gmail,      heartbeat
     skills)   Calendar,    tasks)
               Drive, GCP)
```

---

## Heartbeat — what it does on its own

A single config file (`HEARTBEAT.md`) defines scheduled tasks. A runner reads it every 30 minutes and fires what's due. The clone works while I sleep.

| Task | When | What it does |
|---|---|---|
| **wiki-reindex** | daily 03:00 | Incremental reindex of wiki + docs + memory into the sqlite-vec search database. |
| **daily-email-summary** | daily 04:00 | Pre-dawn inbox triage — I wake to zero surprises. |
| **user-md-sync** | daily 04:00 | Pulls tasks from the Google Sheet and updates `USER.md`. |
| **daily-brief** | daily 06:30 | Morning briefing emailed to me — top 3 tasks, portfolio status, health anchors. |
| **daily-system-status** | daily 07:00 | System health report — every daemon, service, integration. |
| **friendly-nudge** | every 30m | Random check-ins like a friend who cares. Max 4/day, 2h gap, 25% probability each run — based on profile, time of day, and current sprint. |

The config is plain markdown. Adding a new heartbeat is a 6-line edit.

---

## Top 10 skills

The brain has ~120 skills. These ten carry most of the weight:

| Skill | What it does |
|---|---|
| **planning-team** | Assembles rival-pair domain experts on the fly. Debates the decision. Produces a plan with dissent preserved. |
| **wiki** | Search, write, and lint the markdown library. Hybrid semantic + full-text. |
| **session-save** | Writes every session to the library as a dated markdown file with frontmatter, decisions, and next actions. |
| **memory** | Auto-memory across conversations. Learns preferences once, loads them every future session. |
| **decision-log** | Append-only log of every meaningful decision — rationale, alternatives rejected, expected outcome. |
| **research** | Deep research across web + library. Produces a structured brief, not a summary. |
| **debug-research** | GCP / infra troubleshooting. Walks crash loops, logs, service health, and fixes. |
| **gcp-deploy** | Deploy, monitor, and restart the always-on remote body on GCP. |
| **book-factory** | Long-form writing → structured audiobook with chapter metadata (Kokoro TTS). |
| **weekly-review** | Weekly reflection cadence — what shipped, what slipped, what to adjust. |

---

## Stack

Python (`uv`) · Markdown · sqlite-vec + FTS5 · Claude Code · launchd · GCP Compute Engine (free tier) · Kokoro TTS (local).

---

## Public pieces extracted from this

- [**rgstack/planning-team**](https://github.com/rgstack/planning-team) — rival-pair expert debate skill
- [**rgstack/wiki-mcp**](https://github.com/rgstack/wiki-mcp) — local semantic + full-text search MCP server over markdown
- [**rgstack/blogging**](https://github.com/rgstack/blogging) — rajangupta.ai source (Hugo)
  
---

## Code access

The clone's code is private to protect personal memory, credentials, and the SOUL file that makes it *me*. If you're evaluating me for a role, **contact me** and I'll grant 14-day read access.
