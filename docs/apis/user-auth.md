## User & Auth APIs

Base paths: `/api/auth`, `/api/users`

### Register
`POST /api/auth/register` { email, password, name }

### Login
`POST /api/auth/login` -> { accessToken, refreshToken? }

### Refresh
`POST /api/auth/refresh`

### Logout
`POST /api/auth/logout`

### Get Profile
`GET /api/users/me`

### Update Profile
`PUT /api/users/me` { name?, password? }

