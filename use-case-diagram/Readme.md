# 🏡 Property Booking Platform – Backend Documentation

## 📚 Overview

This backend supports a property booking platform where users can register as guests or hosts, manage property listings, make bookings, process payments, and leave reviews. Admin users oversee the system. Below are the documented **use cases**, **core user stories**, and **detailed backend requirements** for key modules.

---

## 📌 Use Case Summary

### 👤 User Registration & Login
- Guests and Hosts can register and log in securely.
- JWT is used for authentication.
- OAuth (Google/Facebook) is supported optionally.

### 🏠 Property Management
- Hosts can create, update, or delete their property listings.
- Listings include availability, location, amenities, and pricing.

### 📅 Booking System
- Guests can book available properties.
- Prevents double bookings.
- Booking status is tracked (pending, confirmed, canceled).

### 💳 Payment Integration
- Guests pay upfront via Stripe or PayPal.
- Hosts are paid after the stay is completed.
- Multiple currencies supported.

---

## ✅ Key Features

| Feature              | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| User Authentication  | Secure login and signup with JWT + OAuth (optional)                         |
| Property Management  | Host-driven property CRUD with validation, amenities, and availability      |
| Booking System       | Prevents overlaps, tracks status, and triggers payments and notifications   |
| Payments             | Processes with Stripe/PayPal and links to confirmed bookings                |
| Admin Dashboard      | Manages users, properties, bookings, and reviews                            |

---

## 📂 Structure

- `requirements.md`: Detailed technical specifications
- `user-stories.md`: User stories and personas
- `flowchart.puml`: Flowchart in PlantUML
- `use-cases.puml`: Use case diagram in PlantUML

---

## 🛠️ Technologies

- Backend: Django / Node.js / Laravel (your choice)
- Database: PostgreSQL / MySQL
- Auth: JWT + OAuth
- Payments: Stripe / PayPal
- Notifications: SendGrid / Mailgun

---

## ✉️ Contact

For any suggestions or questions, contact the team at `herkodandy@gmail.com`.

