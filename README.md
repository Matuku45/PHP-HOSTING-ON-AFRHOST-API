# PHP-HOSTING-ON-AFRHOST-API

📘 Project Title:

PHP Hosting on Afrihost — Shuttle Booking API

🧩 Project Description:

This project hosts a PHP-based REST API on Afrihost web hosting, connected to a MySQL database.
It allows external clients (for example, mobile apps, websites, or other APIs) to read from and write to the database pool securely.

The database stores booking information for a Shuttle Service, including details like passenger name, contact info, route, and price.

⚙️ Core Functionality:

Database Connection

Connects to a remote MySQL database hosted on Afrihost.

Uses PDO for secure and reliable database access.

Example:

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$pdo = new PDO($dsn, $user, $pass, $options);


Public API Endpoints

The system exposes simple GET endpoints for CRUD operations:

?action=select → Fetch all bookings

?action=insert → Add a new booking

?action=create_table → Create new tables dynamically

Dynamic Data Handling

JSON-based data exchange for easy integration with external systems.



Web Interface (Admin Panel)

The same api.php file includes an HTML management page:

View, edit, and delete records

Create new tables

Monitor API status

🗄️ Database Structure (Table: bookings):
Column	Type	Description
id	INT (PK, Auto Increment)	Unique booking ID
shuttle_id	VARCHAR(20)	Internal shuttle reference
passengerName	VARCHAR(100)	Passenger full name
email	VARCHAR(100)	Passenger email address
phone	VARCHAR(20)	Passenger contact number
route	VARCHAR(255)	Shuttle route (e.g., “Pretoria – Johannesburg”)
date	DATE	Travel date
time	TIME	Departure time
seats	INT	Number of seats booked
price	DECIMAL(10,2)	Booking cost
path	TEXT	Route path or metadata
car	VARCHAR(100)	Vehicle name or model
createdAt	DATETIME	When the record was created
updatedAt	DATETIME (nullable)	Last update time
🔓 Purpose of the API Exposure:

You’re exposing the API so that:

External clients (mobile or web) can submit shuttle bookings directly.

Partner systems can read booking data for analytics or coordination.

Developers can integrate their own interfaces without direct database credentials.

🧰 Tools and Environment:

Hosting Provider: Afrihost

Backend Language: PHP (version 7.4+)

Database: MySQL (via phpMyAdmin)

API Format: JSON-based RE


-- Table: users
CREATE TABLE `users` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `name` VARCHAR(100) NOT NULL,
  `email` VARCHAR(100) UNIQUE NOT NULL,
  `phone` VARCHAR(20),
  `password` VARCHAR(255) NOT NULL,
  `role` ENUM('admin', 'passenger', 'user') DEFAULT 'user',
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- Table: shuttles
CREATE TABLE `shuttles` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `route` VARCHAR(255) NOT NULL,
  `date` DATE NOT NULL,
  `time` TIME NOT NULL,
  `duration` VARCHAR(100) NOT NULL,
  `pickup` VARCHAR(255) NOT NULL,
  `seats` INT NOT NULL,
  `price` DECIMAL(10,2) NOT NULL,
  `updated_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- Table: location_forms
CREATE TABLE `location_forms` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `fromLocation` VARCHAR(255) NOT NULL,
  `toLocation` VARCHAR(255) NOT NULL,
  `email` VARCHAR(255) NOT NULL,
  `createdAt` TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  `updatedAt` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- Table: directions
CREATE TABLE `directions` (
  `id` CHAR(36) PRIMARY KEY,  -- store UUID from Node.js
  `email` VARCHAR(255) NOT NULL,
  `path` TEXT NOT NULL,
  `createdAt` TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  `updatedAt` TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- Table: payments
CREATE TABLE `payments` (
  `id` INT AUTO_INCREMENT PRIMARY KEY,
  `passenger_name` VARCHAR(100) NOT NULL,
  `passenger_phone` VARCHAR(20),
  `shuttle_id` VARCHAR(50) NOT NULL,
  `booking_id` INT DEFAULT NULL,
  `seats` INT NOT NULL,
  `amount` DECIMAL(10,2) NOT NULL,
  `status` VARCHAR(50) NOT NULL,
  `car` VARCHAR(100) DEFAULT 'Toyota Hiace',
  `payment_date` DATETIME DEFAULT CURRENT_TIMESTAMP,
  `created_at` DATETIME DEFAULT CURRENT_TIMESTAMP,
  `updated_at` DATETIME NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

-- Table: api_pool (already exists, example)
-- SELECT * FROM `api_pool`;

