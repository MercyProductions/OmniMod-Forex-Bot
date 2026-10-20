# OmniMod Forex Bot

Discover account-supported FX pairs and test a defined intraday breakout using practice-market data. `npm start` launches **only Forex**. Automated tests establish code behavior; current provider coverage and forward performance require separate evidence.

## How it works

1. Discover eligible account-supported FX pairs in OANDA mode. Configured priority pairs do not describe the entire account universe.
2. Cheaply screen current quotes, spread, tradeability and currency metadata before capping expensive candle work.
3. Require an M15 range breakout aligned with H1 EMA20/EMA50, complete recent candles and fresh executable bid/ask.
4. Check the instrument session, scheduled-catalyst review, conversion to USD, explicit costs and shared currency/portfolio exposure.
5. Use ATR-based invalidation, a modeled 2R target and a session exit. Later practice quotes drive paper fills/marks/exits; no order endpoint is used.

Highlights are not the full universe and watches are not automatically approved entries. Model probability, heuristic strength and data quality have different meanings. Zero results can mean a closed session, disabled provider, missing evidence, pending model or risk rejection.

## Requirements and layout

Use Git, **Node.js 22.9+** (the export was checked with Node 24), npm and your own Discord app/server. The primary project is [`new-bots/forex/`](new-bots/forex/). The existing six-market source integration bundle is preserved because shared adapters/tests import sibling projects. Their presence does not start those bots. The root wrapper selects only this repository’s named application.

`repository.json` records the original export/source hashes. Later Git commits/tags are authoritative for subsequent changes. Dependencies remain locked in the existing project lockfiles.

## Install from a clean checkout

```sh
git clone https://github.com/MercyProductions/OmniMod-Forex-Bot.git
cd OmniMod-Forex-Bot
npm run bootstrap
npm run info
npm test
npm run check
```

Bootstrap installs locked dependencies with lifecycle scripts disabled. It does not create a provider subscription. Tests use isolated fixture/mocked inputs.

Copy the template on Windows PowerShell:

```powershell
Copy-Item new-bots/forex/.env.example new-bots/forex/.env
```

Or on Linux/macOS:

```sh
cp new-bots/forex/.env.example new-bots/forex/.env
```

Edit that **local** `.env`; never copy the maintainer’s tokens or publish your file. [Every shipped template setting is listed here](docs/CONFIGURATION.md), with sensitive values replaced by instructions to supply your own.

## Create your own Discord application

1. In the [Developer Portal](https://discord.com/developers/applications), create your own application and bot user. Choose its name/avatar.
2. Reset/copy its bot token into `DISCORD_TOKEN`; set the application ID as `DISCORD_CLIENT_ID`. They are different values. Each independently running bot needs its own application/token.
3. Enable Discord Developer Mode and copy your server ID to `DISCORD_GUILD_ID`. Configure DISCORD_CHANNEL_ID; never reuse the owner’s destination IDs.
4. Install it to your server with `bot` and `applications.commands` scopes. Allow View Channel, Send Messages, Embed Links and Read Message History in its channels. Setup that creates channels/roles needs the corresponding management permission.
5. Register commands and start this application:

```sh
npm run register
npm start
```

For this app, `npm --prefix new-bots/forex run setup` exposes its setup workflow after guild/channel configuration. Registration/startup connects to your own Discord application and can publish messages. A connected gateway does not establish feed readiness.

The identity skeleton is deliberately empty:

```dotenv
DISCORD_TOKEN=
DISCORD_CLIENT_ID=
DISCORD_GUILD_ID=
```

Add the project’s own destination/provider fields from its template. Do not share tokens in issues, screenshots or pull requests.

## Free data and paid upgrades

| Source | Role | Settings in local .env | Limits / prerequisites |
| --- | --- | --- | --- |
| OANDA v20 Practice | Practice-account data | FOREX_SOURCE=oanda-practice; OANDA_ENV=practice; OANDA_API_TOKEN; OANDA_ACCOUNT_ID | Use your own eligible practice account/API access. Region/division availability varies. |
| Finnhub calendar | Optional entitlement-based enrichment | FOREX_CATALYST_SOURCE=finnhub; FINNHUB_API_KEY | Missing calendar data fails closed. |
| Manual/disabled | Offline or paused research | FOREX_SOURCE=disabled; manual catalyst settings | Disabled is not a successful market scan. Reviews must be current and sourced. |
| Yahoo reference adapter | Permission-dependent observations | See primary documentation | No executable bid/ask; not a substitute for the practice feed. |

Review this mode skeleton; blank credentials intentionally do not authenticate:

```dotenv
FOREX_SOURCE=oanda-practice
OANDA_ENV=practice
OANDA_API_TOKEN=
OANDA_ACCOUNT_ID=
FOREX_DYNAMIC_DISCOVERY=true
OMNIMOD_EMERGENCY_STOP=true
OMNIMOD_LIVE_TRADING_ENABLED=false
```

The [configuration reference](docs/CONFIGURATION.md) lists all shipped variables. A key enables only the implemented adapters, not every endpoint sold by the provider. Read the primary project’s [existing technical guide](new-bots/forex/README.md) for deeper settings and market-specific workflows.

### Preview provider profiles

```sh
npm --prefix new-bots run data:setup -- --bot forex --profile free
npm --prefix new-bots run data:setup -- --list
```

Without `--apply`, this previews settings/missing prerequisites without editing `.env` or calling a provider. A free profile can be unsupported (Futures) or observation-only (limited/delayed feeds). Upgrade names differ by bot: inspect `--list` rather than assuming every market has a `paid` profile. Use `--apply` only after adding your own credentials and reviewing selectors. Equity, cost reserves, contract reviews and catalysts still require configuration.

## Paper accounts and shared risk

No live order route is implemented. Keep `OMNIMOD_LIVE_TRADING_ENABLED=false`. The emergency stop defaults to true. For paper reservations, deliberately configure positive paper equity, instrument-specific fees/slippage, current catalyst evidence and reviewed risk limits before setting `OMNIMOD_EMERGENCY_STOP=false`.

Stocks/Crypto use `OMNIMOD_PAPER_ACCOUNT_EQUITY_USD`; the other four bots use `PAPER_ACCOUNT_EQUITY_USD`. The first reservation anchors that ledger’s equity. A missing validated model, quote, review, cost assumption or account basis can block entries while discovery still operates.

For multiple clones on one computer, set the **same absolute `TRADING_RISK_STATE_PATH` and `OMNIMOD_SIGNAL_RESEARCH_PATH`** in every participating bot’s private configuration. Separate clones have separate default portfolios. Match equity/cost assumptions and keep marks current. File locks do not coordinate different hosts. Shared research never overrides the primary owner’s strategy/risk approval.

Watch, reservation, fill and target-hit counts have different meanings. Paper entry requires a later eligible quote. Stops/targets/excursions/returns are quote-sampled simulations after recorded costs, not calibrated broker fills. See [shared risk](new-bots/shared/paperRisk.js) and [fill checks](new-bots/shared/FILL_PORTFOLIO_RISK.md).

## Configure an account step by step

Create an eligible OANDA v20 practice account. In its account-management portal use Manage API Access to generate your personal token, and copy the practice account ID (not your login name). Keep `OANDA_ENV=practice`; supply the two matching fields, choose `FOREX_SOURCE=oanda-practice` and run the universe probe. The account instrument list is the coverage boundary. An optional calendar upgrade needs your own Finnhub key and the documented `paid-calendar` profile, plus calendar entitlement. Manual review remains available but must be recent, sourced and explicit.

## Operation and diagnostics

/forex help and /forex status; use the provider, last-scan and performance views listed by help.

Additional commands from this repository root:

```sh
npm --prefix new-bots/forex run probe:universe
npm --prefix new-bots/forex run scan
```

Probes/scans can contact the configured provider; metered history or explicit odds refresh may consume your credits. Review request/cost caps first. Do not start duplicate workers against one Discord identity/data store.

| Symptom | Check |
| --- | --- |
| No slash commands | Own token/client-ID pair, correct guild installation, registration and permissions. |
| Connected but zero candidates | Selected source, discovery/screen counts, session, current inputs and rejected-gate reasons. |
| HTTP 401/403 | Key validity, account region/permissions and endpoint entitlement; do not report it as no opportunities. |
| HTTP 429 | Quota headers, cooldown/concurrency and duplicate workers sharing the same provider account. |
| Watches without setups | Data age, model readiness, confirmation, catalyst evidence, explicit costs, emergency stop and risk limits. |
| Unexpected result summary | Separate research/shadow observations, issued alerts, delivery and actual paper fills. Consult durable records. |
| Stale records after restart | Actual data path/OS user, timezone, last successful request and old state; preserve the store when investigating. |

Runtime stores can contain private server settings and credentials saved by admin commands. Keep them outside Git/public web roots, persist them across restarts and back them up privately before upgrades. Original hosting documents may describe older deployments; source publication does not configure cPanel or start a production service.

## Baseline and contributing

The pre-change version is preserved as [`baseline/pre-readme-sports-audit-2026-10-20`](https://github.com/MercyProductions/OmniMod-Forex-Bot/tree/baseline/pre-readme-sports-audit-2026-10-20), commit `0dafd9223564a0574456d7c4e079529723c95e8b`. Inspect it without erasing later work:

```sh
git switch -c inspect-baseline baseline/pre-readme-sports-audit-2026-10-20
```

Fork, create a development branch and use your own local credentials. Add regression tests for confirmed defects. Freeze model/strategy versions, dates, horizons and costs before evaluating changes. Compare the same chronological out-of-sample game/trade populations, reporting proper scores/calibration, sample sizes, costs and unresolved outcomes. A few good days or more alerts do not establish improvement. Preserve source and private runtime evidence before model changes.

`npm test` runs this primary project’s tests. `npm run check` runs configured syntax checks. `npm run test:all` checks the full shared/new-market, Stocks and Crypto integration bundle. Submit the problem/change/checks/limits in your PR; share sanitized diagnostics rather than private state.

## Source map

- [Strategy](new-bots/forex/src/dayStrategy.js)
- [Runner/discovery](new-bots/forex/src/index.js)

## Provider documentation

- [Discord setup](https://docs.discord.com/developers/quick-start/getting-started)
- [Alpaca coverage](https://docs.alpaca.markets/us/docs/about-market-data-api)
- [CoinGecko Demo authentication](https://docs.coingecko.com/demo/reference/authentication)
- [OANDA API access](https://developer.oanda.com/rest-live-v20/introduction/)
- [Databento access](https://databento.com/docs/getting-started/build-first-app)
- [Tradier sandbox/data differences](https://docs.tradier.com/docs/market-data)
- [The Odds API v4](https://the-odds-api.com/liveapi/guides/v4/)

References checked on 2026-10-20. Confirm current region, licensing, quota and endpoint entitlement in your own account before enabling a paid selector. Each contributor needs their own provider account; this code does not redistribute the maintainer’s data subscriptions.
