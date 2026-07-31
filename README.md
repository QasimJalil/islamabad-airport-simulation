# Optimising Passenger and Cargo Flow at Islamabad International Airport

**BSc Business Computing Final Year Project — Brunel University London, 2025**
Business process re-engineering of terminal passenger flow, using BPMN modelling and discrete-event simulation to quantify the impact of proposed changes before any money is spent.

Graded as part of a First Class degree.

---

## The problem

Islamabad International Airport's terminal processes were built around manual, staff-mediated steps: agent-led check-in, single-stream immigration, and a security funnel with no parallel capacity. Passengers experienced long, compounding queues, and the airport had no way to test an intervention without disrupting live operations.

**AS-IS — current terminal flow, modelled in Simul8**

![AS-IS Simul8 model of Islamabad International Airport terminal flow](results/AS-IS.png)

Every passenger funnels through the same sequence. Class-based lanes exist at check-in and boarding, but immigration and security are single-stream for everyone — which is exactly where the queues compound.

## What I did

1. **Elicited requirements** from an airport stakeholder through informal interviews under Brunel-approved research ethics.
2. **Modelled the AS-IS process** in BPMN (Visual Paradigm) — every touchpoint from arrival to boarding, split by passenger class.
3. **Built a discrete-event simulation** in Simul8, calibrated against observed arrival rates and service times.
4. **Designed a TO-BE process** applying business process re-engineering principles: self-service check-in and bag drop, a fast-track immigration lane, parallel body-scanning capacity, and self-boarding gates.
5. **Re-ran the simulation** against the TO-BE model and measured the difference on a fixed set of KPIs.

**TO-BE — re-engineered terminal flow**

![TO-BE Simul8 model with parallel capacity — e-gate entry, self-service check-in, automated bag drop, fast-track immigration and self-boarding](results/TO-BE.png)

The structural change is visible without reading a single number: where the AS-IS model is one path, the TO-BE model opens parallel capacity at every stage — electronic gate entry, self-service kiosks alongside conventional check-in, automated luggage drop, a fast-track immigration lane, and self-boarding gates. Passengers who can self-serve stop blocking those who can't.

**Full BPMN process models** (Visual Paradigm source in `models/`, rendered diagrams for viewing without a licence):
[AS-IS BPMN →](models/as-is/as-is-terminal-bpmn.jpg) · [TO-BE BPMN →](models/to-be/to-be-terminal-bpmn.jpg)

## Results

Simulated over an equivalent operating period, same arrival profile:

| KPI (minutes unless stated) | AS-IS | TO-BE | Change |
|---|---|---|---|
| **Overall time in system** | **151.99** | **78.73** | **−48%** |
| **Passengers processed** | **5,364** | **6,129** | **+14%** |
| Security queue | 34.13 | 3.71 | −89% |
| Immigration queue | 25.42 | 7.85 | −69% |
| Initial entry queue | 17.59 | 4.59 | −74% |
| Bag drop — economy / premium economy | 19.98 | 5.04 | −75% |
| Bag drop — first / business | 13.97 | 2.38 | −83% |
| Check-in — economy / premium economy | 19.93 | 6.88 | −65% |
| Check-in — first / business | 11.48 | 4.62 | −60% |
| Boarding — economy / premium economy | 11.49 | 5.20 | −55% |
| Boarding — first / business | 6.60 | 3.70 | −44% |

The dominant single win was security: adding parallel body-scanning capacity removed the terminal's hardest bottleneck. Halving end-to-end journey time while *increasing* throughput 14% means the gain came from removing queueing waste, not from adding headcount.

Raw figures: [`results/kpi-graphs.xlsx`](results/kpi-graphs.xlsx)

### The numbers, straight out of Simul8

Rather than ask anyone to take the table on trust, here is the TO-BE run in Simul8's Results Manager — average time in system **78.73 minutes**, number completed **6,129**, each with 95% confidence intervals from multiple trials:

![Simul8 Results Manager showing TO-BE run — 78.73 min average time in system, 6,129 passengers completed, with 95% confidence ranges](results/TO-BE-RESULTS.png)

The AS-IS equivalent is at [`results/AS-IS-RESULTS.png`](results/AS-IS-RESULTS.png). Model configuration evidence — arrival distributions, routing logic, resource allocation, clock properties and trial settings — is in [`results/simul8-screens/`](results/simul8-screens/), so the model can be audited rather than just believed.

## Repository contents

```
models/as-is/       AS-IS BPMN model (Visual Paradigm .vpp) + rendered diagram
models/to-be/       TO-BE BPMN model (Visual Paradigm .vpp) + rendered diagram
simulation/         AS-IS and TO-BE Simul8 models (.S8), input distribution tables,
                    simulation report
results/            KPI comparison screenshots and the underlying spreadsheet
results/simul8-screens/   Model configuration evidence — distributions, routing,
                          resources, clock properties, labels
docs/               Dissertation, project synopsis, final presentation, references
```

## Tools

Visual Paradigm (BPMN 2.0) · Simul8 (discrete-event simulation) · Excel · Business Process Re-engineering methodology

## Opening the files

- `.vpp` — Visual Paradigm. The rendered `.jpg` alongside each model lets you read the process without a licence.
- `.S8` — Simul8. There are two: `simulation/as-is-islamabad-airport.S8` is the baseline model of current operations, and `simulation/to-be-islamabad-airport.S8` is the re-engineered design. The results table above is the direct comparison between them. If you don't have Simul8, `simulation/simulation-report.pdf` documents both models and their outputs.
- **[Video demonstration of the simulation running →](https://youtu.be/zFs3OnL9DQU)** — submitted with the project. Worth watching if you want to see the models in motion without installing Simul8.

## A note on research data

This project involved a human participant under Brunel University London ethics approval. The consent documentation, participant information sheet, and raw interview and questionnaire data are **deliberately excluded** from this repository. The approved protocol committed to anonymisation, restricted storage, and non-attributable use only. Published here are the models, the simulation, the results, and the written analysis — all of which are my own work.

---

**Qasim Jalil** — BSc Business Computing (First Class), Brunel University London
[github.com/QasimJalil](https://github.com/QasimJalil)
