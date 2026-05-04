# AGENTS.md

This repo is the OpenClaw research/design workspace. It is documentation-first unless a later explicit implementation lane is opened.

## Mission

Help turn OpenClaw usage into reusable understanding:

- runtime literacy
- capability and surface mapping
- governance and approval design
- traceability and safety observations
- bounded experiment packets
- paper / patent / method framing when evidence supports it

## Non-goals

Do not turn this repo into:

- the OpenClaw source fork
- a production automation service
- a daily planner
- the raw brainstorming home
- a credentials store
- a place for personal inbox or private customer data

## Repo Boundary

Connected repos:

- `planning-everything-track` owns priority, capacity, day notes, weekly plans, and project locators.
- `brainstorming-lab` owns raw idea development, critique, option shaping, and graduation packets.
- `second-brain-openclaw` owns OpenClaw research/design artifacts after the idea has a bounded test.

## Working Rules

1. Keep this repo docs-first until an explicit implementation decision exists.
   - Prefer Markdown notes, diagrams, tables, and small reproducible command logs.
   - Do not add a server, app, or automation loop just because the idea is interesting.

2. Use FIRST PRINCIPLE before implementation.
   - Name the scarce resource: safety, trust, time, evidence, money, or execution bandwidth.
   - Name the action surface: file, shell, network, browser, message, memory, schedule, or external API.
   - Name the approval boundary before any external side effect.

3. Every experiment needs a safe packet.
   - Purpose
   - Setup
   - Commands or steps
   - Expected traces
   - Risks and blocked actions
   - Result
   - Next decision

4. Do not touch real accounts first.
   - Use sandbox fixtures before Gmail, Slack, Telegram, billing, purchases, production files, or private research evidence.
   - Redact sensitive inputs before sending them to cloud models.
   - Keep live credentials out of tracked files.

5. Keep OpenClaw and Codex roles distinct.
   - Codex remains the mature coding/workspace execution engine.
   - OpenClaw may be studied as a runtime, router, channel surface, watcher, or approval relay.
   - Do not rebuild Codex's coding harness inside OpenClaw without a concrete reason.

6. Use a design gate before hardware or always-on setup.
   - A one-page minimum design must exist before buying hardware or opening an implementation sprint.
   - The design must specify entrypoint, redaction point, approval gate, action log, rollback path, and one sandbox task.

7. Keep planning updated only at decision points.
   - Update `planning-everything-track` when priority, capacity, status, or next action changes.
   - Do not mirror every note back into planning.

## Good Output

Good output in this repo produces one of:

- a clearer OpenClaw runtime map;
- a bounded design note;
- a safe experiment packet;
- a governance or approval rule;
- a research-ready observation with evidence;
- a clear reason to park or reject an implementation path.
