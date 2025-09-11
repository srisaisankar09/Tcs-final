# Hotel Management Microservices

This repository contains a Spring Boot multi-module project implementing the documented microservices:

- Discovery Service (Eureka) `discovery-service`
- API Gateway (Spring Cloud Gateway) `api-gateway`
- Catalog Service `catalog-service`
- Booking Service `booking-service`
- User & Auth Service `user-auth-service`

Quick start (dev):

1. Start Discovery Service: `mvn -pl discovery-service spring-boot:run`
2. Start API Gateway: `mvn -pl api-gateway spring-boot:run`
3. Start services: `mvn -pl catalog-service,booking-service,user-auth-service spring-boot:run`

Build all:

```
mvn -q -DskipTests package
```