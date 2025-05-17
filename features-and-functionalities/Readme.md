# 🧠 Backend Features & Functionalities

This document outlines the **comprehensive set of backend features and functionalities** for a property rental system platform that connects guests and hosts. It also includes admin controls, payment integration, and notification handling.

---

## 1. 👥 User Management

### 1.1 User Registration
- Users can register as either:
  - `guest` – Can search, book, and review properties.
  - `host` – Can list, manage, and respond to bookings.
- Input:
  - First name, last name, email, password, role
- Security:
  - Passwords are hashed (e.g., bcrypt)
  - Uses JWT for authentication and session management

### 1.2 User Login & Authentication
- Login via:
  - Email and password (JWT)
  - Optional OAuth (Google, Facebook)
- Response:
  - JWT token, user profile

### 1.3 Profile Management
- Users can update:
  - First name, last name
  - Profile picture (file storage/cloud)
  - Contact information
  - Preferences (language, currency, etc.)

---

## 2. 🏠 Property Listings Management

### 2.1 Add Listings (Host Only)
- Fields:
  - Title, description, location, price per night, max guests, amenities, images
- Hosts can upload images (stored in filesystem/cloud)

### 2.2 Edit/Delete Listings
- Hosts can update or delete listings they own.
- Listings must not be deletable if they have active bookings.

---

## 3. 🔍 Search and Filtering

- Users can search properties by:
  - Location (city or country)
  - Price range
  - Number of guests
  - Amenities (Wi-Fi, pool, pet-friendly, etc.)
- Implements pagination for performance and UX
- Optional: geo-based filtering (using coordinates or map APIs)

---

## 4. 📆 Booking System

### 4.1 Create Booking (Guest Only)
- Guests select a property and book for a date range.
- The system:
  - Validates no overlapping bookings
  - Calculates total price
  - Sets booking status as `pending`

### 4.2 Booking Status Management
- Status can be:
  - `pending` (awaiting payment/approval)
  - `confirmed` (booked and paid)
  - `cancelled` (by host/guest)
  - `completed` (after checkout date)

### 4.3 Booking Cancellation
- Both guest and host can cancel bookings
- Enforce cancellation policies (e.g., refund rules)
- Trigger notifications and possible refunds

---

## 5. 💳 Payment Integration

### 5.1 Guest Payments
- Integrate with Stripe or PayPal
- Supports:
  - Secure payment by credit/debit card
  - Different currencies
- Stores payment method, amount, date

### 5.2 Host Payouts (Simulation)
- Automatically mark host payout as successful after booking is completed
- Optional: payout delay buffer (e.g., 24 hours after checkout)

---

## 6. 🌟 Reviews and Ratings

- Guests can leave a review (1-5 stars + comment)
- Host can view and optionally respond to reviews
- Constraints:
  - Reviews only possible after a confirmed, completed booking
  - One review per booking

---

## 7. 🔔 Notifications System

- Sends notifications via:
  - Email (e.g., SendGrid, Mailgun)
  - In-app (toasts, dashboard messages)
- Triggered for:
  - Booking confirmations and cancellations
  - Payment receipt or failure
  - Review submission
  - Profile updates

---

## 8. 🛠 Admin Dashboard (Role: admin)

Admins can:
- View and manage all users
- Manage and moderate listings
- View all bookings, payments, reviews
- Deactivate accounts
- See system stats (optional)

---

## 🔐 Authentication & Authorization

- Use **JWT** for session-based authentication
- Middleware for **Role-Based Access Control (RBAC)**
  - Guest routes (search, book, review)
  - Host routes (add/edit listings, respond to messages)
  - Admin routes (monitor, block, remove)

---

## 🗃️ Database Design

- RDBMS: PostgreSQL / MySQL
- Normalized schema (3NF)
- Main tables:
  - `users`
  - `properties`
  - `bookings`
  - `payments`
  - `reviews`
  - `messages`
- Foreign key constraints to ensure referential integrity
- Indexed columns: `email`, `property_id`, `booking_id`

---

## 📁 File Storage

- Store images locally or via services like AWS S3 or Cloudinary
- Files:
  - User profile pictures
  - Property listing images

---

## 🧩 API Architecture

- **RESTful** APIs with:
  - `GET`: fetch listings, bookings, reviews
  - `POST`: create users, bookings, payments
  - `PUT/PATCH`: update listings, user info
  - `DELETE`: remove listings, cancel bookings
- Optional: GraphQL support for nested data fetching

---

## 🧪 Testing and Quality

- Unit tests for models and logic (e.g., booking overlaps, price calculation)
- Integration tests for REST API endpoints using `pytest` or `Postman`
- Edge cases tested:
  - Invalid booking dates
  - Double booking prevention
  - Overdue payments
  - Invalid file uploads

---

## 🚀 Non-Functional Features

| Feature | Description |
|--------|-------------|
| ⚙️ Scalability | Modular services, ready for microservices or containerization |
| 🔐 Security | JWT, password hashing, input sanitization, HTTPS |
| 🚀 Performance | Caching (Redis), database indexing, async email sending |
| 💾 Logging | Request logs, error logs, audit trails |
| 🌐 Internationalization | Multi-language and currency support (optional) |

---

## ✅ Summary

This backend system supports a scalable, secure, and full-featured property rental platform. It ensures modularity, clean data design, authentication, authorization, and smooth data flow between users, properties, bookings, and payments.

---

## 🧠 Author

**Dandy Herko**  
3rd Year Student — Addis Ababa University  
Backend & Security Enthusiast | Django | REST APIs | SQL | ASP.NET  
