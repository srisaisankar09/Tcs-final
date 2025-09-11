## Sequence: Admin Adding a Room

1. Admin opens hotel details page.
2. UI calls Gateway → Catalog `GET /api/catalog/hotels/{id}`.
3. Admin submits Add Room form.
4. UI calls Gateway → Catalog `POST /api/admin/hotels/{hotelId}/rooms`.
5. Catalog persists new Room and returns 201.
6. UI refreshes hotel room list.

