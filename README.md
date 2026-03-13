# Entornos-7.5_AGD
```mermaid
flowchart LR

subgraph GymMasterSystem

Login((Login))
ReserveClass((Reserve Class))
JoinWaitlist((Join Waitlist))
ViewClasses((View Classes))
CreateClass((Create Class))
CancelSession((Cancel Session))

ReserveClass -->|<<include>>| Login
JoinWaitlist -.->|<<extend>>| ReserveClass

end

Member --> ViewClasses
Member --> ReserveClass

Administrator --> CreateClass
Administrator --> CancelSession

```
