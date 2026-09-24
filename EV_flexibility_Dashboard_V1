import streamlit as st
import numpy as np
import pandas as pd
import plotly.graph_objects as go
from plotly.subplots import make_subplots

st.set_page_config(layout="wide")

# ================= GLOBAL FONT SETTINGS =================

TITLE_FONT_SIZE = 30
AXIS_TITLE_FONT_SIZE = 24#40
AXIS_TICK_FONT_SIZE = 22#34
LEGEND_FONT_SIZE = 26#32
WORK_LABEL_FONT_SIZE = 22 #34
MARKET_LABEL_FONT_SIZE = 26#34
HOVER_FONT_SIZE = 18
ANNOTATION_FONT_SIZE = 50

# ================= LOAD DATA =================
@st.cache_data
def load_data():
    df = pd.read_excel("Data/Results_optimisation KPI_V1.xlsx")
    df.rename(columns={df.columns[0]: "Scenario"}, inplace=True)
    return df

df = load_data()

# ================= KPI HANDLER =================
def get_kpi(series_df, kpi_name):
    mapping = {
        "Total cost": series_df["Total Cost"],
        "FCRN Returns": series_df["Total FCRN Returns"],
        "FCRD Returns": series_df["Total FCRD Returns"],
        "Peak Cost": series_df["Total Peak Cost"],

        "BESS Calender Ageing (%)": series_df["Total BESS Cal_Ageing"],
        "BESS Cyclic Ageing (%)": series_df["Total BESS Cyc_Ageing"],
        "Total BESS Ageing (%)": series_df["Total BESS Cyc_Ageing"] + series_df["Total BESS Cal_Ageing"],
        "EV Calender ageing (%)": series_df["Total EV Cal_Ageing"],
        "EV Cyclic ageing (%)": series_df["Total EV Cyc_Ageing"],
        "Total EV ageing (%)": series_df["Total EV Cyc_Ageing"] + series_df["Total EV Cal_Ageing"],

        "FCRN Participation Hours": series_df["Hours_FCRN"],
        "FCRD Participation Hours": series_df["Hours_FCRD"],
        "Spot Import Hours": series_df["Hours_import_spot"],
        "Spot Export Hours": series_df["Hours_export_spot"],
        "EV Availability Hours": series_df["EV market availability"],

        "EV charge Energy (FCRN)": series_df["Total EV charge Energy (FCRN)"],
        "EV discharge Energy (FCRN)": series_df["Total EV discharge Energy (FCRN)"],
        "EV charge Energy (FCRD)": series_df["Total EV charge Energy (FCRD)"],
        "EV discharge Energy (FCRD)": series_df["Total EV discharge Energy (FCRD)"],
        "Spot Import Energy": series_df["Spot Import Energy"],
        "Spot Export Energy": series_df["Spot Export Energy"],
        "BESS charge Energy (FCRN)": series_df["Total BESS charge Energy (FCRN)"],
        "BESS discharge Energy (FCRN)": series_df["Total BESS discharge Energy (FCRN)"],
        "BESS charge Energy (FCRD)": series_df["Total BESS discharge Energy (FCRD)"],
        "BESS discharge Energy (FCRD)": series_df["Total BESS discharge Energy (FCRD)"],

        "FCRN Bid Capacity": series_df["FCRN Bid Capacity"],
        "FCRDU Bid Capacity": series_df["FCRDU Bid Capacity"],
        "FCRDD Bid Capacity": series_df["FCRDD Bid Capacity"],

        "Average EV SOC": series_df["Average EV SOC"],
        "Peak load": series_df["Peak load"],
        "EV Energy Throughput": series_df["EV Battery energy throughput"],
    }
    return mapping[kpi_name]

# ================= KPI GROUPS =================
KPI_GROUPS = {
    "cost": ["Total cost", "FCRN Returns", "FCRD Returns", "Peak Cost"],
    "hours": ["FCRN Participation Hours", "FCRD Participation Hours",
              "Spot Import Hours", "Spot Export Hours", "EV Availability Hours"],
    "ageing": ["BESS Calender Ageing (%)", "BESS Cyclic Ageing (%)", "Total BESS Ageing (%)",
              "EV Calender ageing (%)", "EV Cyclic ageing (%)", "Total EV ageing (%)"],
    "soc": ["Average EV SOC"],
    "load": ["Peak load"],
    "Bid Capacity": ["FCRN Bid Capacity", "FCRDU Bid Capacity", "FCRDD Bid Capacity" ],
    "Energy": ["EV charge Energy (FCRN)", "EV discharge Energy (FCRN)", "EV charge Energy (FCRD)", 
                "EV discharge Energy (FCRD)", "Spot Import Energy", "Spot Export Energy",
                "BESS charge Energy (FCRN)", "BESS discharge Energy (FCRN)", "BESS charge Energy (FCRD)", "BESS discharge Energy (FCRD)" ],
    "Energy Throughput": ["EV Energy Throughput"]
}

GROUP_LABELS = {
    "cost": "Costs (SEK)",
    "hours": "Hours",
    "ageing": "Ageing (%)",
    "soc": "SOC",
    "load": "Load (kW)",
    "Bid Capacity": "Bid Capacity (kW)",
    "Energy": "Energy Import/Export (kWh)",
    "Energy Throughput": "Energy Throughput (kWh)"
}

# ================= FIXED KPI COLORS =================

KPI_COLORS = {

    # ================= COST KPIs =================
    "Total cost": "#1F77B4",          # Blue
    "Peak Cost": "#D62728",           # Red

    # ================= FCRN PALETTE - Greens =================
    "FCRN Returns": "#2CA02C",
    "FCRN Participation Hours": "#1B7837",
    "FCRN Bid Capacity": "#5AAE61",
    "EV charge Energy (FCRN)": "#A6DBA0",
    "EV discharge Energy (FCRN)": "#00441B",
    "BESS charge Energy (FCRN)": "#66C2A4",
    "BESS discharge Energy (FCRN)": "#238B45",

    # ================= FCRD PALETTE - Yellow / Orange / Brown =================
    "FCRD Returns": "#F5C542",
    "FCRD Participation Hours": "#E69F00",
    "FCRDU Bid Capacity": "#D95F02",
    "FCRDD Bid Capacity": "#A6761D",
    "EV charge Energy (FCRD)": "#FDB863",
    "EV discharge Energy (FCRD)": "#B35806",
    "BESS charge Energy (FCRD)": "#FFE082",
    "BESS discharge Energy (FCRD)": "#8C510A",

    # ================= SPOT PALETTE - Purple / Violet =================
    "Spot Import Hours": "#6A3D9A",
    "Spot Export Hours": "#9E77C8",
    "Spot Import Energy": "#542788",
    "Spot Export Energy": "#C2A5CF",

    # ================= EV PALETTE - Blues / Cyan =================
    "EV Availability Hours": "#0571B0",
    "Average EV SOC": "#0455BE",
    "EV Energy Throughput": "#67A9CF",

    # ================= AGEING PALETTE - Pink / Grey =================
    "BESS Calender Ageing (%)": "#8C564B",
    "BESS Cyclic Ageing (%)": "#C49A6C",
    "Total BESS Ageing (%)": "#5D4037",

    "EV Calender ageing (%)": "#E990CE",
    "EV Cyclic ageing (%)": "#C51B7D",
    "Total EV ageing (%)": "#5A2D37",

    # ================= LOAD =================
    "Peak load": "#4D4D4D"
}


# ================= COST BREAKDOWN COLORS =================

COST_BREAKUP_COLORS = {
    "Supplier Cost": "#034D81",
    "DSO Cost": "#FF7F0E",
    "Tax Cost": "#D62728",
    "FCRN Returns": "#2CA02C",
    "FCRD Returns": "#F5C542"
}

# ================= PARSER =================
def parse_scenario(name):
    name = name.upper()
    return {
        "BASE": "BASE" in name,
        "WFH": "WFH" in name,
        "WFO": "WFO" in name,
        "HYBRID": "HYBRID" in name,
        "PV": "PV" in name,
        "HEAT": "HEAT" in name,
        "BESS": "BESS" in name,
        "AGEING": "AGEING" in name,
        "Spot": "V2G" in name and all(x not in name for x in ["FCRN", "FCRD", "FCRN,D"]),
        "Spot+FCRN": "V2G_FCRN" in name and "V2G_FCRN,D" not in name,
        "Spot+FCRD": "V2G_FCRD" in name,
        "Spot+FCRN+FCRD": "V2G_FCRN,D" in name,
        "SC": "SC" in name,
        "DC": "DC" in name
    }

# ================= FILTER =================
def filter_scenarios(
    df,
    ev_selection,
    selected_markets,
    selected_work,
    tech_filters,
    year
):
    filtered_rows = []

    for _, row in df.iterrows():

        scenario = row["Scenario"].upper()

        # ---------------- YEAR ----------------
        if str(year) not in scenario:
            continue

        parsed = parse_scenario(scenario)
        is_base = parsed["BASE"]

        # =====================================================
        # EV SELECTION
        # =====================================================

        # EV = YES -> exclude BASE
        if ev_selection == "Yes" and is_base:
            continue

        # EV = NO -> BASE only
        if ev_selection == "No" and not is_base:
            continue

        # =====================================================
        # BASE SCENARIOS
        # =====================================================

        if is_base:

            # BASE was duplicated for WFO / HYBRID / WFH.
            # Keep only HYBRID internally.
            if not parsed["HYBRID"]:
                continue

        # =====================================================
        # EV SCENARIOS
        # =====================================================

        else:

            if not any(
                parsed.get(m, False)
                for m in selected_markets
            ):
                continue

            if not any(
                parsed.get(w, False)
                for w in selected_work
            ):
                continue

        # =====================================================
        # TECHNOLOGY FILTERS
        # =====================================================

        valid = True

        # PV / HEAT / BESS apply to both BASE and EV scenarios
        for tech in ["PV", "HEAT", "BESS"]:

            mode = tech_filters.get(tech, "All")

            if mode == "With" and not parsed.get(tech, False):
                valid = False

            elif mode == "Without" and parsed.get(tech, False):
                valid = False

        # AGEING only makes sense when EV exists
        if not is_base:

            ageing_mode = tech_filters.get("AGEING", "All")

            if ageing_mode == "With" and not parsed["AGEING"]:
                valid = False

            elif ageing_mode == "Without" and parsed["AGEING"]:
                valid = False

        if valid:
            filtered_rows.append(row)

    return pd.DataFrame(filtered_rows)

# ================= CLEAN LABEL =================
def clean_scenario_name(name, year):

    name = name.upper()

    # Remove RESULTS_
    name = name.replace("RESULTS_", "")

    # Remove year
    name = name.replace(str(year), "")

    # =====================================================
    # MARKET DISPLAY NAMES
    # Replace most specific names first
    # =====================================================

    name = name.replace(
        "V2G_FCRN,D",
        "Spot+FCRN+FCRD"
    )

    name = name.replace(
        "V2G_FCRN",
        "Spot+FCRN"
    )

    name = name.replace(
        "V2G_FCRD",
        "Spot+FCRD"
    )

    name = name.replace(
        "V2G",
        "Spot"
    )

    # =====================================================
    # BASE SCENARIO
    # HYBRID exists only because of backend scenario generation.
    # It should not appear to the dashboard user.
    # =====================================================

    if "BASE" in name:
        name = name.replace("HYBRID", "")

    # Remove empty pieces caused by replacements
    parts = [
        p for p in name.split("_")
        if p
    ]

    return "_".join(parts)

# ================= SORT =================
def sort_scenarios(data, tech_filters):

    def get_market(name):
        name = name.upper()
        if "BASE" in name: return "BASE"
        if "DC" in name: return "DC"
        elif "SC" in name: return "SC"
        elif "V2G_FCRN,D" in name: return "Spot+FCRN+FCRD"
        elif "V2G_FCRN" in name: return "Spot+FCRN"
        elif "V2G_FCRD" in name: return "Spot+FCRD"
        elif "V2G" in name: return "Spot"

    def get_work(name):
        name = name.upper()
        if "WFO" in name: return "WFO"
        elif "HYBRID" in name: return "HYBRID"
        elif "WFH" in name: return "WFH"

    market_order_list = ["BASE", "DC", "SC", "Spot", "Spot+FCRD", "Spot+FCRN", "Spot+FCRN+FCRD"]
    work_order_list = ["WFO", "HYBRID", "WFH"]

    def sort_key(name):
        name = name.upper()

        m = get_market(name)
        w = get_work(name)

        m_idx = market_order_list.index(m) if m in market_order_list else 99
        w_idx = work_order_list.index(w) if w in work_order_list else 99

        heat_idx = 1 if "HEAT" in name else 0
        ageing_idx = 1 if "AGEING" in name else 0

        pv = 1 if "PV" in name else 0
        bess = 1 if "BESS" in name else 0

        combo_map = {(0,0):0,(1,0):1,(0,1):2,(1,1):3}
        combo_idx = combo_map[(pv, bess)]

        return (m_idx, w_idx, heat_idx, ageing_idx, combo_idx)

    data["sort_key"] = data["Scenario"].apply(sort_key)
    return data.sort_values("sort_key").drop(columns="sort_key")

# ================= UI =================
st.markdown(
    f"<h1 style='font-size:{TITLE_FONT_SIZE}px;'>EV Flexibility in Residential Energy Systems</h1>",
    unsafe_allow_html=True
)

st.markdown(
    """
    A dashboard to analyse and compare the **impact of EV flexibility** under varying technical and behavioural conditions for a residential energy system in Sweden
    """
)

# ============================================================
# ABOUT / HOW TO USE
# ============================================================

with st.expander("ℹ️ About this dashboard & How to use"):

    st.markdown("""
    ### What is this dashboard?

    This is an interactive dashboard which presents results from an optimisation framework
    investigating EV flexibility and its dependence on different factors when coupled with residential energy system. Through this dashboard, the user can toggle between different **charging strategies and electricity markets,
    EV user behaviours, Technologies like PV, BESS and space heating, and the influence of EV battery ageing cost**,
    and compare the results among different KPIs

    ---

    ###  How to use the dashboard?

    **1. Select the year**  
    Explore scenarios representing electricity-market conditions in
    **2022 or 2025** by choosing the **Year**.

    **2. Select Scenarios with/without EV**  
    The user can select results with EV, without EV or Both. Selecting "No" shows the results for scenarios with only the resedential demand. Selecting "Both" compares scenarios with and without EV

    **3. Select the Charging Strategy and/or Markets**  
    Under this filter, the user can choose the charging strategies or electricity market the EV participates in. Charging strategies are **Direct Charging (DC) and Smart Charging (SC)**. 
    Electrity markets considered are **Spot market (Spot), combined spot and FCRN participation (Spot+FCRN), combined spot and FCRD participation (Spot+FCRN) and 
    combined spot, FCRN and FCRD participation (Spot+FCRN+FCRD)**. Apart from this, the **BASE** scenario shows results without an EV in the grid.

    **4. Choose EV user behaviour**  
    Select whether the EV user is **working from the office (WFO), working from
    home (WFH), or following a hybrid working pattern (HYBRID)**

    **5. Select the available technologies**  
    Select different combinations of **solar PV, stationary battery
    storage (BESS), and heating technologies** as part of the residential load

    **6. Select the KPI**  
    By selecting the primary and/or secondary KPI, the user can see the results for the selected scenario


    ---

    ### New to energy systems?

    **EV — Electric Vehicle**  

    **Direct Charging (DC) and Smart Charging (SC)**  
    Different ways in which an EV can be charged. By Direct charging, the EV charges at the maximum attainable capacity at the shortest time. Through Smart charging, the EV adopts a dynamic charging capacity according
    to the real-time electricity prices in the grid.

    **Spot, FCR-N and FCR-D Markets**  
    Different markets where electricity is being bought and sold for different purposes

    **PV — Solar Photovoltaics**  
    Solar panels connected at the residence that generate electricity

    **BESS — Battery Energy Storage System**  
    A stationary battery installed in the at the residence

    **EV Battery Ageing**  
    The EV battery degradation is calculated as ageing (%) over the period of its lifetime


    ---

    ### About this project
    
    This dashboard was developed as part of research on
    **EV flexibility in residential energy systems**.

    **Author:** Sankar Mangalath Ramasan  
    **Affiliation:** Chalmers University of Technology

    📄 **Research publication:** [View publication](https://dx.doi.org/10.2139/ssrn.7403061)

    💻 **Source code:** [GitHub Repository](https://github.com/sankar-mangalam/EV-flexibility-in-Residential-Energy-System)

    Please cite the associated research publication when using results as below:

    *Mangalath Ramasan, Sankar and Sridhar, Araavind and Steen, David and Anh Tuan, Le, To V2G or Not? Assessing EV Flexibility Across Electricity Markets and User Behaviour in Residential Energy Systems. Available at SSRN: http://dx.doi.org/10.2139/ssrn.7403061*
    
    """)

st.divider()

st.sidebar.header("Filters")

year = st.sidebar.selectbox("Year", [2025, 2022])


# ================= ELECTRIC VEHICLE =================
st.sidebar.markdown("### Electric Vehicle (EV)")

ev_selection = st.sidebar.radio(
    "Select if EV is considered in the system",
    ["Yes", "No", "Both"],
    horizontal=True
)


# ================= EV-DEPENDENT FILTERS =================
# Only show these when EV scenarios are included

if ev_selection in ["Yes", "Both"]:

    st.sidebar.markdown("### Charging Strategies and Markets")

    selected_markets = st.sidebar.multiselect(
        "Select Strategy(s)/Market(s)",
        ["DC", "SC", "Spot", "Spot+FCRN", "Spot+FCRD", "Spot+FCRN+FCRD"]
    )

    st.sidebar.markdown("### EV User Behaviour")

    selected_work = st.sidebar.multiselect(
        "Select Work Type(s)",
        ["WFO", "HYBRID", "WFH"]
    )

else:
    selected_markets = []
    selected_work = []


# ================= TECHNOLOGY =================
st.sidebar.markdown("### Technology")

tech_filters = {}

for tech in ["PV", "HEAT", "BESS"]:
    tech_filters[tech] = st.sidebar.radio(
        tech,
        ["All", "With", "Without"],
        horizontal=True
    )


# ================= EV BATTERY AGEING =================
# Only relevant when EV is present

if ev_selection in ["Yes", "Both"]:

    st.sidebar.markdown("### EV battery ageing")

    tech_filters["AGEING"] = st.sidebar.radio(
        "Select if EV battery ageing cost is part of the Objective",
        ["All", "With", "Without"],
        horizontal=True
    )

else:
    # AGEING is irrelevant for BASE scenarios
    tech_filters["AGEING"] = "All"

# ================= KPI SELECTION =================
st.sidebar.markdown("### KPI Selection")

primary_group = st.sidebar.selectbox("Primary Axis Type", list(KPI_GROUPS.keys()),
                                     format_func=lambda x: GROUP_LABELS[x])

primary_kpis = st.sidebar.multiselect("Primary KPIs", KPI_GROUPS[primary_group])

secondary_group = st.sidebar.selectbox("Secondary Axis Type", list(KPI_GROUPS.keys()),
                                       format_func=lambda x: GROUP_LABELS[x])

secondary_kpis = st.sidebar.multiselect("Secondary KPIs", KPI_GROUPS[secondary_group])

EV_ONLY_KPIS = {
    "FCRN Returns",
    "FCRD Returns",

    "EV Calender ageing (%)",
    "EV Cyclic ageing (%)",
    "Total EV ageing (%)",

    "FCRN Participation Hours",
    "FCRD Participation Hours",
    "Spot Import Hours",
    "Spot Export Hours",
    "EV Availability Hours",

    "EV charge Energy (FCRN)",
    "EV discharge Energy (FCRN)",
    "EV charge Energy (FCRD)",
    "EV discharge Energy (FCRD)",
    "Spot Import Energy",
    "Spot Export Energy",

    "FCRN Bid Capacity",
    "FCRDU Bid Capacity",
    "FCRDD Bid Capacity",

    "Average EV SOC",
    "EV Energy Throughput"
}

selected_kpis = primary_kpis + secondary_kpis

if ev_selection == "No":

    unavailable_kpis = [
        kpi
        for kpi in selected_kpis
        if kpi in EV_ONLY_KPIS
    ]

    available_kpis = [
        kpi
        for kpi in selected_kpis
        if kpi not in EV_ONLY_KPIS
    ]

    if unavailable_kpis:
        st.info(
            "No results for the selected scenario"
        )
        st.stop()

    primary_kpis = [
        kpi
        for kpi in primary_kpis
        if kpi not in EV_ONLY_KPIS
    ]

    secondary_kpis = [
        kpi
        for kpi in secondary_kpis
        if kpi not in EV_ONLY_KPIS
    ]

# ================= DATA =================
if ev_selection in ["Yes", "Both"]:

    if not selected_markets:
        st.warning(
            "Select at least one Charging Strategy or Market."
        )
        st.stop()

    if not selected_work:
        st.warning(
            "Select at least one EV User Behaviour."
        )
        st.stop()

data = filter_scenarios(
    df,
    ev_selection,
    selected_markets,
    selected_work,
    tech_filters,
    year
)
data = sort_scenarios(data, tech_filters)

if data.empty:
    st.warning("No scenarios match selection.")
    st.stop()

x_labels = [clean_scenario_name(s, year) for s in data["Scenario"]]

# ================= CHECK IF ANY KPI IS SELECTED =================

has_primary_kpis = len(primary_kpis) > 0
has_secondary_kpis = len(secondary_kpis) > 0
has_any_kpis = has_primary_kpis or has_secondary_kpis

# Do not create any graph until at least one KPI is selected
if not has_any_kpis:
    st.info("Select at least one Primary KPI or Secondary KPI.")
    st.stop()


# ================= CHECK IF COST BREAKUP NEEDED =================
# Cost breakdown appears ONLY when:
#   1. the corresponding axis type is Costs (SEK), AND
#   2. at least one KPI has actually been selected on that axis.

primary_cost_selected = (
    primary_group == "cost"
    and has_primary_kpis
)

secondary_cost_selected = (
    secondary_group == "cost"
    and has_secondary_kpis
)

show_cost_breakup = (
    primary_cost_selected
    or secondary_cost_selected
)


# ================= CREATE SUBPLOTS =================

rows = 2 if show_cost_breakup else 1

fig = make_subplots(
    rows=rows,
    cols=1,
    shared_xaxes=True,
    vertical_spacing=0.08,

    row_heights=(
        [0.6, 0.4]
        if show_cost_breakup
        else [1]
    ),

    specs=(
        [
            [{"secondary_y": True}],
            [{"secondary_y": False}]
        ]
        if show_cost_breakup
        else
        [
            [{"secondary_y": True}]
        ]
    )
)


# ================= KPI GRAPH (ROW 1) =================

# ---------------- PRIMARY KPIs ----------------
if has_primary_kpis:

    for kpi in primary_kpis:

        fig.add_trace(
            go.Bar(
                x=x_labels,
                y=get_kpi(data, kpi),
                name=kpi,

                offsetgroup="cost",
                width=0.6,

                marker_color=KPI_COLORS.get(
                    kpi,
                    "#636EFA"
                ),

                marker_line_color="rgba(80,80,80,0.6)",
                marker_line_width=0.75
            ),

            row=1,
            col=1,
            secondary_y=False
        )


# ---------------- SECONDARY KPIs ----------------
if has_secondary_kpis:

    for kpi in secondary_kpis:

        fig.add_trace(
            go.Scatter(
                x=x_labels,
                y=get_kpi(data, kpi),

                mode="lines+markers",

                name=kpi,

                line=dict(
                    color=KPI_COLORS.get(
                        kpi,
                        "#636EFA"
                    ),
                    width=3
                ),

                marker=dict(
                    color=KPI_COLORS.get(
                        kpi,
                        "#636EFA"
                    ),
                    size=8
                )
            ),

            row=1,
            col=1,
            secondary_y=True
        )


# ================= COST BREAKUP (ROW 2) =================

if show_cost_breakup:

    supplier = data["Supplier Cost"]
    dso = data["DSO Cost"]
    tax = data["Tax Cost"]

    fcrn = -abs(
        data["Total FCRN Returns"]
    )

    fcrd = -abs(
        data["Total FCRD Returns"]
    )

    cost_breakdown_data = {
        "Supplier Cost": supplier,
        "DSO Cost": dso,
        "Tax Cost": tax,
        "FCRN Returns": fcrn,
        "FCRD Returns": fcrd
    }

    for name, values in cost_breakdown_data.items():

        fig.add_trace(
            go.Bar(
                x=x_labels,
                y=values,
                name=name,

                offsetgroup="cost",
                width=0.6,

                marker_color=COST_BREAKUP_COLORS.get(
                    name,
                    "#636EFA"
                ),

                marker_line_color="rgba(80,80,80,0.6)",
                marker_line_width=0.75
            ),

            row=2,
            col=1
        )

    # DOTTED LINES ONLY IN COST SUBPLOT
    for i in range(len(x_labels)):
        fig.add_shape(
            type="line",
            x0=i, x1=i,
            y0=0, y1=1,
            xref=f"x{'' if rows==1 else '2'}",
            yref="paper",
            line=dict(color="black", width=0.2, dash="dot"),
        )

# ================= SHADING + 2-LEVEL GROUPING =================
def get_market(name):
    name = name.upper()
    if "BASE" in name: return "BASE"
    if "DC" in name: return "DC"
    elif "SC" in name: return "SC"
    elif "V2G_FCRN,D" in name: return "Spot+FCRN+FCRD"
    elif "V2G_FCRN" in name: return "Spot+FCRN"
    elif "V2G_FCRD" in name: return "Spot+FCRD"
    elif "V2G" in name: return "Spot"

def get_work(name):
    name = name.upper()
    if "WFO" in name: return "WFO"
    elif "HYBRID" in name: return "HYBRID"
    elif "WFH" in name: return "WFH"

# Market display names
def get_market_label(market):
    return {
        "BASE": "Residential Demand Only",
        "DC": "Direct Charging",
        "SC": "Smart Charging",
        "Spot": "Spot Market",
        "Spot+FCRN": "Spot + FCRN",
        "Spot+FCRD": "Spot + FCRD",
        "Spot+FCRN+FCRD": "Spot + FCRN + FCRD"
    }.get(market, market)

# Base color (for lines)
def get_market_base_color(market):
    return {
        "BASE": "rgb(139,69,19)",
        "DC": "rgb(0,102,204)",
        "SC": "rgb(220,20,60)",
        "Spot": "rgb(34,139,34)",
        "Spot+FCRN": "rgb(255,140,0)",
        "Spot+FCRD": "rgb(138,43,226)",
        "Spot+FCRN+FCRD": "rgb(139,69,19)"
    }.get(market, "rgb(120,120,120)")

# Shading color
def get_market_work_color(market, work):
    base_colors = {
        "BASE": "rgba(139,69,19,{})",
        "DC": "rgba(0,102,204,{})",
        "SC": "rgba(220,20,60,{})",
        "Spot": "rgba(34,139,34,{})",
        "Spot+FCRN": "rgba(255,140,0,{})",
        "Spot+FCRD": "rgba(138,43,226,{})",
        "Spot+FCRN+FCRD": "rgba(139,69,19,{})"
    }

    opacity = {
        "WFO": 0.08,
        "HYBRID": 0.15,
        "WFH": 0.25
    }

    return base_colors.get(market, "rgba(200,200,200,{})").format(opacity.get(work, 0.1))


# ============================================================
# SHADING VERTICAL RANGE
# ============================================================
# Use paper coordinates so shading works even when only the secondary y-axis has data.
# When the cost-breakdown subplot is present, shade only the upper KPI subplot.
if show_cost_breakup:
    shading_y0 = 0.46
    shading_y1 = 1.00
else:
    shading_y0 = 0.00
    shading_y1 = 1.00

# ================= LOOP =================
current_market = None
current_work = None

market_start = 0
work_start = 0

for i, scenario in enumerate(data["Scenario"]):

    # Determine market and work type for EVERY scenario
    m = get_market(scenario)
    w = get_work(scenario)

    # Safety check
    if m is None:
        continue

    # BASE has no EV user behaviour
    if m == "BASE":
        w = ""

    # Initialise first block
    if current_market is None:
        current_market = m
        current_work = w
        market_start = i
        work_start = i

    # =========================================================
    # WORK BLOCK CHANGE
    # =========================================================
    if m != current_market or w != current_work:

        # Add shading for previous work block
        fig.add_shape(
            type="rect",
            x0=work_start - 0.5,
            x1=i - 0.5,
            y0=shading_y0,
            y1=shading_y1,
            xref="x",
            yref="paper",
            fillcolor=get_market_work_color(
                current_market,
                current_work
            ),
            layer="below",
            line_width=0
        )

        color = get_market_base_color(current_market)
        mid = (work_start + i - 1) / 2

        # -----------------------------------------------------
        # Only draw work grouping when there is an EV
        # BASE has no WFO / HYBRID / WFH meaning
        # -----------------------------------------------------
        if current_market != "BASE" and current_work:

            # WORK LINE
            fig.add_shape(
                type="line",
                x0=work_start - 0.5,
                x1=i - 0.5,
                y0=1.02,
                y1=1.02,
                xref="x",
                yref="paper",
                line=dict(
                    color=color,
                    width=2
                )
            )

            # Vertical ticks
            for x in [work_start - 0.5, i - 0.5]:
                fig.add_shape(
                    type="line",
                    x0=x,
                    x1=x,
                    y0=1.00,
                    y1=1.04,
                    xref="x",
                    yref="paper",
                    line=dict(
                        color=color,
                        width=2
                    )
                )

            # WORK LABEL
            fig.add_annotation(
                x=mid,
                y=1.09,
                xref="x",
                yref="paper",
                text=current_work,
                showarrow=False,
                font=dict(
                    size=WORK_LABEL_FONT_SIZE,
                    color=color
                )
            )

        work_start = i

        # =====================================================
        # MARKET BLOCK CHANGE
        # =====================================================
        if m != current_market:

            color = get_market_base_color(current_market)
            mid = (market_start + i - 1) / 2

            # MARKET LINE
            fig.add_shape(
                type="line",
                x0=market_start - 0.5,
                x1=i - 0.5,
                y0=1.10,
                y1=1.10,
                xref="x",
                yref="paper",
                line=dict(
                    color=color,
                    width=2.5
                )
            )

            # Vertical ticks
            for x in [market_start - 0.5, i - 0.5]:
                fig.add_shape(
                    type="line",
                    x0=x,
                    x1=x,
                    y0=1.07,
                    y1=1.13,
                    xref="x",
                    yref="paper",
                    line=dict(
                        color=color,
                        width=2.5
                    )
                )

            # MARKET LABEL
            fig.add_annotation(
                x=mid,
                y=1.19,
                xref="x",
                yref="paper",
                text=get_market_label(current_market),
                showarrow=False,
                font=dict(
                    size=MARKET_LABEL_FONT_SIZE,
                    color=color
                )
            )

            market_start = i
            current_market = m

        current_work = w


# ================= FINAL BLOCK =================
end = len(data)

if end > 0 and current_market is not None:

    # ---------------------------------------------------------
    # FINAL SHADING
    # ---------------------------------------------------------
    fig.add_shape(
        type="rect",
        x0=work_start - 0.5,
        x1=end - 0.5,
        y0=shading_y0,
        y1=shading_y1,
        xref="x",
        yref="paper",
        fillcolor=get_market_work_color(
            current_market,
            current_work
        ),
        layer="below",
        line_width=0
    )

    color = get_market_base_color(current_market)
    mid = (work_start + end - 1) / 2

    # ---------------------------------------------------------
    # FINAL WORK BLOCK
    # Do NOT draw work label for BASE
    # ---------------------------------------------------------
    if current_market != "BASE" and current_work:

        fig.add_shape(
            type="line",
            x0=work_start - 0.5,
            x1=end - 0.5,
            y0=1.02,
            y1=1.02,
            xref="x",
            yref="paper",
            line=dict(
                color=color,
                width=2
            )
        )

        for x in [work_start - 0.5, end - 0.5]:
            fig.add_shape(
                type="line",
                x0=x,
                x1=x,
                y0=1.00,
                y1=1.04,
                xref="x",
                yref="paper",
                line=dict(
                    color=color,
                    width=2
                )
            )

        fig.add_annotation(
            x=mid,
            y=1.09,
            xref="x",
            yref="paper",
            text=current_work,
            showarrow=False,
            font=dict(
                size=WORK_LABEL_FONT_SIZE,
                color=color
            )
        )

    # ---------------------------------------------------------
    # FINAL MARKET BLOCK
    # ---------------------------------------------------------
    mid = (market_start + end - 1) / 2

    fig.add_shape(
        type="line",
        x0=market_start - 0.5,
        x1=end - 0.5,
        y0=1.10,
        y1=1.10,
        xref="x",
        yref="paper",
        line=dict(
            color=color,
            width=2.5
        )
    )

    for x in [market_start - 0.5, end - 0.5]:
        fig.add_shape(
            type="line",
            x0=x,
            x1=x,
            y0=1.07,
            y1=1.13,
            xref="x",
            yref="paper",
            line=dict(
                color=color,
                width=2.5
            )
        )

    fig.add_annotation(
        x=mid,
        y=1.19,
        xref="x",
        yref="paper",
        text=get_market_label(current_market),
        showarrow=False,
        font=dict(
            size=MARKET_LABEL_FONT_SIZE,
            color=color
        )
    )


# ================= LAYOUT =================
fig.update_layout(

    width= 2800,

    margin=dict(
    t=150,
    r=0,#180,
    l=0,#130,
    b=0,#150
    ),

    height=1000 if show_cost_breakup else 800,

    font=dict(
        size=ANNOTATION_FONT_SIZE
    ),

    xaxis=dict(
        tickangle=45,
        tickfont=dict(size=AXIS_TICK_FONT_SIZE)
    ),

    hovermode="x unified",
    barmode="relative",

    hoverlabel=dict(
        font_size=HOVER_FONT_SIZE
    ),

    legend=dict(
        x=1.02,
        y=1.08,
        xanchor="left",
        yanchor="top",
        font=dict(size=LEGEND_FONT_SIZE),
    ),
    
    autosize=True
)

fig.update_xaxes(
    tickfont=dict(size=AXIS_TICK_FONT_SIZE),
    tickangle=-45,
    automargin=True,

    showline=True,
    linewidth=2,
    linecolor="rgba(80,80,80,0.5)"
)

fig.update_yaxes(
    title_text=(
        GROUP_LABELS[primary_group]
        if has_primary_kpis
        else ""
    ),
    title_font=dict(size=AXIS_TITLE_FONT_SIZE),
    tickfont=dict(size=AXIS_TICK_FONT_SIZE),
    row=1,
    col=1,
    automargin=True,

    zeroline=True,
    zerolinewidth=2,
    zerolinecolor="rgba(80,80,80,0.5)"
)

fig.update_yaxes(
    title_text=(
        GROUP_LABELS[secondary_group]
        if has_secondary_kpis
        else ""
    ),
    title_font=dict(size=AXIS_TITLE_FONT_SIZE),
    tickfont=dict(size=AXIS_TICK_FONT_SIZE),
    row=1,
    col=1,
    secondary_y=True,
    automargin=True,

    zeroline=True,
    zerolinewidth=2,
    zerolinecolor="rgba(100,100,100,0.3)"
)

if show_cost_breakup:
    fig.update_yaxes(
        title_text="Cost Breakdown (SEK)",
        title_font=dict(size=AXIS_TITLE_FONT_SIZE),
        tickfont=dict(size=AXIS_TICK_FONT_SIZE),
        row=2,
        col=1,

        zeroline=True,
        zerolinewidth=2,
        zerolinecolor="rgba(80,80,80,0.5)"
    )

st.plotly_chart(fig, use_container_width=1600)

# ============================================================
# FOOTER
# ============================================================

#st.divider()

# st.caption(
# "Please cite the associated research publication when using results as below\n"

# "Mangalath Ramasan, Sankar and Sridhar, Araavind and Steen, David and Anh Tuan, Le, To V2G or Not? Assessing EV Flexibility Across Electricity Markets and User Behaviour in Residential Energy Systems. Available at SSRN: http://dx.doi.org/10.2139/ssrn.7403061"
# )
