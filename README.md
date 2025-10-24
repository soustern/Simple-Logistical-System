# SLS - Simple Logistical System (C Edition)

[![Language](https://img.shields.io/badge/Language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Compiler](https://img.shields.io/badge/Compiler-GCC%20%2F%20Clang-lightgrey.svg)](https://gcc.gnu.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

SLS (Simple Logistical System) is a high-performance, command-line logistical management application built from the ground up in pure **C**. It showcases a deep understanding of core computer science fundamentals, including custom data structures, manual memory management, and persistent storage through file I/O.

The system provides a robust, menu-driven interface for managing products, employees, and suppliers, complete with role-based access control and detailed reporting capabilities.

### ▶️ [Watch the Video Demo on YouTube](https://www.youtube.com/watch?v=pSxkruwjchE)

---

## Architectural Highlights & CS Fundamentals

This project was developed with a primary focus on code organization, performance, and the application of fundamental computer science principles in C.

### 1. High-Performance Data Core (Hash Tables)
The core of the application's data management relies on custom-implemented **hash tables**.
- **Performance:** Each data model (accounts, products, employees, dealers) is stored in a dedicated hash table in memory. This provides an average time complexity of **O(1)** for all critical CRUD (Create, Read, Update, Delete) and search operations, ensuring the application remains fast and responsive regardless of data volume.
- **Collision Handling:** Collisions are handled using the **separate chaining** method, where each index in the hash table points to the head of a linked list. This is a classic and robust solution for managing hash collisions.

### 2. Manual Memory Management & Safety
As a pure C application, all memory is managed manually, demonstrating a critical low-level programming skill.
- **Dynamic Allocation:** Memory for all data structures is dynamically allocated on the heap using `malloc`.
- **Leak Prevention:** The `unload_*_databases()` functions are meticulously designed to traverse every hash table and linked list, explicitly calling `free()` on each dynamically allocated node. This ensures that the application releases all memory it has acquired, preventing memory leaks.

### 3. Modular & Maintainable Codebase
The program is componentized into multiple `.c` files, promoting a clean and scalable architecture.
- **Separation of Concerns:**
  - **`sls.c`**: Main entry point, handling the initial setup and login flow.
  - **`functions.h`**: A central header file defining all function prototypes, `structs`, and macros, acting as the public API for the modules.
  - **`functions_admin.c` / `functions_limited.c`**: Encapsulates all logic exclusive to specific user roles, implementing the Role-Based Access Control.
  - **`functions_general.c`**: Contains all logic shared between user roles (login, searching, hash functions, etc.).
  - **`tutorials.c`**: Isolates all UI text and user guidance logic.

### 4. Custom Flat-File Database Persistence
All in-memory data structures are persisted to disk using a custom system built with standard file I/O.
- **Startup:** On launch, the `load_*_databases()` functions read data from `.txt` files and populate the hash tables in memory.
- **Runtime:** Every create, update, or delete operation is immediately and atomically written back to the corresponding `.txt` file, guaranteeing data integrity and persistence between sessions.
- **Robust I/O:** The system correctly uses different file modes (`"r"`, `"w"`, `"a"`) to safely read from and write to the database files.

## Key Features

- **Full CRUD Functionality:** Create, Read, Search, Edit, and Remove products, providers, and employees.
- **Role-Based Access Control:** A secure account system with "Admin" (full access) and "Limited" (read-only) user roles.
- **Advanced Search:** Filter data by multiple criteria (e.g., search employee by name, role, or salary).
- **Data Reporting:** Generate and display comprehensive reports on all data within the system.
- **Onboarding & Guidance:** A guided first-run setup creates an initial admin account, and a built-in manual provides detailed instructions.

## Getting Started

To compile and run the project, you will need a C compiler such as GCC or Clang. The project includes dedicated versions for both Linux and Windows.

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/soustern/simple-logistical-system.git
    cd simple-logistical-system
    ```

2.  **Navigate to the appropriate directory:**
    ```sh
    # For Linux
    cd programa_linux
    
    # For Windows
    cd programa_windows
    ```

3.  **Compile the source code:**
    The following command will compile all necessary files and create an executable named `sls`.
    ```sh
    gcc -o sls sls.c functions_admin.c functions_general.c functions_limited.c tutorials.c
    ```

4.  **Run the application:**
    ```sh
    # For Linux
    ./sls
    
    # For Windows
    .\sls.exe
    ```
> **Note:** On the first run, the system will automatically guide you through creating the initial **admin** account required to use the application.

## License

This project is licensed under the MIT License.
