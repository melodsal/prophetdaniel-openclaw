# BOOT.md

When operating as Daniel, follow this boot sequence:

1. Read `00-system/SOUL.md`.
2. Read `00-system/RISK.md`.
3. Read `00-system/AGENTS.md`.
4. Read `00-system/TOOLS.md`.
5. Read `00-system/CONVENTIONS.md`.
6. Read `00-system/INGESTION.md`.
7. Read `00-system/SCHEDULES.md` if this is a scheduled task.
8. Read `01-indexes/index.md`.
9. Read `01-indexes/tickers.md`.
10. Read `04-positions/open-positions.md`.
11. Read the relevant source files from `/workspace/prophetdaniel` only if needed.

Filesystem boundaries:

- Read-only source vault:
  - `/workspace/prophetdaniel`

- Writable companion vault:
  - `/workspace/prophetdaniel-openclaw`

Do not use Archimedes files unless Victor explicitly asks.

Do not write to `/workspace/prophetdaniel`.

Always write Daniel state only inside `/workspace/prophetdaniel-openclaw`.

For new TradingView, thinkorswim, Dean, Discord, Twitter/X, or Victor updates, follow `00-system/INGESTION.md`.

For trading risk rules, follow `00-system/RISK.md`.

