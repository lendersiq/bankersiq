# BankersIQ Agent Instructions

## 🤖 LTV Agent Overview

The **IQ Banking Intelligence Agent** is live at [https://bankersiq.com/agent/ltv/](https://bankersiq.com/agent/ltv/)

This is an **AI agent** for banking intelligence, not a traditional API. It provides financial product lifetime value calculations with AI reasoning and transparency.

---

## 🔒 Authentication (API Key)

**POST requests require an API key.**  
**GET requests (status check) do not.**

### Setting Your Key

In `config.php` (already included at top of the agent code):

### Using the Key

When making a request:

```bash
curl -X POST https://bankersiq.com/agent/ltv/   -H "Content-Type: application/json"   -H "X-API-Key: AgentIsFreeForNow"   -d '{"value": 50000, "type": "savings"}'
```

---

## 🧠 Agentic Features

**Starting with:**
- Provides reasoning and explanations for calculations  
- Shows step-by-step financial logic  
- Adapts to different financial product types  
- Offers transparent decision-making processes  
- Focuses on intelligence and insight, not just data  

---

## 🚀 Quick Start

### Agent Status Check
```bash
curl https://bankersiq.com/agent/ltv/
```

### Calculate Financial Product Lifetime Value
```bash
curl -X POST https://bankersiq.com/agent/ltv/   -H "Content-Type: application/json"   -H "X-API-Key: AgentIsFreeForNow"   -d '{"value": 50000, "type": "savings"}'
```

---

## 📊 Supported Financial Products

| Product     | Life      | Rate | Key Features                          |
|-------------|-----------|------|---------------------------------------|
| **Checking** | 10 years | 0%   | $12/month fees, 3% funding credit     |
| **Savings**  | 10 years | 0%   | No fees, 3% funding credit            |
| **CD**       | 5 years  | 2.5% | 0.5% early withdrawal penalty         |
| **Loans**    | 5 years  | WSJ Prime Rate | Commercial loans, 3% COF |

---

## 💡 Agent Intelligence Features

### Funding Credit Analysis
- **Deposits:** Show 3% annual funding credit (based on market rate) [revenue]  
- **Loans:** Include 3% cost of funds (based on market rate) [expense]  
- **Transparency:** All calculations include funding credit details  

### Agent Reasoning
- **Explanations:** Each response includes reasoning  
- **Step-by-step:** Optional detailed calculation breakdowns  
- **Context-aware:** Different logic for different product types  

---

## 🔧 Example Agent Interactions

### 1. Checking Account Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/   -H "Content-Type: application/json"   -H "X-API-Key: AgentIsFreeForNow"   -d '{"value": 10000, "type": "checking"}'
```
---

## 📊 Checking Supported Arguments
| Argument ID | Description |
|-------------|-----------|
| rate | annual interest rate |
| fundingRate | credit for funding (annual rate) |
| life | expected life in years |
| monthlyFees | monthly service fee revenue |
| transactionFees | monthly checking transaction fee revenue |
| operatingCost | annual operating costs |
| discountRate | discount rate for present value calculation |
| compoundInterest | compound the interest monthly (true or false) | 

---

**Expected Response:**
```json
{
  "value": 10000,
  "type": "checking",
  "results": {
    "pvFundingCredit": "$2,300.12",
    "pvInterestExpense": "$0.00",
    "pvFeeIncome": "$1,200.00",
    "pvOperatingCosts": "$1,382.10",
    "lifetimeValue": "$2,118.02"
  },
  "explanation": "Checking account lifetime value: 0% rate, $12 monthly fees, 10-year analysis (includes funding credit)"
}
```

---

### 2. Savings Account Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/   -H "Content-Type: application/json"   -H "X-API-Key: AgentIsFreeForNow"   -d '{"value": 50000, "type": "savings"}'
```

---

## 📊 Savings Supported Arguments
| Argument ID | Description |
|-------------|-----------|
| rate | annual interest rate |
| fundingRate | credit for funding (annual rate) |
| life | expected life in years |
| monthlyFees | monthly service fee revenue |
| transactionFees | monthly savings transaction fee revenue |
| operatingCost | annual operating costs |
| discountRate | discount rate for present value calculation |
| compoundInterest | compound the interest monthly (true or false) | 

---

**Expected Response:**
```json
{
  "value": 50000,
  "type": "savings",
  "results": {
    "pvFundingCredit": "$13,259.80",
    "pvInterestExpense": "$0.00",
    "pvFeeIncome": "$0.00",
    "pvOperatingCosts": "$0.00",
    "lifetimeValue": "$13,259.80"
  },
  "explanation": "Savings account lifetime value: 0% compound rate, 10-year analysis (includes funding credit)"
}
```

---

### 3. CD Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/   -H "Content-Type: application/json"   -H "X-API-Key: AgentIsFreeForNow"   -d '{"value": 25000, "type": "cd"}'
```

---

## 📊 CD Supported Arguments
| Argument ID | Description |
|-------------|-----------|
| rate | annual interest rate |
| fundingRate | credit for funding (annual rate) |
| life | expected life in years |
| monthlyFees | monthly service fee revenue (rare - default is $0) |
| operatingCost | annual operating costs |
| discountRate | discount rate for present value calculation |
| compoundInterest | compound the interest monthly (true or false) | 

---

**Expected Response:**
```json
{
  "value": 25000,
  "type": "cd",
  "results": {
    "pvFundingCredit": "$3,484.37",
    "pvInterestExpense": "$3,285.21",
    "pvFeeIncome": "$0.00",
    "pvOperatingCosts": "$0.00",
    "lifetimeValue": "$199.16",
    "endingBalanceIfCompounded": "$28,285.21"
  },
  "explanation": "CD lifetime value: 2.5% rate, 5-year term, 0.5% early withdrawal penalty (includes funding credit)"
}
```

---

### 4. Loan Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/   -H "Content-Type: application/json"   -H "X-API-Key: AgentIsFreeForNow"   -d '{"value": 1000000, "type": "loans"}'
```

---

## 📊 Loan Supported Arguments
| Argument ID | Description |
|-------------|-----------|
| loanType | specify type of loan (consumer or commercial) |
| rate | annual interest rate |
| costOfFunds | cost of funds rate (annual rate) |
| life | expected life in years |
| Amortization | Amortization period in years |
| monthlyFees | monthly fee revenue (rare) |
| operatingCost | annual operating costs |
| upfrontCosts | other upfront costs |
| upfrontFeeIncome | upfront fee income |
| discountRate | discount rate for present value calculation |
| compoundInterest | compound the interest monthly (true or false) | 

---


**Expected Response:**
```json
{
  "value": 1000000,
  "type": "loans",
  "results": {
    "pvInterestIncome": "$326,491.11",
    "pvCostOfFunds": "$131,254.88",
    "pvFeeIncome": "$0.00",
    "pvOperatingCosts": "$0.00",
    "lifetimeValue": "$195,236.23",
    "remainingBalance": "$899,320.87",
    "monthlyPayment": "$6,443.01"
  },
  "explanation": "Commercial loan lifetime value calculation: 5-year term, 25-year amortization, 6% rate, 3% COF, 2.5% discount rate"
}
```

---

## 🧮 Agent Calculation Logic

### Deposit Products (Checking, Savings, CD)
- **Funding Credit:** 3% annual (bank can lend these dollars, so this credit should be applied)  
- **Interest Paid:** Expense to bank (reduces lifetime value)  
- **Fees:** Revenue to bank (increases lifetime value)  
- **Operating Costs:** Monthly expenses reduce value  
- **Lifetime Value Formula:** PV(Funding Credit) - PV(Interest) + PV(Fees) - PV(Costs)  

### Loan Products
- **Interest Earned:** Revenue to bank (increases lifetime value)  
- **Cost of Funds:** 3% annual expense (reduces lifetime value)  
- **Origination Costs:** Subtracted at t=0  
- **Upfront Fees:** Added at t=0  
- **Lifetime Value Formula:** NPV(Interest Income − Cost of Funds + Fees − Operating Costs) − Upfront Costs + Upfront Fees  

---

## 🔍 Agent Validation

The agent validates inputs and provides helpful error messages:

```json
{
  "error": "Invalid type: invalid. Valid types are: checking, savings, cd, loans"
}
```

---

## 📈 Agent Capabilities

- **Multi-product analysis:** Handles all major banking products  
- **Realistic economics:** Proper funding credit and cost modeling  
- **Transparent reasoning:** Shows how calculations are derived  
- **Agent-like responses:** Explanations and context, not just numbers  
- **Production ready:** Deployed and accessible via HTTPS  

---

## 🌐 Integration Examples

### JavaScript/Node.js
```javascript
const response = await fetch('https://bankersiq.com/agent/ltv/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'X-API-Key': 'AgentIsFreeForNow'
  },
  body: JSON.stringify({
    value: 50000,
    type: 'savings'
  })
});

const result = await response.json();
console.log(result.explanation);
console.log('Lifetime Value:', result.results.lifetimeValue);
```

### Python
```python
import requests
import json

response = requests.post('https://bankersiq.com/agent/ltv/', 
  headers={
    'Content-Type': 'application/json',
    'X-API-Key': 'AgentIsFreeForNow'
  },
  data=json.dumps({
    'value': 50000,
    'type': 'savings'
  })
)

result = response.json()
print(result['explanation'])
print(f"Lifetime Value: {result['results']['lifetimeValue']}")
```

### PHP
```php
$data = [
    'value' => 50000,
    'type' => 'savings'
];

$options = [
    'http' => [
        'header' => "Content-Type: application/json
X-API-Key: AgentIsFreeForNow
",
        'method' => 'POST',
        'content' => json_encode($data)
    ]
];

$context = stream_context_create($options);
$result = file_get_contents('https://bankersiq.com/agent/ltv/', false, $context);
$response = json_decode($result, true);

echo $response['explanation'] . "
";
echo "Lifetime Value: " . $response['results']['lifetimeValue'] . "
";
```

---

## 🎯 Agent Endpoints

- **Agent Status:** `GET https://bankersiq.com/agent/ltv/`  
- **Agent Calculations:** `POST https://bankersiq.com/agent/ltv/`

---

## 🔒 Security & Reliability

- **HTTPS:** All communications encrypted  
- **API Key Required:** All POST requests must include `X-API-Key`  
- **Input Validation:** Comprehensive error handling  
- **Production Ready:** Deployed on reliable hosting  
- **Agent Intelligence:** Transparent reasoning and explanations  

---

This agent provides banking intelligence with reasoning and transparency.  
Access it at [https://bankersiq.com/agent/ltv/](https://bankersiq.com/agent/ltv/) for all your financial product lifetime value calculations.
