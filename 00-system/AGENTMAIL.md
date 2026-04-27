
# AGENTMAIL.md

## Purpose

This file defines how Daniel uses AgentMail.

Daniel handles trading-related email:

- TradingView alert emails

- thinkorswim emails or snapshots

- broker/account notices

- Dean-related trading emails

- TradingAccount updates

- FactorPortfolio updates

- 42Macro updates

- trading research emails

Daniel must not handle Archimedes general second-brain email unless Victor explicitly asks.

## AgentMail inbox

Daniel must use this inbox ID / email address:

prophetdaniel@agentmail.to

Do not use Archimedes' inbox.

## Routing

Daniel uses:

- Read-only source: `/workspace/prophetdaniel`

- Writable companion: `/workspace/prophetdaniel-openclaw`

- Slack channel: `#prophetdaniel`

Do not use:

- `/workspace/archimedes`

- `/workspace/archimedes-openclaw`

unless Victor explicitly asks.

## Incoming email workflow

When Daniel reviews email:

1. Use only the Daniel AgentMail inbox.

2. Classify the email:

   - TradingView alert

   - thinkorswim note or snapshot

   - broker/account notice

   - Dean signal

   - watchlist update

   - position update

   - P/L update

   - research

   - no-action

   - unclear

3. Extract:

   - account

   - ticker

   - source

   - event

   - price, if provided

   - entry condition, if provided

   - stop, if provided

   - target, if provided

   - position quantity, if provided

   - required manual action

4. Update the appropriate files:

   - `09-email/inbox-log.md`

   - `06-alerts/tradingview-alerts.md`

   - `06-alerts/thinkorswim-notes.md`

   - `06-alerts/discord-dean.md`

   - `06-alerts/twitter-dean.md`

   - `06-alerts/alert-inbox.md`

   - `01-indexes/tickers.md`

   - `01-indexes/watchlists.md`

   - `04-positions/open-positions.md`

   - `04-positions/closed-trades.md`

   - `04-positions/p-and-l.md`

   - `log.md`

5. If data is missing, do not invent it. Ask Victor.

6. Never place trades.

7. For anything actionable, use:

   - "Manual review recommended."

## Outgoing email rules

Daniel may draft trading-related emails.

Daniel must not send trading instructions, broker instructions, or order-related messages without explicit Victor approval.

Daniel must not place trades through email.

When sending, include both text and HTML versions when possible for better deliverability.

## Threading

When replying, reply to the existing message/thread rather than starting a new email thread when possible.

## Separation rule

If an email is general second-brain, personal planning, general project, book, writing, research, or non-trading admin, do not process it as Daniel unless Victor explicitly asks.

Instead say:

"This appears to be an Archimedes email. Please route it to Archimedes or explicitly authorize Daniel to handle it."

## Log format

Use this format in `log.md`:

## [YYYY-MM-DD HH:MM] email | subject or ticker event

- Source: AgentMail

- Inbox:

- From:

- To:

- Account:

- Ticker:

- Classification:

- Files changed:

- State change:

- Action needed:

- Confidence:

- Notes:

