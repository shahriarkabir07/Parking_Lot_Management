# 🚗 Parking Lot Management System

A console-based Parking Lot Management System built with **Java** and **MySQL**. It allows admins to manage vehicles, assign parking spots, track entry/exit times, and calculate parking fees automatically.

---

## 📋 Features

- 🔐 **Admin Authentication** — Register and log in as an admin
- 🚘 **Vehicle Management** — Add, view, search, update, and delete vehicles
- 🅿️ **Parking Operations** — Park and unpark vehicles with auto spot assignment
- 🗺️ **Parking Map** — Visual grid showing occupied and free spots
- 💰 **Fee Calculation** — Automatic fee based on vehicle type and duration
- 📊 **Vehicle Summary** — Count of vehicles by type

---

## 🛠️ Tech Stack

| Layer      | Technology          |
|------------|---------------------|
| Language   | Java (JDK 17+)      |
| Database   | MySQL               |
| Connector  | MySQL Connector/J   |
| IDE        | Apache NetBeans     |
| Build Tool | Apache Ant          |

---

## 🗄️ Database Setup

1. Open **MySQL** and create the database:

```sql
CREATE DATABASE parking_system;
USE parking_system;
```

2. Create the required tables:

```sql
CREATE TABLE admin (
    name     VARCHAR(100),
    phone    VARCHAR(20),
    email    VARCHAR(100),
    password VARCHAR(100)
);

CREATE TABLE owner (
    id        VARCHAR(20) PRIMARY KEY,
    name      VARCHAR(100),
    phone     VARCHAR(20),
    vehicleId VARCHAR(20)
);

CREATE TABLE vehicle (
    id        VARCHAR(20) PRIMARY KEY,
    plate     VARCHAR(50) UNIQUE,
    ownerId   VARCHAR(20),
    ownerName VARCHAR(100),
    phone     VARCHAR(20),
    type      VARCHAR(50),
    parked    BOOLEAN DEFAULT FALSE,
    spot      INT DEFAULT 0,
    entryTime BIGINT DEFAULT 0
);
```

---

## ⚙️ Configuration

In `DBConnection.java`, update your MySQL credentials if needed:

```java
String url      = "jdbc:mysql://localhost:3306/parking_system";
String user     = "root";
String password = "";   // ← change to your MySQL password
```

---

## 🚀 How to Run

### Option 1 — NetBeans IDE
1. Open NetBeans and select **File → Open Project**
2. Choose the `ParkingLotManagementSystem` folder
3. Make sure the **MySQL Connector/J** JAR is added to the project libraries
4. Press **Run (F6)**

### Option 2 — Command Line
```bash
# Compile
javac -cp .;mysql-connector-j-x.x.x.jar -d build/classes src/parkinglotmanagementsystem/*.java

# Run
java -cp build/classes;mysql-connector-j-x.x.x.jar parkinglotmanagementsystem.Main
```
> On Linux/macOS replace `;` with `:` in the classpath.

---

## 📂 Project Structure

```
ParkingLotManagementSystem/
├── src/
│   └── parkinglotmanagementsystem/
│       ├── Main.java           # Entry point
│       ├── ParkingService.java # Core business logic & menus
│       ├── DBConnection.java   # MySQL connection setup
│       ├── Vehicle.java        # Vehicle model
│       ├── Owner.java          # Owner model
│       └── Admin.java          # Admin model
├── build/                      # Compiled .class files
├── nbproject/                  # NetBeans project config
├── build.xml                   # Ant build script
└── manifest.mf
```

---

## 💵 Parking Fee Rates

| Vehicle Type | Rate (per hour) |
|--------------|-----------------|
| Bike         | 20 BDT          |
| Car (default)| 50 BDT          |
| Truck        | 100 BDT         |

> Minimum charge is **1 hour**. Partial hours are rounded up.

---

## 🖥️ Menu Overview

```
====== PARKING SYSTEM ======
1. Login
2. Register Admin
3. Exit

===== ADMIN MENU =====
1. Add Vehicle
2. View Vehicles
3. Park Vehicle
4. Unpark Vehicle
5. Search Vehicle
6. Update Vehicle
7. Delete Vehicle
8. View Parking Map
9. Fee Summary
10. Exit
```

---

## 📌 Notes

- The system supports **50 parking spots** by default (`TOTAL_SPOTS = 50` in `ParkingService.java`)
- Vehicle IDs are auto-generated (e.g., `VH1`, `VH2`) and Owner IDs as (`OWN1`, `OWN2`)
- Passwords are stored in plain text — consider hashing for production use

---

## 👥 Team

This project was built collaboratively by:

| Name               |
|--------------------|
| 👩‍💻 Jeb-Un-Nesa Tithy |
| 👨‍💻 Nishat Pranto     |
| 👨‍💻 Shahriar Kabir    |

Developed as a Java console project using NetBeans and MySQL.
