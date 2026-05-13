# 💊 Bahaa Pharmacy — Profitability & Restock Analysis
### January – April 2026 | Powered by Python & Jupyter Notebook

---

## 📌 Project Overview

This project is a comprehensive data analysis pipeline built for **Bahaa Pharmacy** (Dirout, Egypt), transforming raw ERP sales exports into actionable business intelligence.

Starting from 1,318 confirmed POS transactions across 477 unique products, the notebook delivers two critical outputs:

1. **A profitability dashboard** — identifying which products truly drive revenue
2. **A data-driven restock recommendation list** — a ready-to-use Q2 2026 purchase order

> *Built cell by cell using Python, Jupyter Notebook, and Claude AI as a coding partner.*

---

## 📂 Project Structure

```
Januray_April_2026_Pharmacy_Bahaa_Analysis/
│
├── Datasets/
│   └── الربح لكل عنصر لنقط البيع و الفواتير (report.profit.item.details).xlsx
│
├── Januray_April_2026_Pharmacy_Bahaa_Analysis.ipynb   ← Main notebook
├── profitability_dashboard.png                         ← 4-chart visual dashboard
├── Restock_Recommendation_Q2_2026.xlsx                 ← Final purchase order
└── README.md
```

---

## 📊 Data Source

| Field | Details |
|---|---|
| **System** | Dawatk ERP (built on Odoo) |
| **Report** | Profit per Item — Sales & Invoices |
| **Period** | January 1, 2026 → April 29, 2026 |
| **Raw rows** | 3 × 22 columns after export |
| **Clean rows** | 1,318 confirmed POS transactions |
| **Unique products** | 477 |

---

## 🔬 Methodology

### 1. Data Cleaning & Preparation
- Renamed 22 Arabic column headers to clean English equivalents
- Filtered to confirmed POS sales only (`تم الإعتماد` + `طلبات نقطة البيع`)
- Stripped whitespace from string columns to fix encoding artifacts
- Extracted month and date features from transaction timestamps

### 2. Product-Level Aggregation
Grouped all transactions by product to compute:
- Total quantity sold
- Total revenue, cost, and profit
- Average profit margin %
- Transaction count

### 3. ABC Classification

| Class | Cumulative Profit | Products | Strategy |
|---|---|---|---|
| 🟢 A | 0% – 70% | 145 products | Always in stock — 20% safety buffer |
| 🔵 B | 70% – 90% | 145 products | Monitor closely — 10% safety buffer |
| 🔴 C | 90% – 100% | 187 products | Stock minimally — not prioritized |

### 4. Restock Recommendation Engine
For each Class A and B product:

```
Monthly Velocity  = Total Units Sold ÷ 4 months
Projected Demand  = Monthly Velocity × 3 months
Recommended Qty   = ⌈ Projected Demand × Safety Multiplier ⌉
Estimated Cost    = Recommended Qty × Avg Unit Cost
```

---

## 📈 Key Results

| Metric | Value |
|---|---|
| Total profit (Jan–Apr 2026) | **14,124.85 EGP** |
| Best month | **February — 3,911 EGP** |
| Weakest month | **March — 2,999 EGP** |
| Class A profit share | **69.8%** from just 145 products |
| Restock list size | **290 products** |
| Estimated Q2 restock cost | **36,662.45 EGP** |
| Expected Q2 profit return | **12,707.57 EGP** |

---

## 📦 Deliverables

### `profitability_dashboard.png`
A 4-chart visual dashboard including:
- **Top 20 Most Profitable Products** — horizontal bar chart colored by ABC class
- **ABC Profit Share** — pie chart showing class distribution
- **Monthly Profit Trend** — Jan → Apr line chart with annotations
- **Margin Distribution by Class** — histogram overlay by ABC class

### `Restock_Recommendation_Q2_2026.xlsx`
A formatted, color-coded Excel purchase order containing:
- Product name, ABC class, and profit rank
- Units sold over 4 months & monthly velocity
- Recommended restock quantity for Q2 2026
- Average unit cost & estimated total restock cost
- Total profit & average margin %
- Grand total row at the bottom

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| `Python 3.13` | Core language |
| `pandas` | Data manipulation & aggregation |
| `matplotlib` + `seaborn` | Data visualization |
| `arabic_reshaper` + `python-bidi` | Arabic text rendering in plots |
| `xlsxwriter` | Formatted Excel export |
| `Jupyter Notebook` | Interactive development environment |
| `Dawatk / Odoo` | ERP data source |

---

## ⚙️ How to Run

**1. Clone or download the project folder**

**2. Install dependencies**
```bash
pip install pandas matplotlib seaborn arabic-reshaper python-bidi xlsxwriter openpyxl
```

**3. Place the dataset**

Ensure the Dawatk export file is in the `Datasets/` folder with the exact original filename.

**4. Open and run the notebook**
```bash
jupyter notebook Januray_April_2026_Pharmacy_Bahaa_Analysis.ipynb
```

Run all cells in order — each cell is preceded by a Markdown explanation of the step.

---

## 💡 Insights & Next Steps

- **March dip** (2,999 EGP vs ~3,700 avg) warrants investigation — possible supply disruption or seasonal pattern
- **Class C products (187 items)** occupy shelf space while contributing only 10% of profit — candidates for phase-out review
- **Future enhancements:**
  - [ ] Vendor-level profitability breakdown
  - [ ] Per-product monthly trend (which products grew or declined?)
  - [ ] Automated monthly refresh pipeline
  - [ ] Integration with reorder alerts in Dawatk

---

## 👨‍⚕️ Author

**Dr. Bahaa** — Pharmacist & Pharmacy Owner  
Bahaa Pharmacy, Dirout, Egypt  
*Built with curiosity, Python, and a commitment to data-driven decisions.*

---

> *"The data is already there — sitting in your ERP right now. The question is: are you listening to it?"*
