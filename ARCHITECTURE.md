# Architecture Diagrams

## C4 Context diagrams

```mermaid
C4Context
    title C4 Context Diagram
    
    Person(p_partner, "Collaborator User", "Collaborator for key activities")
    Person(p_mgmt, "Manager User", "Manages operational and business information")
    Person(p_client, "Client User", "Business client of the platform")
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
        System_Boundary(b_p,"Private Site"){
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
    title C4 Container Diagram PRIVATE
    Person(p_partner, "Partner User", "Business partner for key activities")
    Person(p_mgmt, "Management User", "Manages operational and business information")
    Person(p_client, "Client User", "Business client of the platform")
    Person(p_investor, "Investor User", "Capital partner and co-investor")

    Boundary(b_system, "Integrated Platform") {
        System_Boundary(b_management,"Management"){
            Container(c_mui, "Frontend UI", "Mobile Web App")
            Rel(p_mgmt, c_mui, "Manages and monitors")
            Rel(p_client, c_mui, "Uses services")
            Container(c_dui, "Frontend UI", "Desktop Web App")
            Container(c_mbff, "Backend For Frontend", "Mobile BFF")
            Rel(c_mui, c_mbff, "Consults investments")

            Container(c_dbff, "Backend For Frontend", "Desktop BFF")
            Rel(c_dui, c_dbff, "Consults investments")

            Container_Boundary(b_backend, "Backend Team"){
                Container(c_clients, "Microservice", "Clients")
                Rel(c_dbff, c_clients, "API")
                Rel(c_mbff, c_clients, "API")

                Container(c_movements, "Microservice", "Movements")
                Rel(c_dbff, c_movements, "API")
                Rel(c_mbff, c_movements, "API")

                Container(c_apportionments, "Microservice", "Apportionments")
                Rel(c_dbff, c_apportionments, "API")
                Rel(c_mbff, c_apportionments, "API")

                Container(c_guarantees, "Microservice", "Guarantees")
                Rel(c_dbff, c_guarantees, "API")
                Rel(c_mbff, c_guarantees, "API")

            ContainerDb(db_system, "Databases", "System")
            Rel(c_guarantees, db_system, "API")
            Rel(c_apportionments, db_system, "API")
            Rel(c_movements, db_system, "API")
            Rel(c_clients, db_system, "API")

            }
        }
        System_Boundary(b_investment,"Investment"){
            Container(c_simulations, "Investment simulations", "Serverless")
            Container(c_investment, "Home investment", "Serverless")
            Rel(p_investor, c_investment, "Consults investments")
        }
        System_Boundary(b_activities,"Activities"){
            Container(c_activities, "Show Activities", "Serverless")
            Rel(p_partner, c_activities, "Collaborates")
            BiRel(c_activities, db_system, "Data Access")
        }
    }

```

## C4 Container Diagram · Management System


## C4 Container Diagram · Investment System


