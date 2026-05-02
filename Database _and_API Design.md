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
