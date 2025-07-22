# Bus Booking System - ER Diagrams

## Level 0 (Context Level) ER Diagram
```mermaid
erDiagram
    USER ||--o{ BOOKING : makes
    BUS ||--o{ BOOKING : receives
    SEAT ||--o{ BOOKING : contains
```

## Level 1 (Conceptual Level) ER Diagram
```mermaid
erDiagram
    USER ||--o{ BOOKING : makes
    USER {
        long id PK
        string name
        string email
        string password
        string role
        int age
        string gender
        boolean isPregnant
    }

    BOOKING ||--o{ SEAT : contains
    BOOKING {
        long id PK
        long userId FK
        long busId FK
        datetime bookingDate
        string seatNumber
        decimal amount
        string status
    }

    BUS ||--o{ BOOKING : receives
    BUS {
        long id PK
        string name
        string route
        string departureTime
        string arrivalTime
        int availableSeats
        int totalSeats
        decimal price
    }

    SEAT {
        long id PK
        long busId FK
        string seatNumber
        enum seatType
        enum status
    }
```

## Level 2 (Logical Level) ER Diagram
```mermaid
erDiagram
    USER ||--o{ BOOKING : makes
    USER {
        long id PK "IDENTITY"
        string name "NOT NULL, length=100"
        string email "NOT NULL, UNIQUE, length=100"
        string password "NOT NULL, length=100"
        string role "NOT NULL, length=20"
        int age
        string gender "length=20"
        boolean isPregnant
    }

    BOOKING ||--o{ SEAT : contains
    BOOKING {
        long id PK "IDENTITY"
        long userId FK "NOT NULL"
        long busId FK "NOT NULL"
        datetime bookingDate "NOT NULL"
        string seatNumber "NOT NULL"
        decimal amount "NOT NULL, precision=10, scale=2"
        string status "NOT NULL, length=20"
    }

    BUS ||--o{ BOOKING : receives
    BUS {
        long id PK "IDENTITY"
        string name "NOT NULL, length=100"
        string route "NOT NULL, length=200"
        string departureTime "NOT NULL, length=50"
        string arrivalTime "NOT NULL, length=50"
        int availableSeats
        int totalSeats
        decimal price "NOT NULL, precision=10, scale=2"
    }

    SEAT {
        long id PK "IDENTITY"
        long busId FK "NOT NULL"
        string seatNumber "NOT NULL"
        enum seatType "NOT NULL, (REGULAR, ELDER, PREGNANT)"
        enum status "NOT NULL, (AVAILABLE, BOOKED)"
    }
```

## Entity Descriptions

### User Entity
- Represents users of the system (both passengers and administrators)
- Contains personal information and authentication details
- Has a role field to distinguish between different user types
- Includes special status fields (age, gender, pregnancy) for seat allocation

### Bus Entity
- Represents the bus vehicles in the system
- Contains route information and timing details
- Tracks seat availability and pricing
- Has a unique identifier and descriptive information

### Booking Entity
- Represents a booking made by a user
- Links users, buses, and seats together
- Contains booking details like date, amount, and status
- Tracks the specific seat booked

### Seat Entity
- Represents individual seats on a bus
- Has different types (Regular, Elder, Pregnant)
- Tracks availability status
- Associated with a specific bus

## Relationships
1. User to Booking: One-to-Many
   - A user can make multiple bookings
   - Each booking belongs to one user

2. Bus to Booking: One-to-Many
   - A bus can have multiple bookings
   - Each booking is associated with one bus

3. Booking to Seat: One-to-Many
   - A booking can contain multiple seats
   - Each seat can be part of one booking

4. Bus to Seat: One-to-Many
   - A bus has multiple seats
   - Each seat belongs to one bus 