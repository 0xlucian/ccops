# Deployment

## Pre-deployment Checklist

- [ ] All tests pass
- [ ] No linting errors
- [ ] PR approved and merged to deploy branch
- [ ] Environment variables verified

## {{REPO_1_NAME}}

**Deploy target**: {{DEPLOY_TARGET}}
**Deploy branch**: `main`

```bash
# Deploy command
{{DEPLOY_COMMAND}}
```

**Rollback**:
```bash
{{ROLLBACK_COMMAND}}
```

## {{REPO_2_NAME}}

**Deploy target**: {{DEPLOY_TARGET}}
**Deploy branch**: `main`

```bash
# Build and deploy
{{DEPLOY_COMMAND}}
```

## {{REPO_3_NAME}}

**Deploy target**: {{DEPLOY_TARGET}}
**Deploy branch**: `main`

```bash
# Build and deploy
{{DEPLOY_COMMAND}}
```

## Post-deployment Verification

1. Check application logs for errors
2. Verify health endpoints respond
3. Run smoke tests if available
4. Monitor error rates for 15 minutes
