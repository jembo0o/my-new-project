# SmartSpend — AI Personal Finance Advisor 

> *An AI-powered tool that analyzes your daily spending habits and gives personalized advice to help you save money and reach your financial goals.*

---

## Background

Managing personal finances is a challenge that millions of people face every day. Many people overspend without realizing it, struggle to save, or simply don't know where their money is going each month. Traditional budgeting apps exist, but they require manual effort and don't give intelligent, personalized recommendations.

**The problem SmartSpend solves:**
- People spend money on habits they are not fully aware of
- It's hard to predict whether you'll reach the end of the month without running out of money
- Generic financial advice doesn't account for individual spending patterns

This is a common and growing problem — especially among young adults and people living in cities with high costs of living. My motivation for this idea is simple: most people want to save more but don't know where to start. AI can bridge that gap by turning raw transaction data into actionable insight.

---

## Data and AI Techniques

### Data Sources
- **Personal bank/card transaction history** — exported as CSV (most banks support this)
- **Public datasets** — e.g. anonymized personal finance datasets on [Kaggle](https://www.kaggle.com/)
- **User input** — monthly income, savings goals, fixed expenses

### AI Techniques

| Technique | Purpose |
|---|---|
| **Classification** | Automatically categorize transactions (food, transport, entertainment, etc.) |
| **Regression** | Predict end-of-month balance based on current spending pace |
| **Clustering** | Group spending patterns to detect unusual or recurring habits |
| **NLP (optional)** | Parse transaction descriptions to improve categorization accuracy |

### Simple Python Demo

```python
import pandas as pd

# Load transaction data
df = pd.read_csv('transactions.csv')

# Simple categorization by keyword
def categorize(description):
    description = description.lower()
    if any(word in description for word in ['restaurant', 'cafe', 'pizza', 'uber eats']):
        return 'Food & Dining'
    elif any(word in description for word in ['uber', 'bolt', 'bus', 'train']):
        return 'Transport'
    elif any(word in description for word in ['netflix', 'spotify', 'cinema']):
        return 'Entertainment'
    else:
        return 'Other'

df['category'] = df['description'].apply(categorize)

# Summarize spending by category
summary = df.groupby('category')['amount'].sum().sort_values(ascending=False)
print(summary)

# Simple prediction: project monthly spending based on first N days
days_passed = 15
total_days = 30
current_spend = df['amount'].sum()
projected = (current_spend / days_passed) * total_days
print(f"\nProjected monthly spending: €{projected:.2f}")
```

---

## How It Is Used

**Who uses it:**
- Individuals who want to understand and improve their spending habits
- Young adults managing their first salary or student budget
- Anyone with a financial goal (saving for a trip, a car, an emergency fund)

**Context:**
- The user exports their bank transaction history as a CSV file
- SmartSpend processes it and displays a dashboard with spending breakdown, trends, and predictions
- The AI provides simple, friendly recommendations: *"You spent 35% more on dining out this month compared to last month."*

**Who is affected:**
- **Users** benefit directly from better financial awareness
- **Banks/fintech companies** could integrate this as a value-added feature
- **Privacy** is an important concern — all data should be processed locally or with strong encryption, and never shared with third parties without consent

---

## Challenges

SmartSpend is not a complete financial solution. It has important limitations:

- **Data quality** — transaction descriptions from banks are often cryptic or inconsistent, making automatic categorization imperfect
- **No real-time data** — the tool works with exported snapshots, not live account feeds
- **Cultural differences** — spending categories and habits vary widely across countries and demographics
- **Privacy risks** — financial data is highly sensitive; any real deployment requires strong security measures
- **No financial advice** — SmartSpend gives observations, not professional financial guidance. It cannot replace a financial advisor
- **Behavioral change is hard** — knowing you overspend doesn't automatically mean you'll change

---

## What Next

With more time and resources, SmartSpend could grow into:

-  **A mobile app** with real-time bank API integration (Open Banking / PSD2 in Europe)
-  **A chatbot interface** — ask questions like *"How much did I spend on food last month?"*
-  **Goal tracking** — set a savings goal and get weekly progress updates
-  **Smart alerts** — notify when you're about to exceed a category budget
-  **Multi-currency support** for people who travel or work internationally
-  **Peer comparison** — anonymized benchmarks: *"You spend less on transport than 70% of people in your city"*

---

## Acknowledgments

- Inspiration from the [Elements of AI — Building AI](https://buildingai.elementsofai.com/) course by Reaktor and University of Helsinki
- Public finance datasets: [Kaggle Personal Finance Datasets](https://www.kaggle.com/search?q=personal+finance)
- Python libraries: [pandas](https://pandas.pydata.org/), [scikit-learn](https://scikit-learn.org/), [matplotlib](https://matplotlib.org/)
- Open Banking standard: [PSD2 / Open Banking EU](https://www.openbanking.org.uk/)

---

*This project was created as part of the Building AI course final project.*
