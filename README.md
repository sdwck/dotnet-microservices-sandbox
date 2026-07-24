# 🧪 .NET Microservices Sandbox

> Educational proof-of-concept exploring microservice patterns with ASP.NET Core Minimal APIs, React, WebSockets, and Docker.

## Architecture

```
┌─────────────┐    HTTP     ┌─────────────┐
│  Order.API  │────────────▶│  Stock.API  │
│  :8080      │  stock check│  :8081      │
└──────┬──────┘             └─────────────┘
       │
       │  ┌──────────────┐
       └──│ Order.Client │  React + TypeScript
          └──────────────┘

┌─────────────┐  WebSocket  ┌─────────────┐
│ Todo.Server │◀═══════════▶│ Todo.Client │
│  PostgreSQL │  real-time  │  React + TS │
│  SMTP/IMAP  │  broadcast  │             │
└─────────────┘             └─────────────┘
```

## What's Inside

| Service | Stack | Notes |
|---------|-------|-------|
| **Order.API** | ASP.NET Core Minimal API, EF Core | CRUD + inter-service HTTP calls to Stock.API for inventory validation |
| **Stock.API** | ASP.NET Core Minimal API, EF Core | Product inventory management with Scalar API docs |
| **Todo.Server** | ASP.NET Core, PostgreSQL, WebSockets | Real-time broadcast on create/update/delete, email notifications via SMTP/IMAP/POP3 |
| **Order.Client** | React, TypeScript, Vite | Orders dashboard with status management |
| **Todo.Client** | React, TypeScript, Vite | Real-time todo list with WebSocket sync |

## Key Patterns Demonstrated

- **Inter-service communication** — Order.API validates stock availability via HTTP before creating orders
- **WebSocket broadcasting** — Todo changes are pushed to all connected clients in real-time
- **Multi-container deployment** — Docker Compose orchestrates all services + Nginx reverse proxy
- **CI/CD** — GitHub Actions pipeline with Docker build and deployment

## Running

```bash
docker compose up --build
```

| Service | URL |
|---------|-----|
| Order.Client | `http://localhost:3000` |
| Order.API (Scalar docs) | `http://localhost:8080/scalar` |
| Stock.API (Scalar docs) | `http://localhost:8081/scalar` |
| Todo.Client | `http://localhost:3001` |

## License

MIT
