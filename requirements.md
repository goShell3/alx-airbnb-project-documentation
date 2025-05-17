# 📘 Feature Requirements Specification

This document outlines the technical requirements for core backend features of the Property Booking Platform.

---

## 1. 🔐 User Authentication

### API Endpoints

| Method | Endpoint        | Description           |
|--------|------------------|-----------------------|
| POST   | `/api/register` | Register a new user   |
| POST   | `/api/login`    | Authenticate and issue JWT |
| GET    | `/api/profile`  | Get current user info |
| PUT    | `/api/profile`  | Update user profile   |

### Input/Output Specification

- **Registration Input**:
  - `first_name`, `last_name`, `email`, `password`, `role`, `phone_number` (optional)
- **Login Input**:
  - `email`, `password`
- **Output**: JWT Token, user data

### Validation Rules

- Password: Minimum 8 chars, includes letter and number
- Email: Must be unique, valid format
- Role: ENUM (`guest`, `host`, `admin`)

### Performance Criteria

- Token should be issued within 500ms.
- Hash passwords using bcrypt/argon2.

---

## 2. 🏠 Property Management

### API Endpoints

| Method | Endpoint                 | Description               |
|--------|---------------------------|---------------------------|
| POST   | `/api/properties`        | Create property           |
| GET    | `/api/properties`        | List/search properties    |
| GET    | `/api/properties/:id`    | Get property by ID        |
| PUT    | `/api/properties/:id`    | Update property           |
| DELETE | `/api/properties/:id`    | Delete property           |

### Input Fields

- `name`, `description`, `location`, `pricepernight`, `availability`, `amenities`

### Validation Rules

- Name: Required
- Price: Must be a positive decimal
- Host ID: Must match authenticated user

### Performance Criteria

- Search with pagination: 100ms response under normal load
- Full-text search on name and location (use PostgreSQL `tsvector` or MySQL `MATCH AGAINST`)

---

## 3. 📅 Booking System

### API Endpoints

| Method | Endpoint             | Description            |
|--------|-----------------------|------------------------|
| POST   | `/api/bookings`     | Create new booking     |
| GET    | `/api/bookings`     | List bookings (filterable) |
| PUT    | `/api/bookings/:id` | Cancel/update booking  |

### Input Fields

- `property_id`, `start_date`, `end_date`, `user_id`, `total_price`

### Output

- Booking status, property info, user info, confirmation code

### Validation Rules

- Dates must not overlap existing bookings for the same property.
- Start date must be today or in the future.
- Total price = (end_date - start_date) * pricepernight (calculated on server)

### Performance Criteria

- Booking conflict checks in < 200ms
- Use SQL `EXISTS` + index on (`property_id`, `start_date`, `end_date`)

---

## 💳 Payment Gateway (Add-on)

> Optionally included as a future enhancement.

### Integration

- Use Stripe SDK (or PayPal)
- Trigger payment only on confirmed bookings
- Webhooks for payment success/failure
