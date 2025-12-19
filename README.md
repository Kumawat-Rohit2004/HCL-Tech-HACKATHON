# HCL-Tech-HACKATHON


                  ┌─────────────────────────┐
                  │   CSV / Generated Data  │
                  │ (Sales, Customers, etc) │
                  └───────────┬─────────────┘
                              │
                              ▼
               ┌─────────────────────────────┐
               │  Data Ingestion Layer (ETL) │
               │  • Python / Java            │
               │  • CSV Reader               │
               └───────────┬─────────────────┘
                           │
                           ▼
        ┌────────────────────────────────────────┐
        │              RAW DATABASE               │
        │  raw.store_sales_header                 │
        │  raw.store_sales_line_items             │
        └───────────┬────────────────────────────┘
                    │
                    ▼
     ┌─────────────────────────────────────────────┐
     │     Data Quality & Validation Engine         │
     │  • Missing values                            │
     │  • Negative sales                            │
     │  • Invalid store/product IDs                 │
     │  • Header vs Line-item mismatch              │
     └───────────┬─────────────────────┬───────────┘
                 │                     │
                 ▼                     ▼
┌──────────────────────────┐   ┌──────────────────────────┐
│   STAGING (Clean Data)   │   │   QUARANTINE (Bad Data)  │
│  staging.sales_header    │   │  quarantine.rejects     │
│  staging.sales_items     │   │  (for audit & analysis) │
└───────────┬──────────────┘   └──────────────────────────┘
            │
            ▼
┌───────────────────────────────────────────────────────────┐
│                   BUSINESS LOGIC LAYER                     │
│                                                           │
│  ┌─────────────────────────────────────────────────────┐ │
│  │ Promotion Effectiveness Analyzer                     │ │
│  │ Loyalty Point Calculation Engine                     │ │
│  │ Customer Segmentation (RFM)                           │ │
│  │ Inventory & Sales Correlation                         │ │
│  └─────────────────────────────────────────────────────┘ │
└───────────┬───────────────────────────────────────────────┘
            │
            ▼
┌───────────────────────────────────────────────────────────┐
│                  ANALYTICS & OUTPUT                        │
│                                                           │
│  • Dashboards (Top Promotions, Sales Lift)                │
│  • Customer Segments (High-Spenders, At-Risk)             │
│  • Inventory Loss Reports                                 │
│  • Loyalty Notification Emails (Simulated)                │
└───────────────────────────────────────────────────────────┘
