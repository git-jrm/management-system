## C4 Context diagram

```mermaid
C4Context
    title C4 Context Diagram
    
    Person(p_mgmt, "Manager User", "Manages operational and business information")

    Boundary(b_system, "Solution") {
        System(sys_management, "Management System", "Operational and administrative management")
        Rel(p_client, sys_management, "Uses services")
        Rel(p_mgmt, sys_management, "Manages and monitors")
    }
```
