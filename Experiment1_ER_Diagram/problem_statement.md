# ER Diagram Workshop – Submission Template
## Name: DINESH S
## Register No: 212224240038
## Date: 28-10-2026
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
<img width="1312" height="682" alt="image" src="https://github.com/user-attachments/assets/1de405da-bf9e-494e-b95c-fbe7e36ead49" />


### Entities and Attributes

| Entity  | Attributes (PK, FK)                                                | Notes                                                     |
| ------- | ------------------------------------------------------------------ | --------------------------------------------------------- |
| MEMBER  | **Member_ID (PK)**, Name, Membership_Type, Start_Date              | Stores gym member details                                 |
| PROGRAM | **Program_ID (PK)**, Program_Name, Schedule, Fee                   | Stores fitness programs offered                           |
| TRAINER | **Trainer_ID (PK)**, Name, Specialization, Phone                   | Stores trainer information; Phone is shown as multivalued |
| SESSION | **Session_ID (PK)**, Session_Date, Session_Time, Attendance_Status | Stores personal/program session details and attendance    |
| PAYMENT | **Payment_ID (PK)**, Amount, Payment_Date, Payment_Type            | Stores membership/session payment details                 |


### Relationships and Constraints

| Relationship                    | Cardinality | Participation                  | Notes                                                                         |
| ------------------------------- | ----------- | ------------------------------ | ----------------------------------------------------------------------------- |
| MEMBER **JOINS** PROGRAM        | M:N         | Partial on both                | A member may join several programs and a program may contain several members  |
| PROGRAM **ASSIGNED TO** TRAINER | M:N         | Partial on both                | A program may have several trainers and a trainer may handle several programs |
| MEMBER **BOOKS** SESSION        | 1:N         | Member–Partial, Session–Total  | One member can book several sessions                                          |
| TRAINER **CONDUCTS** SESSION    | 1:N         | Trainer–Partial, Session–Total | A trainer can conduct multiple sessions                                       |
| MEMBER **MAKES** PAYMENT        | 1:N         | Member–Partial, Payment–Total  | A member can make multiple payments                                           |

### Assumptions
- A member can enroll in more than one fitness program.
- A trainer may be associated with more than one program and conduct multiple sessions.
- Each session records an attendance status, while payments may represent membership or session payments.

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
<img width="1083" height="739" alt="image" src="https://github.com/user-attachments/assets/c0db6759-a7fe-4daa-a212-4d080bfcdbb2" />


### Entities and Attributes

| Entity  | Attributes (PK, FK)                                   | Notes                                           |
| ------- | ----------------------------------------------------- | ----------------------------------------------- |
| MEMBER  | **Member_ID (PK)**, Name, Phone, Join_Date            | Stores registered library member information    |
| BOOK    | **Book_ID (PK)**, Title, Author, Category             | Stores details of books                         |
| FINE    | **Fine_ID (PK)**, Amount, Status                      | Stores overdue fine details                     |
| EVENT   | **Event_ID (PK)**, Event_Name, Event_Date, Event_Type | Stores cultural/library event information       |
| SPEAKER | **Speaker_ID (PK)**, Name, Profile, Contact           | Stores speakers/authors participating in events |
| ROOM    | **Room_ID (PK)**, Room_Name, Capacity, Room_Type      | Stores rooms used for events and study bookings |


### Relationships and Constraints
| Relationship                   | Cardinality | Participation                   | Notes                                                                               |
| ------------------------------ | ----------- | ------------------------------- | ----------------------------------------------------------------------------------- |
| MEMBER **BORROWS** BOOK        | M:N         | Partial on both                 | Members may borrow different books over time                                        |
| BORROW **HAS** FINE            | 1 : 0..1    | Fine–Optional                   | A borrowing transaction may have no fine or one fine                                |
| MEMBER **REGISTERS FOR** EVENT | M:N         | Partial on both                 | Members can register for multiple events                                            |
| EVENT **SPEAKS AT** SPEAKER    | M:N         | Partial/Required by event rules | Events may contain multiple speakers and speakers may attend multiple events        |
| EVENT **HOSTED IN** ROOM       | N:1         | Event–Total                     | Multiple events can use a room at different times; each event is hosted in one room |
| MEMBER **STUDY BOOKING** ROOM  | M:N         | Partial on both                 | Members may book rooms for specified dates and time slots                           |

### Assumptions
- A fine is generated only when a borrowed book is returned late.
- A member may participate in several library events and make several study-room bookings.
- Room bookings and event scheduling occur at different dates/time slots to prevent conflicts.

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
<img width="1083" height="733" alt="image" src="https://github.com/user-attachments/assets/9a3dbcad-e2d4-4164-82b4-8c666e33d8cf" />


### Entities and Attributes
| Entity      | Attributes (PK, FK)                                            | Notes                                                      |
| ----------- | -------------------------------------------------------------- | ---------------------------------------------------------- |
| CUSTOMER    | **Customer_ID (PK)**, Name, Phone, Email                       | Stores customer information; Phone is shown as multivalued |
| TABLE       | **Table_ID (PK)**, Table_No, Capacity, Status                  | Stores restaurant table information                        |
| WAITER      | **Waiter_ID (PK)**, Name, Phone, Shift                         | Stores waiter information                                  |
| RESERVATION | **Reservation_ID (PK)**, Res_Date, Res_Time, Guest_Count, Type | Type identifies Advance or Walk-in                         |
| ORDER       | **Order_ID (PK)**, Order_Date, Order_Status                    | Stores orders associated with reservations                 |
| DISH        | **Dish_ID (PK)**, Dish_Name, Price, Availability               | Stores menu dishes                                         |
| CATEGORY    | **Category_ID (PK)**, Category_Name, Description               | Stores dish categories                                     |
| BILL        | **Bill_ID (PK)**, Food_Charge, Service_Charge, Total_Amount    | Stores billing information                                 |

### Relationships and Constraints

| Relationship                       | Cardinality | Participation                       | Notes                                                                    |
| ---------------------------------- | ----------- | ----------------------------------- | ------------------------------------------------------------------------ |
| CUSTOMER **MAKES** RESERVATION     | 1:N         | Customer–Partial, Reservation–Total | One customer may make several reservations                               |
| RESERVATION **ALLOCATED TO** TABLE | N:1         | Reservation–Total                   | Each reservation is allocated to one table                               |
| RESERVATION **SERVED BY** WAITER   | N:1         | Reservation–Total                   | One waiter can serve several reservations                                |
| RESERVATION **HAS** ORDER          | 1:N         | Reservation–Partial, Order–Total    | A reservation may contain one or more orders                             |
| ORDER **CONTAINS** DISH            | M:N         | Total for Order                     | An order can contain several dishes; a dish can appear in several orders |
| DISH **BELONGS TO** CATEGORY       | N:1         | Dish–Total                          | Several dishes can belong to the same category                           |
| RESERVATION **GENERATES** BILL     | 1:1         | Total                               | Each reservation generates one bill                                      |


### Assumptions
- Both advance bookings and walk-in customers are represented through the RESERVATION entity.
- One reservation is allocated to one table and served by one waiter at a particular time.
- The bill total is calculated from Food_Charge + Service_Charge, while dish quantity is recorded in the CONTAINS relationship.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
