# Contributing

Thanks for helping improve this collection. Contributions should make a skill more useful, easier to understand, or safer without expanding its scope unnecessarily.

## Before you start

- Search existing issues and pull requests for related work.
- Prefer a focused change over a broad rewrite.
- Open an issue first when a proposal changes a skill's purpose, activation boundary, output contract, or license.
- Never include secrets, private user data, generated credentials, or machine-specific paths.

## Add or update a skill

Each skill belongs in `skills/<skill-name>/` and must contain a `SKILL.md` with valid YAML frontmatter:

```yaml
---
name: skill-name
description: Explain what the skill does and when it should be used.
---
```

Keep the directory name and frontmatter `name` identical. Use lowercase letters, digits, and hyphens.

When changing a skill:

- Keep the description concise and discriminating because agents use it for discovery.
- Put essential workflow guidance in `SKILL.md`; move conditional detail into linked references.
- Add scripts only when deterministic automation materially improves reliability.
- Keep core instructions provider-neutral where practical.
- Preserve authorization boundaries: a skill must not imply permission for unrelated external actions.
- Include license and attribution information for imported or adapted work.
- Update the catalog in `README.md` when adding, removing, or renaming a skill.
- Keep `.claude-plugin/marketplace.json` in sync so every published skill remains independently installable in Claude Code.

## Validate your change

Confirm the repository can discover every skill:

```bash
npx skills add . --list
claude plugin validate . --strict
```

For each changed skill:

1. Install it from the local repository into a disposable project.
2. Test at least one realistic request that should activate it.
3. Test one nearby request that should not activate it when the boundary matters.
4. Inspect generated artifacts or side effects rather than relying only on the agent's summary.
5. Run `git diff --check` before submitting.

## Pull requests

Explain the user-visible problem, why the change is appropriately scoped, and what you actually verified. Keep unrelated formatting or refactors out of the pull request.

By contributing, you agree that your contribution is licensed under the Apache License 2.0.
