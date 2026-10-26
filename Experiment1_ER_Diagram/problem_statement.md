# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1312" height="672" alt="image" src="https://github.com/user-attachments/assets/c0db3511-3fac-4e8e-8c9a-cb77f043f561" />



### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---|---|---|
| Member | `MemberID (PK)`, `Name`, `MembershipType`, `StartDate` | Stores registered gym members. |
| Program | `ProgramID (PK)`, `ProgramName`, `Description` | Stores programs such as Yoga, Zumba, and Weight Training. |
| Trainer | `TrainerID (PK)`, `TrainerName`, `Specialization`, `Phone` | Stores trainer information. |
| MemberProgram | `MemberID (PK, FK)`, `ProgramID (PK, FK)`, `JoinDate` | Associative entity linking members and programs. |
| ProgramTrainer | `ProgramID (PK, FK)`, `TrainerID (PK, FK)` | Associates trainers with fitness programs. |
| TrainingSession | `SessionID (PK)`, `MemberID (FK)`, `TrainerID (FK)`, `SessionDate`, `StartTime`, `EndTime` | Stores personal training sessions booked by members. |
| Attendance | `AttendanceID (PK)`, `SessionID (FK)`, `AttendanceDate`, `Status` | Records attendance for each session. |
| Payment | `PaymentID (PK)`, `MemberID (FK)`, `SessionID (FK, nullable)`, `Amount`, `PaymentDate`, `PaymentType`, `Status` | Records membership and personal training session payments. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|---|---|---|---|
| Member — MemberProgram | 1:N | MemberProgram: Total; Member: Partial | A member can join multiple programs. |
| Program — MemberProgram | 1:N | MemberProgram: Total; Program: Partial | A program can have multiple members. |
| Program — ProgramTrainer | 1:N | ProgramTrainer: Total; Program: Partial | A program may have multiple trainers. |
| Trainer — ProgramTrainer | 1:N | ProgramTrainer: Total; Trainer: Partial | A trainer may be assigned to multiple programs. |
| Member — TrainingSession | 1:N | TrainingSession: Total; Member: Partial | A member may book multiple personal training sessions. |
| Trainer — TrainingSession | 1:N | TrainingSession: Total; Trainer: Partial | A trainer may conduct multiple sessions. |
| TrainingSession — Attendance | 1:1 | Attendance: Total; TrainingSession: Partial | Each attendance record refers to one session. A session may not yet have an attendance record. |
| Member — Payment | 1:N | Payment: Total; Member: Partial | A member may make multiple payments. |

### Assumptions
1.Each member has a unique MemberID, and each program and trainer has a unique identifier.
2.A member can join multiple fitness programs, and a program can have multiple members.
3.A program can have multiple trainers, and a trainer can be assigned to multiple programs.
4.Each personal training session is booked by one member and conducted by one trainer.
5.Each session has at most one attendance record, which is created when attendance is recorded.
6.Every payment belongs to one member. A session payment identifies the session, while a membership payment does not require a session identifier.

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1185" height="622" alt="image" src="https://github.com/user-attachments/assets/8821bf3d-1246-40a3-bd15-5cd6c3b5edb4" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---|---|---|
| Member | `MemberID (PK)`, `MemberName`, `Email`, `Phone` | Stores registered library members. |
| Book | `BookID (PK)`, `Title`, `Author`, `Category` | Stores book details. |
| Loan | `LoanID (PK)`, `MemberID (FK)`, `BookID (FK)`, `LoanDate`, `DueDate`, `ReturnDate` | Records book borrowing and return details. |
| Fine | `FineID (PK)`, `LoanID (FK)`, `Amount`, `FineDate`, `PaymentStatus` | Stores overdue fines associated with loans. |
| LibraryEvent | `EventID (PK)`, `EventName`, `EventDate`, `StartTime`, `EndTime`, `Description` | Stores library cultural events. |
| EventRegistration | `RegistrationID (PK)`, `MemberID (FK)`, `EventID (FK)`, `RegistrationDate` | Records members registered for events. |
| Speaker | `SpeakerID (PK)`, `SpeakerName`, `Email`, `Specialization` | Stores speaker or author details. |
| EventSpeaker | `EventID (PK, FK)`, `SpeakerID (PK, FK)` | Associates speakers with events. |
| Room | `RoomID (PK)`, `RoomName`, `Capacity`, `RoomType` | Stores rooms available for events and study. |
| RoomBooking | `BookingID (PK)`, `RoomID (FK)`, `MemberID (FK, nullable)`, `EventID (FK, nullable)`, `BookingDate`, `StartTime`, `EndTime`, `BookingType` | Records room bookings for events or study. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|---|---|---|---|
| Member — Loan | 1:N | Loan: Total; Member: Partial | A member can borrow multiple books. |
| Book — Loan | 1:N | Loan: Total; Book: Partial | A book can appear in multiple loan records over time. |
| Loan — Fine | 1:N | Fine: Total; Loan: Partial | A loan may have no fine or multiple fine records if the library permits separate charges. |
| Member — EventRegistration | 1:N | EventRegistration: Total; Member: Partial | A member can register for multiple events. |
| LibraryEvent — EventRegistration | 1:N | EventRegistration: Total; LibraryEvent: Partial | An event can have multiple registered members. |
| LibraryEvent — EventSpeaker | 1:N | EventSpeaker: Total; LibraryEvent: Total | Each event must have at least one speaker, according to the given requirements. |
| Speaker — EventSpeaker | 1:N | EventSpeaker: Total; Speaker: Partial | A speaker can participate in multiple events. |
| Room — RoomBooking | 1:N | RoomBooking: Total; Room: Partial | A room can be booked multiple times at different times. |
| Member — RoomBooking | 1:N | RoomBooking: Partial; Member: Partial | A member may book a room for study. |
| LibraryEvent — RoomBooking | 1:1 | RoomBooking: Partial; LibraryEvent: Partial | An event may be associated with a room booking. |

### Assumptions
1.Each member, book, event, speaker, and room has a unique identifier.
2.Each loan refers to one book and one member. A book can be borrowed repeatedly over time.
3.A member may register for multiple events, and an event can have multiple registered members.
4.Each event has at least one speaker or author.
5.A room booking can be made for an event or for individual study. It must have a room, a booking date, and a time period.
6.Fine amounts and payment status are stored separately from loan details. The library determines the applicable fine based on its overdue policy.

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="977" height="666" alt="image" src="https://github.com/user-attachments/assets/900f9577-0fce-4e6d-8b70-58dfea9a3337" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---|---|---|
| Customer | `CustomerID (PK)`, `CustomerName`, `Phone`, `Email` | Stores customer details. |
| RestaurantTable | `TableID (PK)`, `TableNumber`, `Capacity`, `TableStatus` | Stores restaurant table information. |
| Reservation | `ReservationID (PK)`, `CustomerID (FK)`, `TableID (FK, nullable)`, `ReservationDate`, `ReservationTime`, `NumberOfGuests`, `ReservationType`, `Status` | Records reservations and walk-in visits. |
| Waiter | `WaiterID (PK)`, `WaiterName`, `Phone` | Stores waiter details. |
| ReservationWaiter | `ReservationID (PK, FK)`, `WaiterID (PK, FK)` | Associates waiters with reservations. |
| FoodOrder | `OrderID (PK)`, `ReservationID (FK)`, `OrderDate`, `OrderTime`, `OrderStatus` | Records food orders associated with reservations. |
| DishCategory | `CategoryID (PK)`, `CategoryName` | Stores categories such as starters, main courses, and desserts. |
| Dish | `DishID (PK)`, `CategoryID (FK)`, `DishName`, `Price`, `Description` | Stores menu items and their categories. |
| OrderItem | `OrderID (PK, FK)`, `DishID (PK, FK)`, `Quantity`, `UnitPrice` | Connects orders with dishes and records quantity and price. |
| Bill | `BillID (PK)`, `ReservationID (FK)`, `FoodAmount`, `ServiceCharge`, `TotalAmount`, `BillDate`, `PaymentStatus` | Stores billing information for each reservation. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|---|---|---|---|
| Customer — Reservation | 1:N | Reservation: Total; Customer: Partial | A customer can make multiple reservations. |
| RestaurantTable — Reservation | 1:N | Reservation: Partial; RestaurantTable: Partial | A table can be reserved multiple times at different times. A walk-in reservation may initially have no table assigned. |
| Reservation — FoodOrder | 1:N | FoodOrder: Total; Reservation: Partial | A reservation can have multiple food orders. |
| FoodOrder — OrderItem | 1:N | OrderItem: Total; FoodOrder: Total | Each order contains one or more order items. |
| Dish — OrderItem | 1:N | OrderItem: Total; Dish: Partial | A dish can appear in multiple order items. |
| DishCategory — Dish | 1:N | Dish: Total; DishCategory: Partial | Each dish belongs to one category. |
| Reservation — ReservationWaiter | 1:N | ReservationWaiter: Total; Reservation: Total | Each reservation is assigned at least one waiter. |
| Waiter — ReservationWaiter | 1:N | ReservationWaiter: Total; Waiter: Partial | A waiter may serve multiple reservations. |
| Reservation — Bill | 1:1 | Bill: Total; Reservation: Partial | Each generated bill belongs to one reservation. A reservation may not yet have a bill. |

### Assumptions
1. Each customer, table, reservation, waiter, order, dish, category, and bill has a unique identifier.
2. Walk-in customers can be recorded as reservations with ReservationType = 'Walk-in'.
3. Each food order belongs to one reservation. A reservation can have multiple orders.
4. An order contains one or more dishes. The OrderItem entity records the quantity and price of each dish at the time of ordering.
5. Each dish belongs to one category.
6. Each reservation is assigned at least one waiter, and a waiter can serve multiple reservations.
7. Each reservation can have at most one bill. The total bill includes food charges and service charges.
8. A table cannot have overlapping reservations during the same time period.

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
