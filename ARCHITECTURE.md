## C4 Context diagram

```mermaid
C4Context
    title C4 Context Diagram
    
    Person(p_partner, "Collaborator User", "Collaborator for key activities")
    Person(p_client, "Client User", "Business client of the platform")
    Person(p_mgmt, "Manager User", "Manages operational and business information")
    Person(p_investor, "Partner User", "Would be investor, referrer or MBP")
    Person_Ext(p_web, "Web User", "Anonymous visitor of the public website")

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

## C4 Container Diagram · Public Site

```mermaid
C4Container
    title C4 Container Diagram PUBLIC

    Person_Ext(p_web, "Web User", "Anonymous visitor of the public website")
    Boundary(b_system, "Solution") {
        System_Boundary(b_public,"Public Site"){
            Container(c_home, "Portal page", "Serverless")
            Container(c_guests, "Guests page", "Serverless")
            Container(c_partners, "Partners page", "Serverless")
            Rel(p_web, c_home, "Browses")
            Rel(c_home, c_partners, "Navegate")
            Rel(c_home, c_guests, "Navegate")
        }
        System_Boundary(b_p,"Private Solution"){
            Container(c_login, "Secure Login", "Serverless")
            
        }
        Rel(c_home, c_login, "access")
        Rel(c_partners, c_login, "access")
        Rel(c_guests, c_login, "access")
    }
```

## C4 Container Diagram · Activities System

```mermaid
C4Container
    title C4 Container Diagram Activities System

    Person(p_mgmt, "Manager User", "Manages operational and business information")
    Person(p_collaborator, "Collaborator User", "Business client of the platform")
    Boundary(b_system, "Private Solution") {
        System_Boundary(b_management,"Activities System"){
            Container_Boundary(b_frontend, "Mobile Team"){
                Container(c_fuim, "Frontend UI", "Mobile Web App")
                Container(c_bffm, "Backend For Frontend", "Mobile BFF")
            }
            Container_Boundary(b_desktop, "Desktop Team"){
                Container(c_fuid, "Frontend UI", "Desktop Web App")
                Container(c_bffd, "Backend For Frontend", "Desktop BFF")
            }
            Container_Boundary(b_backend, "Backend Team"){
                Container(c_mbff, "Backend For Frontend", "Mobile BFF")
                Container(c_dbff, "Backend For Frontend", "Desktop BFF")
                Container(c_clients, "Microservice", "Clients")
                Container(c_movements, "Microservice", "Movements")
                Container(c_apportionments, "Microservice", "Apportionments")
                Container(c_guarantees, "Microservice", "Guarantees")
                ContainerDb(db_system, "Databases", "System")
            }
        }
    }
```



## C4 Container Diagram · Management System



## C4 Container Diagram · Investment System

