## C4 Context diagram: Integrated System

```mermaid
C4Context
    title C4 Context Diagram
    
    Person(p_partner, "Collaborator User", "Collaborator for key activities")
    Person(p_client, "Client User", "Business client of the platform")
    Person(p_mgmt, "Manager User", "Manages operational and business information")
    Person(p_investor, "Partner User", "Would be investor, referrer or MBP")
    Person_Ext(p_web, "Web Visitor", "Anyone visitor of the public website")

    Boundary(b_system, "Solution") {

        System(sys_public_web, "Public Site", "Public-facing website")
        Rel(p_web, sys_public_web, "Browses")

        System(sys_activities, "Activities System", "Business activities coordination")
        Rel(p_partner, sys_activities, "Collaborates")
        Rel(sys_activities, sys_management, "Sends activity updates")

        System(sys_management, "Management System", "Operational and administrative management")
        Rel(p_client, sys_management, "Uses services")
        Rel(p_mgmt, sys_management, "Manages and monitors")

        System(sys_investments, "Investments System", "Investment and portfolio management")
        Rel(p_investor, sys_investments, "Consults investments")
        Rel(sys_investments, sys_management, "Sends investments reports")
    }
```

