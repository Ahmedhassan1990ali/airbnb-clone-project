# **Airbnb clone project**
![](https://drive.google.com/uc?export=view&id=101sJtlr2kZhDblKYOofUJlLQhgnkBc1k)


## **👥 Team Roles**

- **Backend Developer**: Responsible for implementing API endpoints, database schemas, and business logic.
- **Database Administrator**: Manages database design, indexing, and optimizations.
- **DevOps Engineer**: Handles deployment, monitoring, and scaling of the backend services.
- **QA Engineer**: Ensures the backend functionalities are thoroughly tested and meet quality standards.

## **⚙️ Technology Stack**
- **Django**: A high-level Python web framework used for building the RESTful API.
- **Django REST Framework**: Provides tools for creating and managing RESTful APIs.
- **PostgreSQL**: A powerful relational database used for data storage.
- **GraphQL**: Allows for flexible and efficient querying of data.
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments.
- **Redis**: Used for caching and session management.
- **Docker**: Containerization tool for consistent development and deployment environments.
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes.

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
- `status`: e.g., pending, completed, failed

**Relationships**:
- A payment belongs to one booking.
