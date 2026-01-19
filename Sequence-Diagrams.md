## Partner invests Investment

```mermaid
sequenceDiagram
    Partner->>+Model: Invests
    Model-->>-Partner: Benefits
```
## Partner refer Referred

```mermaid
sequenceDiagram
    Partner->>+Referred: refers
    Referred->>+Model: Invests
    Model-->>-Referred: Benefits
    Model-->>+Partner: Commission
```

## Master invite Partner

```mermaid
sequenceDiagram
    participant MBP as Master Business Partner
    participant Partner as Partner
    participant Ref as Refer
    participant BM as Business Model

    MBP->>Partner: Invite
    Partner->>Ref: Reffer
    Ref->>BM: Invests
    BM-->>Ref: Benefits (10-30%)
    BM-->>Partner: Reference commission (4%)
    BM-->>MBP: Master commission (6%)
```
