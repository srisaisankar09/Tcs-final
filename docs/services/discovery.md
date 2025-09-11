## Discovery Service (Eureka)

### Responsibility
Central service registry to enable dynamic discovery of microservices. Avoids hardcoded host/ports and supports client-side load balancing.

### Key Capabilities
- Service registration and heartbeat.
- Registry UI at `/` (port 8761 by default).
- Health checks via Spring Boot actuator.

### External Interfaces
- HTTP UI: `GET /` (dashboard)
- REST (internal to Spring clients): registration/renewal endpoints.

### Configuration (env vars)
- `EUREKA_CLIENT_REGISTER_WITH_EUREKA=true|false`
- `EUREKA_CLIENT_FETCH_REGISTRY=true|false`
- `EUREKA_SERVER_ENABLE_SELF_PRESERVATION=true|false`

### Availability & Scaling
Run at least 2 instances in production with peer awareness for HA.

