# System Architecture Design – Food Waste Reduction Marketplace

## 1. Introduction
This document presents the system architecture for the Food Waste Reduction Marketplace. The architecture is designed based on the requirements defined in the Software Requirement Specification (SRS), aiming to connect food sellers (restaurants, stores) with buyers to reduce food waste.

---

## 2. Architecture Style

The system follows a **Modular Monolith Architecture**.

### Justification:
- Simpler to develop and deploy compared to microservices  
- Easier debugging and testing  
- Suitable for small-to-medium scale applications  
- Can be scaled later if needed  

---

## 3. High-Level Architecture

The system consists of the following layers:

### Client Layer
- Web application used by buyers and sellers  

### Application Layer (Backend)
- Handles business logic and API requests  

### Data Layer
- Stores all system data (users, food listings, orders)

### External Services
- Payment Gateway (for transactions)  
- Notification System (email/SMS alerts)

---

## 4. Core Components

### 4.1 User Service
- Handles user registration and login  
- Manages user profiles  
- Implements authentication (JWT-based)

### 4.2 Food Listing Service
- Allows sellers to upload surplus food  
- Manages food details (price, quantity, expiry time)  

### 4.3 Order Service
- Handles purchase/reservation of food  
- Tracks order status  

### 4.4 Notification Service
- Sends alerts for:
  - Order confirmations  
  - Expiry reminders  
  - Promotions  

---

## 5. System Architecture Diagram
Client (Web Application)
|
v
API Gateway
|
v
| User Service |
| Food Listing Service |
| Order Service |
| Notification Service |
    |
    v
 Database

---

## 6. Data Flow

### 6.1 User Registration
1. User enters details on frontend  
2. Request sent to User Service  
3. Data stored in database  
4. Confirmation returned  

### 6.2 Food Listing
1. Seller uploads food details  
2. Food Listing Service processes request  
3. Data stored in database  

### 6.3 Order Placement
1. Buyer selects food item  
2. Request sent to Order Service  
3. Order stored in database  
4. Notification sent to user  

---

## 7. Communication Design

- **Frontend to Backend:** REST API over HTTP  
- **Backend to Database:** Direct queries  
- **Internal Communication:** Function/module calls (modular structure)

---

## 8. Non-Functional Requirements Mapping

### Scalability
- Modular services allow future scaling  

### Security
- JWT-based authentication  
- Secure API communication (HTTPS)

### Performance
- Optimized database queries  
- Efficient data handling  

---

## 9. Summary

The proposed architecture ensures a scalable, maintainable, and efficient system for reducing food waste by enabling seamless interaction between buyers and sellers.
