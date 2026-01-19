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

