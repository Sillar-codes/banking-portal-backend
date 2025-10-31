# Banking Portal API

Lightweight Spring Boot backend for a demo banking portal. Provides account management, authentication (OTP + PIN), transactions, and admin endpoints. Intended as a sample/starting point for building banking-style APIs.

## Table of contents

- [Features](#features)
- [Tech stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Quick start](#quick-start)
- [Configuration](#configuration)
- [API documentation](#api-documentation)
- [Testing](#testing)
- [Postman collection](#postman-collection)
- [Contributing](#contributing)
- [License](#license)

## Features

- User registration, authentication, and password reset
- Account management and balance queries
- Fund transfers and transaction history
- OTP handling with retry limits and PIN management
- JWT-based authentication
- OpenAPI/Swagger UI for interactive API exploration

## Tech stack

- Java 17
- Spring Boot 3.3.x
- Spring Data JPA (MySQL)
- Spring Security + JWT
- Spring Mail (for email flows)
- SpringDoc OpenAPI (Swagger UI)
- Maven build

## Prerequisites

- Java 17 (JDK 17)
- Maven (or use the included Maven wrapper)
- MySQL (or another JDBC-compatible database)

## Quick start

1. Clone the repository

	```bash
	git clone https://github.com/Sillar-codes/banking-portal-backend.git
	cd banking-portal-backend
	```

2. Copy the sample config and update values

	```bash
	cp src/main/resources/application.properties.sample src/main/resources/application.properties
	# then edit application.properties to set DB credentials, mail settings, jwt.secret, etc.
	```

3. Build and run (using Maven wrapper)

	```bash
	# build
	./mvnw clean package -DskipTests

	# run
	./mvnw spring-boot:run
	```

	Or using an installed Maven:

	```bash
	mvn clean package -DskipTests
	mvn spring-boot:run
	```

The application default port in the sample is 8180; change `server.port` in `application.properties` if needed.

## Configuration

Primary sample config is at `src/main/resources/application.properties.sample`. Important keys to review:

- `spring.datasource.url` — JDBC URL for your database (sample: `jdbc:mysql://localhost:3306/bankingapp`)
- `spring.datasource.username` / `spring.datasource.password`
- `spring.jpa.hibernate.ddl-auto` — sample uses `update` for development
- JWT settings:
  - `jwt.secret` — set a secure secret for signing tokens
  - `jwt.expiration` — milliseconds until token expiry
  - `jwt.header` / `jwt.prefix`
- Mail settings (`spring.mail.*`) — required for email flows (password reset, OTP by email)
- Geolocation API (`geo.api.url` / `geo.api.key`) — used by geolocation features

Keep secrets (JWT secret, mail password) out of source control. Use environment variables or external config in production.

## API documentation

SpringDoc OpenAPI is included. After the app is running, visit:

- Swagger UI: http://localhost:8180/swagger-ui.html or http://localhost:8180/swagger-ui/index.html
- OpenAPI JSON: http://localhost:8180/v3/api-docs

Check the controllers under `src/main/java/com/webapp/bankingportal/controller` for available endpoints and request/response DTOs.

## Testing

Run unit/integration tests with Maven:

```bash
./mvnw test
```

There are test classes under `src/test/java/com/webapp/bankingportal` covering controllers and services.

## Postman collection

There's a Postman collection in the repository root: `Banking Portal.postman_collection.json`. Import it into Postman to exercise the endpoints.

## Contributing

See `CONTRIBUTING.md` for contribution guidelines. Keep changes small, write tests for new behavior and ensure existing tests pass.

## Notes & Development tips

- The project uses Lombok — enable annotation processing in your IDE.
- MapStruct is used for mapping DTOs — ensure annotation processing is enabled so generated mappers compile.
- The sample `application.properties.sample` sets `spring.jpa.hibernate.ddl-auto=update` which is OK for development but not recommended for production.

## License

This project is licensed under the terms in the repository root. See the `LICENSE` file.

---

If you'd like, I can also:

- Add a short developer checklist (How to add a new API, testing checklist)
- Create a Docker compose snippet showing MySQL + the app
- Run a quick Maven build in this environment to verify compilation

If you want any of those, tell me which and I'll proceed.

