# Portfolio Variance Monitor

An interactive insurance portfolio analytics dashboard built with vanilla HTML, CSS, and JavaScript — no server or build step required. Open the file in a browser and it runs instantly.

---

## Features

**Live Portfolio Monitoring**
- 8 commercial insurance segments (Construction, Transportation, Healthcare, and more) populated with real industry benchmarks from NAIC, NCCI, and Verisk
- Weighted loss ratio tracking against plan with variance and z-score anomaly detection
- Dual alert threshold: `z ≥ 2.5` OR `|variance| ≥ 5pp` triggers an ALERT flag
- Interactive segment drill-down with monthly trend charts, broker breakdowns, and policy-level tables

**Real Industry Benchmarks**
- Expected loss ratios, claim frequencies, and severities sourced from NAIC 2023 Annual Report, NCCI 2024 State of the Line, and Verisk GL Actuarial Hub
- Policy-level data generated via seeded Monte Carlo simulation (Mulberry32 RNG, Box-Muller normal distribution) using those benchmarks as parameters

**AI What-If Simulator (Claude API)**
- Toggle segments in/out of the portfolio and apply loss ratio stress (±20pp) per segment
- Free-text macro scenario input — type any geopolitical or market context (e.g. *"US goes to war with Iran — oil prices spike 40%"*) and it is injected directly into the prompt
- Claude streams a structured underwriting committee narrative in real time
- Markdown rendered into styled HTML on completion — bold, headings, and bullet points match the dashboard aesthetic

---

## Tech Stack

| Layer | Detail |
|---|---|
| Charts | Chart.js 4.4 (time-series, scatter, sparklines) |
| AI | Claude API (`claude-sonnet-4-6`) via Server-Sent Events streaming |
| Data | Monte Carlo simulation seeded from NAIC/NCCI/Verisk benchmarks |
| Styling | Vanilla CSS with dark theme and CSS custom properties |
| Dependencies | Zero build tools — single self-contained HTML file |

---

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/portfolio-variance-monitor.git
   ```

2. Open `portfolio_variance_monitor.html` in any modern browser (Chrome, Firefox, Edge, Safari).

3. To use the **AI What-If Simulator**, you need a Claude API key from [console.anthropic.com](https://console.anthropic.com). Enter it in the API key field in the What-If panel.

> **Note:** The dashboard makes direct browser-to-API calls using the `anthropic-dangerous-direct-browser-access` header. This is suitable for local/demo use. For production, route API calls through a backend proxy so the key is never exposed in client-side code.

---

## Project Structure

```
portfolio-variance-monitor/
├── portfolio_variance_monitor.html   # Main dashboard (self-contained)
├── portfolio_variance_presentation.html  # Companion slide deck
└── README.md
```

---

## Data Sources

- [NAIC 2023 Annual Report](https://content.naic.org/sites/default/files/inline-files/2023-annual-report.pdf)
- [NCCI 2024 State of the Line](https://www.ncci.com/SecureDocuments/SOLGuide_2024.html)
- [Verisk GL Actuarial Hub](https://core.verisk.com/Actuarial-Hub-Pages/AH-Articles/2024/Q3/General-Liability-Loss-Ratios)

All policy-level data is synthetic. No PII, no live system access.

---

## AI Integration

The What-If Simulator sends a structured prompt to Claude containing:
- Current portfolio baseline metrics
- Per-segment actuals vs. plan
- The selected scenario (segment exclusions + LR stress)
- Any free-text macro/geopolitical context provided by the analyst

Claude returns a streamed narrative covering trade-offs, recommended actions, and unintended consequences — rendered as formatted HTML inside the dashboard.

---

## Roadmap

- [ ] CSV export of segment and policy data
- [ ] Saved scenario comparison (side-by-side what-if)
- [ ] Backend proxy for secure API key handling
- [ ] Live data connector (CSV/JSON upload)
- [ ] Additional lines of business (Property, Marine, Cyber)

---

## Acknowledgements

Built as a demonstration of integrating public insurance industry data with generative AI for actuarial and underwriting use cases. AI narration powered by [Claude (Anthropic)](https://www.anthropic.com).
