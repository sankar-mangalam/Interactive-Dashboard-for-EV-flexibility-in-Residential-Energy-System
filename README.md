# Interactive-Dashboard-for-EV-flexibility-in-Residential-Energy-System
The dashboard presents results from an optimisation framework developed to investigate electric vehicle (EV) flexibility in residential energy systems.

The underlying study investigates the implications of various technical, market-related, and behavioural factors affecting the adoption and operation of EV flexibility. The research is conducted as a case study in Gothenburg, Sweden, using a Mixed-Integer Linear Programming (MILP) optimisation framework.

This dashboard was developed as part of research on  **Implementation of Vehicle-to-Grid services in Sweden** funded by Vinnova and coordinated by Polestar Performance AB


## Interactive Dashboard
****<img width="1587" height="944" alt="image" src="https://github.com/user-attachments/assets/9ea4d479-b9cc-408e-b651-74c22a2f76d0" />


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
The results presented in this repository are based on a Mixed-Integer Linear Programming (MILP) optimisation framework for residential energy systems with EV flexibility. Based on the input data, the model simulates the dispatch of EV based on an **objective to minimise the total costs**.
- **Input Data:** The input data for the model includes historical prices from the spot market, FCR-N and FCR-D markets, residential demand, Solar PV generation data, EV arrival and desired SOC based on user behaviour, grid frequency deviation and ambient temperature.

The specification of EV and household technologies are given as in the table below:

<table>
<tr>
<td valign="top">
<h3>EV Specifications</h3>

<table>
<tr><th>Parameter</th><th>Value</th></tr>
<tr><td>EV battery capacity</td><td>65 kWh</td></tr>
<tr><td>Maximum charge/discharge power</td><td>11 kW</td></tr>
<tr><td>Charge/discharge efficiency</td><td>93%</td></tr>
</table>

</td>

<td width="40"></td>

<td valign="top">

<h3>Household Technologies</h3>

<table>
<tr><th>Parameter</th><th>Value</th></tr>
<tr><td>PV capacity</td><td>10 kWp</td></tr>
<tr><td>BESS capacity</td><td>30 kWh</td></tr>
<tr><td>Maximum charge/discharge power</td><td>11 kW</td></tr>
<tr><td>Charge/discharge efficiency</td><td>93%</td></tr>
</table>

</td>
</tr>
</table>


### EV User behaviour
The EV user behaviour is formulated according to the working characteristics of the user and broadly classified as Work-from-Home (WFH), Hybrid and Work-from-Office (WFO). Based on the characteristics, the arrival and desired SOC is formulated for the entire year as given in the flowchart below:

<img width="1180" height="1022" alt="image" src="https://github.com/user-attachments/assets/383607d3-17e0-4e3c-b4be-bd1ac2f95b90" />

The SOC variation over the weekdays and weekends for all the user behaviour types are given as in the images below:

<table>
<tr>
<td align="center">
  <strong>Weekday Characteristics</strong>
</td>
<td align="center">
  <strong>Weekend Characteristics</strong>
</td>
</tr>

<tr>
<td align="center" valign="top">
  <img
    src="https://github.com/user-attachments/assets/13f67cd0-d39b-49b6-b5a0-e5c778f8c60d"
    alt="Weekday Characteristics"
    height="500"
  />
</td>

<td align="center" valign="top">
  <img
    src="https://github.com/user-attachments/assets/ded8ccf2-6243-4c20-89a1-65236a47a347"
    alt="Weekend Characteristics"
    height="500"
  />
</td>
</tr>
</table>



## Would you like to know more?
**The link to the journal paper with detailed methodology and analysis will be updated soon**

**Author:** Sankar Mangalath Ramasan  
**Affiliation:** Chalmers University of Technology

📄 **Research publication:** [Will be updated soon]()
💻 **Source code:** [GitHub Repository](https://github.com/sankar-mangalam/EV-flexibility-in-Residential-Energy-System)

Please cite the associated research publication when using results as below:

*Mangalath Ramasan, Sankar and Sridhar, Araavind and Steen, David and Anh Tuan, Le, To V2G or Not? Assessing EV Flexibility Across Electricity Markets and User Behaviour in Residential Energy Systems. Available at SSRN: http://dx.doi.org/10.2139/ssrn.7403061*

