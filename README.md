# PulseCheck

PulseCheck is a self-hosted uptime-monitoring application that periodically checks websites and HTTP APIs, records availability and response times, and presents service health in a dashboard and shareable public status page.

> **Why I’m building it:** I’m using PulseCheck to learn Docker, DevOps fundamentals, CI/CD, deployment, and the infrastructure practices involved in running an application reliably. The app itself provides a practical reason to learn and apply those skills.

## Planned features

- Add and manage HTTP/HTTPS endpoints to monitor
- Run periodic checks and record status codes, availability, and response times
- View current status and recent check history in a dashboard
- Publish a read-only status page for monitored services
- Run the application and its supporting services with Docker Compose
- Test changes automatically with GitHub Actions
- Deploy to a Linux server with HTTPS and persistent storage

## Planned technology

| Area | Choice | Purpose |
|---|---|---|
| Frontend | React, TypeScript, Vite | Monitoring dashboard and status page |
| API | Python, FastAPI | Endpoint management and monitoring data API |
| Database | PostgreSQL | Persist monitored endpoints and check history |
| Checker | Python worker | Run scheduled HTTP checks separately from API requests |
| Local environment | Docker, Docker Compose | Build and run services consistently |
| CI | GitHub Actions | Run tests and checks on changes |
| Public deployment | Linux VM and Caddy | Host the app and provide HTTPS/reverse proxy |

This stack is a starting point, not a requirement to introduce every component immediately. The goal is to understand each piece before adding more infrastructure.

## Roadmap

The roadmap below is intentionally high-level. Track concrete tasks and bugs as [GitHub Issues](https://github.com/ade-royal/pulsecheck/issues)

- [ ] **1. Define the MVP**: data model, check behavior, and basic architecture
- [ ] **2. Build the API and database**: manage endpoints and persist check results
- [ ] **3. Build the checker**: perform periodic checks and handle timeouts and failures
- [ ] **4. Build the dashboard**: show current status, latency, and recent history
- [ ] **5. Containerize the app**: Dockerfiles, Compose configuration, environment variables, and persistent database storage
- [ ] **6. Add automated checks**: tests and a GitHub Actions CI workflow
- [ ] **7. Deploy publicly**: Linux server, domain, HTTPS, and a repeatable deployment process
- [ ] **8. Harden and document**: security review, backups/recovery notes, and setup documentation

## Security and scope

- Only HTTP and HTTPS endpoints will be supported.
- Because the checker makes outbound requests to user-configured URLs, URL validation and protections against requests to private/internal network addresses are required before exposing endpoint management publicly.
- The public status page should be read-only. Endpoint management must not be left openly writable on a public deployment.
- Alerts, complex user roles, Kubernetes, and other advanced infrastructure are out of the initial MVP unless they solve a demonstrated need.

## Running locally

Local setup instructions will be added when the first runnable version is implemented. The intended development environment is Docker Compose, with configuration supplied through environment variables.

1. Install Docker Desktop (or Docker Engine with the Compose plugin).
2. Clone the repository.
3. Copy `.env.example` to `.env` and fill in any required values.
4. Start the services with `docker compose up --build`.

> The commands above describe the intended workflow. The initial scaffold does not yet contain a runnable application or complete Compose configuration.

## Project principles

- Build the smallest working version before adding infrastructure.
- Prefer readable, maintainable code over clever abstractions.
- Keep secrets out of Git; commit `.env.example`, never real `.env` files.
- Make tests and deployment repeatable.
- Document meaningful decisions and what was learned.

## License

This project is intended to use the MIT License. See [`LICENSE`](LICENSE).
