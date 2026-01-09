# Diseño de la solución: Plataforma integrada

## C4 Context Diagram (level 1)

```mermaid
C4Context
    title C4 Context Diagram
    
    Person(p_partner, "Partner User", "Business partner for key activities")
    Person(p_mgmt, "Management User", "Manages operational and business information")
    Person(p_client, "Client User", "Business client of the platform")
    Person(p_investor, "Investor User", "Capital partner and co-investor")
    Person_Ext(p_web, "Web User", "Anonymous visitor of the public website")

    System_Boundary(b_system, "AWS") {

        System(sys_public_web, "Public Website", "Public-facing website")
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

        System_Ext(ext_data_api, "Data Indicators API", "External data provider")
        Rel(sys_public_web, ext_data_api, "Requests data")
    }

```

## C4 Container Diagram (level 2)

```mermaid

C4Context
    title C4 Container Diagram
    
    Person(p_partner, "Partner User", "Business partner for key activities")
    Person(p_mgmt, "Management User", "Manages operational and business information")
    Person(p_client, "Client User", "Business client of the platform")
    Person(p_investor, "Investor User", "Capital partner and co-investor")
    Person_Ext(p_web, "Web User", "Anonymous visitor of the public website")

    System_Boundary(b_system, "AWS") {
        
        

        System_Boundary(b_public,"Public Website"){
            Container(c_investment, "Investment page", "AWS Serverless")
            Container(c_home, "Landing page", "AWS Serverless")
            Rel(p_web, c_home, "Browses")
            Rel(c_home, c_investment, "Navegate")
        }
        System_Boundary(b_ext,"External"){
            System_Ext(ext_data_api, "Data Indicators API", "External data provider")
            Rel(c_home, ext_data_api, "Requests data")
        }

        System_Boundary(b_activities,"Activities"){
            Container(c_activities, "Show Activities", "AWS Serverless")
            Rel(p_partner, c_activities, "Collaborates")

            
        }
        System_Boundary(b_management,"Management"){
            Container(c_management, "Management dashboard", "AWS Serverless")
            Rel(p_mgmt, c_management, "Manages and monitors")
            Rel(p_client, c_management, "Uses services")

            Container(c_clients, "Clients management", "AWS Serverless")
            Container(c_movement, "Movements management", "AWS Serverless")
            Container(c_guarantees, "Guarantees management", "AWS Serverless")
            
            ContainerDb(db_system,"System DB","AWS Transactional DB")
            Rel(c_activities, db_system, "Request activities")

            Rel(c_management, db_system, "Request activities")

            BiRel(c_management, c_clients, "Navegate")
            BiRel(c_management, c_movement, "Navegate")
            BiRel(c_management, c_guarantees, "Navegate")

        }
        System_Boundary(b_investment, "Investment"){
            Container(c_simulations, "Investment simulations", "AWS Serverless")
            Rel(c_investment, c_simulations, "Simulate - Signin")
            Container(c_investments, "Investments dashboard", "AWS Serverless")
            Rel(p_investor, c_investments,"My Investments - Login")
            BiRel(c_simulations, c_investments,"Navegate")


            Rel(c_simulations, db_system, "Request business rules")
            Rel(c_investments, db_system, "Request business data")
            
        }
        
    }


```
