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
![WhatsApp Image 2025-10-06 at 13 55 01_a83a1c8a](https://github.com/user-attachments/assets/31c4f50a-773b-4d86-897d-991e2c2cc9a5)


### Entities and Attributes
| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Members** | `member_id` (PK), `member_name`, `membership_type`, `start_date`, `contact_info` | Stores primary information for each gym member. |
| **Trainers** | `trainer_id` (PK), `trainer_name`, `specialization` | Contains details for each fitness trainer. |
| **Programs** | `program_id` (PK), `program_name`, `description` | Lists all available fitness programs like Yoga or Zumba. |
| **Member_Enrollments** | `enrollment_id` (PK), `member_id` (FK), `program_id` (FK), `enrollment_date` | A junction table linking members to the programs they join. |
| **Personal_Sessions** | `session_id` (PK), `member_id` (FK), `trainer_id` (FK), `session_datetime` | Records one-on-one training sessions booked by members. |
| **Attendance** | `attendance_id` (PK), `session_id` (FK, UNIQUE), `status` | Tracks if a member attended their scheduled personal session. |
| **Payments** | `payment_id` (PK), `member_id` (FK), `related_session_id` (FK), `amount`, `payment_date`, `payment_for` | Logs all payments for memberships and sessions. |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
| :--- | :--- | :--- | :--- |
| **Members ↔ Programs** | Many-to-Many (M:N) | **Optional** on both sides. | A member can join multiple programs, and a program has multiple members. Implemented via the `Member_Enrollments` table. |
| **Members → Personal Sessions** | One-to-Many (1:N) | **Optional** for Members, **Mandatory** for Sessions. | One member can book many personal sessions, but each session must belong to exactly one member. |
| **Trainers → Personal Sessions** | One-to-Many (1:N) | **Optional** for Trainers, **Mandatory** for Sessions. | One trainer can conduct many sessions, but each session must be assigned to exactly one trainer. |
| **Personal Sessions ↔ Attendance** | One-to-One (1:1) | **Optional** for Sessions, **Mandatory** for Attendance. | Each session has one corresponding attendance record, which is created after the session time. |
| **Members → Payments** | One-to-Many (1:N) | **Optional** for Members, **Mandatory** for Payments. | One member can make many payments, but every payment must be linked to a member. |
| **Personal Sessions → Payments** | One-to-One (1:1) | **Optional** on both sides. | A payment might be for a specific session, but not all payments are for sessions (e.g., membership fees). |

### Assumptions
- Scope of Attendance Tracking
The schema assumes that attendance tracking is primarily required for personal training sessions, not for general group programs like Yoga or Zumba. There is no Class_Schedule table or a mechanism to record attendance for multiple members in a single group event.
- Simple Membership Model
It is assumed that the membership_type is a simple descriptive label (e.g., 'Monthly', 'Annual') and does not carry complex rules. The design does not account for different access rights, booking privileges, or automated billing cycles based on the membership tier, which would require a more detailed Membership_Plans table.
- Straightforward Financials
The Payments table assumes a simple, direct transaction model. It doesn't handle more complex financial scenarios such as installment plans, automatic recurring billing, discounts, promotional credits, or different pricing for the same service (e.g., peak vs. off-peak session rates).

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
![WhatsApp Image 2025-10-06 at 14 03 03_90c63f53](https://github.com/user-attachments/assets/d1f20e26-bd75-4dcb-8ce9-2e66b534ed66)


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Members** | `member_id` (PK), `member_name`, `join_date`, `contact_info` | Stores information for each library member. |
| **Authors** | `author_id` (PK), `author_name`, `bio` | A normalized table for book authors. |
| **Categories** | `category_id` (PK), `category_name` | A normalized table for book genres/categories. |
| **Books** | `book_id` (PK), `author_id` (FK), `category_id` (FK), `title`, `isbn`, `status` | Contains details for every book in the library's collection. |
| **Book_Loans** | `loan_id` (PK), `book_id` (FK), `member_id` (FK), `loan_date`, `due_date`, `return_date` | Tracks every book lending transaction. `return_date` is NULL until returned. |
| **Fines** | `fine_id` (PK), `loan_id` (FK), `member_id` (FK), `amount`, `issue_date`, `status` | Logs overdue fines linked to a specific loan. |
| **Events** | `event_id` (PK), `event_name`, `event_datetime`, `description` | Stores details about cultural events organized by the library. |
| **Speakers** | `speaker_id` (PK), `speaker_name`, `bio` | Contains information about event speakers or guest authors. |
| **Event_Speakers**| `event_speaker_id` (PK), `event_id` (FK), `speaker_id` (FK) | Junction table linking events to their multiple speakers. |
| **Event_Registrations**|`registration_id` (PK), `event_id` (FK), `member_id` (FK), `registration_date`| Junction table linking members to the events they registered for. |
| **Rooms** | `room_id` (PK), `room_name`, `capacity`, `type` | Lists all available rooms for events or study. |
| **Room_Bookings** | `booking_id` (PK), `room_id` (FK), `event_id` (FK), `member_id` (FK), `start_time`, `end_time` | Records all room reservations for events or personal study. |

### Relationships and Constraints
| Relationship | Cardinality | Participation | Notes |
| :--- | :--- | :--- | :--- |
| **Members ↔ Books** | Many-to-Many (M:N) | **Optional** on both sides. | Managed through the `Book_Loans` table. A member can borrow many books over time. |
| **Authors → Books** | One-to-Many (1:N) | **Optional** for Authors, **Mandatory** for Books. | Each book must have an author, but an author might not have books in this library. |
| **Members ↔ Events** | Many-to-Many (M:N) | **Optional** on both sides. | Managed through `Event_Registrations`. A member can attend multiple events. |
| **Events ↔ Speakers** | Many-to-Many (M:N) | **Optional** for Events, **Mandatory** for this link. | Managed through `Event_Speakers`. An event can have one or more speakers. |
| **Rooms ↔ Events/Members** | One-to-Many (1:N) | **Optional** for Rooms, **Mandatory** for Bookings. | A room can be booked many times. A booking must be for a room. |
| **Book_Loans → Fines** | One-to-One (1:1) | **Optional** on both sides. | A single late loan generates one fine. Not all loans result in a fine. |

### Assumptions
- One Author Per Book: The schema assumes each book has only one primary author. To support multiple authors per book, a junction table (Book_Authors) would be needed between Books and Authors.
- Simple Room Bookings: It's assumed that room bookings do not have conflicting schedules. The application layer would be responsible for preventing double-booking a room for the same time slot.
- Static Fine Calculation: The Fines table stores a fixed amount. This assumes the fine is calculated externally and logged. It does not automatically calculate fines based on how many days a book is overdue, which would require more complex application logic.

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
![WhatsApp Image 2025-10-06 at 14 10 26_11a3e6d0](https://github.com/user-attachments/assets/27ef194f-b05c-47b5-9814-a9c663cb908e)


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
| :--- | :--- | :--- |
| **Customers** | `customer_id` (PK), `customer_name`, `phone_number` | Stores details of customers who make reservations. |
| **Waiters** | `waiter_id` (PK), `waiter_name` | A list of all waitstaff members. |
| **Tables** | `table_id` (PK), `table_number`, `capacity` | Represents the physical tables in the restaurant. |
| **Reservations** | `reservation_id` (PK), `customer_id` (FK), `table_id` (FK), `waiter_id` (FK), `reservation_time`, `num_guests`, `status` | Central table tracking all table bookings and walk-ins. |
| **Menu_Categories** | `category_id` (PK), `category_name` | Stores dish categories (e.g., 'Starter', 'Main Course'). |
| **Dishes** | `dish_id` (PK), `category_id` (FK), `dish_name`, `price`, `description` | The restaurant's menu items. |
| **Orders** | `order_id` (PK), `reservation_id` (FK), `order_time` | Represents a single order placed by a table. |
| **Order_Items** | `order_item_id` (PK), `order_id` (FK), `dish_id` (FK), `quantity`, `item_price` | A junction table listing each dish and its quantity within an order. |
| **Bills** | `bill_id` (PK), `reservation_id` (FK), `food_total`, `service_charge`, `grand_total`, `bill_time`, `status` | Contains the final financial details for a reservation. |
### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
| :--- | :--- | :--- | :--- |
| **Customers → Reservations** | One-to-Many (1:N) | **Optional** for Customers, **Optional** for Reservations. | A customer can make many reservations. A reservation might not have a pre-registered customer (for walk-ins). |
| **Waiters → Reservations** | One-to-Many (1:N) | **Optional** for Waiters, **Mandatory** for Reservations. | A waiter can serve many tables, but each reservation must have an assigned waiter. |
| **Reservations → Orders** | One-to-Many (1:N) | **Optional** for Reservations, **Mandatory** for Orders. | A table can place multiple orders (e.g., drinks, then food), but every order must belong to a reservation. |
| **Orders ↔ Dishes** | Many-to-Many (M:N) | **Optional** on both sides. | Managed via the `Order_Items` table. An order can have many dishes, and a dish can be in many orders. |
| **Reservations → Bills** | One-to-One (1:1) | **Optional** for Reservations, **Mandatory** for Bills. | Each reservation results in exactly one bill. |

### Assumptions
- Single Waiter Assignment: The schema assumes that one primary waiter is assigned to each reservation. It does not model scenarios where multiple waiters serve a single table collaboratively.
- Simple Billing Model: It is assumed that bills are generated for the entire table. The design does not natively support splitting bills among guests or applying complex, item-specific discounts.
- Walk-ins as Reservations: The system assumes a walk-in customer is treated as an immediate reservation. The customer_id in the Reservations table can be optional (NULL) to accommodate guests who do not provide contact details.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
