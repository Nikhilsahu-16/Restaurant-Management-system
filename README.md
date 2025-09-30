🍴 Restaurant Management System

A Full-Stack Restaurant Management Application built using:

Frontend: ReactJS

Backend: Spring Boot (Java)

Database: MySQL

Payments: Stripe API

Authentication: JWT + Spring Security

🚀 Features

✅ User Authentication & Authorization (JWT-based, Roles: Admin, Customer)
✅ Restaurant Management (Add, Update, Delete, Toggle Open/Close)
✅ Food Management (CRUD Operations)
✅ Cart Management (Add/Remove/Update Items, Clear Cart)
✅ Order Processing (Order Lifecycle: Pending → Delivered)
✅ Secure Payments via Stripe API
✅ Email Notifications (Order Confirmation)
✅ Admin Panel (Manage Users, Analytics)

📊 System Architecture
graph TB
    subgraph "Frontend (React)"
        A[React App] --> B[API Calls]
    end
    
    subgraph "Backend (Spring Boot)"
        B --> C[Security Layer]
        C --> D[Controller Layer]
        D --> E[Service Layer]
        E --> F[Repository Layer]
        F --> G[Database Layer]
    end
    
    subgraph "External Services"
        G --> H[MySQL Database]
        E --> I[Stripe Payment]
        E --> J[Email Service]
    end

🔑 Authentication Flow
sequenceDiagram
    participant Client
    participant Security
    participant JWTValidator
    participant Controller
    participant Service
    participant Database
    
    Client->>Security: Send Request with JWT
    Security->>JWTValidator: Validate Token
    alt Valid
        Security->>Controller: Forward Request
        Controller->>Service: Business Logic
        Service->>Database: Query Data
        Database-->>Service: Return Data
        Service-->>Controller: Response
        Controller-->>Client: Success Response
    else Invalid
        Security-->>Client: 401 Unauthorized
    end

🗄️ Database Schema (ER Diagram)
erDiagram
    USER ||--o{ ORDER : places
    USER ||--o{ CART : owns
    RESTAURANT ||--o{ FOOD : serves
    ORDER ||--o{ ORDER_ITEM : contains
    
    USER {
        Long id PK
        String fullName
        String email
        String password
        String role
    }
    
    RESTAURANT {
        Long id PK
        String name
        String cuisineType
        String address
        Boolean open
    }
    
    FOOD {
        Long id PK
        String name
        Double price
        String category
        Long restaurantId FK
    }
    
    ORDER {
        Long id PK
        String status
        Double totalAmount
        Long customerId FK
        Long restaurantId FK
        Date createdAt
    }

📡 API Endpoints
🔐 Auth

POST /auth/signup – Register User

POST /auth/signin – Login User

POST /auth/reset-password – Reset Password

👤 Customer

GET /restaurants – View All Restaurants

GET /restaurants/{id} – View Restaurant Menu

POST /cart/add – Add Item to Cart

GET /cart – View Cart

POST /orders – Place Order

GET /orders – View Order History

🏢 Admin

POST /admin/restaurants – Add Restaurant

PUT /admin/restaurants/{id} – Update Restaurant

DELETE /admin/restaurants/{id} – Delete Restaurant

POST /admin/food – Add Food Item

PUT /admin/food/{id} – Update Food Item

GET /admin/users – Manage Users

GET /admin/analytics – View Analytics

⚙️ Setup Instructions
1️⃣ Backend (Spring Boot)
cd backend
mvn clean install
mvn spring-boot:run

2️⃣ Frontend (React)
cd frontend
npm install
npm start

3️⃣ Database (MySQL)

Create database:

CREATE DATABASE restaurant_db;


Update application.properties with MySQL username & password.

🔐 Security Flow
flowchart TD
    A[HTTP Request] --> B[JWT Validator]
    B --> C{Token Valid?}
    C -->|No| D[401 Unauthorized]
    C -->|Yes| E[Role Check]
    E --> F{Authorized?}
    F -->|No| G[403 Forbidden]
    F -->|Yes| H[Forward to Controller]

✅ Conclusion

This Restaurant Management System provides a robust and scalable backend architecture with:

🔐 Secure Authentication

🍔 Restaurant & Food CRUD

🛒 Cart & Ordering System

💳 Stripe Payment Integration

🏢 Admin Management

It can be extended with:

Delivery Tracking 🚚

Discount Coupons 🎟️

Multi-Restaurant Marketplace 🏬
