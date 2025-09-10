## Sequence: Customer Booking a Room

1. Customer searches hotels/rooms via UI.
2. UI calls Gateway → Catalog `GET /api/catalog/hotels?city=...`.
3. UI calls Gateway → Booking `GET /api/booking/availability?...` to show available rooms.
4. Customer selects room and submits booking.
5. UI calls Gateway → Booking `POST /api/booking/bookings` with idempotency key.
6. Booking Service validates:
   - Reads room and status from Catalog (optional cached).
   - Checks no `BookingDate(roomId, day)` rows exist for [checkIn, checkOut).
   - Inserts Booking and BookingDates in one transaction.
7. Booking returns 201 with booking id; UI shows confirmation.

