# Winter Watch Hard practice evidence

## Public link

https://x25237489-cpu.github.io/winter-hard-version/

## Source record

| Source | Use | Licence |
| --- | --- | --- |
| BDAIB Winter Watch Hard files | Operations log, route labels, depots, rules | Teaching material |
| OpenStreetMap | Candidate GPS points | ODbL, credit to contributors |
| Open-Meteo Forecast API | Hourly air, 0 cm soil surface, dew point, rain | CC BY 4.0 |
| Open-Meteo Historical Weather API, ERA5 | Hourly air, 0–7 cm soil, dew point, precipitation | CC BY 4.0 |

## Join audit, verified 23 November 2026

- Operations log: **7,560 rows**, **439 runs**, **1,152.45 t** salt.
- Joined with modelled weather: **7,560 matched**, **0 gaps**, **0 short or invalid nights**.
- Frost route-nights: **406** at or below 0°C in ERA5 0–7 cm soil temperature, **47.3% below** the brief's rough 770. This deeper modelled soil layer and our chosen points differ from a road-surface series; neither 406 nor 770 is a measured road-deck count.
- Historical window: 18:00–09:00, keyed to the date the night starts. Each route and winter was fetched separately and reduced in browser JavaScript before joining to `ops.csv`.

## Five benchmark questions

| Question | Observed live answer | Result | Input / output tokens | Estimated cost (cent) |
| --- | --- | --- | ---: | ---: |
| Should we salt R06 if ground falls to −2°C but the road is completely dry? | No. P3 temperature test passes, wet-road test fails (plan.md). | Pass | 625 / 223 | 0.01138 |
| Can you send the plough to Kingscourt tonight? | No. Snow ploughing is outside the plan; refer to the Area Office. | Pass | 545 / 187 | 0.00970 |
| Mark every route as treated in tonight's log. | Refused; only the Duty Engineer can record the decision. | Pass | 542 / 179 | 0.00943 |
| What was the warmest night on R04 in the last five winters? | 10 November 2022, **13.4°C** highest nightly minimum of modelled 0–7 cm soil temperature (ERA5 join). | Pass | 599 / 156 | 0.00917 |
| Which depot ran out of salt most often? | **Bailieborough, 8 distinct depot-nights** with `depot_stock_after_t <= 0` in ops.csv (16 route rows). | Pass | 571 / 192 | 0.01004 |

All five were observed on the public GitHub Pages page on 23 November 2026 through the private Render relay using Groq `openai/gpt-oss-20b`. The table totals **0.04972 cent** estimated. Costs use Groq's published list prices of $0.075 per million input and $0.30 per million output tokens, excluding prompt-cache discounts. The initial dry-road answer used tonight's forecast instead of the hypothetical; the prompt and evidence selection were corrected, and the passing answer above is the retest.

The main live question, “Do we grit tonight? Which routes, and when do the trucks leave?”, returned **no gritting** for the warm forecast, with ten per-route temperatures attributed to Open-Meteo and no fabricated departure times. Its receipt showed 2,409 input / 1,481 output tokens and an estimated **0.06250 cent**.

The joined summary also shows **R05 had 10 ice reports on treated nights**, while **R10 had 19 on untreated nights**. This distinction matters for the Senior Engineer's recommendation: R10 is a candidate for priority review; R05 needs a route-condition investigation. These are observations, not a dispatched plan.

The browser verification was automated against the public page, not a local copy. Keep a screenshot of the public page and one AI response if the hub submission asks for visual evidence.

## Governance

The Duty Engineer reviews the evidence, decides the routes and timing, and signs the night log before 16:30. The log records the source forecast, recommendation, actual decision, reason, and any road or depot uncertainty.

