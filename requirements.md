# Backend Requirement Specifications

This document outlines the **technical and functional requirements** for the Airbnb Clone Backend.

---

## 1. User Authentication
- **Endpoint:**
  - `POST /auth/register`
  - `POST /auth/login`
- **Inputs:**
  - Register → `{ "name": string, "email": string, "password": string }`
  - Login → `{ "email": string, "password": string }`
- **Outputs:**
  - Register → `{ "message": "User created", "userId": int }`
  - Login → `{ "token": "JWT", "userId": int }`
- **Validation Rules:**
  - Email must be unique
  - Password must be ≥ 8 characters
- **Performance:**
  - Handle up to 100 requests/second

---

## 2. Property Management
- **Endpoints:**
  - `POST /properties` → Create property
  - `GET /properties` → Retrieve all
  - `GET /properties/:id` → Retrieve one
  - `PUT /properties/:id` → Update property
  - `DELETE /properties/:id` → Remove property
- **Inputs:**
  - `{ "title": string, "description": string, "location": string, "price": number, "availability": boolean }`
- **Outputs:**
  - Property JSON object
- **Validation:**
  - Title, location, price required
  - Price must be a positive number

---

## 3. Booking System
- **Endpoints:**
  - `POST /bookings` → Create booking
  - `GET /bookings/:id` → Retrieve booking
  - `DELETE /bookings/:id` → Cancel booking
- **Inputs:**
  - `{ "userId": int, "propertyId": int, "checkIn": date, "checkOut": date }`
- **Outputs:**
  - `{ "bookingId": int, "status": "confirmed" }`
- **Validation:**
  - Property must be available
  - Dates must be valid & non-overlapping

---

## 4. Payment Processing
- **Endpoints:**
  - `POST /payments` → Process payment
- **Inputs:**
  - `{ "bookingId": int, "amount": number, "paymentMethod": string }`
- **Outputs:**
  - `{ "paymentId": int, "status": "success" }`
- **Validation:**
  - Booking must exist
  - Amount must match booking cost
- **Integration:**
  - Stripe/PayPal SDK
- **Security:**
  - Use HTTPS for all payment operations

---

## Notes
- All API responses must return appropriate HTTP status codes.
- JWT is required for protected routes (properties, bookings).
- System must log all errors and failed requests.
