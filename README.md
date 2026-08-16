# Pamawas Website

The official website for **Pamawas** — AI Infrastructure Incident Investigator.

Built with [Astro](https://astro.build) and deployed to GitHub Pages at `pamawas.github.io`.

## What is Pamawas?

Pamawas transforms alert floods into actionable incident reports. It's an AI-powered infrastructure incident investigator that:

1. **Ingests** alerts from Grafana, Prometheus, Loki, and generic webhooks
2. **Correlates** raw alerts into meaningful incidents (deterministic: 2,300+ alerts → ~17 incidents)
3. **Investigates** root cause using a bounded LLM agent with PromQL, LogQL, and deployment history tools
4. **Reports** concise morning digests via Discord, Telegram, and Email
5. **Schedules** daily reports + immediate high-severity alerts

## Components

| Component | Repository | Description |
|-----------|------------|-------------|
| **Ingest** | [pamawas-ingest](https://github.com/Pamawas/pamawas-ingest) | Webhook ingestion & event normalization (Go) |
| **Correlator** | [pamawas-correlator](https://github.com/Pamawas/pamawas-correlator) | Deterministic alert→incident correlation (Go) |
| **Investigator** | [pamawas-investigator](https://github.com/Pamawas/pamawas-investigator) | Bounded LLM investigator with tool access (Python) |
| **Reporter** | [pamawas-reporter](https://github.com/Pamawas/pamawas-reporter) | Report generation & delivery adapters (Go) |
| **Scheduler** | [pamawas-scheduler](https://github.com/Pamawas/pamawas-scheduler) | Daily cron + immediate high-severity triggers (Go) |
| **Schema** | [pamawas-schema](https://github.com/Pamawas/pamawas-schema) | Shared DB schema, migrations, Go types (Go/SQL) |
| **Infra** | [pamawas-infra](https://github.com/Pamawas/pamawas-infra) | Docker Compose, K8s, Helm, ArgoCD configs |

## Development

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Deployment

This site auto-deploys to GitHub Pages on pushes to `main` via GitHub Actions (`.github/workflows/deploy.yml`).

## Documentation

- **MVP Design**: [ai-infra-incident-investigator-mvp-design.md](../ai-infra-incident-investigator-mvp-design.md)
- **Grand Design**: [ai-infra-incident-investigator-grand-design.md](../ai-infra-incident-investigator-grand-design.md)
- **Project README**: [Main Pamawas README](../README.md)

## License

MIT License — See individual component licenses.