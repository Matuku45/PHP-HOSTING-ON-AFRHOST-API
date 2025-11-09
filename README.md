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

Example request:

https://yourdomain.com/api.php?action=insert&data={"shuttle_id":1,"passengerName":"Thabiso","email":"thabiso@example.com","phone":"+27831234567","route":"Pretoria - Johannesburg","seats":2,"price":200}


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

API Format: JSON-based REST

Security: PDO prepared statements prevent SQL injection.

🚀 Example API Usage

Insert a booking:

GET https://your-afrihost-domain.com/api.php?action=insert&data={"shuttle_id":12345,"passengerName":"Kgabo Thabiso","email":"kgabo@example.com","phone":"+27831234567","route":"Pretoria – Johannesburg","date":"2025-11-10","time":"08:00:00","seats":2,"price":200,"path":"/route/path","car":"Toyota Quantum"}


Get bookings:

GET https://your-afrihost-domain.com/api.php?action=select&limit=10


Response:

{
  "success": true,
  "data": [
    {
      "id": 1,
      "passengerName": "Kgabo Thabiso",
      "route": "Pretoria – Johannesburg",
      "price": "200.00",
      "createdAt": "2025-11-09 02:18:23"
    }
  ]
}
