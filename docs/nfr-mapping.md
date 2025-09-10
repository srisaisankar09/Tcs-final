## Non-Functional Requirements Mapping

- NFR-01 Double booking prevention: Booking Service uses `BookingDate(roomId, date)` unique index and transactional writes.
- NFR-02 Usability: Gateway provides CORS; frontend-friendly, consistent REST; pagination & filtering on list endpoints.
- NFR-03 Clear error messages: Standard error schema `{ code, message, details }`; 409 for conflicts, 422 for validation.
- NFR-04 Modify/cancel billing policy: Booking Service enforces policy layer before state transition.
- NFR-05 Form validation: Backend bean validation annotations; descriptive messages; field-level errors.
- NFR-06 Encryption: TLS in transit; at-rest encryption via DB/cloud KMS; bcrypt for passwords; JWT with secure keys.
- NFR-07 Extensibility: Event hooks (`BookingCreated`, `BookingCancelled`) for downstream integrations; service-per-db for independent scaling.

