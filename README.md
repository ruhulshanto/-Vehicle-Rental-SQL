# 🚗 Vehicle Rental System – Database Design & SQL Queries

## 📋 Project Overview
This project implements a **Vehicle Rental System database** using **PostgreSQL**.  
It focuses on **database schema design**, **data integrity**, **sample data insertion**, and **SQL queries** to demonstrate common database operations used in real-world systems.

---

## 🗄️ Database Schema

### 1️⃣ Users Table
Stores information about system users (Customers and Admins).

| Column | Type | Constraints | Description |
|------|------|------------|-------------|
| user_id | SERIAL | PRIMARY KEY | Unique user identifier |
| name | VARCHAR(100) | NOT NULL | Full name of the user |
| email | VARCHAR(100) | UNIQUE, NOT NULL | Email address (must be unique) |
| phone | VARCHAR(20) | — | Contact phone number |
| role | VARCHAR(20) | CHECK ('Customer', 'Admin') | User role in the system |

---

### 2️⃣ Vehicles Table
Stores information about available rental vehicles.

| Column | Type | Constraints | Description |
|------|------|------------|-------------|
| vehicle_id | SERIAL | PRIMARY KEY | Unique vehicle identifier |
| name | VARCHAR(100) | NOT NULL | Vehicle name or brand |
| type | VARCHAR(20) | CHECK ('car', 'bike', 'truck') | Type of vehicle |
| model | VARCHAR(50) | — | Vehicle model year |
| registration_number | VARCHAR(50) | UNIQUE, NOT NULL | Vehicle registration number |
| rental_price | NUMERIC(10,2) | NOT NULL | Daily rental price |
| status | VARCHAR(20) | CHECK ('available', 'rented', 'maintenance') | Availability status |

---

### 3️⃣ Bookings Table
Stores booking records connecting users and vehicles.

| Column | Type | Constraints | Description |
|------|------|------------|-------------|
| booking_id | SERIAL | PRIMARY KEY | Unique booking identifier |
| user_id | INT | FOREIGN KEY → users(user_id) | User who made the booking |
| vehicle_id | INT | FOREIGN KEY → vehicles(vehicle_id) | Vehicle being booked |
| start_date | DATE | NOT NULL | Booking start date |
| end_date | DATE | NOT NULL | Booking end date |
| status | VARCHAR(20) | CHECK ('pending', 'confirmed', 'completed', 'cancelled') | Booking status |
| total_cost | NUMERIC(10,2) | — | Total booking cost |

---

## 🔗 Entity Relationship Diagram (ERD)

Users (1) ----< Bookings (M)
Vehicles (1) ----< Bookings (M)


**Relationship Explanation:**
- One user can create **multiple bookings**
- One vehicle can be booked **multiple times over different periods**
- Each booking links **exactly one user** with **one vehicle**

---

## 📊 Sample Data

### 👤 Users
- Alice (Customer)
- Bob (Admin)
- Charlie (Customer)

### 🚘 Vehicles
- Toyota Corolla (car, available)
- Honda Civic (car, rented)
- Yamaha R15 (bike, available)
- Ford F-150 (truck, maintenance)

### 📑 Bookings
- 3 bookings for **Honda Civic**
- 1 booking for **Toyota Corolla**

---

## 📝 SQL Queries

### 🔹 Query 1: JOIN Operation
**Purpose:** Retrieve booking information along with customer and vehicle details.

**Expected Output:**

| booking_id | customer_name | vehicle_name | start_date | end_date | status |
|-----------|---------------|--------------|------------|----------|--------|
| 1 | Alice | Honda Civic | 2023-10-01 | 2023-10-05 | completed |
| 2 | Alice | Honda Civic | 2023-11-01 | 2023-11-03 | completed |
| 3 | Charlie | Honda Civic | 2023-12-01 | 2023-12-02 | confirmed |
| 4 | Alice | Toyota Corolla | 2023-12-10 | 2023-12-12 | pending |

---

### 🔹 Query 2: EXISTS Operation
**Purpose:** Find vehicles that have **never been booked**.

**Expected Output:**

| vehicle_id | name | type | model | registration_number | rental_price | status |
|-----------|------|------|-------|---------------------|--------------|--------|
| 3 | Yamaha R15 | bike | 2023 | GHI-789 | 30 | available |
| 4 | Ford F-150 | truck | 2020 | JKL-012 | 100 | maintenance |

---

### 🔹 Query 3: WHERE Operation
**Purpose:** Retrieve all **available cars**.

**Expected Output:**

| vehicle_id | name | type | model | registration_number | rental_price | status |
|-----------|------|------|-------|---------------------|--------------|--------|
| 1 | Toyota Corolla | car | 2022 | ABC-123 | 50 | available |

---

### 🔹 Query 4: GROUP BY & HAVING
**Purpose:** Find vehicles with **more than 2 bookings**.

**Expected Output:**

| vehicle_name | total_bookings |
|-------------|----------------|
| Honda Civic | 3 |

---

## 🚀 Setup Instructions

### Prerequisites
- PostgreSQL installed and running
- Basic SQL knowledge
- Database tool (pgAdmin, DBeaver, or terminal)

---

### Installation Steps

1. Create the database:
```sql
CREATE DATABASE vehicle_rental_system;

2. Connect to the database:

\c vehicle_rental_system;

3. Execute the SQL script:
Copy and run vehicle_rental_system.sql

OR via terminal:
psql -U username -d vehicle_rental_system -f vehicle_rental_system.sql


📚 Learning Objectives
This project demonstrates:
✅ Proper database table design
✅ ERD relationships (1-to-Many, Many-to-1)
✅ Primary and Foreign Key usage
✅ SQL queries using JOIN, EXISTS, WHERE, GROUP BY, HAVING
✅ Data validation using CHECK constraints

🔧 Technical Features


Data Integrity: UNIQUE constraints on email & registration number


Referential Integrity: Foreign keys enforce valid relationships


Domain Constraints: CHECK constraints restrict invalid values


Auto-increment IDs: SERIAL primary keys



📁 File Structure
vehicle-rental-system/
├── README.md
├── vehicle_rental_system.sql
└── erd_diagram.png


📄 License
This project is created strictly for educational purposes as part of a database design assignment.

👨‍🎓 Author
Ruhul Amin Shanto
Database Design Assignment
Vehicle Rental System Project

---

### ✅ Why this version is **professional**
✔ Academic tone  
✔ Clean Markdown formatting  
✔ Clear objectives + expected output  
✔ Teacher-friendly  
✔ GitHub-ready  

If you want:
- **Even more formal university style**
- **Shorter version**
- **Bangla README**
- **ERD explanation paragraph for viva**

Just tell me 👍
