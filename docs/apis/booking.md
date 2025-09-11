## Booking APIs

Base path: `/api/booking`

### Create Booking
`POST /bookings`
Request:
```
{ "hotelId": 1, "roomId": 202, "guestName": "Alex", "checkIn": "2025-09-02", "checkOut": "2025-09-04" }
```
Headers: `Idempotency-Key: <uuid>`
Responses: 201 with booking; 409 on conflict; 422 on invalid range.

### Get Booking
`GET /bookings/{id}`

### My Bookings
`GET /bookings?userId=me`

### Cancel Booking
`POST /bookings/{id}:cancel`

### Modify Booking
`PUT /bookings/{id}` body with updated dates; 409 if conflicts

### Availability
`GET /availability?hotelId=1&roomTypeId=2&checkIn=2025-09-02&checkOut=2025-09-04`
Returns list of available rooms with numbers.

