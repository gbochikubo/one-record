# One Record

Unified Registration System for Individuals and Legal Entities. Manages the full lifecycle of records — creation, retrieval, update, and deactivation — following Hexagonal Architecture principles.

## Tech Stack

| Layer          | Technology                   |
|----------------|------------------------------|
| Language       | Java 25                      |
| Framework      | Spring Boot 4.0.3            |
| Database       | PostgreSQL 15                |
| Migrations     | Flyway                       |
| API Docs       | SpringDoc OpenAPI 3.0.1      |
| Monitoring     | Spring Boot Actuator         |
| Containers     | Docker / Docker Compose      |

## Prerequisites

- Java 25
- Docker & Docker Compose
- Maven (wrapper included via `./mvnw`)

## Getting Started

### 1. Start the infrastructure

```bash
docker compose up -d
```

This starts:
- **PostgreSQL 15** on port `5432` (user: `onerecord` / password: `onerecord` / db: `onerecord`)
- **PgAdmin** on port `5050` (email: `admin@onerecord.com` / password: `admin`)

### 2. Run the application

```bash
./mvnw spring-boot:run
```

The app starts on port `8080` with the `local` profile active by default.

### 3. Verify

| Resource        | URL                                       |
|-----------------|-------------------------------------------|
| Swagger UI      | http://localhost:8080/swagger-ui.html      |
| OpenAPI Spec    | http://localhost:8080/one-record-api.json  |
| Health Check    | http://localhost:8080/actuator/health      |

## Project Structure (Hexagonal Architecture)

```
src/main/java/com/onerecord/
├── domain/                  # Core — pure Java, zero framework dependencies
│   ├── model/vo/            # Entities and Value Objects
│   ├── port/in/             # Input ports (use case interfaces)
│   ├── port/out/            # Output ports (repository interfaces)
│   ├── service/             # Use case implementations
│   └── exception/           # Domain exceptions
├── application/             # Orchestration — DTOs and mappers
│   ├── dto/
│   └── mapper/
├── adapter/                 # Adapters — port implementations
│   ├── in/web/              # Driving (REST controllers)
│   └── out/persistence/     # Driven (JPA repositories)
├── config/                  # Spring configuration and wiring
└── OneRecordApplication.java
```

## Stopping the Infrastructure

```bash
docker compose down
```

To also remove the database volume:

```bash
docker compose down -v
```
