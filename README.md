# HCL-Tech-HACKATHON


Retail DB (tree representation)
└─ ENTITIES
   ├─ STORES
   │  ├─ store_id (PK, INT)
   │  ├─ store_name (VARCHAR)
   │  ├─ store_city (VARCHAR)
   │  ├─ store_region (VARCHAR)
   │  └─ opening_date (DATE)
   │
   ├─ PRODUCTS
   │  ├─ product_id (PK, INT)
   │  ├─ product_name (VARCHAR)
   │  ├─ product_category (VARCHAR)
   │  ├─ unit_price (DECIMAL)
   │  └─ current_stock_level (INT)
   │
   ├─ CUSTOMER_DETAILS
   │  ├─ customer_id (PK, INT)
   │  ├─ first_name (VARCHAR)
   │  ├─ email (VARCHAR)
   │  ├─ loyalty_status (VARCHAR)
   │  ├─ total_loyalty_points (INT)
   │  ├─ last_purchase_date (DATE)
   │  └─ segment_id (VARCHAR)   # derived by segmentation logic
   │
   ├─ PROMOTION_DETAILS
   │  ├─ promotion_id (PK, INT)
   │  ├─ promotion_name (VARCHAR)
   │  ├─ start_date (DATE)
   │  ├─ end_date (DATE)
   │  ├─ discount_percentage (DECIMAL)
   │  └─ applicable_category (VARCHAR)
   │
   ├─ LOYALTY_RULES
   │  ├─ rule_id (PK, INT)
   │  ├─ rule_name (VARCHAR)
   │  ├─ points_per_unit_spend (DECIMAL)
   │  ├─ min_spend_threshold (DECIMAL)
   │  └─ bonus_points (INT)
   │
   ├─ STORE_SALES_HEADER
   │  ├─ transaction_id (PK, VARCHAR)   # unique transaction id
   │  ├─ customer_id (FK -> CUSTOMER_DETAILS.customer_id, INT)
   │  ├─ store_id (FK -> STORES.store_id, INT)
   │  ├─ transaction_date (DATETIME)
   │  └─ total_amount (DECIMAL)         # validate == sum of line items
   │
   └─ STORE_SALES_LINE_ITEMS
      ├─ line_item_id (PK, INT)
      ├─ transaction_id (FK -> STORE_SALES_HEADER.transaction_id, VARCHAR)
      ├─ product_id (FK -> PRODUCTS.product_id, INT)
      ├─ promotion_id (FK -> PROMOTION_DETAILS.promotion_id, INT)  # nullable
      ├─ quantity (INT)
      └─ line_item_amount (DECIMAL)

RELATIONSHIPS (cardinality)
└─
   ├─ STORES 1 ──< * STORE_SALES_HEADER
   │   (one store has many transactions)
   │
   ├─ CUSTOMER_DETAILS 1 ──< * STORE_SALES_HEADER
   │   (one customer can make many transactions)
   │
   ├─ STORE_SALES_HEADER 1 ──< * STORE_SALES_LINE_ITEMS
   │   (one transaction contains many line items)
   │
   ├─ PRODUCTS 1 ──< * STORE_SALES_LINE_ITEMS
   │   (one product appears in many line items)
   │
   ├─ PROMOTION_DETAILS 1 ──< * STORE_SALES_LINE_ITEMS
   │   (one promotion can be applied to many line items)
   │
   └─ LOYALTY_RULES  (business logic) -> used to calculate/award points for CUSTOMER_DETAILS

NOTES
└─
   ├─ Use STORE_SALES_HEADER.total_amount to validate data quality against sum(line_item_amount).
   ├─ promotion_id in line items may be NULL (item not promoted).
   ├─ segment_id in CUSTOMER_DETAILS is not a FK to a table in the PDF; it is derived via RFM/segmentation logic.
   └─ Keep raw/staging/quarantine layers in your pipeline (not shown as tables here) for ETL & QA.


