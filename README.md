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

## Adopting the preset in a repository

1. Add the `renovate.json` above.
2. Turn off Dependabot security updates (Settings → Code security → Dependabot
   security updates), or with `gh api -X DELETE
   repos/altissimo-hq/<repo>/automated-security-fixes`. New repositories in the
   org start with them on, so that alerts get fix PRs before Renovate is set
   up. Once Renovate is set up it opens the security PRs, and leaving
   Dependabot on means two PRs for the same fix.
3. Leave Dependabot alerts on. Renovate reads them to find security fixes.
4. Close any open Dependabot PRs. Renovate's PRs replace them.

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
