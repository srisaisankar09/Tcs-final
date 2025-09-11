## Catalog Public APIs

Base path (through Gateway): `/api/catalog`

### Hotels & Rooms
- `GET /hotels?city=Mumbai` -> list of hotels with summary
- `GET /hotels/{id}` -> hotel detail with room types and basic room listing
- `GET /hotels/{id}/rooms?status=AVAILABLE` -> rooms filtered by status
- `GET /roomtypes` -> all room types

For availability by date range, use Booking API `/api/booking/availability`.

