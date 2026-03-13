# Entornos-7.5_AGD
ej 1
Muestra los actores (Member y Administrator) y las acciones que pueden hacer en el sistema GymMaster, como ver o reservar clases. También incluye login (include) y lista de espera (extend).
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
ej 2
Muestra el proceso cuando un socio confirma una reserva. El sistema comprueba en la base de datos si hay plazas y confirma la reserva o informa que la clase está llena.
```mermaid
sequenceDiagram

actor Member
participant WebInterface
participant ReservationManager
participant Database

Member ->> WebInterface: confirmReservation(classId)

WebInterface ->> ReservationManager: requestReservation(memberId,classId)

ReservationManager ->> Database: checkAvailability(classId)

Database -->> ReservationManager: availabilityResult

alt seats available

ReservationManager -->> WebInterface: reservationConfirmed()
WebInterface -->> Member: showSuccessMessage()

else class full

ReservationManager -->> WebInterface: classFull()
WebInterface -->> Member: showWaitlistOption()

end
```

ej 3
Este diagrama muestra la comunicación entre los objetos del sistema durante el proceso de reserva. Los números indican el orden en el que se envían los mensajes.
```mermaid
flowchart LR

Member
WebInterface
ReservationManager
Database

Member -- "1: confirmReservation()" --> WebInterface

WebInterface -- "1.1: requestReservation()" --> ReservationManager

ReservationManager -- "1.2: checkAvailability()" --> Database

Database -- "1.3: availabilityResult" --> ReservationManager

ReservationManager -- "2: reservationConfirmed()" --> WebInterface
```

ej4
Este diagrama muestra el proceso de validación de una reserva. El sistema comprueba si el socio tiene la cuota pagada y si hay plazas antes de confirmar la reserva.
```mermaid
flowchart TD

Start((Start))

A[Receive reservation request]

B{Membership paid}

C[Reject reservation]

D{Seats available}

E[Add to waitlist]

F[Lock seat]

G[Send confirmation email]

End((End))

Start --> A
A --> B

B --> C
B --> D

D --> E
D --> F

F --> G
G --> End

C --> End
E --> End
```
