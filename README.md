# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) preset for `altissimo-hq` repositories.

To use it, a repository's `renovate.json` extends this preset:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>altissimo-hq/renovate-config"]
}
```

Repo-specific settings can sit alongside `extends` and override the preset.

## What the preset does

`default.json`:

- Groups all minor, patch, pin and digest updates into one PR a month. Major
  updates get their own PRs.
- Refreshes `poetry.lock` monthly, so fixes for indirect dependencies (where
  most security alerts are) get picked up.
- Opens security fixes at any time, labeled `security`, from GitHub's
  Dependabot alerts and from OSV.
- Ignores `.python-version`, which is the local dev interpreter.

The schedule is the whole first day of the month (UTC). The earlier window,
"before 6am on the first day of the month", produced no scheduled PRs in
October in any repo that used it.
