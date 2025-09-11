## User & Auth Service

### Responsibility
Account lifecycle, authentication, authorization, and profile management. Issues JWTs for clients and the gateway.

### Entities
- User: `id`, `email`, `passwordHash`, `name`, `role` (ADMIN|CUSTOMER), `status` (ACTIVE|INACTIVE), timestamps.
- RefreshToken (optional): `id`, `userId`, `token`, `expiresAt`, `revoked`.

### APIs (via Gateway)
- `POST /api/auth/register` { email, password, name, role? }
- `POST /api/auth/login` { email, password } -> { accessToken, refreshToken? }
- `POST /api/auth/refresh` -> rotate tokens
- `POST /api/auth/logout`
- `GET /api/users/me` -> profile
- `PUT /api/users/me` -> update profile

### Security
- Password hashing with BCrypt.
- JWT with roles/claims; short-lived access tokens; optional refresh tokens.
- Admin endpoints in other services require `role=ADMIN`.

