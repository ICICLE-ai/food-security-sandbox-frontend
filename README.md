# Food Security Sandbox frontend

React (Create React App) user interface for the Food Security Sandbox.

## API calls

All requests use relative `/api/...` paths. In the deployed image, Nginx forwards them to the app
server set in the `BACKEND_URL` environment variable. No backend URL is compiled into the bundle.

| Variable | Value |
|---|---|
| `BACKEND_URL` | App server URL (origin only, no path) |
| `BACKEND_MAX_BODY_SIZE_MB` | `50`, for CSV uploads |
| `BACKEND_READ_TIMEOUT_SECONDS` | `300` |

## Run locally

```bash
npm ci
npm start
```

`npm run build` writes the production build to `dist/`, which the ICICLE Nginx image serves.

## Deployment

Deployed to the `fss` Tapis pod (image `ghcr.io/icicle-ai/fss`) by `.github/workflows/deploy.yaml`, using the shared
[ICICLE CI/CD templates](https://github.com/ICICLE-ai/cicd-templates/wiki/Quick-start) (`v2.3.0`).
Bump `service-version` in `icicle-service.yaml` and push to `main` to release.
CI checks the rollout through `GET /healthcheck` (served by Nginx).
