## Partner invests Investment
```mermaid
sequenceDiagram
    Partner->>+Model: Invests
    Model-->>-Partner: Benefits 10-30%
```

## Partner refer Referred
```mermaid
sequenceDiagram
    Partner->>+Referred: refers
    Referred->>+Model: Invests
    Model-->>-Referred: Benefits 10-30%
    Model-->>+Partner: Commission 2%
```

## Master refer Referred
```mermaid
sequenceDiagram
    Partner->>+Referred: refers
    Referred->>+Model: Invests
    Model-->>-Referred: Benefits 10-30%
    Model-->>+Partner: Commission 4%
```

## Master invite Partner to refer
```mermaid
sequenceDiagram
    participant MBP as Master Business Partner
    participant Partner as Partner
    participant Ref as Refer
    participant BM as Business Model

    MBP->>Partner: Invite (Reffer)
    Partner->>Ref: Reffer
    Ref->>BM: Invests
    BM-->>Ref: Benefits 10-30%
    BM-->>Partner: Reference commission 4%
    BM-->>MBP: Master commission 6%
```
