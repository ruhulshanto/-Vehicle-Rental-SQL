Vehicle Rental System - Database Design & SQL Queries
📋 Project Overview
This project implements a Vehicle Rental System database using PostgreSQL. It includes database schema design, sample data insertion, and SQL queries to demonstrate various database operations.

🗄️ Database Schema
1. Users Table
Stores information about system users (Customers and Admins).

Column	Type	Constraints	Description
user_id	SERIAL	PRIMARY KEY	Unique user identifier
name	VARCHAR(100)	NOT NULL	Full name of the user
email	VARCHAR(100)	UNIQUE, NOT NULL	Email address (must be unique)
phone	VARCHAR(20)	-	Contact phone number
role	VARCHAR(20)	CHECK IN ('Customer', 'Admin')	User role in the system
2. Vehicles Table
Stores information about available rental vehicles.

Column	Type	Constraints	Description
vehicle_id	SERIAL	PRIMARY KEY	Unique vehicle identifier
name	VARCHAR(100)	NOT NULL	Vehicle name/brand
type	VARCHAR(20)	CHECK IN ('car', 'bike', 'truck')	Type of vehicle
model	VARCHAR(50)	-	Vehicle model year
registration_number	VARCHAR(50)	UNIQUE, NOT NULL	Vehicle registration number
rental_price	NUMERIC(10,2)	NOT NULL	Daily rental price
status	VARCHAR(20)	CHECK IN ('available', 'rented', 'maintenance')	Current availability status
3. Bookings Table
Stores booking records connecting users and vehicles.

Column	Type	Constraints	Description
booking_id	SERIAL	PRIMARY KEY	Unique booking identifier
user_id	INT	FOREIGN KEY REFERENCES users(user_id)	User who made the booking
vehicle_id	INT	FOREIGN KEY REFERENCES vehicles(vehicle_id)	Vehicle being booked
start_date	DATE	NOT NULL	Booking start date
end_date	DATE	NOT NULL	Booking end date
status	VARCHAR(20)	CHECK IN ('pending', 'confirmed', 'completed', 'cancelled')	Booking status
total_cost	NUMERIC(10,2)	-	Total cost of booking
🔗 Entity Relationship Diagram (ERD)
The database follows these relationships:

text
Users (1) ----< Bookings (M)
Vehicles (1) ----< Bookings (M)
One-to-Many: One user can have multiple bookings

One-to-Many: One vehicle can have multiple bookings over time

Each booking connects exactly one user to one vehicle

📊 Sample Data
The database is pre-populated with sample data for testing:

Users
Alice (Customer)

Bob (Admin)

Charlie (Customer)

Vehicles
Toyota Corolla (car, available)

Honda Civic (car, rented)

Yamaha R15 (bike, available)

Ford F-150 (truck, maintenance)

Bookings
3 bookings for vehicle ID 2 (Honda Civic)

1 booking for vehicle ID 1 (Toyota Corolla)

📝 SQL Queries
Query 1: JOIN Operation
Purpose: Retrieve booking information with customer and vehicle details.

Expected Output:

booking_id	customer_name	vehicle_name	start_date	end_date	status
1	Alice	Honda Civic	2023-10-01	2023-10-05	completed
2	Alice	Honda Civic	2023-11-01	2023-11-03	completed
3	Charlie	Honda Civic	2023-12-01	2023-12-02	confirmed
4	Alice	Toyota Corolla	2023-12-10	2023-12-12	pending
Query 2: EXISTS Operation
Purpose: Find vehicles that have never been booked.

Expected Output:

vehicle_id	name	type	model	registration_number	rental_price	status
3	Yamaha R15	bike	2023	GHI-789	30	available
4	Ford F-150	truck	2020	JKL-012	100	maintenance
Query 3: WHERE Operation
Purpose: Retrieve all available cars.

Expected Output:

vehicle_id	name	type	model	registration_number	rental_price	status
1	Toyota Corolla	car	2022	ABC-123	50	available
Query 4: GROUP BY and HAVING
Purpose: Find vehicles with more than 2 bookings.

Expected Output:

vehicle_name	total_bookings
Honda Civic	3
🚀 Setup Instructions
Prerequisites
PostgreSQL installed and running

Basic SQL knowledge

Database management tool (pgAdmin, DBeaver, or command line)

Installation Steps
Create a database in PostgreSQL:

sql
CREATE DATABASE vehicle_rental_system;
Connect to the database:

sql
\c vehicle_rental_system;
Execute the SQL script:

Copy the entire SQL code from vehicle_rental_system.sql

Execute it in your PostgreSQL environment

The script will:

Create all tables with constraints

Insert sample data

Run all demonstration queries

Alternative: Execute via File
bash
psql -U username -d vehicle_rental_system -f vehicle_rental_system.sql
📚 Learning Objectives
This project demonstrates:

✅ Database table design with proper constraints

✅ ERD relationships (1-to-Many, Many-to-1)

✅ Primary and Foreign Key implementation

✅ SQL queries using JOIN, EXISTS, WHERE, GROUP BY, HAVING

✅ Data integrity through CHECK constraints

🔧 Technical Features
Data Integrity: UNIQUE constraints on email and registration number

Referential Integrity: Foreign key constraints maintain relationship integrity

Domain Constraints: CHECK constraints validate role, type, and status values

Auto-incrementing IDs: SERIAL data type for primary keys

🧪 Testing the Queries
After executing the script, you can manually test each query by:

Connecting to the vehicle_rental_system database

Running individual query sections

Verifying outputs match expected results

📁 File Structure
text
vehicle-rental-system/
├── README.md               # This documentation file
├── vehicle_rental_system.sql  # Complete SQL script
└── erd_diagram.png         # Entity Relationship Diagram
🤝 Contributing
To contribute to this project:

Fork the repository

Create a feature branch

Make your changes

Test thoroughly

Submit a pull request

📄 License
This project is created for educational purposes as part of a database design assignment.

👨‍🏫 Author
Student Name
Database Design Assignment
Vehicle Rental System Project
