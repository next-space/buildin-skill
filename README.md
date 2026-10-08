# Buildin CLI Skill

Use the Buildin CLI safely for authorized Buildin V2 API and content tasks.

## Install from ClawHub

```bash
openclaw skills install @buildin/buildin-skills
```

The Skill checks CLI and authentication state first. Installation, updates and login follow the user\'s authorization. Requested
remote changes execute within the already-authorized task; routine ID resolution
and implementation choices do not require another confirmation. Ambiguous targets
or changes outside that task require clarification.

## Development

```bash
npm run check
```
