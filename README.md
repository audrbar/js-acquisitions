# Acquisitions API

Node.js/Express API for managing users and authentication, backed by Postgres via Drizzle ORM and secured with Arcjet.

## Features

- **Auth**: Sign up, sign in, sign out with JWT stored in HTTP-only cookies.
- **Users**: CRUD endpoints with role-aware authorization.
- **Security**: Arcjet Shield + DetectBot + rate limiting (role-based limits).
- **Validation**: Zod request validation with structured errors.
- **Logging**: Winston logging + request logging via Morgan.
- **Database**: Drizzle ORM over Neon Postgres.
- **Testing**: Jest + Supertest.

## Tech Stack

- **Runtime**: Node.js (ESM)
- **Framework**: Express
- **ORM**: Drizzle ORM
- **Database**: Postgres (Neon)
- **Security**: Arcjet
- **Validation**: Zod
- **Logging**: Winston + Morgan

## Project Structure

- `src/app.js` – Express app wiring and routes
- `src/server.js` – HTTP server startup
- `src/config` – database, Arcjet, logger
- `src/controllers` – request handlers
- `src/services` – business logic + data access
- `src/middleware` – auth + security middleware
- `src/models` – Drizzle schema
- `src/routes` – route definitions
- `src/utils` – helpers (JWT, cookies, formatting)
- `src/validations` – Zod schemas

## Getting Started

### Prerequisites

- Node.js 18+
- Postgres database (Neon recommended)

### Install

```bash
npm install
```

### Environment

Create a `.env` file (or use `.env.example` as a base):

```env
PORT=3000
NODE_ENV=development
LOG_LEVEL=info
JWT_SECRET=your-secret
DATABASE_URL=postgres://user:pass@host:port/db?sslmode=require
ARCJET_KEY=your-arcjet-key
```

### Run

```bash
npm run dev
```

The server starts at http://localhost:3000

## Scripts

- `npm run dev` – start in watch mode
- `npm start` – start server
- `npm run lint` – lint
- `npm run lint:fix` – lint + fix
- `npm run format` – format with Prettier
- `npm run format:check` – check formatting
- `npm run db:generate` – generate Drizzle migrations
- `npm run db:migrate` – run migrations
- `npm run db:studio` – open Drizzle Studio

## API

### Health

- `GET /health` – service status
- `GET /api` – API greeting

### Auth

- `POST /api/auth/sign-up`
  - body: `{ name, email, password, role? }`
- `POST /api/auth/sign-in`
  - body: `{ email, password }`
- `POST /api/auth/sign-out`

### Users (JWT cookie required)

- `GET /api/users` – list users
- `GET /api/users/:id` – get user
- `PUT /api/users/:id` – update user (self or admin; only admin can change role)
- `DELETE /api/users/:id` – delete user (admin only; cannot delete self)

## Security Notes

- Arcjet blocks bot traffic and enforces rate limits.
- Rate limits are role-based: guest < user < admin.
- JWT is stored in a signed cookie named `token`.

## Testing

```bash
npm test
```

Coverage output is written to `coverage/`.

## Docker

See [DOCKER_SETUP.md](DOCKER_SETUP.md) for full dev/prod Docker workflows.

## License

MIT

## Acknowledgements

[DevOps by JavaScript Mastery](https://www.youtube.com/watch?v=H5FAxTBuNM8)
