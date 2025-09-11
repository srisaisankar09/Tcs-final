## Booking Service

### Responsibility
Manages the end-to-end booking lifecycle and prevents double booking for the same room and overlapping dates. Handles creation, modification, cancellation, and retrieval of bookings.

### Core Concepts
- Booking: reservation for a specific `roomId` over a date range `[checkIn, checkOut)`; guest details; status.
- Anti-overbooking: enforce non-overlapping reservations per room using one of:
  1) database uniqueness with daily slots (BookingDate per day), or
  2) serialized check-and-insert in a transaction with `SELECT ... FOR UPDATE` on a room/day index.
  Approach 1 is recommended for simplicity and robust constraints.

### Entities (recommended schema)
- Booking: `id`, `hotelId`, `roomId`, `userId` (nullable for guest checkout), `guestName`, `checkIn` (date), `checkOut` (date), `status` (CONFIRMED|CANCELLED), `createdAt`, `updatedAt`.
- BookingDate: `id`, `bookingId`, `roomId`, `date` (unique index on `(roomId, date)`), ensures no double booking.
- IdempotencyKey: `key`, `requestHash`, `userId`, `createdAt` for safe retries on create.

### APIs (via Gateway under `/api/booking/...`)
- `POST /bookings` Create booking
  - body: `{ hotelId, roomId, guestName, checkIn, checkOut }`
  - rules: check room status via Catalog; ensure no BookingDate exists for any day in range; create Booking + BookingDate rows atomically.
- `GET /bookings/{id}`
- `GET /bookings?userId=me` Current user's bookings
- `POST /bookings/{id}:cancel` Cancel booking (releases dates)
- `PUT /bookings/{id}` Modify (date change) with conflict checks
- `GET /availability?hotelId=...&roomTypeId=...&checkIn=...&checkOut=...`
  - computes available rooms by subtracting booked dates from rooms returned by Catalog and status not `MAINTENANCE`.

### Integration
- Reads room metadata from Catalog (room status, type, hotel).
- Optionally emits domain events `BookingCreated`, `BookingCancelled` for analytics or caches.

### Validation & Policies
- Prevent overlaps including edge conditions: exclusive `checkOut` day, inclusive `checkIn` day.
- Respect Catalog `MAINTENANCE` rooms: unavailable.
- Idempotent create using client-provided header `Idempotency-Key`.

