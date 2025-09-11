## API Gateway

### Responsibility
Single entry point for clients. Performs routing, authentication/authorization, CORS, and cross-cutting concerns (rate limiting, request logging, timeouts).

### Suggested Routes
- `/api/admin/**` → Catalog Service (admin controllers)
- `/api/catalog/**` → Catalog Service (public read-only)
- `/api/booking/**` → Booking Service
- `/api/auth/**` and `/api/users/**` → User & Auth Service

### Security
- Validates JWT on incoming requests (except auth endpoints).
- Propagates user claims to downstream services via Authorization header; may add `X-User-Id` and `X-User-Role` if needed.

### Resilience
- Per-route timeouts and circuit breakers.
- Rate limits on booking endpoints to protect against brute force.

### CORS
Allow Angular frontend origin(s), methods GET/POST/PUT/DELETE, and headers Authorization, Content-Type.

