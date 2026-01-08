# Postman-Automation-Independency-Project

# API Automation Testing Suite - Postman & JavaScript 🚀

This repository contains a professional API testing suite designed for robust and independent execution. The project focuses on the **Conduit (RealWorld) API**, implementing advanced automation techniques that go far beyond simple request-response checks.

## 🌟 Key Highlight: "Independency & Smart Auth"

The core strength of this collection is the **Automated Session Manager** written in JavaScript (Pre-request Scripts). 

### What makes it special?
* **Self-Healing Authorization**: The script automatically detects if a Bearer Token is missing or expired.
* **Dynamic User Provisioning**: If a test user doesn't exist, the suite automatically performs a `Sign Up` or `Login` on the fly before the actual test starts.
* **Independent Test Execution**: Each request is a "standalone" unit. You don't need to run the whole collection in order – you can pick any single request, and the Pre-request script ensures you are authorized and have the necessary test data (e.g., `authToken`, `takenEmail`).
* **Multi-User Scenarios**: Built-in helper to generate "User B" (Attacker/Second User) dynamically to test authorization boundaries and security.

## 🛠 Technical Stack

* **Tool**: Postman
* **Engine**: Newman (CLI Runner)
* **Scripting**: JavaScript (Postman Sandbox)
* **Data Generation**: Dynamic timestamps and randomized strings for unique test entities.

## 📋 Automation Coverage

Each request in this collection includes **unique automated test scripts** verifying:
* **Functional correctness**: Validation of JSON response bodies and data integrity.
* **Negative Testing**: Handling of 401 Unauthorized, 403 Forbidden, and 422 Unprocessable Entity (e.g., registering with a taken email).
* **Security**: Verification of permissions (e.g., User B cannot modify User A's resources).
* **Performance**: Response time assertions (< 500ms).
* **Schema Validation**: Ensuring the API adheres to the expected data structure.

## 🚀 Script Logic Breakdown (JavaScript)

The `Collection Pre-request Script` handles the heavy lifting:
1. **Token Check**: Scans `collectionVariables` for an active `authToken`.
2. **Conditional Auth**: 
   - If no token & no email -> Performs **Signup**.
   - If no token & email exists -> Performs **Login**.
3. **Data Setup**: Generates `takenUsername` and `takenEmail` specifically for negative test cases.
4. **Second User Logic**: Automatically provisions an `authToken_UserB` to enable cross-user security testing.

## ⚙️ How to Run

1. **Install Newman**:
   ```bash
   npm install -g newman


   Run the Collection:

2. **Run the Collection**:
    ```bash
    newman run collection.json -e environment.json
