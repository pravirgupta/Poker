# Poker Calculator

A lightweight, single-file web app for tracking buy-ins, cash-outs, and lifetime P&L for a recurring poker game with friends. No server, no build step, no dependencies — just open `index.html` in any modern browser.

## Features

- **Track buy-ins per player** — Set a buy-in amount and increment each player's buy-in count with `+`/`−` buttons. A player can buy in any number of times within a single game.
- **Cash paid upfront** — Each player has a "Cash Paid" field for money they've handed over during the game. The settlement math accounts for this, so a player who buys in for $20, pays $20 cash, and cashes out $0 owes nothing at the end.
- **Live totals** — Each row shows two numbers: **Settle** (what they still owe or are owed right now) and **P&L** (game profit/loss). The summary bar tracks total bought in, cash paid, cashed out, and pot balance.
- **Reconciliation check** — A warning appears when total cash-outs don't match total buy-ins, so you can catch errors before saving.
- **Game history** — Every saved game records date, buy-in amount, and per-player buy-ins, cash paid, cash out, settlement, and P&L.
- **Lifetime stats** — Cumulative standings across all games: games played, total in, cash paid, total out, current unsettled balance, and net P&L per person.
- **Local persistence** — All data is saved to `localStorage`, so it survives page reloads. Nothing leaves your browser.

## Usage

1. Open `index.html` in any modern browser (Chrome, Safari, Firefox, etc.).
2. **Current Game tab**:
   - Set the buy-in amount (e.g., `$20`).
   - Add each player by name.
   - Use `+` / `−` to track how many times each player buys in during the game.
   - Enter any cash a player hands over during the game in the **Cash Paid** field.
   - At the end of the night, enter each player's final **Cash Out** amount.
   - The **Settle** column shows who still owes money and who should receive money back; **P&L** shows game profit/loss.
   - Click **End Game & Save** to commit the game to history.

### Settlement math

For each player:

- `Total Buy-in = buy-ins × buy-in amount`
- `P&L = Cash Out − Total Buy-in` (positive means they won)
- `Settle = Total Buy-in − Cash Paid − Cash Out` (positive means they still owe; negative means they should be paid back)

Example: a player buys in once at $20, hands $20 cash to the banker, and cashes out $0 in chips. `Settle = 20 − 20 − 0 = 0` (they owe nothing) and `P&L = 0 − 20 = −$20` (they lost $20 for the night).
3. **History tab** — Review past games and per-player results.
4. **Lifetime Stats tab** — See who's up and who's down across all sessions.

## Data

All state is stored in your browser's `localStorage` under the key `pokerCalc.v1`. To reset everything, clear site data for the page in your browser settings.

Player names are matched case-insensitively for the lifetime stats aggregation, so `Alice` and `alice` are treated as the same player.

## File structure

```
.
├── index.html   # The entire app — HTML, CSS, and JS in one file
└── README.md
```

## Tech

Plain HTML, CSS, and vanilla JavaScript. No frameworks, no build tooling.
