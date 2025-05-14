# FareSentinel

*Smart, data‑driven playbook for timing your international flight purchases like a pro trader.*

---

## 📈 What is FareSentinel?

FareSentinel transforms the **Three‑Threshold Model** outlined in our chat into a reproducible workflow:

| Threshold     | Relative to 90‑day low                     | Action                                       | Default Window   |
| ------------- | ------------------------------------------ | -------------------------------------------- | ---------------- |
| **Buy**       | ≤ Low + 5 %                                | Buy immediately (use 24 h refund)            | 120–180 days out |
| **Watch**     | Low + 5 % → Avg + 10 %                     | Set alerts, record daily                     | Flexible         |
| **Stop‑Loss** | > Avg + 10 % **OR** ≤ 21 days to departure | Buy with miles / split tickets / shift dates | 0–21 days        |

FareSentinel turns this logic into:

1. **Data capture** – scrape or import prices once per day.
2. **Decision engine** – evaluate against thresholds in `config.yaml`.
3. **Notifier** – push alerts to email / Slack / iOS Shortcuts.

---

## 🗂 Repo structure

```
FareSentinel/
├── README.md         ← you are here
├── faresentinel/
│   ├── __init__.py
│   ├── collector.py  # headless price grabber
│   ├── engine.py     # threshold & rule evaluator
│   ├── notifier.py   # email / Slack hooks
│   └── utils.py      # helpers
├── notebooks/
│   └── example.ipynb # data‑viz & back‑testing
├── config.yaml       # user‑editable thresholds & routes
├── requirements.txt  # selenium, pandas, pyyaml …
├── .gitignore
└── LICENSE           # MIT by default
```

---

## 🚀 Quick start

```bash
# 1. Clone
$ git clone https://github.com/yourname/FareSentinel.git
$ cd FareSentinel

# 2. Set up env
$ python -m venv venv && source venv/bin/activate
$ pip install -r requirements.txt

# 3. Edit config.yaml
routes:
  - origin: AUS
    destination: PVG
    date: 2025-12-15
    low_price: 850   # historical low (USD)
    avg_price: 1100  # 90‑day rolling average (USD)
alerts:
  email: you@example.com
  slack_webhook: https://hooks.slack.com/…

# 4. Run daily (CRON/GitHub Actions)
$ python -m faresentinel
```

The first run fetches today’s fare, writes `data/history_AUS_PVG.csv`, and triggers a notification if a threshold is crossed.

---

## ✨ Fancy bits

* **Headless scraping** via undetected‑chromedriver (works with Google Flights).
* **Price‑bucket inference** – estimates current fare bucket (A–Z) from HTML.
* **Back‑tester** – Jupyter notebook to validate thresholds with historical data (Skyscanner CSV export).
* **Anonymised sessions** – rotates IP & user‑agent to avoid "seen once then price jump" phenomenon.

---

## 🧑‍💻 Roadmap

* [ ] Hopper API integration (if/when publicly available)
* [ ] Telegram bot notifier
* [ ] Simple Streamlit dashboard for non‑coders

Feel free to submit PRs or open issues! 🎫

---

## 📝 License

MIT – see [LICENSE](LICENSE) for details. Contributions welcome.
