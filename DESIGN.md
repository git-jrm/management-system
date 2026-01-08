# Diseño de la solución: Plataforma integrada

## 1) C4 Context

```mermaid
C4Context
    title Integrated Platform Context diagram

    Enterprise_Boundary(b0, "Organization Context") {
        Person(p1, "Management User", "Manages operational and business information")
        Person(p3, "Client User", "Business client of the platform")
        Person(p2, "Partner User", "Business partner for key activities")
        
        Person(p4, "Investor User", "Capital partner and co-investor")
        Person_Ext(p0, "Web User", "Anonymous visitor of the public website")

        Enterprise_Boundary(b1, "Integrated Plarform in AWS") {
            
            System_Boundary(b2, "Public Platform") {
                System(SystemAA, "Public Website", "Public-facing website")
                System_Ext(SystemA, "Economic Indicators", "API")
                System_Ext(SystemB, "Climate Indicators", "API")
            }
            System_Boundary(b3, "Private Platform") {
                System(SystemAAA, "Managment System")
                System(SystemBBB, "Activities System")
                System(SystemCCC, "Investments System")
            }

        }
    }

    Rel(p0, SystemAA, "Browses")
    Rel(SystemAA, SystemA, "Request")
    Rel(SystemAA, SystemB, "Request")

    Rel(p1, SystemAAA, "Manages and monitors")
    Rel(p2, SystemBBB, "Collaborates")
    Rel(p3, SystemAAA, "Uses services")
    Rel(p4, SystemCCC, "Consults reports")



```
