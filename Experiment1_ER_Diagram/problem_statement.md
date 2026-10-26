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
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_fitness.png)

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
1. Each member, book, event, speaker, and room has a unique identifier.
2. Each loan refers to one book and one member. A book can be borrowed repeatedly over time.
3. A member may register for multiple events, and an event can have multiple registered members.
4. Each event has at least one speaker or author.
5. A room booking can be made for an event or for individual study. It must have a room, a booking date, and a time period.
6. Fine amounts and payment status are stored separately from loan details. The library determines the applicable fine based on its overdue policy.

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
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_library.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

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
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
