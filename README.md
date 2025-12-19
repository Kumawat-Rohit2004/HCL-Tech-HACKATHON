# HCL-Tech-HACKATHON

```text
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
   │  └─ segment_id (VARCHAR)
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
   │  ├─ transaction_id (PK, VARCHAR)
   │  ├─ customer_id (FK -> CUSTOMER_DETAILS.customer_id)
   │  ├─ store_id (FK -> STORES.store_id)
   │  ├─ transaction_date (DATETIME)
   │  └─ total_amount (DECIMAL)
   │
   └─ STORE_SALES_LINE_ITEMS
      ├─ line_item_id (PK, INT)
      ├─ transaction_id (FK -> STORE_SALES_HEADER.transaction_id)
      ├─ product_id (FK -> PRODUCTS.product_id)
      ├─ promotion_id (FK -> PROMOTION_DETAILS.promotion_id)
      ├─ quantity (INT)
      └─ line_item_amount (DECIMAL)

RELATIONSHIPS
└─
   ├─ STORES 1 ──< * STORE_SALES_HEADER
   ├─ CUSTOMER_DETAILS 1 ──< * STORE_SALES_HEADER
   ├─ STORE_SALES_HEADER 1 ──< * STORE_SALES_LINE_ITEMS
   ├─ PRODUCTS 1 ──< * STORE_SALES_LINE_ITEMS
   ├─ PROMOTION_DETAILS 1 ──< * STORE_SALES_LINE_ITEMS
   └─ LOYALTY_RULES → CUSTOMER_DETAILS (business logic)

NOTES
└─
   ├─ Header total_amount must equal sum of line_item_amount.
   ├─ promotion_id can be NULL if no promotion applied.
   └─ segment_id is derived (RFM), not a foreign key.
```



<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/841b95a4-93c2-4211-9f3e-7ed3f1f422a1" />
