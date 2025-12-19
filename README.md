# HCL-Tech-HACKATHON


flowchart LR
    A[CSV Files<br/>Store Sales Header<br/>Store Sales Line Items] 
    --> B[Raw Data Layer<br/>raw_* tables]

    B --> C[Data Quality Engine]

    C -->|Valid Records| D[Staging Layer<br/>stg_* tables]
    C -->|Invalid Records| E[Quarantine Layer<br/>error_* tables]

    D --> F[Downstream Analytics<br/>Use Case 2+]
