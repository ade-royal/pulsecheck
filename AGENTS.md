# Agent Instructions

## Project purpose

PulseCheck is a self-hosted uptime monitor. It periodically checks configured HTTP/HTTPS endpoints, stores availability and response-time data, and presents that data through a dashboard and a read-only public status page.

The project is also a learning exercise focused on Docker, DevOps fundamentals, CI/CD, deployment, and operating a small service reliably. Prefer changes that teach and demonstrate these concepts without adding unnecessary complexity.

## Current scope

- Frontend: React + TypeScript + Vite
- API: Python + FastAPI
- Persistence: PostgreSQL
- Scheduled checking: a separate Python worker
- Local orchestration: Docker Compose
- CI: GitHub Actions
- Intended deployment: Linux VM with Caddy for HTTPS/reverse proxy

Treat these as the planned stack. Check the current repository state before assuming a component has been implemented.

## Working rules

1. **Inspect before editing.** Read relevant files and existing tests before proposing or making changes.
2. **Work incrementally.** Implement the smallest coherent step. Do not build the whole roadmap in one change.
3. **Explain important decisions.** When introducing a dependency, service, abstraction, or infrastructure component, briefly explain what it does and why it is needed.
4. **Avoid overengineering.** Do not add Kubernetes, Terraform, Redis, microservices, elaborate authentication, or other infrastructure without a clear requirement and an explanation of the learning benefit.
5. **Keep documentation accurate.** Do not claim a feature, test, deployment, or command works unless it has been implemented or verified.
6. **Test changes.** Add or update relevant tests and run the checks available in the current environment. Clearly report checks that could not be run.
7. **Keep changes focused.** Avoid unrelated refactors and unnecessary formatting changes.
8. **Protect secrets.** Never commit credentials, tokens, private keys, or real environment files. Update `.env.example` when configuration changes.
9. **Use clear names and types.** Prefer straightforward functions and explicit data models over clever or opaque abstractions.
10. **Keep the README and roadmap current** as implementation status changes.

## Security requirements

- Treat configured endpoint URLs as untrusted input.
- Support only `http` and `https` schemes.
- Before enabling public endpoint management, implement and test protections against server-side request forgery (SSRF), including requests to loopback, private, link-local, and internal destinations. Consider DNS resolution and redirects, not only the original hostname.
- Apply request timeouts and sensible response-size limits to checks.
- Do not expose secrets or sensitive internal error details in API responses or logs.
- The public status page must be read-only. Management operations must be protected before public deployment.
- Never disable TLS certificate validation as a routine workaround.

## Backend conventions

- Keep HTTP route handlers thin; place reusable application logic in services.
- Validate incoming data with explicit schemas.
- Keep database access and transaction boundaries understandable.
- Store timestamps consistently in UTC.
- Handle timeouts, connection errors, non-success HTTP responses, and unexpected failures explicitly.
- Do not treat an HTTP error status as the same thing as a network-level failure; preserve enough information to diagnose a check.

## Worker conventions

- Keep scheduled checks independent from API request handling.
- Avoid overlapping checks for the same endpoint unless deliberately supported.
- Use bounded timeouts and avoid downloading unlimited response bodies.
- Persist a result for both successful checks and expected failures.
- Make scheduling behavior configurable rather than scattering timing constants throughout the code.

## Frontend conventions

- Use TypeScript types for API data.
- Keep API calls separate from presentation components where practical.
- Provide clear loading, empty, and error states.
- Make status labels understandable; do not rely on color alone.
- Keep the public status view read-only.

## Docker and deployment conventions

- Keep configuration in environment variables and document required values.
- Use `.env.example` for variable names and safe placeholders only.
- Persist PostgreSQL data through a named volume in local Compose.
- Keep containers and exposed ports to the minimum needed.
- Prefer reproducible builds and explicit health checks where useful.
- Do not describe a service as production-ready merely because it runs in Docker.
- Deployment instructions must match the actual configuration in the repository.

## Before finishing a change

- Summarize what changed and why.
- List tests or validation commands run and their outcomes.
- Mention known limitations or follow-up work.
- Identify any new environment variables or setup steps.
