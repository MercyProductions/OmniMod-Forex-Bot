# Configuration reference

Generated from `new-bots/forex/.env.example`. Copy the template, never another person's `.env`. Template defaults are starting settings, not account/risk recommendations. Read its comments and source before changing a safety control.

| Variable | Template default | Role |
| --- | --- | --- |
| `DISCORD_TOKEN` | your own value; optional when its source is disabled | Private credential from your own account/application. |
| `DISCORD_CLIENT_ID` | your own value; optional when its source is disabled | Your own server/application/account identifier. |
| `DISCORD_GUILD_ID` | your own value; optional when its source is disabled | Your own server/application/account identifier. |
| `DISCORD_CHANNEL_ID` | your own value; optional when its source is disabled | Your own server/application/account identifier. |
| `DISCORD_DELIVERY_MODE` | bot | Runtime, data-source, cost, review or safety setting; see template comments. |
| `SCAN_TIMEOUT_MINUTES` | 20 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_SOURCE` | disabled | Runtime, data-source, cost, review or safety setting; see template comments. |
| `OANDA_ENV` | practice | Runtime, data-source, cost, review or safety setting; see template comments. |
| `OANDA_API_TOKEN` | your own value; optional when its source is disabled | Private credential from your own account/application. |
| `OANDA_ACCOUNT_ID` | your own value; optional when its source is disabled | Your own server/application/account identifier. |
| `FOREX_INSTRUMENTS` | EUR_USD,GBP_USD | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_DYNAMIC_DISCOVERY` | true | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MAX_SCAN_INSTRUMENTS` | 20 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_DIRECTORY_REFRESH_MS` | 3600000 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_PRIMARY_SIGNAL_MAP_JSON` | {} | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_PRIMARY_SIGNAL_MAX_AGE_MS` | 300000 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_GRANULARITIES` | M15,H1,H4,D | Runtime, data-source, cost, review or safety setting; see template comments. |
| `MAX_QUOTE_AGE_SECONDS` | 120 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_TARGET_ATR_MULTIPLE` | 1.5 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_CLOSED_SESSION_DATES` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_EARLY_CLOSES_ET_JSON` | {} | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_CATALYST_SOURCE` | manual | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FINNHUB_API_KEY` | your own value; optional when its source is disabled | Private credential from your own account/application. |
| `FOREX_CATALYST_CLEAR` | false | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_CATALYST_REVIEWED_AT` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_CATALYST_REVIEW_SOURCE` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_CATALYST_REVIEW_SUMMARY` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_ROUND_TRIP_FEES_PER_UNIT` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_SLIPPAGE_RESERVE_PER_UNIT` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MAX_SPREAD_PCT` | 0.03 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MAX_TRADE_RISK_PCT` | 0.25 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MAX_TOTAL_OPEN_RISK_PCT` | 1 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MAX_GROSS_EXPOSURE_PCT` | 200 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MAX_DAILY_LOSS_PCT` | 1 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `FOREX_MIN_REWARD_RISK` | 1.5 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `PAPER_ACCOUNT_EQUITY_USD` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `OMNIMOD_EMERGENCY_STOP` | true | Runtime, data-source, cost, review or safety setting; see template comments. |
| `OMNIMOD_LIVE_TRADING_ENABLED` | false | Runtime, data-source, cost, review or safety setting; see template comments. |
| `TRADING_RISK_STATE_PATH` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `SCAN_INTERVAL_MINUTES` | 15 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `DISCORD_ALERT_COOLDOWN_MINUTES` | 30 | Runtime, data-source, cost, review or safety setting; see template comments. |
| `DISCORD_WEBHOOK_USERNAME` | OmniMod Forex | Runtime, data-source, cost, review or safety setting; see template comments. |
| `DISCORD_WEBHOOK_AVATAR_URL` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `DISCORD_WEBHOOK_URL` | (empty; review before enabling) | Runtime, data-source, cost, review or safety setting; see template comments. |
| `PAPER_MONITOR_INTERVAL_SECONDS` | 0 | Runtime, data-source, cost, review or safety setting; see template comments. |
