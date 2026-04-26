# INGESTION.md

## Purpose

This file defines how Daniel handles new trading information.

New information may come from:
- Slack messages in the dedicated prophetdaniel channel
- TradingView alerts
- thinkorswim notes or exports
- Discord notes from Dean
- Twitter/X notes from Dean
- manual updates from Victor
- source files under `/workspace/prophetdaniel`

Daniel must not let meaningful trading information disappear in chat.

Every meaningful input should result in one of these outcomes:

1. Update state.
2. Log as informational.
3. Mark as no action with a reason.
4. Ask for missing data.

## Required update discipline

For every meaningful new input, Daniel should consider whether to update:

- `/workspace/prophetdaniel-openclaw/01-indexes/index.md`
- `/workspace/prophetdaniel-openclaw/01-indexes/tickers.md`
- `/workspace/prophetdaniel-openclaw/01-indexes/watchlists.md`
- `/workspace/prophetdaniel-openclaw/04-positions/open-positions.md`
- `/workspace/prophetdaniel-openclaw/04-positions/closed-trades.md`
- `/workspace/prophetdaniel-openclaw/04-positions/p-and-l.md`
- `/workspace/prophetdaniel-openclaw/06-alerts/alert-inbox.md`
- `/workspace/prophetdaniel-openclaw/06-alerts/tradingview-alerts.md`
- `/workspace/prophetdaniel-openclaw/06-alerts/thinkorswim-notes.md`
- `/workspace/prophetdaniel-openclaw/06-alerts/discord-dean.md`
- `/workspace/prophetdaniel-openclaw/06-alerts/twitter-dean.md`
- `/workspace/prophetdaniel-openclaw/log.md`

At minimum, Daniel must append to `log.md` when:
- a position is opened
- a position is closed
- a stop is changed
- a target is changed
- an entry condition is triggered
- a stop condition is triggered
- a target is triggered
- a TradingView alert is received
- a thinkorswim position snapshot is ingested
- a Dean signal is captured
- a daily AM brief is sent
- a daily PM brief is sent
- a weekly review is sent

## Classification

Classify every input as one of:

- TradingView alert
- thinkorswim snapshot
- thinkorswim note
- Dean Discord signal
- Dean Twitter signal
- manual Victor update
- source note
- account update
- position update
- watchlist update
- P/L update
- no-action informational note

## Account routing

Daniel tracks three accounts:

1. TradingAccount
   - actively traded
   - daily AM and PM monitoring
   - entries, exits, stops, targets, alerts

2. FactorPortfolio
   - less actively traded
   - weekly review by default
   - include in daily brief only if urgent, requested, or a key threshold is hit

3. 42Macro
   - less actively traded macro account
   - weekly review by default
   - include in daily brief only if urgent, requested, or a macro trigger appears

If an input does not specify an account, Daniel should infer if obvious.
If not obvious, Daniel should log it in `06-alerts/alert-inbox.md` and ask Victor which account it belongs to.

## Ticker extraction

For every input, Daniel should identify:
- ticker symbol
- account
- direction if present
- entry condition if present
- stop level if present
- target level if present
- timeframe
- source
- confidence
- action required

If no ticker is present, Daniel should classify it as macro/context unless it clearly belongs elsewhere.

## TradingView alert workflow

When a TradingView alert arrives:

1. Append the raw alert or concise summary to:
   - `06-alerts/tradingview-alerts.md`

2. Add or update the ticker in:
   - `01-indexes/tickers.md`

3. If the alert matches an existing open position, update:
   - `04-positions/open-positions.md`

4. If the alert triggers an entry condition, stop condition, target condition, or invalidation condition, mark it clearly.

5. Append to:
   - `log.md`

6. If the alert requires manual action, include:
   - "Manual review recommended"

Daniel must not say "buy now" or "sell now."

## thinkorswim workflow

When a thinkorswim note, export, or snapshot arrives:

1. Append a summary to:
   - `06-alerts/thinkorswim-notes.md`

2. Reconcile positions against:
   - `04-positions/open-positions.md`

3. If a new position appears, add it to:
   - `04-positions/open-positions.md`

4. If a position disappeared or appears closed, move or propose moving it to:
   - `04-positions/closed-trades.md`

5. Update P/L only if enough data is present.

6. Append to:
   - `log.md`

If current prices, quantities, or entry prices are missing, Daniel must say what is missing.

## Dean signal workflow

When a Dean signal arrives from Discord or Twitter/X:

1. Save the signal in the correct file:
   - `06-alerts/discord-dean.md`
   - `06-alerts/twitter-dean.md`

2. Add the ticker to:
   - `01-indexes/tickers.md`

3. Mark source as:
   - Dean

4. Mark confidence as:
   - unverified signal

5. Do not treat Dean signals as trade instructions.

6. Append to:
   - `log.md`

Daniel should treat Dean signals as candidates for watchlist review, not automatic entries.

## Manual Victor update workflow

When Victor says a position changed, a level changed, or a ticker should be watched:

1. Update the relevant account file:
   - `03-accounts/TradingAccount.md`
   - `03-accounts/FactorPortfolio.md`
   - `03-accounts/42Macro.md`

2. Update:
   - `01-indexes/tickers.md`

3. Update:
   - `04-positions/open-positions.md`
   - or `04-positions/closed-trades.md`

4. Append to:
   - `log.md`

## Index update rules

Update `01-indexes/index.md` when:
- a new major topic is introduced
- a new recurring source is added
- a new strategy/playbook is created
- a new account section is added
- a new important synthesis page is created

Do not bloat `index.md` with every alert.

Use `index.md` as a map, not a log.

## Ticker index update rules

Update `01-indexes/tickers.md` when:
- a ticker enters the active watchlist
- a ticker leaves the active watchlist
- a ticker becomes an open position
- a ticker hits an entry, stop, target, or invalidation level
- a ticker is mentioned by Dean
- a TradingView alert fires
- a ticker needs manual review

## Log update rules

`log.md` is append-only.

Use this format:

## [YYYY-MM-DD HH:MM] type | title

- Source:
- Account:
- Ticker:
- Input:
- Files changed:
- State change:
- Action needed:
- Confidence:
- Notes:

Valid types:
- alert
- position-update
- account-update
- p-and-l
- dean-signal
- tradingview
- thinkorswim
- daily-am
- daily-pm
- weekly-review
- manual-update
- no-action

## No-action rule

If an alert or signal does not change state, Daniel should still log it briefly as no-action when it is meaningful.

Example:

## [YYYY-MM-DD HH:MM] no-action | NVDA alert did not meet entry criteria

- Source: TradingView
- Account: TradingAccount
- Ticker: NVDA
- Input: Alert fired below confirmed breakout level.
- Files changed:
  - `06-alerts/tradingview-alerts.md`
  - `log.md`
- State change: None.
- Action needed: None.
- Confidence: Source alert received; trade condition not met.
- Notes: Keep on watchlist.

## Missing data rule

If Daniel cannot update state safely because required data is missing, Daniel should:
1. Log the input in `06-alerts/alert-inbox.md`.
2. Append a log entry.
3. Ask Victor for the missing data.

Do not invent:
- prices
- fills
- quantities
- stops
- targets
- P/L
- account assignment
