## Catalog Service

### Responsibility
Owns hotel metadata: `Hotel`, `RoomType`, `Room`, and `Manager`. Provides admin CRUD and public read APIs. Room operational status (e.g., `MAINTENANCE`) is managed here; booking availability is managed by the Booking Service.

### Entities
- Hotel: `id`, `name`, `city`, `address`, `status` (ACTIVE/INACTIVE)
- RoomType: `id`, `name`, `capacity`, `price`
- Room: `id`, `hotelId`, `roomTypeId`, `number`, `status` (AVAILABLE|BOOKED|MAINTENANCE) [Note: `BOOKED` may be derived by booking queries; keep primarily for coarse status]
- Manager: `id`, `hotelId`, `name`, `email`, `phone`

### Admin Endpoints (via Gateway under `/api/admin/...`)
- `POST /hotels`
- `PUT /hotels/{id}`
- `DELETE /hotels/{id}` (guard if active bookings exist)
- `POST /roomtypes`
- `PUT /roomtypes/{id}` | `DELETE /roomtypes/{id}`
- `POST /hotels/{hotelId}/rooms`
- `PUT /hotels/{hotelId}/rooms/{roomId}` | `DELETE ...`
- `POST /managers`
- `PUT /managers/{id}` | `DELETE /managers/{id}`

### Public Read Endpoints (via Gateway under `/api/catalog/...`)
- `GET /hotels?city=...`
- `GET /hotels/{id}` (with rooms + room types)
- `GET /hotels/{id}/rooms?status=AVAILABLE|MAINTENANCE`
- `GET /roomtypes`

### Persistence
- JPA + H2 for dev; Postgres recommended in prod.

### Integration
- Reads booking availability via Booking Service when needed by UI (client can also call booking availability directly).

