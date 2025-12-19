# HCL-Tech-HACKATHON


erDiagram

    STORES {
        int store_id PK
        varchar store_name
        varchar store_city
        varchar store_region
        date opening_date
    }

    PRODUCTS {
        int product_id PK
        varchar product_name
        varchar product_category
        decimal unit_price
        int current_stock_level
    }

    CUSTOMER_DETAILS {
        int customer_id PK
        varchar first_name
        varchar email
        varchar loyalty_status
        int total_loyalty_points
        date last_purchase_date
        varchar segment_id
    }

    PROMOTION_DETAILS {
        int promotion_id PK
        varchar promotion_name
        date start_date
        date end_date
        decimal discount_percentage
        varchar applicable_category
    }

    LOYALTY_RULES {
        int rule_id PK
        varchar rule_name
        decimal points_per_unit_spend
        decimal min_spend_threshold
        int bonus_points
    }

    STORE_SALES_HEADER {
        varchar transaction_id PK
        int customer_id FK
        int store_id FK
        datetime transaction_date
        decimal total_amount
    }

    STORE_SALES_LINE_ITEMS {
        int line_item_id PK
        varchar transaction_id FK
        int product_id FK
        int promotion_id FK
        int quantity
        decimal line_item_amount
    }

    %% Relationships
    STORES ||--o{ STORE_SALES_HEADER : has
    CUSTOMER_DETAILS ||--o{ STORE_SALES_HEADER : makes
    STORE_SALES_HEADER ||--o{ STORE_SALES_LINE_ITEMS : contains
    PRODUCTS ||--o{ STORE_SALES_LINE_ITEMS : sold_as
    PROMOTION_DETAILS ||--o{ STORE_SALES_LINE_ITEMS : applied_to

