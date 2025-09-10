## Architecture Overview

### Context
The system exposes external-facing functionality for admins and customers:
- Admins manage hotels, room types, rooms, and managers.
- Customers search hotels/rooms and make, modify, or cancel bookings.

### Microservices (bounded contexts)
- Discovery Service: Service registry for dynamic discovery.
- API Gateway: Single entry point; routing, CORS, auth, and rate-limiting.
- Catalog Service: Hotel catalogue (Hotels, RoomTypes, Rooms, Managers). Source of truth for hotel metadata and operational statuses (e.g., maintenance). Provides admin and public read APIs.
- Booking Service: Booking lifecycle and anti-overbooking enforcement. Availability checks based on bookings; emits booking events.
- User & Auth Service: Account lifecycle, roles (ADMIN, CUSTOMER), JWT issuance, profile management.

Each service owns its data (separate databases). Communication is synchronous REST via Gateway; intra-service calls use service discovery. For eventual consistency between bookings and derived availability/UI views, booking events can be published (optional future extension) to update read models or caches.

### Technology
- Spring Boot (Java) for all services.
- Spring Cloud Netflix Eureka for discovery.
- Spring Cloud Gateway for API Gateway.
- Persistence: H2 for dev; Postgres (recommended) per service in higher envs.
- Security: JWT (HS256/RS256) via Gateway + service-side validation.

### Ports (suggested defaults)
- Discovery: 8761
- API Gateway: 8080
- Catalog: 8081
- Booking: 8082
- User/Auth: 8083

### High-level Flow
- Admin creates catalogue entities in Catalog Service.
- Customers query public catalog endpoints to view hotels/rooms.
- Customer books a room via Booking Service, which validates no overlaps and records booking. Availability is calculated using bookings (and room maintenance status from Catalog).

### Data Ownership
- Catalog DB: `Hotel`, `RoomType`, `Room`, `Manager`.
- Booking DB: `Booking`, `BookingDate` (daily slots), `IdempotencyKey`.
- User DB: `User`, `Role`, `RefreshToken` (optional).

