# BankersIQ Agent Instructions

## 🤖 LTV Agent Overview

The **IQ Banking Intelligence Agent** is live at [https://bankersiq.com/agent/ltv/](https://bankersiq.com/agent/ltv/)

This is an **AI agent** for banking intelligence, not a traditional API. It provides financial product lifetime value calculations with agent-like reasoning and transparency.

## 🧠 Agentic Features

**Starting with:**
- Provides reasoning and explanations for calculations
- Shows step-by-step financial logic
- Adapts to different financial product types
- Offers transparent decision-making processes
- Focuses on intelligence and insight, not just data

## 🚀 Quick Start

### Agent Status Check
```bash
curl https://bankersiq.com/agent/ltv/
```

### Calculate Financial Product Lifetime Value
```bash
curl -X POST https://bankersiq.com/agent/ltv/ \
  -H "Content-Type: application/json" \
  -d '{"value": 50000, "type": "savings"}'
```

## 📊 Supported Financial Products

| Product | Life | Rate | Key Features |
|---------|------|------|--------------|
| **Checking** | 10 years | 0% | $12/month fees, 3% funding credit |
| **Savings** | 10 years | 0% | No fees, 3% funding credit |
| **CD** | 5 years | 2.5% | 0.5% early withdrawal penalty |
| **Loans** | 5 years | Wallstreet Journal Prime Rate | Commercial loans, 3% COF |

## 💡 Agent Intelligence Features

### Funding Credit Analysis
- **Deposits:** Show 3% annual funding credit (revenue)
- **Loans:** Include 3% cost of funds (expense)
- **Transparency:** All calculations include funding credit details

### Agent Reasoning
- **Explanations:** Each response includes reasoning
- **Step-by-step:** Optional detailed calculation breakdowns
- **Context-aware:** Different logic for different product types

## 🔧 Example Agent Interactions

### 1. Checking Account Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/ \
  -H "Content-Type: application/json" \
  -d '{"value": 10000, "type": "checking"}'
```

**Expected Response:**
```json
{
  "value": 10000,
  "type": "checking",
  "results": {
    "monthlyFundingCredit": 25,
    "fundingCreditRate": 3.0,
    "fundingCreditAnnual": 300,
    "lifetimeValue": 1379.02
  },
  "explanation": "Checking account lifetime value: 0% rate, $12 monthly fees, 10-year analysis (includes funding credit)"
}
```

### 2. Savings Account Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/ \
  -H "Content-Type: application/json" \
  -d '{"value": 50000, "type": "savings"}'
```

**Expected Response:**
```json
{
  "value": 50000,
  "type": "savings",
  "results": {
    "totalFundingCredit": 13259.8,
    "fundingCreditRate": 3.0,
    "fundingCreditAnnual": 1500,
    "lifetimeValue": 24309.63
  },
  "explanation": "Savings account lifetime value: 0% compound rate, 10-year analysis (includes funding credit)"
}
```

### 3. CD Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/ \
  -H "Content-Type: application/json" \
  -d '{"value": 25000, "type": "cd"}'
```

**Expected Response:**
```json
{
  "value": 25000,
  "type": "cd",
  "results": {
    "maturityValue": 28285.21,
    "totalInterest": 3285.21,
    "fundingCreditRate": 3.0,
    "fundingCreditAnnual": 750,
    "lifetimeValue": 3484.37
  },
  "explanation": "CD lifetime value: 2.5% rate, 5-year term, 0.5% early withdrawal penalty (includes funding credit)"
}
```

### 4. Loan Analysis
```bash
curl -X POST https://bankersiq.com/agent/ltv/ \
  -H "Content-Type: application/json" \
  -d '{"value": 1000000, "type": "loans"}'
```

**Expected Response:**
```json
{
  "value": 1000000,
  "type": "loans",
  "results": {
    "monthlyPayment": 6443.01,
    "balloonPayment": 899320.87,
    "totalPayments": "$433,684.12",
    "averageLife": 5,
    "lifetimeValue": 22398.82
  },
  "explanation": "Commercial loan lifetime value calculation: 5-year term, 25-year amortization, 6% rate, 3% COF, 2.5% discount rate"
}
```

## 🧮 Agent Calculation Logic

### Deposit Products (Checking, Savings, CD)
- **Funding Credit:** 3% annual (bank can lend these dollars, so this credit should be applied)
- **Interest Paid:** Expense to bank (reduces lifetime value)
- **Fees:** Revenue to bank (increases lifetime value)
- **Lifetime Value Formula:** PV(Funding Credit) - PV(Interest) - PV(Fees) + Initial Balance

### Loan Products
- **Interest Earned:** Revenue to bank (increases lifetime value)
- **Cost of Funds:** 3% annual expense (reduces lifetime value)
- **Lifetime Value Formula:** PV(Payments) + PV(Balloon) - Principal - PV(Costs)

## 🔍 Agent Validation

The agent validates inputs and provides helpful error messages:

```json
{
  "error": "Invalid type: invalid. Valid types are: checking, savings, cd, loans"
}
```

## 📈 Agent Capabilities

- **Multi-product analysis:** Handles all major banking products
- **Realistic economics:** Proper funding credit and cost modeling
- **Transparent reasoning:** Shows how calculations are derived
- **Agent-like responses:** Explanations and context, not just numbers
- **Production ready:** Deployed and accessible via HTTPS

## 🌐 Integration Examples

### JavaScript/Node.js
```javascript
const response = await fetch('https://bankersiq.com/agent/ltv/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    value: 50000,
    type: 'savings'
  })
});

const result = await response.json();
console.log(result.explanation);
console.log('lifetime Value:', result.results.lifetimeValue);
```

### Python
```python
import requests
import json

response = requests.post('https://bankersiq.com/agent/ltv/', 
  headers={'Content-Type': 'application/json'},
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
        'header' => "Content-Type: application/json\r\n",
        'method' => 'POST',
        'content' => json_encode($data)
    ]
];

$context = stream_context_create($options);
$result = file_get_contents('https://bankersiq.com/agent/ltv/', false, $context);
$response = json_decode($result, true);

echo $response['explanation'] . "\n";
echo "Lifetime Value: " . $response['results']['lifetimeValue'] . "\n";
```

## 🎯 Agent Endpoints

- **Agent Status:** `GET https://bankersiq.com/agent/ltv/`
- **Agent Calculations:** `POST https://bankersiq.com/agent/ltv/`

## 🔒 Security & Reliability

- **HTTPS:** All communications encrypted
- **Input Validation:** Comprehensive error handling
- **Production Ready:** Deployed on reliable hosting
- **Agent Intelligence:** Transparent reasoning and explanations

This agent provides banking intelligence with the reasoning and transparency. Access it at [https://bankersiq.com/agent/ltv/](https://bankersiq.com/agent/ltv/) for all your financial product lifetime value calculations.
