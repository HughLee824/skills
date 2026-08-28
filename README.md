# Agent Skills

[English](README.md) | [简体中文](README.zh-CN.md)

Small, auditable agent skills for closing understanding gaps before they become implementation gaps.

This repository contains focused skills that can be installed independently. The core instructions follow the open [Agent Skills](https://agentskills.io/) format, while optional integrations improve the experience in Codex and Claude Code.

## Why this exists

Agents do not only fail because they cannot write the code. They also fail when intent, terminology, assumptions, or explanations drift apart unnoticed.

![Two complementary ways to close understanding gaps: Common Ground aligns mismatched maps into a shared blueprint, while ELI5 turns a tangled system into a clear visual model.](docs/assets/skills-overview.webp)

This collection addresses both sides of that problem:

- `common-ground` helps a user and an agent discover material gaps before acting on them.
- `eli5` turns a complex topic into a visual explanation that is easy to inspect and share.

The goal is not to accumulate as many skills as possible. It is to maintain a small set of useful, understandable workflows with explicit boundaries.

## Skills

| Skill | Use it when | Result |
| --- | --- | --- |
| [`common-ground`](skills/common-ground/) | Intent, terminology, acceptance criteria, or consequential assumptions may differ | A shared working map with visible facts, decisions, assumptions, unknowns, and deviation rules |
| [`eli5`](skills/eli5/) | A complex topic would be easier to understand through diagrams and minimal prose | A portable, standalone visual explainer in HTML |

## Install with the `skills` CLI

Review the available skills before installing them:

```bash
npx skills add HughLee824/skills --list
```

Install one skill globally for Codex:

```bash
npx skills add HughLee824/skills --skill common-ground -g -a codex
npx skills add HughLee824/skills --skill eli5 -g -a codex
```

Install one skill globally for Claude Code:

```bash
npx skills add HughLee824/skills --skill common-ground -g -a claude-code
npx skills add HughLee824/skills --skill eli5 -g -a claude-code
```

Omit `-g` for a project-scoped installation.

Agent skills run with the permissions available to your agent. Read a skill's `SKILL.md` and any bundled scripts before installing or invoking it.

## Install from the [Claude Code marketplace](https://code.claude.com/docs/en/plugin-marketplaces)

Add this repository as a marketplace once:

```text
/plugin marketplace add HughLee824/skills
```

Then install either skill independently:

```text
/plugin install common-ground@hughlee-skills
/plugin install eli5@hughlee-skills
```

Run `/reload-plugins` if Claude Code prompts you to activate newly installed plugins. Marketplace installs use Claude Code's namespaced commands: `/common-ground:common-ground` and `/eli5:eli5`.

### Manual installation

Clone the repository and copy the skill you want into the user-level skills directory for your agent:

```bash
git clone https://github.com/HughLee824/skills.git agent-skills

# Codex
mkdir -p "$HOME/.agents/skills"
cp -R agent-skills/skills/common-ground "$HOME/.agents/skills/common-ground"

# Claude Code
mkdir -p "$HOME/.claude/skills"
cp -R agent-skills/skills/common-ground "$HOME/.claude/skills/common-ground"
```

Restart the agent if the new skill does not appear automatically.

## Use

Invoke a skill explicitly when you want its workflow:

```text
# Codex
$common-ground Help us align on the checkout redesign before implementation.

$eli5 Explain how DNS turns a domain name into a server address.

# Claude Code via the skills CLI or manual installation
/common-ground Help us align on the checkout redesign before implementation.

/eli5 Explain how DNS turns a domain name into a server address.
```

Both skills may also be selected automatically when the request clearly matches their descriptions.

## Compatibility

- Structured as standalone Agent Skills with a required `SKILL.md` per skill.
- Tested with Codex, Claude Code, and the `skills` CLI.
- Core instructions are kept independent of a specific agent where practical.
- `agents/openai.yaml` provides optional Codex-facing display metadata and invocation policy.
- `.claude-plugin/marketplace.json` exposes each skill as an independently installable Claude Code plugin without duplicating its instructions.

Compatibility with another agent depends on that agent's support for the Agent Skills format and the capabilities required by the individual skill.

## Project structure

```text
.
├── .claude-plugin/
│   └── marketplace.json
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
├── docs/
│   └── assets/
│       └── skills-overview.webp
├── skills/
│   ├── common-ground/
│   │   ├── SKILL.md
│   │   ├── agents/
│   │   └── references/
│   └── eli5/
│       ├── SKILL.md
│       ├── agents/
│       ├── LICENSE
│       └── NOTICE
├── CONTRIBUTING.md
├── LICENSE
├── NOTICE
├── README.md
├── README.zh-CN.md
└── SECURITY.md
```

## Design principles

- **Focused:** one skill, one coherent job.
- **Discriminating:** descriptions say when a skill should and should not activate.
- **Auditable:** important decisions and boundaries live in readable Markdown.
- **Portable:** optional references, assets, metadata, and attribution travel with the skill that owns them.
- **Evidence-driven:** changes should follow observed failures or realistic usage, not speculative complexity.

## Contributing

Bug reports, documentation fixes, and focused skill improvements are welcome. Read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

For security-sensitive reports, follow [SECURITY.md](SECURITY.md).

## Acknowledgements

- `common-ground` was informed by the known/unknown framing, [Matt Pocock's Grilling skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md), and Anthropic's [field guide to finding unknowns](https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns).
- `eli5` is a portable rewrite inspired by the `eli5` skill from Anthropic's [`claude-plugins-community`](https://github.com/anthropics/claude-plugins-community/tree/main/eli5), originally authored by Thariq Shihipar. See [`skills/eli5/NOTICE`](skills/eli5/NOTICE) for details.

These references are acknowledgements, not runtime dependencies.

## License

Licensed under the [Apache License 2.0](LICENSE). Third-party attribution and adaptation notices are preserved in [NOTICE](NOTICE) and within the skill that owns them.
