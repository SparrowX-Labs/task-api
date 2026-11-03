# Task API

FastAPI operational task service for SparrowX. It provides task management, PostgreSQL persistence in the Crossplane-managed `taskdb` database, health checks, and Prometheus metrics.

The API is served under `/api/tasks/`; `/health` supports probes, `/api/tasks/health` supports smoke tests, `/metrics` exposes metrics, and `/docs`/`/redoc` provide API documentation.

The service is deployed by Argo CD into separate `dev` and `prod` namespaces on the same EKS cluster using the corresponding Helm values file. Shared workflows handle immutable image builds, security checks, promotion, synchronization, and post-deployment validation.

Define `HEALTH_CHECK_PATH`; use repository-level `AWS_ROLE_NAME` only for a separate IAM role. Shared AWS variables, URLs, and Argo CD credentials are inherited.

## Local development

```bash
python -m pip install -r requirements-dev.txt
pytest
uvicorn src.main:app --reload --port 8000
```

Configure `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USERNAME`, `DB_PASSWORD`, and optional `CORS_ALLOW_ORIGINS`.

## License

See [LICENSE.md](LICENSE.md).
