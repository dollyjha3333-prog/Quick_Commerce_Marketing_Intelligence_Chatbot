Absolutely. Here is the **complete README.md in one place**, ready to copy directly into your GitHub repository.

````markdown
# Q-Commerce Marketing Intelligence Chatbot

An AI-powered marketing intelligence chatbot built for quick-commerce analysis. The system combines campaign performance, keyword-level advertising metrics, SKU-level sales, inventory availability, and Days of Inventory (DOI) into a conversational analytics workflow.

The chatbot is designed to answer practical marketing and inventory questions and convert performance data into specific, actionable recommendations.

> **Note:** This project uses synthetic/dummy data created for demonstration and portfolio purposes. The analysis does not represent actual performance data from any company or platform.

---

## Project Overview

Quick-commerce marketing teams need to evaluate advertising efficiency while simultaneously monitoring product availability and inventory risk.

Looking at ROAS alone can miss important operational issues. A campaign may have poor returns because of inefficient keywords, while a high-performing SKU may require immediate replenishment because of low inventory.

This project brings these dimensions together into a single analytical chatbot.

The system analyzes:

- Overall marketing performance
- Campaign-level ROAS
- Keyword-level ROAS
- Advertising spend and revenue
- Keyword-level impressions
- Bleeding and high-performing keywords
- SKU-level GMV
- Stock on hand
- Average daily sales
- Days of Inventory (DOI)
- Inventory risk
- Monday morning action priorities

The chatbot then uses this prepared analytical context to answer business questions conversationally.

---

## Business Problem

Marketing teams operating on quick-commerce platforms need to make decisions such as:

- Which campaigns are consuming budget without sufficient returns?
- Which keywords should have their bids reduced?
- Which keywords should be paused?
- Which keywords are generating strong returns?
- Which SKUs are approaching stockout?
- Which products require immediate purchase orders?
- How should marketing and inventory priorities be coordinated?

Traditional dashboards can provide the numbers, but they often require the analyst to manually connect multiple metrics.

This project creates a conversational interface that allows users to ask these questions directly.

---

## Key Features

### 1. Marketing Performance Analysis

The system calculates and summarizes:

- Total ad spend
- Total ad revenue
- Total GMV
- ROAS
- ROI
- Campaign-level performance

ROAS is calculated as:

```text
ROAS = Ad Revenue / Ad Spend
````

ROI is calculated as:

```text
ROI = Total GMV / Ad Spend
```

---

### 2. Campaign-Level Diagnostics

Campaigns are evaluated using spend, revenue, and ROAS.

The project uses a ROAS threshold to identify underperforming campaigns:

```text
ROAS < 1.5x  → Low ROAS
ROAS ≥ 1.5x  → Good
```

This allows the chatbot to identify campaigns where advertising budget may require optimization.

---

### 3. Keyword-Level ROAS Analysis

The system evaluates individual advertising keywords using:

* Keyword
* Campaign
* Match type
* Spend
* Revenue
* Impressions
* ROAS
* Status

The chatbot distinguishes between:

**Bleeding keywords**

```text
Spend > 0 AND ROAS < 1.5x
```

and:

**Good-performing keywords**

```text
ROAS ≥ 1.5x
```

This allows recommendations to move from campaign-level analysis to individual keyword-level actions.

---

### 4. Bid Optimization Recommendations

The chatbot provides specific actions for underperforming keywords.

Recommendations can include:

* Decrease bid
* Pause keyword
* Maintain bid
* Increase bid

Recommendations are supported by the relevant performance metrics and business reasoning.

Example questions:

```text
Which keywords are bleeding budget?

Give me specific bid recommendations for the top bleeding keywords.

Which keywords are performing well?
```

---

### 5. Inventory and Days of Inventory Analysis

The project combines stock on hand with average daily sales to calculate Days of Inventory.

```text
DOI = Stock on Hand / Average Daily Sales
```

Inventory is categorized as:

```text
DOI < 3 days       → CRITICAL
DOI 3–7 days       → WARNING
DOI > 7 days       → SAFE
```

The chatbot uses these categories to identify products that may require replenishment.

---

### 6. Stockout Risk Detection

The chatbot can answer questions such as:

```text
Which SKUs are at stockout risk this week?
```

For each SKU, the analysis considers:

* Current stock
* Weekly GMV
* Average daily sales
* Days of Inventory
* Inventory risk
* Recommended action

Critical inventory situations can trigger recommendations to raise a purchase order immediately.

---

### 7. Conversational Memory

The chatbot maintains conversation history using LangChain message objects.

This allows follow-up questions to reference information from previous interactions.

For example:

```text
User:
Which campaigns are bleeding budget?

Bot:
Provides campaign-level analysis.

User:
Give me specific bid recommendations.

Bot:
Uses the previous analytical context to provide keyword-level recommendations.
```

The conversation can also be reset using the reset functionality.

---

## Example Business Questions

The chatbot can answer questions such as:

```text
What is our overall ROAS and ROI on Zepto this week?

Which campaigns are bleeding budget?

Give me specific bid recommendations for the top bleeding keywords.

Which SKUs are at stockout risk this week?

Which products are safe from an inventory perspective?

Which keywords are generating the best ROAS?

Based on everything you know, give me a Monday morning action plan in priority order.
```

---

## Monday Morning Action Planning

One of the main objectives of the chatbot is to move beyond reporting and provide a prioritized action plan.

The chatbot combines:

1. Inventory risk
2. Zero-revenue keywords
3. Low-ROAS keywords
4. High-performing keywords
5. Budget reallocation opportunities

The resulting recommendations are organized by urgency and business impact.

The project demonstrates an action framework such as:

```text
Priority 1: Prevent Critical Stockout

Priority 2: Cut Pure Ad Waste

Priority 3: Reduce Bids on Bleeding Keywords

Priority 4: Reallocate Budget to Proven Winners
```

This turns the chatbot from a simple question-answering system into a decision-support tool.

---

## Data

This project uses **synthetic/dummy data** created specifically for demonstration and portfolio purposes.

The data represents a simulated quick-commerce environment covering marketing, sales, inventory, and keyword performance.

### Inventory Data

The inventory dataset includes fields such as:

* City
* SKU Name
* SKU Code
* SKU Category
* SKU Sub Category
* Brand Name
* Units

Example cities include:

* Mumbai
* Delhi
* Bengaluru
* Hyderabad
* Pune

---

### Sales Data

The sales dataset includes:

* Sales Date
* SKU Name
* SKU ID
* City
* Brand Name
* Manufacturer Name
* SKU Category
* Quantity
* GMV

The project uses a seven-day sales period to calculate sales velocity and inventory risk.

---

### Marketing Data

The marketing dataset includes:

* Date
* Brand ID
* Brand Name
* Revenue
* Spends

---

### Keyword Data

The keyword dataset includes:

* Campaign Name
* Keyword Name
* Keyword Match Type
* Spend
* Revenue
* Impressions
* Status

These fields are used to evaluate keyword-level advertising efficiency and identify opportunities for bid optimization.

---

## Analytical Workflow

```text
                 ┌─────────────────────┐
                 │   Synthetic Data    │
                 └──────────┬──────────┘
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
          ▼                 ▼                 ▼
     Inventory           Sales           Marketing
       Data              Data              Data
          │                 │                 │
          └────────────┬────┴───────┬─────────┘
                       │            │
                       ▼            ▼
                  DOI Analysis   ROAS Analysis
                       │            │
                       ▼            ▼
                  Stock Risk    Campaign Analysis
                                    │
                                    ▼
                              Keyword Analysis
                                    │
                       ┌────────────┴────────────┐
                       │                         │
                       ▼                         ▼
                Bleeding Keywords          Good Keywords
                       │                         │
                       └────────────┬────────────┘
                                    │
                                    ▼
                           Analytical Summary
                                    │
                                    ▼
                             LLM Context
                                    │
                                    ▼
                           LangChain + Gemini
                                    │
                                    ▼
                         Conversational Chatbot
                                    │
                                    ▼
                         Business Recommendations
```

---

## Tech Stack

### Programming

* Python
* Pandas
* NumPy

### AI / LLM

* Google Gemini API
* LangChain
* LangChain Core

### Analytics

* Marketing analytics
* ROAS analysis
* ROI analysis
* Campaign analysis
* Keyword performance analysis
* Inventory analytics
* Days of Inventory calculation
* Stockout risk analysis

### Environment

* Google Colab
* Python

---

## Project Structure

```text
q-commerce-marketing-intelligence-chatbot/
│
├── chatbot.py
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Installation

Clone the repository:

```bash
git clone <your-repository-url>
cd q-commerce-marketing-intelligence-chatbot
```

Install the required dependencies:

```bash
pip install -r requirements.txt
```

---

## API Key Setup

The project uses the Google Gemini API.

The API key should **not** be hard-coded or committed to GitHub.

Use an environment variable instead:

```python
import os

GOOGLE_API_KEY = os.getenv("GOOGLE_API_KEY")
```

For Google Colab, the API key can be stored securely using **Colab Secrets**.

### Important

Never commit an actual API key to the repository.

If an API key has previously been exposed publicly, revoke it and generate a new one.

---

## Running the Project

Run the Python script:

```bash
python chatbot.py
```

The project workflow includes:

1. Creating the synthetic datasets
2. Calculating marketing metrics
3. Calculating campaign ROAS
4. Identifying bleeding keywords
5. Identifying high-performing keywords
6. Calculating Days of Inventory
7. Classifying inventory risk
8. Building the analytical summary
9. Preparing the LLM context
10. Starting the conversational chatbot

---

## Example Output

### Overall Performance

```text
Total Ad Spend
Total Ad Revenue
Total GMV
ROAS
ROI
```

### Campaign Performance

```text
Campaign Name
Spend
Revenue
ROAS
Performance Status
```

### Keyword Analysis

```text
Campaign
Keyword
Match Type
Spend
Revenue
ROAS
Status
```

### Inventory Analysis

```text
SKU
Stock on Hand
Average Daily Sales
DOI
Risk
```

---

## Example Interaction

### User

```text
Which campaigns are bleeding budget?
```

### Chatbot

The chatbot identifies campaigns below the defined ROAS threshold and explains their spend, revenue, ROAS, and recommended optimization direction.

---

### User

```text
Which SKUs are at stockout risk this week?
```

### Chatbot

The chatbot evaluates current stock against sales velocity and reports critical, warning, and safe SKUs using the DOI framework.

---

### User

```text
Based on everything you just told me, give me a Monday morning action plan in priority order.
```

### Chatbot

The chatbot combines marketing and inventory analysis to produce a prioritized action plan covering:

* Critical stock replenishment
* Zero-revenue keyword waste
* Low-ROAS keyword optimization
* Budget reallocation toward stronger keywords

---

## Design Approach

The chatbot does not rely on the LLM to independently calculate all business metrics from raw data.

Instead, the analytical pipeline first transforms the datasets into structured business-level summaries.

These summaries are then provided to the chatbot as analytical context.

The overall architecture follows:

```text
Raw Data
    ↓
Data Processing
    ↓
Business Metrics
    ↓
Analytical Summary
    ↓
LLM Context
    ↓
User Question
    ↓
Conversational Response
    ↓
Business Recommendation
```

This approach keeps the chatbot grounded in the analytical framework defined by the project while allowing the LLM to handle natural-language interaction and recommendation generation.

---

## Business Decision Framework

The chatbot follows a structured analytical hierarchy:

```text
1. Overall Performance
          ↓
2. Campaign Performance
          ↓
3. Keyword Performance
          ↓
4. Inventory Risk
          ↓
5. Recommended Action
```

This framework connects reported metrics to practical business actions.

---

## Limitations

This project is a portfolio prototype built using synthetic/dummy data.

It does not currently represent a production deployment or a live connection to a quick-commerce platform.

The project does not include:

* Live platform API integration
* Automated campaign changes
* Automated purchase-order creation
* Production database infrastructure
* User authentication
* Web application deployment
* Real-time inventory synchronization
* Automated execution of recommendations

The chatbot provides analytical recommendations but does not directly execute advertising or inventory actions.

---

## Future Improvements

Potential next steps include:

* Streamlit dashboard and chatbot interface
* PostgreSQL database integration
* Automated data ingestion pipelines
* Real-time campaign monitoring
* Historical ROAS trend analysis
* Automated anomaly detection
* Campaign-level budget optimization
* Automated inventory alerts
* LLM-powered SQL generation
* FastAPI deployment
* Dockerized deployment
* Production monitoring and logging
* Role-based access control

---

## Key Skills Demonstrated

This project demonstrates practical experience with:

* Python
* Pandas
* NumPy
* Marketing analytics
* Quick-commerce analytics
* ROAS analysis
* ROI analysis
* Campaign performance analysis
* Keyword-level advertising analysis
* Bid optimization logic
* Inventory analytics
* Days of Inventory
* Stockout risk analysis
* Business rule design
* LLM application development
* LangChain
* Google Gemini API
* Conversational memory
* Prompt engineering
* Decision-support systems
* Business recommendation generation

---

## Author

**Dolly Jha**

AI / Analytics Portfolio Project focused on combining business analytics, marketing intelligence, inventory analytics, and Generative AI into a conversational decision-support system.
