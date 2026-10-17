# Planned repository structure

```text
pulsecheck/
├── .github/workflows/     # CI workflows (GitHub Actions)
├── backend/
│   ├── app/
│   │   ├── api/routes/    # FastAPI route handlers
│   │   ├── core/          # Configuration and shared app setup
│   │   ├── db/            # Database session and persistence setup
│   │   ├── models/        # Database models
│   │   ├── schemas/       # Request/response validation schemas
│   │   ├── services/      # Application logic
│   │   └── main.py        # API entry point
│   └── tests/
├── deploy/caddy/          # Reverse proxy and HTTPS configuration
├── docs/                  # Architecture notes and learning notes
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/    # Shared UI components
│       ├── pages/         # Dashboard and status page views
│       ├── lib/           # API client and shared utilities
│       └── types/         # Shared TypeScript types
├── worker/
│   ├── app/               # Periodic endpoint checker and scheduler
│   └── tests/
├── .dockerignore
├── .env.example
├── .gitignore
├── AGENTS.md
├── LICENSE
├── PROJECT_STRUCTURE.md
└── README.md
```

This is a planned structure, not a claim that the application is implemented. Add files when their purpose becomes clear; remove or rename directories if the implementation shows a simpler design is better.
