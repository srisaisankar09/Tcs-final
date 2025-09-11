## Deployment Guide

### Services and Ports
- Discovery (Eureka): 8761
- API Gateway: 8080
- Catalog: 8081
- Booking: 8082
- User/Auth: 8083

### Environment Variables (examples)
- Common: `SPRING_PROFILES_ACTIVE=prod`, `LOG_LEVEL=INFO`
- Gateway: `JWT_PUBLIC_KEY`, CORS origins
- Catalog: `DB_URL`, `DB_USER`, `DB_PASSWORD`
- Booking: `DB_URL`, `DB_USER`, `DB_PASSWORD`
- User/Auth: `DB_URL`, `DB_USER`, `DB_PASSWORD`, `JWT_PRIVATE_KEY`

### Startup Order
1. Discovery
2. Catalog, Booking, User/Auth (register with discovery)
3. API Gateway (fetches registry)

### Database
- Dev: H2 (in-memory or file)
- Prod: Postgres per service. Apply migrations with Flyway or Liquibase.

### Observability
- Enable Actuator on all services: `/actuator/health`, `/actuator/metrics`.
- Centralized logging with correlation id propagated by Gateway.

### Scaling
- Stateless services scaled horizontally; each service behind its own load balancer.
- Booking Service requires strong transaction isolation on create/modify paths.

