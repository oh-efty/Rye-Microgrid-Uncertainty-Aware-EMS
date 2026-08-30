# Uncertainty-Aware Microgrid Energy Management Framework

This repository contains the datasets, optimization models, simulation
framework, and evaluation codes developed for an uncertainty-aware microgrid
energy management study.

The framework investigates the impact of renewable generation and load
forecast uncertainty in a PV-Wind-Diesel-BESS microgrid under both
grid-connected and islanded operation.

Four energy management strategies are evaluated:

- Deterministic Day-Ahead Dispatch (DET-DA)
- Two-Stage Stochastic Day-Ahead Dispatch (STO-DA)
- Rolling-Horizon Model Predictive Control (MPC)
- Perfect Foresight Benchmark (PF)

The study quantifies forecast uncertainty impacts through:

- Cost of Uncertainty (CoU)
- Stochastic Mitigation Ratio (SMR)
- MPC Recovery Ratio (RR)
- Energy Not Served (EENS)
- Forced grid-outage resilience analysis


---

# Microgrid System

The investigated system consists of:

- Photovoltaic generation
- Wind generation
- Diesel generator
- Battery Energy Storage System (BESS)
- Utility grid connection
- Critical and non-critical loads


Main simulation parameters:

| Parameter | Value |
|---|---|
| Scheduling horizon | 24 h |
| Time resolution | 1 h |
| PV capacity | 86.4 kWp |
| Wind capacity | 225 kW |
| BESS capacity | 500 kWh |
| BESS power rating | 400 kW |
| Critical load share | 33% |
| Development dataset | 304 days |
| Out-of-sample dataset | 127 days |
| Forecast uncertainty levels | 5%, 10%, 20%, 30% |


---

# Repository Structure
uncertainty-aware-microgrid-ems
├── 01_Data
│   ├── rye_development_304days.csv
│   └── rye_oos_127days.csv
│
├── 02_Configuration
│   └── study_parameters_frozen_v12.json
│
├── 03_DET_PF
│   └── 03_DET_PF_Pyomo_HiGHS.ipynb
│
├── 04_STO_DA
│   ├── 04_STO_DA_Scenario_Generation_BRA.ipynb
│   └── 05_STO_DA_Pyomo_HiGHS_K_Convergence.ipynb
│
├── 05_OOS_Evaluation
│   └── 06_STO_DA_127Day_OOS_Evaluation_FIXED.ipynb
│
├── 06_MPC
│   └── 07_Rolling_Horizon_MPC_OOS_FIXED_DYNAMIC_ANCHOR.ipynb
│
├── 07_Sensitivity_Analysis
│   └── 08_Uncertainty_Source_Sensitivity_FULL.ipynb
│
├── 08_Grid_Outage
│   └── 09_Forced_Grid_Outage_Islanding_FULL_v3.ipynb
│
└── README.md



---

# Computational Framework

Implemented using:

- Python
- Pyomo
- HiGHS MILP Solver
- NumPy
- Pandas
- SciPy
- Matplotlib


---

# Simulation Workflow
Microgrid Data
    ↓
Forecast Uncertainty Modeling
    ↓
Monte Carlo Scenario Generation
    ↓
Backward Reduction Algorithm (BRA)
    ↓
DET-DA / STO-DA / MPC / PF Evaluation
    ↓
Out-of-Sample Validation
    ↓
Sensitivity and Grid-Outage Analysis

---

# Scenario Generation

The stochastic optimization framework uses:

Initial Monte Carlo scenarios:
500

Reduced representative scenarios:

50

The scenario size is selected through cost-computation convergence analysis
to achieve a balance between solution quality and computational efficiency.


---

# Notebook Description


## Deterministic and Perfect Foresight

03_DET_PF_Pyomo_HiGHS.ipynb

Builds the MILP optimization model and generates:

- DET-DA baseline
- PF benchmark


## STO Scenario Generation

04_STO_DA_Scenario_Generation_BRA.ipynb

Generates uncertainty scenarios using Monte Carlo simulation and applies
Backward Reduction Algorithm.


## STO Convergence Analysis

05_STO_DA_Pyomo_HiGHS_K_Convergence.ipynb

Evaluates scenario number versus:

- OOS cost stability
- Computational time


## STO OOS Evaluation

06_STO_DA_127Day_OOS_Evaluation_FIXED.ipynb

Evaluates stochastic scheduling performance on unseen 127 days.


## MPC Evaluation

07_Rolling_Horizon_MPC_OOS_FIXED_DYNAMIC_ANCHOR.ipynb

Implements rolling-horizon MPC using:

- Updated forecasts
- Updated BESS SOC
- Re-optimization


## Sensitivity Analysis

08_Uncertainty_Source_Sensitivity_FULL.ipynb

Evaluates:

- PV uncertainty
- Wind uncertainty
- Load uncertainty
- Combined uncertainty


## Forced Grid-Outage Analysis

09_Forced_Grid_Outage_Islanding_FULL_v3.ipynb

Evaluates:

- Islanding transition
- Diesel response
- BESS support
- Critical load protection

---

# Performance Metrics

Economic metrics:

- Mean operating cost
- Cost of Uncertainty (CoU)
- Stochastic Mitigation Ratio (SMR)
- MPC Recovery Ratio (RR)


Reliability metrics:

- Critical EENS
- Non-critical EENS
- Load interruption probability


Operational metrics:

- Diesel generation
- Renewable curtailment
- Grid import/export
- BESS throughput
- Computational time

---

# Reproduction

Install required packages:

```bash
pip install numpy pandas scipy pyomo matplotlib highspy
