## Catalog Admin APIs

Base path (through Gateway): `/api/admin`

### Hotels
- `POST /hotels` { name, city, address, status }
- `PUT /hotels/{id}` { name?, city?, address?, status? }
- `DELETE /hotels/{id}` 409 if active bookings exist

### Room Types
- `POST /roomtypes` { name, capacity, price }
- `PUT /roomtypes/{id}`
- `DELETE /roomtypes/{id}`

### Rooms
- `POST /hotels/{hotelId}/rooms` { number, roomTypeId, status }
- `PUT /hotels/{hotelId}/rooms/{roomId}` { number?, roomTypeId?, status? }
- `DELETE /hotels/{hotelId}/rooms/{roomId}` 409 if active bookings exist

### Managers
- `POST /managers` { hotelId, name, email, phone }
- `PUT /managers/{id}`
- `DELETE /managers/{id}`

All endpoints require `ADMIN` role.

