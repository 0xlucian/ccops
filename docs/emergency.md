# Emergency Runbook

## Triage

1. **Identify** — Which service is affected? Check monitoring dashboard.
2. **Assess** — Is it user-facing? How many users impacted?
3. **Communicate** — Notify the team in {{SLACK_CHANNEL}}.
4. **Act** — Follow the relevant playbook below.

## Playbooks

### Application Down

1. Check hosting provider status page
2. Check application logs: `{{LOG_COMMAND}}`
3. Check recent deployments: `{{DEPLOY_HISTORY_COMMAND}}`
4. If caused by recent deploy, rollback: `{{ROLLBACK_COMMAND}}`
5. If infrastructure issue, check {{HOSTING_PROVIDER}} dashboard

### Database Issues

1. Check database status / metrics
2. Check connection count — are we hitting pool limits?
3. Check for long-running queries
4. Check disk usage
5. If replication lag, check secondary nodes

### High Error Rate

1. Check error logs for patterns
2. Identify if errors correlate with a specific endpoint
3. Check if an external dependency is down
4. Check recent code changes for the affected service

### Memory / CPU Spike

1. Check which process is consuming resources
2. Check for memory leaks (growing heap over time)
3. Check for runaway queries or background jobs
4. Restart the affected dyno/container as temporary fix
5. Investigate root cause

## Contacts

| Role | Name | Contact |
|---|---|---|
| {{ROLE}} | {{NAME}} | {{CONTACT}} |
