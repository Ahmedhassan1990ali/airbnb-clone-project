# **Airbnb clone project**
![](https://drive.google.com/uc?export=view&id=101sJtlr2kZhDblKYOofUJlLQhgnkBc1k)


## **👥 Team Roles**

- **Backend Developer**: Responsible for implementing API endpoints, database schemas, and business logic.
- **Database Administrator**: Manages database design, indexing, and optimizations.
- **DevOps Engineer**: Handles deployment, monitoring, and scaling of the backend services.
- **QA Engineer**: Ensures the backend functionalities are thoroughly tested and meet quality standards.

---
---
## **⚙️ Technology Stack**
- **Django**: A high-level Python web framework used for building the RESTful API.
- **Django REST Framework**: Provides tools for creating and managing RESTful APIs.
- **PostgreSQL**: A powerful relational database used for data storage.
- **GraphQL**: Allows for flexible and efficient querying of data.
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments.
- **Redis**: Used for caching and session management.
- **Docker**: Containerization tool for consistent development and deployment environments.
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes.

---
---
## 🗄️ Database Design

This section outlines the core entities and their relationships within the application.

### 1. Users
Represents individuals using the platform, either as hosts or guests.

- `id`: Unique identifier
- `name`: Full name of the user
- `email`: Unique email address
- `password_hash`: Hashed user password
- `role`: Either "host" or "guest"

**Relationships**:
- A user can own multiple properties (if host).
- A user can make multiple bookings (if guest).
- A user can leave multiple reviews.

---

### 2. Properties
Represents listings available for booking.

- `id`: Unique identifier
- `user_id`: Foreign key referencing the host (Users)
- `title`: Title of the property
- `description`: Detailed info about the property
- `price_per_night`: Cost per night in currency

**Relationships**:
- Each property belongs to one host (user).
- A property can have many bookings.
- A property can have many reviews.

---

### 3. Bookings
Represents reservations made by guests.

- `id`: Unique identifier
- `user_id`: Foreign key referencing the guest
- `property_id`: Foreign key referencing the property
- `start_date`: Start of the booking
- `end_date`: End of the booking

**Relationships**:
- A booking is made by one user (guest).
- A booking is for one property.
- A booking may be linked to a payment.

---

### 4. Reviews
Feedback from guests after staying at a property.

- `id`: Unique identifier
- `user_id`: Foreign key referencing the reviewer
- `property_id`: Foreign key referencing the property
- `rating`: Numeric score (e.g., 1–5)
- `comment`: Optional review message

**Relationships**:
- A review is written by one user.
- A review is for one property.

---

### 5. Payments
Records of successful transactions.

- `id`: Unique identifier
- `booking_id`: Foreign key referencing the booking
- `amount`: Total payment amount
- `payment_method`: e.g., credit card, PayPal
- `status`: e.g., pending, completed, faileds

**Relationships**:
- A payment belongs to one booking.

---
---
## 🛠️ Feature Breakdown

### 1. API Documentation
- **OpenAPI Standard**: The backend APIs are documented using the OpenAPI standard for clarity and ease of integration.
- **Django REST Framework (DRF)**: Provides a comprehensive RESTful API for handling CRUD operations on users and properties.
- **GraphQL Support**: Offers a flexible and efficient query mechanism as an alternative to REST.

---

### 2. User Authentication
- **Endpoints**: `/users/`, `/users/{user_id}/`
- **Features**:
  - Register new users
  - Authenticate existing users
  - View and update user profiles

---

### 3. Property Management
- **Endpoints**: `/properties/`, `/properties/{property_id}/`
- **Features**:
  - Create new property listings
  - Update existing listings
  - Retrieve and display property details
  - Delete listings

---

### 4. Booking System
- **Endpoints**: `/bookings/`, `/bookings/{booking_id}/`
- **Features**:
  - Make bookings for properties
  - Update booking details (e.g. check-in/out dates)
  - Cancel or view existing bookings

---

### 5. Payment Processing
- **Endpoint**: `/payments/`
- **Features**:
  - Handle transactions related to bookings
  - Integrate payment methods such as credit cards or PayPal
  - Track payment status (e.g. pending, completed, failed)

---

### 6. Review System
- **Endpoints**: `/reviews/`, `/reviews/{review_id}/`
- **Features**:
  - Post reviews on properties after a stay
  - Edit or delete personal reviews
  - Rate properties using a numeric score

---

### 7. Performance & Optimization
- **Indexing**: Frequently queried fields are indexed for faster database access.
- **Caching**: Implemented caching strategies to reduce database load and improve response time.

---
---
## 🔐 API Security

Security is a top priority in this application to ensure user trust, data integrity, and safe financial transactions. The following measures are implemented to secure the API:

### 1. Authentication
- **Method**: Token-based authentication (e.g., JWT or DRF Token Authentication).
- **Purpose**: Verifies the identity of users before granting access to protected endpoints.
- **Why it matters**: Prevents unauthorized users from accessing or manipulating user accounts and sensitive operations like booking or payment.

### 2. Authorization
- **Role-Based Access Control (RBAC)**:
  - Hosts can manage properties they own.
  - Guests can book and review but not modify other users’ data.
  - Admins have elevated access for moderation and oversight.
- **Why it matters**: Ensures users can only perform actions they’re allowed to, minimizing risk of data leaks or privilege abuse.

### 3. Rate Limiting
- **Strategy**: Limit the number of API requests per user/IP over time.
- **Why it matters**: Protects against brute-force attacks, denial-of-service (DoS), and abuse of public APIs.

### 4. Data Encryption
- **At Rest**: Sensitive fields like passwords are hashed and stored securely.
- **In Transit**: HTTPS is enforced for all data transmission between client and server.
- **Why it matters**: Prevents data theft during storage or network interception.

### 5. Input Validation & Sanitization
- **Method**: All user inputs are validated using serializers and sanitized where needed.
- **Why it matters**: Protects against injection attacks (SQL, XSS) and ensures data consistency.

### 6. Secure Payments
- **Integration with third-party payment gateways** (e.g., Stripe, PayPal) using their secure APIs.
- **Why it matters**: Ensures that financial data is not stored or mishandled by the application, reducing liability and risk.

---

These security practices are essential for:
- 🔒 Protecting **user data** (emails, passwords, profile info)
- 💳 Securing **payment operations**
- 🏠 Safeguarding **property and booking details**
- 🛡️ Preventing **unauthorized access** or service abuse

---
---