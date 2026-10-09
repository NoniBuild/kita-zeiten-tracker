# Kita-Zeiten Tracker

A small phone app for tracking daycare drop-off and pick-up times against a weekly hour budget.

Our Kita contract allows a fixed number of hours per week, with rules on top: earliest drop-off, a midday window where you can't pick up, a latest drop-off time. I tracked this by hand for weeks, first on paper and then in a chat. Once the rules were clear, I turned them into an app: tap "Bringen jetzt" in the morning, "Abholen jetzt" in the afternoon, and it tells you when to pick up today so the week lands exactly on budget.

## What it does

- One tap logs drop-off or pick-up with the current time. Every day can be edited afterwards.
- Week view with duration and balance per day, plus target, actual and remaining time for the week.
- Recommends today's pick-up time from the remaining budget and the days still open.
- Days off reduce the weekly budget automatically.
- Daily care hours can change from month to month (6, 7, 8 or 9 hours). On the first open of a new month, the app asks whether the hours stay the same. You can correct them later for any month.
- Flags times that break the rules (late drop-off, midday window) and refuses times outside opening hours.
- CSV export and JSON backup.
- Can be added to the home screen and then behaves like an app.

## How to use it

1. Download `index.html` and put it on any static host (Netlify Drop, GitHub Pages), or just open it in a browser.
2. On the phone: open the address and add it to the home screen.

Data is stored only in that browser (localStorage). No account, no server, nothing leaves the device. Keep the same address: a new address starts with empty storage. Export a backup now and then.

The interface is in German.

## Adapting the rules

All rules live in one place, the `R` object at the top of the script: opening hours, midday window, drop-off deadline and the hour options for the monthly prompt (`hourChoices`). Change the numbers to match your Kita. Times are minutes after midnight (`9*60+40` is 09:40).

The daily hours are not a fixed rule. They are set per month in the app, and the weekly budget is the sum of the hours of the days your child is there. A week that spans two months counts each day with its own month's hours.

The breakfast window and the dates in `R` belong to our Kita's history. Set `start` to the day you begin tracking, and remove or move `breakfastRuleEnds` if your Kita has no such rule.

## How it's built

One HTML file with plain HTML, CSS and JavaScript. No framework, no libraries, no backend. Light and dark mode follow the phone's setting.

Deliberate scope decisions: no backend (one user, one device), no settings screen (the rules rarely change; the only setting is the daily hours, asked once a month), no import button (the backup is a safety net, not a feature).

## License

MIT, see [LICENSE](LICENSE).

Built by [Noni Siampakouli](https://nonisiampakouli.de), with Claude as my development team.
