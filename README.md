# Buildin CLI Skill

Private Codex plugin bundle for the Buildin CLI agent skill.

## Install

Install this private repository as a plugin or install the skill directly:

```bash
npx skills add next-space/buildin-skill --skill buildin-cli
```

Direct path:

```bash
npx skills add https://github.com/next-space/buildin-skill/tree/main/skills/buildin-cli
```

## Usage

Use this skill when an agent needs to call the Buildin V2 API through the
`buildin` command. The skill instructs agents to inspect CLI help first, use
`--json` for machine-readable output, use `BUILDIN_TOKEN` or saved credentials
for authentication, and avoid raw `curl` calls for Buildin API work.

## Development

```bash
npm run check
```

