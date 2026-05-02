# Week 5 — Database & API Design

## Overview
This document defines the database schema and API design for the Smart Bistro system. It shows how data is structured and how the frontend communicates with the backend.

---

## Database Schema

### Tables

#### Users
- id (Primary Key)
- name
- email (Unique)
- password

#### Menu
- id (Primary Key)
- name
- price

#### Orders
- id (Primary Key)
- user_id (Foreign Key → Users.id)
- total



### SQL Schema

sql
CREATE TABLE Users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  password TEXT
);

CREATE TABLE Menu (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  price DECIMAL(10,2)
);

CREATE TABLE Orders (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES Users(id),
  total DECIMAL(10,2)
);

API Specifications

 Simple Smart Bistro Backend (Single File)

const express = require("express");
const jwt = require("jsonwebtoken");

const app = express();
app.use(express.json());

const SECRET = "secret_key";

Mock Database 
let users = [
  { id: 1, name: "John", email: "john@email.com", password: "123456" }
];

let orders = [
  { id: 1, user_id: 1, total: 25 }
];

Auth Middleware 
function authenticate(req, res, next) {
  const token = req.headers["authorization"];

  if (!token) return res.status(401).json({ message: "No token" });

  try {
    const decoded = jwt.verify(token, SECRET);
    req.user = decoded;
    next();
  } catch {
    res.status(401).json({ message: "Invalid token" });
  }
}

 AUTHORISATION ROUTES 

// Register
app.post("/api/auth/register", (req, res) => {
  const { name, email, password } = req.body;

  const newUser = {
    id: users.length + 1,
    name,
    email,
    password
  };

  users.push(newUser);
  res.json({ message: "User registered", user: newUser });
});

// Login
app.post("/api/auth/login", (req, res) => {
  const { email, password } = req.body;

  const user = users.find(u => u.email === email && u.password === password);

  if (!user) return res.status(401).json({ message: "Invalid credentials" });

  const token = jwt.sign({ id: user.id, email: user.email }, SECRET);

  res.json({ token });
});

 ORDER ROUTES

// Create Order
app.post("/api/orders", authenticate, (req, res) => {
  const { total } = req.body;

  const newOrder = {
    id: orders.length + 1,
    user_id: req.user.id,
    total
  };

  orders.push(newOrder);
  res.json({ message: "Order created", order: newOrder });
});

// Get Order by ID
app.get("/api/orders/:id", authenticate, (req, res) => {
  const order = orders.find(o => o.id == req.params.id);

  if (!order) return res.status(404).json({ message: "Order not found" });

  res.json(order);
});

// SERVER 
app.listen(5000, () => {
  console.log("Server running on http://localhost:5000");
});
