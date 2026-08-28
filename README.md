# Agent Skills

A provider-neutral collection of reusable agent skills. Each skill is self-contained under `skills/<skill-name>/` and can be installed or copied independently.

## Catalog

| Skill | Purpose | Invocation |
| --- | --- | --- |
| `common-ground` | Align intent, evidence, assumptions, and deviation rules for ambiguous project work | `$common-ground` |
| `eli5` | Create a beginner-friendly visual explainer as a portable standalone HTML file | `$eli5` |

## Repository layout

```text
.
├── README.md
└── skills/
    ├── common-ground/
    │   ├── SKILL.md
    │   ├── agents/
    │   └── references/
    └── eli5/
        ├── SKILL.md
        ├── agents/
        ├── LICENSE
        └── NOTICE
```

## Collection conventions

- Keep one skill per directory, with the directory name matching the `name` in its `SKILL.md` frontmatter.
- Keep core instructions provider-neutral. Put optional runtime-specific interface metadata under `agents/`.
- Keep references, scripts, assets, licenses, and notices inside the skill that owns them so each skill remains portable.
- Avoid cross-skill relative dependencies unless the dependency is explicit and genuinely required.
- Validate every changed skill independently before publishing it.

## Licensing

Licensing is declared per skill. The imported `eli5` skill is distributed under Apache-2.0 and retains its original notice in `skills/eli5/`.
