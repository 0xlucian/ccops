# Infrastructure

## Hosting

- **Provider**: {{HOSTING_PROVIDER}}
- **Region**: {{REGION}}
- **Apps**:
  - `{{APP_1_NAME}}` — {{APP_1_DESCRIPTION}} ({{APP_1_URL}})
  - `{{APP_2_NAME}}` — {{APP_2_DESCRIPTION}} ({{APP_2_URL}})

## Database

- **Type**: {{DATABASE_TYPE}}
- **Host**: {{DATABASE_HOST}}
- **Databases**:
  - `{{DB_NAME_1}}` — {{DB_DESCRIPTION_1}}

See `db.md` for schema reference.

## Environment Variables

> **Note**: Values are stored in the hosting provider's config. Only names are documented here.

| Variable | Used By | Description |
|---|---|---|
| `DATABASE_URL` | Backend | Database connection string |
| `API_KEY` | Backend | External API key |
| `JWT_SECRET` | Backend | Token signing secret |

## Monitoring

- **Logs**: {{LOG_PROVIDER}} (e.g., Papertrail, Datadog)
- **Alerts**: {{ALERT_PROVIDER}}
- **Dashboard**: {{DASHBOARD_URL}}
