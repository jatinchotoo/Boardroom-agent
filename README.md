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
