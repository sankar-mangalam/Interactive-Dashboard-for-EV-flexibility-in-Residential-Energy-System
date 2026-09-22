# Interactive-Dashboard-for-EV-flexibility-in-Residential-Energy-System
The dashboard presents results from an optimisation framework developed to investigate electric vehicle (EV) flexibility in residential energy systems.

The underlying study investigates the implications of various technical, market-related, and behavioural factors affecting the adoption and operation of EV flexibility. The research is conducted as a case study in Gothenburg, Sweden, using a Mixed-Integer Linear Programming (MILP) optimisation framework.

The underlying research and detailed methodology are described in:
[To V2G or Not? Assessing EV Flexibility Across Electricity Markets and User Behaviour in Residential Energy Systems](https://dx.doi.org/10.2139/ssrn.7403061)


## Interactive Dashboard

--> [Launch the Streamlit dashboard](YOUR_STREAMLIT_URL)

The dashboard allows users to compare optimisation results across different residential energy-system configurations interactively.

## What can you explore?

The dashboard allows comparison across the following Scenarios:
- **Years:** 2022 and 2025
- **EV configurations:** Scenarios with EV, without EV, or both simultaneously
- **Charging strategies and Electricity markets:** Direct Charging (DC) and Smart Charging (SC), Spot market, Spot + FCR-N, Spot + FCR-D, and Spot + FCR-N + FCR-D
- **EV user behaviour:** Work-from-Office (WFO), Hybrid and Work-From-Home (WFH)
- **Technologies:** PV, BESS and space-heating configurations
- **Battery ageing:** Scenarios with or without EV battery ageing cost as part of the optimisation objective

The results of the scenarios can be obtained for the following KPIs across the primary and secondary axes:
- **Costs (SEK):** Total Costs, FCRN Returns, FCRD Returns and Peak Cost
- **Hours:** FCRN and FCRD participation hours, Spot Import/Export hours, EV availability hours
- **Battery Ageing (%):** BESS Calendar and Cyclic ageing, EV Calendar and Cyclic Ageing, BESS Total ageing, EV Total ageing
- **SOC (%):** Average EV SOC
- **Load (kW):** Peak load
- **Bid Capacity (kW):** FCRN, FCRD-Up and FCRD-Down bid capacity
- **Energy Import/Export (kWh):** EV charge Energy (FCRN and FCRD), EV Discharge Energy (FCRN and FCRD), BESS Charge Energy (FCRN and FCRD), BESS Discharge Energy (FCRN and FCRD), Spot Import/Export Energy
- **Energy Throughput (kWh):** EV Energy Throughput

  ## Data and Methodology
  The results presented in this repository are based on a Mixed-Integer Linear Programming (MILP) optimisation framework for residential energy systems with EV flexibility. The optimisation model is based on time-series data at a 15-minute resolution based on data from 2022 and 2025.
- **Input Data:** The input data for the model includes historical prices from the spot market, FCR-N and FCR-D markets, residential demand, Solar PV generation data, EV arrival and desired SOC based on user behaviour, grid frequency deviation and ambient temperature
- **Modelling:** The model simulates the dispatch based on the input data and finds the optimal working condition based on 
