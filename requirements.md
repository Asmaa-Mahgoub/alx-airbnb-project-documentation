# 🧩 Backend Requirement Specifications (API V1)

This document details the **functional** and **non-functional requirements** for three core backend features of the rental marketplace platform.

---

## 🔑 1. Feature: User Authentication and Profile Management

### 1.1 High-Level Goal
To provide **secure**, **reliable**, and **performant** registration, login, and profile update functionalities for both **Guest** and **Host** roles using **JWT-based authentication**.

---

### 1.2 API Endpoints

| Method | URL | Description | Required Role |
|--------|-----|--------------|----------------|
| POST | `/api/v1/auth/register` | Creates a new user (Guest or Host). | Public |
| POST | `/api/v1/auth/login` | Authenticates user via email/password. | Public |
| PUT | `/api/v1/users/profile` | Updates the authenticated user's profile information. | Guest/Host/Admin |
| POST | `/api/v1/users/photo` | Uploads a new profile photo (stored on S3). | Guest/Host/Admin |

---

### 1.3 Input/Output Specifications

#### A. POST `/api/v1/auth/register` (Request Body)

| Parameter | Type | Constraint | Description |
|------------|------|-------------|--------------|
| email | string | Required, Unique | Valid email format. |
| password | string | Required | Must meet complexity rules. |
| firstName | string | Required, Max 50 chars | User’s first name. |
| lastName | string | Required, Max 50 chars | User’s last name. |
| role | string | Required | Must be guest or host. |

#### B. Successful Response (Login/Register)
```json
{
  "status": "success",
  "data": {
    "token": "eyJhbGciOiJIUzI1Ni...",
    "user": {
      "id": "uuid-123",
      "email": "user@example.com",
      "role": "host"
    }
  }
}
