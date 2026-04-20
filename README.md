# Table-Based Restaurant Management System (TBRMS)

A Java console application for managing core restaurant operations — including user authentication, order processing, inventory tracking, and staff management.

---

## Features

- **User Authentication** — Register and log in with username/password validation
- **Order Management** — Place orders, track order history, and view total sales
- **Inventory System** — Add items with prices, monitor stock levels, and receive low-stock alerts
- **Menu Display** — View available items with prices in GBP (£)
- **Staff Management** — Add and view staff members
- **Billing** — Print bill functionality

---

## Project Structure

```
university-java-assignment/
├── Main.java            # Application entry point — welcome menu (Register / Login / Exit)
├── LoginForm.java       # Login UI — validates credentials via UserStore
├── RegisterForm.java    # Registration UI — stores new users via UserStore
├── UserStore.java       # In-memory user store (HashMap-backed)
├── OrderMenu.java       # Main dashboard post-login — orders, inventory, sales, logout
├── InventoryManager.java# Inventory CRUD — stock levels, prices, low-stock alerts
├── StaffManager.java    # Staff list management
└── Login.java           # Legacy login module (hardcoded credentials)
```

---

## Getting Started

### Prerequisites

- Java JDK 8 or later
- A terminal / command prompt

### Compile

```bash
javac *.java
```

### Run

```bash
java Main
```

---

## Usage

On launch, you are presented with the main menu:

```
==============================
  Welcome to TBRMS
==============================
1. Register
2. Login
3. Exit
```

**Register** a new account, then **Login** to access the full dashboard:

```
====== ORDER MENU ======
1.  View Menu
2.  Place Order
3.  Print Bill
4.  Inventory Reminder
5.  View Sales
6.  Logout
7.  Add Inventory Items
8.  View Stock
9.  Send Low Stock Reminder
10. View Order History
```

---

## Architecture

```
Main
 ├── RegisterForm  ──▶  UserStore (HashMap)
 └── LoginForm     ──▶  UserStore (validate)
                           └── OrderMenu
                                 ├── InventoryManager
                                 └── StaffManager
```

All data is held **in-memory** — state resets when the application exits.

---

## Classes at a Glance

| Class | Responsibility |
|---|---|
| `Main` | Entry point; routes to register or login |
| `LoginForm` | Prompts for credentials, delegates to `UserStore` |
| `RegisterForm` | Collects new credentials, stores via `UserStore` |
| `UserStore` | Static HashMap store for username → password pairs |
| `OrderMenu` | Post-login dashboard; orchestrates all operations |
| `InventoryManager` | Manages stock map and price map; triggers low-stock alerts |
| `StaffManager` | Stores and displays staff names |

---

## Tech Stack

- **Language:** Java (Standard Edition)
- **Libraries:** Java Standard Library only (`java.util.*`)
- **Build:** Manual `javac` compilation — no Maven or Gradle required
- **Storage:** In-memory (`HashMap`, `ArrayList`)

---

## Limitations

- No data persistence — all data is lost on exit
- No password hashing — passwords stored as plain text
- `StaffManager` is implemented but not yet wired into the active menu
- `totalSales` tracked as an integer (no decimal precision for currency)

---

## License

This project is for educational purposes as part of a university Java assignment.
