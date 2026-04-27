# Veridi Logistics : Delivery Performance Audit

## A. Executive Summary
This audit of 98,207 orders from the Olist Brazilian E-Commerce dataset 
reveals that while 90.3% of Veridi's deliveries arrive on time, 
the remaining 8% represent nearly 8,000 customers who received packages 
significantly later than promised. Geographic analysis confirms this is 
a regional problem concentrated in Brazil's northeast states,
particularly AL (23.11% late) , MA (19.16% late) and PI(15.51% late) which are furthest 
from São Paulo's main distribution centers. 

Veridi is essentially promising the same delivery date to everyone regardless of where they live.
A customer in São Paulo and a customer in Maranhão get the same estimated delivery date, but the Maranhão customer is 23% more likely to receive it late because:
Longer shipping routes
Fewer logistics partners in remote areas
Poor road infrastructure in the northeast
Less frequent courier routes the monthly trend analysis shows the late delivery rate is WORSENING over time, meaning urgent intervention is required to prevent compounding revenue loss and reputational damage.

## B. The Problem We Are Solving
The CEO of Veridi Logistics noticed a spike in negative customer reviews 
and suspected the problem was linked to inaccurate delivery date promises. 
However, without data, they had no way of knowing where the problem was 
coming from or how serious it was.

This audit solves that problem by answering three critical business questions:

| Question | Answer Found |
|---|---|
| Is this a nationwide or regional problem? | Regional : concentrated in AL, MA and PI |
| Are late deliveries causing bad reviews? | Yes : Super Late orders average just 1.78 stars vs 4.29 for On Time |
| Is the problem getting better or worse? | Worse : monthly trend is worsening over time |

### Business Value Delivered
| Before Audit | After Audit |
|---|---|
| Spending money fixing everything nationwide | Focus budget on AL, MA and PI only |
| Blaming sellers for bad reviews | Proven it is a logistics problem |
| Same delivery estimate for everyone | Can now set realistic dates per region |
| No idea if improving or worsening | Monthly trend shows it is worsening urgently |

In short — this audit saves Veridi from wasting money fixing the wrong thing. 
Instead of a nationwide overhaul, leadership now knows exactly where to focus, 
what is causing the problem, and how urgent the situation is.
---

## C. Project Links

| Deliverable       | Link |
|-------------------|---|
| Notebook          |  [GitHub Notebooks](https://github.com/angela-tk20/The-Logistics-Auditor-Project) |
| Dashboard         | [Power BI Public](https://app.fabric.microsoft.com/view?r=eyJrIjoiNTJiNmExNTgtNGRhMC00MjAzLWJlYzItNTEzZGQ0Mjg0NjExIiwidCI6ImIyMGE4ZjRkLTBkNmEtNGYyZS04M2EyLTE4MWM5NjhmODg4MiIsImMiOjl9) |
| Presentation      | [Google Slides](https://amalitech-my.sharepoint.com/:p:/p/angela_tenkorang/IQCRNMkO9r0vRorHm6KX8ar8AVn9amW84oK4BT5SlIdABZ0?e=DljrCG&nav=eyJzSWQiOjI1Nn0) |
| Video Walkthrough | [YouTube](https://www.loom.com/share/bcb09b3bb60148c7adc253ce3ac29457) |


---

## D. Technical Explanation

### Project Approach
This project was broken down into structured sprints to make it easier 
to tackle in manageable chunks. Each sprint had a clear goal and 
deliverable, building on the previous one to produce a complete 
end-to-end audit:

| Sprint | Goal | Output |
|--------|------|--------|
| Sprint 1 | Join all raw CSV files into one master table | `master_orders.csv` |
| Sprint 2 | Calculate delivery delays and classify each order | `delivery_analysis.csv` |
| Sprint 3 | Map late delivery rates geographically by state | State bar chart + Brazil map |
| Sprint 4 | Prove that late deliveries cause bad reviews | Sentiment correlation charts |
| Bonus 5 | Translate product categories to English | `category_analysis.csv` |
| Candidate's Choice | Analyse monthly delivery trend over time | `monthly_trend.csv` |

This sprint-based approach ensured each piece of analysis was 
clean and validated before being used as the foundation for the next.

---

### Data Cleaning
The raw Olist dataset was split across multiple CSV files requiring 
careful joining to avoid data quality issues:
- **Reviews join:** The reviews table contained multiple reviews per order. 
  We deduplicated by keeping only the latest review per order before joining 
  to prevent row inflation.
- **Date conversion:** All 5 date columns were converted from plain text 
  to datetime objects using `pd.to_datetime()` with `errors='coerce'` 
  to handle missing values gracefully as NaT.
- **Cancelled orders:** Orders with status `canceled` or `unavailable` 
  were excluded from delivery analysis and stored separately to avoid 
  skewing performance metrics.
- **Product categories:** The `product_category_name` column was in 
  Portuguese and joined with `product_category_name_translation.csv` 
  to produce English category names for the dashboard.

### Candidate's Choice : Monthly Delivery Trend
I added a monthly late delivery rate trend analysis to show whether 
Veridi's over-promising problem is getting better or worse over time. 
This feature matters to the business because if the late delivery rate 
is worsening month by month, it signals a compounding problem — each month 
more customers are being failed, leading to fewer repeat purchases, 
more negative reviews, and eventual revenue decline. The analysis confirmed 
the trend is WORSENING, making this the most actionable finding in the 
entire audit — it tells the CEO not just that there is a problem, 
but that the problem is accelerating and requires urgent intervention.

---

## E. Pre-Submission Checklist
- [x] GitHub Repo is Public
- [x] .ipynb notebook files uploaded
- [x] HTML exports uploaded
- [x] Raw dataset NOT uploaded (.gitignore applied)
- [x] Code uses relative paths
- [x] Dashboard link is publicly accessible
- [x] Presentation link is publicly accessible
- [x] README updated with Executive Summary
- [x] User Stories 1-4 completed
- [x] Candidate's Choice completed and explained

---

## F. Project Structure
```
The-Logistics-Auditor-Project/
├── Data/                                     ← raw CSVs (not committed to GitHub)
├── Merged_Olist_Data/                        ← processed CSV outputs
├── html_exports/                             ← HTML exports of all notebooks
├── Notebook files/
│   ├── load_and_join_data.ipynb              ← Sprint 1
│   ├── delay_calculator.ipynb                ← Sprint 2
│   ├── geographic_delivery_analysis.ipynb    ← Sprint 3
│   ├── sentiment_correlation_analysis.ipynb  ← Sprint 4
│   ├── product_translation.ipynb             ← Bonus Story 5
│   └── candidate_choice_delivery_trend.ipynb ← Candidate's Choice
└── README.md
└── veridi_logistics_presentation.ppts
```

## G. How to Clone and Run This Project

### Prerequisites
Make sure you have the following installed on your machine:
- Python 3.9 or higher
- pip 
- Jupyter Notebook or JupyterLab
- Git

### Step 1 - Clone the Repository
```bash
git clone https://github.com/angela-tk20/The-Logistics-Auditor-Project.git
cd The-Logistics-Auditor-Project
```

### Step 2 - Create a Virtual Environment
```bash
python -m venv venv
```

Activate it:
- **Windows:** `venv\Scripts\activate`
- **Mac/Linux:** `source venv/bin/activate`

### Step 3 - Install Required Packages
```bash
pip install pandas numpy matplotlib seaborn plotly streamlit openpyxl jupyter nbconvert
```

### Step 4 - Download the Dataset
The raw dataset is not included in this repository due to file size.
Download it manually from Kaggle:

1. Go to: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
2. Download and unzip the dataset
3. Place all CSV files inside a folder called `Data/` in the project root

### Step 5 - Run the Notebooks in Order
Open Jupyter and run each notebook in this order:

| Order | Notebook | Purpose |
|-------|----------|---------|
| 1 | `load_and_join_data.ipynb` | Build master orders table |
| 2 | `delay_calculator.ipynb` | Calculate delivery delays |
| 3 | `geographic_delivery_analysis.ipynb` | Map late deliveries by state |
| 4 | `sentiment_correlation_analysis.ipynb` | Prove link to bad reviews |
| 5 | `product_translation.ipynb` | Translate product categories |
| 6 | `candidate_choice_delivery_trend.ipynb` | Monthly trend analysis |

### Required CSV Files from Kaggle
Make sure these files are in your `Data/` folder:
- `olist_orders_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_customers_dataset.csv`
- `olist_products_dataset.csv`
- `olist_order_items_dataset.csv`
- `product_category_name_translation.csv`

