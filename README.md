# Quantifying the Climate-Grid Nexus: Causal & Predictive Analysis of Heat Stress on Punjab Grid Electricity Demand

![Notebook CI](https://github.com/sahil161102/dai-mission-group-P/actions/workflows/run-notebook.yml/badge.svg)

---

## Team

| Name | Role |
|------|------|
| Rushikumar Subhashbhai Javiya | Causal Inference |
| Paritosh Sharma | Supervised Learning |
| Sahil Sahil | Lead / Generative |

> No student IDs in this file. Submit IDs separately via the course system (Moodle).

---

## Research Question

What is the marginal causal effect of continuous meteorological heat stress (measured by the Temperature-Humidity Index, THI) on hourly electricity demand (in Megawatts) within the Punjab power grid — when controlling for seasonal, temporal, and environmental confounders — and how robustly can supervised and generative neural architectures predict and simulate demand profile trajectories under extreme heat scenarios?

---

## Methods Overview

| Block | Method(s) |
|-------|-----------|
| Causal Inference | DoWhy — backdoor adjustment with continuous THI treatment; linear & quadratic structural estimands; random-common-cause refutation |
| Supervised Learning | Ridge Regression, Lasso, Random Forest Regressor, MLP Regressor |
| Unsupervised / Generative | Conditional Wasserstein GAN with Gradient Penalty (cWGAN-GP) for 24-hour demand profile generation |

---

## Data Sources

| Dataset | Source / URL | Access method |
|---------|-------------|---------------|
| State-Level Electricity Load Curves — Punjab, 2016–2025 (87,672 hourly observations) | [NITI Aayog ICED Load Curve Portal](https://iced.niti.gov.in/energy/electricity/distribution/national-level-consumption/load-curve) | local CSV (`data/Yearly_Demand_Profile_2016-2025.csv`) |
| Multi-Station Meteorological Surface Parameters — 23 Punjab Districts, 2016–2025 | NASA POWER API (district-level coordinates for 23 Punjab districts) | local CSV (`data/2022/`, `data/2024/`) |

> **Data size rule:** files < 100 MB may be committed directly. Files ≥ 100 MB must either
> be downloaded programmatically in the notebook (API/URL) or linked via a Sciebo share
> placed in this README — do NOT push large files to GitHub.

---

## Key Variables

| Variable | Type | Role | Description |
|----------|------|------|-------------|
| `datetime` | Temporal Index | Identifier | Timestamp (YYYY-MM-DD HH:00:00) |
| `demand_mw` | Continuous Float | Target (Outcome) | Total Punjab state grid consumption in MW |
| `thi` | Continuous Float | Treatment | Temperature-Humidity Index: THI = T_F − (0.55 − 0.0055·RH)·(T_F − 58) |
| `temp_c` | Continuous Float | Upstream Cause | Ambient temperature (°C), 23-station average |
| `rh_pct` | Continuous Float | Upstream Cause | Relative humidity (%), 23-station average |
| `precip_mm` | Continuous Float | Covariate | Hourly precipitation (mm) |
| `cloud_pct` | Continuous Float | Covariate / Confounder | Cloud cover (%) |
| `wind_ms` | Continuous Float | Covariate | Wind speed (m/s) |
| `hour` / `dow` / `month` / `year` | Integer | Fixed Effects | Calendar decomposition for diurnal, weekly, seasonal, and annual patterns |

---

## How to Run

### Option A — GitHub Actions (zero local setup)

Push to `main`. The CI workflow executes `notebook.ipynb` automatically.

- Check the **Actions** tab to see whether the run passed or failed.
- Download the `executed-notebook-*` artifact to inspect all cell outputs.
- The badge at the top of this README turns green when the notebook runs clean.

### Option B — Local environment

```bash
git clone https://github.com/sahil161102/dai-mission-group-P.git
cd dai-mission-group-P

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab notebook.ipynb
```

---

## Presentation Slide Requirements

| Item | Rule |
|------|------|
| Content slides | **Maximum 5** |
| Allowed extras | Title page · Literature/Reference slide · Backup slides |
| Backup slide content | Tables or figures/diagrams **only** |
| Required topics | Motivation & Economic Relevance · Data & Methodology · Results · Limitations & Synthesis |
| File format | **PDF only** — do not submit PPTX |
| Delivery | No live presentation — slides are reviewed during the oral exam |

---

## Oral Exam

- **Format:** 15-minute Q&A per group — questions on your Proposal and Presentation slides
- **Individual accountability:** each member answers questions on their own area (see Work Plan in notebook)
- **Rooms:** Morning sessions → M811 · Afternoon sessions → M827 · Arrive 10 minutes early
- **Grading:** oral performance directly modifies your Mission base score; significant individual
  discrepancies lead to differentiated individual grades

---

## Key Deadlines

| Date | Time | What |
|------|------|------|
| June 18 | 12:00 noon | Rank your session slots in Moodle (group lead) |
| June 30 | 12:00 noon | Submit repository link to Moodle (exactly one member per group) |
| June 30 | 23:59 | Final code deadline — commits after this are not graded |

> **Private repositories:** if your repo is private you MUST invite `pnposch` and
> `kiraschoenhuette` as collaborators before the deadline so the teaching team can clone it.

---

## Repository Structure

```
.
├── .github/workflows/run-notebook.yml   # CI: validates and executes notebook on every push
├── data/                                # local data files (see data/README.md)
│   ├── Yearly_Demand_Profile_2016-2025.csv
│   ├── 2016/
.
.                                        # NASA POWER weather CSVs for 23 Punjab districts
│   ├── 2024/
│   └── 2025/
├── notebook.ipynb                       # main deliverable — proposal + final submission (submit fully executed)
├── presentation.pdf                     # slide deck — PDF only, max 5 content slides
├── README.md                            # this file
└── requirements.txt                     # Python dependencies (required)
```
