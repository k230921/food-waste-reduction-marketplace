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
