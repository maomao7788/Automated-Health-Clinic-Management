# Automated Health Clinic Management System

## Project Overview

The goal of this project is to provide a lightweight HTTP-based clinic management API using C++ and the Crow framework.  

## Project Participants

* Ruochen Liao
* Abdellah Sabhi

**Objectives:**

- Register and manage patients and doctors  
- Book and track appointments  
- Record medical visits, prescriptions, bills and insurance claims  
- Maintain an inventory of medical supplies  


## Functional Requirements

### Functional
| Feature                                    | Description                                                     
|--------------------------------------------|-----------------------------------------------------------------
| Patient CRUD                               | Create, read patient profiles                                   
| Doctor CRUD                                | Create, read doctor profiles                                    
| Appointment booking                        | Validate slot availability and schedule appointments            
| Medical record logging                     | Link visits to the most recent appointment                      
| Prescription management                    | Deduct inventory and record multi-item prescriptions            
| Billing & insurance                        | Auto-generate bills, calculate totals, submit and track claims  
| Inventory tracking                         | Update stock on prescriptions, alert on low levels (<100 units) 

**Design Constraints:**

- No external database; data lives in JSON files under the application folder  
- All HTTP endpoints use GET for simplicity (no REST verbs beyond GET)  
- Business hours limited to 09:00–17:00 in 10-minute increments  
All routes, data models, JSON I/O
## Repository Structure
- CMakeLists.txt
- src/
    - AHCM.cpp        # All routes, data models, JSON I/O
- include/
    - AHCM.h          # Header definitions
    - nlohmann/json.hpp
- third_party/
    - crow/           # Crow framework headers
    - asio/           # Asio headers

## Technology & Architecture

- **C++20** — modern language features  
- **Crow** — a minimalist C++ HTTP server framework  
- **Asio** — asynchronous I/O backend for networking  
- **nlohmann/json** — JSON serialization and parsing  
- **File-based persistence** — each entity stored in its own JSON file  
- **Mutex locking** — thread safety for shared in-memory vectors  

The server starts on port `8080` and exposes only GET routes for simplicity. Each route handles query parameters, performs validation, updates in-memory data, writes back to JSON, and returns a JSON response.

## Installation

1. **Clone the repo**  
   ```bash
   git clone https://github.com/your-username/Automated-Health-Clinic-Management.git
   cd AHCM
2. **Create folder**
   ```bash
   mkdir build
   cd build
3. **Install CMAKE**
   winget install --id Kitware.CMake -e(windows10/11)
   otherwise please download from https://cmake.org/download/
4. **Configure with CMake**
   ```bash
   cmake .. -DCMAKE_BUILD_TYPE=Release
5. **Build the project**
   ```bash
   cmake .. -DCMAKE_TOOLCHAIN_FILE="path/vcpkg/scripts/buildsystems/vcpkg.cmake"
   cmake --build .
6. **Run the server**
   ```bash
   cd Debug
   AHCM.exe

## User Guide

- All endpoints use HTTP GET and return JSON.
- command example:
- Home: http://localhost:8080/
- Register Patient: http://localhost:8080//register?name=John&address=NY&medicalHistory=None&insuranceCompany=ABC
- Register Doctor: http://localhost:8080//register_doctor?name=Dr.Smith&specialty=Cardiology&contactInfo=1234
- Book Appointment: http://localhost:8080//book_appointment?patientId=1&doctorId=1&date=2025-06-01&time=10:00
- Add Medical Record: http://localhost:8080//add_medical_record?patientId=1&doctorId=1&diagnosis=Flu&notes=Treated
- Add Prescription: http://localhost:8080//add_prescription?patientId=1&doctorId=1&datePrescribed=2025-06-01&instructions=AfterMeal&itemsUsed=Bandage,2;Syringe,1
- View Entities
- patients: http://localhost:8080//patients or /patients/1
- Doctors: http://localhost:8080//doctors
- view appointment: http://localhost:8080/appointments
- View appointments by patient id: http://localhost:8080/appointments?patientId=1
- Medical Records: http://localhost:8080//medical_record/1
- Bills: http://localhost:8080//bills
- Inventory: http://localhost:8080//inventory
- Update Inventory: http://localhost:8080//update_inventory_item?itemName=Bandage&quantity=500
