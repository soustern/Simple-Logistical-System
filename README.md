# SLS - Simple Logistical System

SLS is a comprehensive, command-line logistical management system built entirely in **C**. It provides a robust, user-friendly interface for managing inventory, personnel, and suppliers with a strong emphasis on data integrity, security, and best practices.

### ▶️ [Watch the Video Demo on YouTube](https://www.youtube.com/watch?v=pSxkruwjchE)

---

## Key Features

*   **Full CRUD Functionality:** Create, Read, Search, Edit, and Remove items across three distinct categories.
*   **Data Models:**
    *   **Products:** Track items by name, quantity, and value.
    *   **Providers:** Manage supplier information, including contacts and location.
    *   **Employees:** Maintain a record of staff, positions, and salaries.
*   **Role-Based Access Control:**
    *   **Admin Accounts:** Full access to all features, including item management and account creation.
    *   **Limited Accounts:** Read-only access for viewing items and generating reports.
*   **Advanced Search:** Filter data using multiple criteria to find specific entries quickly.
*   **Reporting:** Generate useful reports from the system's data.
*   **Secure Account Management:** A complete system for account creation, login, and removal.

## Tech Stack

*   **Language:** C (C99 standard)
*   **Core Concepts:** Manual Memory Management, File I/O, Hash Tables, Structs
*   **Compiler:** GCC / Clang
*   **Build:** Make (optional, but recommended)

## Getting Started

To compile and run the project on a local machine, you will need a C compiler like GCC.

### Prerequisites

*   GCC or an equivalent C compiler
*   Make (optional, for easy compilation)

### Installation & Execution

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/your-username/Simple-Logistical-System.git
    ```
2.  **Navigate to the project directory:**
    ```sh
    cd Simple-Logistical-System
    ```
3.  **Compile the source files:**
    ```sh
    gcc -o sls sls.c functions_admin.c functions_general.c functions_limited.c tutorials.c
    ```
4.  **Run the application:**
    ```sh
    ./sls
    ```

> On the first run, the system will automatically guide you through creating an initial **admin** account.

## Usage Guide

SLS operates via a simple menu-driven interface. After logging in, you will be presented with a list of options that you can select by typing the corresponding number and pressing `ENTER`.

*   **Admin Users** can perform all actions, including adding, editing, and removing items or user accounts.
*   **Limited Users** can only view items and reports, ensuring data safety.
*   The system is designed to be intuitive, with prompts guiding you through every step, from creating a product to searching for an employee. An in-program manual is also available for detailed guidance.

## Architectural Overview

This project was developed with a strong emphasis on code organization, efficiency, and fundamental computer science principles.

### Data Structures

*   The core of the data management relies on **hash tables**. Each data type (accounts, products, employees, dealers) is stored in its own hash table in memory for fast lookups, insertions, and deletions (`O(1)` average time complexity).
*   All data models are defined using `structs` in the `functions.h` header file to ensure type safety and structured data handling.

### Data Persistence

*   All data is persisted to `.txt` files acting as a simple database.
*   The `load_*_databases()` functions read data from these files on startup, populating the in-memory hash tables.
*   All create, update, or delete operations are immediately written back to the corresponding file, ensuring data integrity between sessions. The files are opened in the appropriate modes (`"w"` for overwrite, `"a"` for append) to handle data manipulation safely.

### Modular Codebase

The program is componentized into multiple `.c` files, each with a specific responsibility, to promote modularity and maintainability:

*   **`sls.c`**: The main entry point of the program. Handles the initial setup and login flow.
*   **`functions.h`**: The header file defining all function prototypes, structs, and constants.
*   **`functions_admin.c`**: Contains all functions exclusive to the "Admin" user role (e.g., creating/deleting items and accounts).
*   **`functions_limited.c`**: Contains functions exclusive to the "Limited" user role.
*   **`functions_general.c`**: Holds functions shared by both user types (e.g., login, searching, displaying items, hash functions).
*   **`tutorials.c`**: Contains functions responsible for printing the manual and other informational text to the console.

### Memory Management

Being a C program, manual memory management is critical. The `unload_*_databases()` functions are responsible for iterating through the hash tables and freeing all dynamically allocated memory (`malloc`) before the program exits, preventing memory leaks.
