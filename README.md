boardroom-agent/
├── README.md
├── requirements.txt
├── app.py
├── agents.py
├── finance_model.py
├── sample_input.json

streamlit
langchain
google-generativeai
pandas

def calculate_runway(burn_rate, cash_reserve):
    return round(cash_reserve / burn_rate, 2)

def forecast_arr_growth(arr, growth_rate, months=12):
    return [arr * ((1 + growth_rate) ** m) for m in range(months)]

def token_liquidity_risk(token_price, treasury_allocation):
    native_token_pct = treasury_allocation.get("native_token", 0)
    if native_token_pct > 40 and token_price < 0.5:
        return "High liquidity risk"
    return "Acceptable"

    from finance_model import calculate_runway, forecast_arr_growth, token_liquidity_risk

def run_scenario(data):
    arr = data["ARR"]
    churn = data["churn_rate"]
    cac = data["CAC"]
    burn = data["burn_rate"]
    token_price = data["token_price"]
    treasury = data["treasury_allocation"]
    jurisdiction = data["jurisdiction"]

    cash_reserve = 500000  # mock value
    runway = calculate_runway(burn, cash_reserve)
    arr_forecast = forecast_arr_growth(arr, 0.05)
    liquidity_risk = token_liquidity_risk(token_price, treasury)

    return {
        "runway_months": runway,
        "arr_forecast": arr_forecast,
        "liquidity_risk": liquidity_risk,
        "jurisdiction": jurisdiction
    }

    import streamlit as st
import json
from agents import run_scenario

st.title("🧠 Boardroom Agent: AI CFO Assistant")

uploaded_file = st.file_uploader("Upload JSON scenario data", type="json")

if uploaded_file:
    data = json.load(uploaded_file)
    st.subheader("📊 Input Data")
    st.json(data)

    if st.button("Run Scenario"):
        result = run_scenario(data)
        st.subheader("📈 Scenario Results")
        st.write(result)

        st.subheader("🧠 Board Summary")
        st.write("Gemini-generated summary would appear here...")

        st.subheader("🛡️ Compliance Check")
        st.write(f"Jurisdiction: {result['jurisdiction']}")
        st.write(f"Liquidity Risk: {result['liquidity_risk']}")

        st.subheader("👨‍🏫 Mentorship Insight")
        st.write("Explain runway and ARR forecast to a junior analyst...")

        {
  "ARR": 1200000,
  "churn_rate": 0.08,
  "CAC": 500,
  "burn_rate": 85000,
  "token_price": 0.42,
  "treasury_allocation": {
    "stablecoins": 60,
    "native_token": 30,
    "ETH": 10
  },
  "jurisdiction": "Switzerland"
}

## 🧠 Conceptual Overview

**Boardroom Agent** is a **LangGraph-powered multi-agent system** that simulates how a CFO would think, plan, and communicate. It’s designed to:

- Run financial scenarios (SaaS + tokenized assets)  
- Generate board-level summaries using AI  
- Flag compliance risks based on jurisdiction  
- Mentor junior analysts with coaching-style insights

This isn’t just a dashboard — it’s a **thinking tool** that blends finance, AI, and leadership.

---

## ⚙️ How It Works (Step-by-Step)

### 1. **User Uploads Financial Data**
- You upload a JSON file with key metrics like ARR, churn, CAC, burn rate, token price, and treasury allocation.

### 2. **LangGraph Agent Flow Activates**
Each agent performs a specific role:

| Agent | What It Does |
|-------|--------------|
| `DataIngestorAgent` | Parses and validates the uploaded data |
| `ScenarioPlannerAgent` | Runs Python-based financial models (e.g., runway, ARR forecast) |
| `NarrativeGeneratorAgent` | Uses Gemini API to write a board summary |
| `ComplianceCheckerAgent` | Flags risks based on jurisdiction and treasury mix |
| `MentorshipAgent` | Explains the scenario in coaching tone for junior analysts |

### 3. **Streamlit Front-End Displays Results**
- You see:
  - 📈 Scenario metrics (runway, forecasts, risks)  
  - 🧠 Board summary (AI-generated)  
  - 🛡️ Compliance alerts  
  - 👨‍🏫 Mentorship insights

---

## 💡 Strategic Impact

This project shows recruiters and companies that you:
- Think like a CFO  
- Build tools that simulate executive decision-making  
- Understand both SaaS and tokenized finance  
- Can mentor others through AI-powered interfaces  
- Know how to integrate LangGraph, Gemini, Python, and Streamlit

