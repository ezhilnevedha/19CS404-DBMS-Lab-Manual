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
<img width="4528" height="2724" alt="image" src="https://github.com/user-attachments/assets/54e2213e-7c85-4734-91e4-be2183489519" />



### Entities and Attributes

| Entity          | Attributes (PK, FK)                                           | Notes                             |
|-----------------|---------------------------------------------------------------|-----------------------------------|
| MEMBERS         |MemberID (PK), Name, MembershipType, StartDate                 |Stores gym members                 |
|PROGRAMS         |ProgramID (PK), ProgramName, ProgramType                       |E.g., Yoga, Zumba                  |
|TRAINERS         |TrainerID (PK), TrainerName, Specialization                    |Each trainer can handle  programs  |
|PERSONAL SESSION |SessionID (PK), MemberID (FK), TrainerID (FK), Date, Time      |Personal training sessions         |
|ATTENDANCE       |AttendanceID (PK), SessionID (FK), MemberID (FK), Status       |Tracks attendance for each session |
|PAYMENTS         |PaymentID (PK), MemberID (FK), Amount, PaymentDate, PaymentType|Tracks membership + PT payments    |

### Relationships and Constraints

| Relationship                 | Cardinality | Participation       |
|------------------------------|------------|----------------------|
|Member –> Program (joins)      | M:N        |Partial on both       |  
|Program –> Trainer (assigned)  | M:N        |Partial on both       |   
|PersonalSession –> Attendance  | 1:N        |Total on attendance   |       
|Member –> Payment              | 1:M        |Partial               |

### Assumptions
- A member can join zero or many fitness programs.
- A program can exist without any members initially.
- A trainer can handle multiple programs, and a program can have multiple trainers.
- Personal training sessions are optional for members.
- Attendance is only recorded for personal training sessions, not regular classes.
- Payments include membership fees and personal session charges.
- Membership types may include Monthly, Quarterly, Yearly.
- A session is associated with exactly one member and one trainer.
- A member may join a program even if no trainer is currently assigned.

---

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
<img width="4844" height="3684" alt="image" src="https://github.com/user-attachments/assets/3601fe86-118f-4c80-8d74-1efdca1881c6" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|------------|----------------------------------------------------------------------|-------|
|MEMBER      |MemberID (PK), Name, Email                                            |Library members|
|BOOK        |BookID (PK), Title, Author, Category                                  |Each book is uniquely identified|
|LOAN        |LoanID (PK), MemberID (FK), BookID (FK), LoanDate, DueDate, ReturnDate|Tracks lending activity|
|FINE        |FineID (PK), LoanID (FK), Amount, PaymentDate                         |For overdue books |
|EVENT       |EventID (PK), EventName, EventDate, RoomID (FK)                       |Cultural/author events       |
|SPEAKER     |SpeakerID (PK), SpeakerName, Expertise                                |Speakers/authors for event       |
|ROOM BOOKING|BookingID (PK), RoomID (FK), EventID (FK), Date                       |Tracks room allocation       |
### Relationships and Constraints

| Relationship | Cardinality | Participation |
|--------------|------------|--------------------------------|
|Member –> Book | 1:M        |Partial on Member, Total on Books|       
|Book –> Loan| 1:M| Total on Loan|     
|Loan –> Fine|1:1|Partial |
|Member –> Event|M:N|Partial|
|Event –> Speaker|M:N|Partial|
|Member -> Room Booking|1:M|Partial on member, total on room booking|
### Assumptions
- A member can borrow multiple books but the same book copy is loaned to only one person at a time.
- A fine is generated only when the return date exceeds the due date.
- Each event is allocated one room for the event time.
- A room can be used for events or study, but not double-booked at the same time.
- An event can have multiple speakers, and a speaker can speak at multiple events.
- Members registering for events is optional.
- Fine payment does not delete loan records; history is maintained.
- Room booking prevents scheduling conflicts by storing date and time.
- Books have only one category; no multi-category classification.
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
<img width="3808" height="2568" alt="image" src="https://github.com/user-attachments/assets/b7a3bf31-ed8f-4495-b1b4-535447b63c56" />


### Entities and Attributes

| Entity     | Attributes (PK, FK) |
|------------|--------------------|
|CUSTOMER    |CustomerID (PK), Name, Phone|       
|RESERVATION |ReservationID (PK), CustomerID (FK), Date, Time, NoOfGuest|
|ORDER       |OrderID (PK), ReservationID (FK), OrderTime|       
|ORDER_ITEM  |OrderID (PK, FK), DishID (PK, FK), Quantity|       
|DISH        |DishID (PK), DishName, Price, Category|

### Relationships and Constraints

| Relationship | Cardinality | Participation |
|--------------|------------|---------------|
|Customer -> Reservation|1 : M |Reservation depends on customer (Total on Reservation)|       
|Reservation → Order|1 : M|A reservation may place multiple orders|       
|Order → Order_Item|1 : M|Each order has multiple dishes (Total on Order_Item)|       
|Dish → Order_Item|1 : M|A dish can appear in many orders|

### Assumptions
- Customers may book tables or walk in; walk-ins still create a reservation record.
- One reservation corresponds to one table only.
- Bills are calculated from order items + service charges.
- Each reservation may have multiple food orders.
- Dishes are classified as a single category (Starter/Main/Dessert).

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
