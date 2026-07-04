---
name: buildin-cli
description: Use when an agent needs to call the Buildin API through the Buildin CLI, authenticate Buildin, upload a file, create or update a page, query a database, search content, edit Markdown page content, or any task involving the `buildin` command.
license: MIT
---

# Buildin CLI

Use the Buildin CLI (`buildin`) for Buildin V2 API work: pages, blocks,
databases, search, Markdown content, and files.

Use only the Buildin command, Buildin base URL, `BUILDIN_*` environment
variables, and Buildin credential store for Buildin work.

## First rule: ask the CLI

The CLI is self-documenting. Prefer these commands over guessing syntax or
request fields:

- `buildin --help` - list global options and top-level commands.
- `buildin help <command...>` - show usage, options, examples, and notes for any
  command or subcommand.
- `buildin api ls` - list public API endpoints and request field hints.
- `buildin api --docs <PATH> -X <METHOD>` - show agent-readable Markdown docs
  for one endpoint, including parameters, examples, and safety notes.
- `buildin api --spec <PATH> -X <METHOD>` - show the exact embedded OpenAPI
  fragment for one endpoint.
- `buildin --json doctor` - inspect local authentication and configuration
  state when auth or base URL selection is unclear.
- `buildin --json whoami` - verify the active Buildin identity.
- `buildin --json markdown get <page-id>` - retrieve page content as Markdown.

If you are unsure about syntax, request body fields, pagination, auth source,
or command coverage, run help first.

## Working rules

- Use `--json` for stable machine-readable stdout.
- Keep JSON request bodies in local files and pass them with `--body <file>`.
- Keep Markdown replacement content in local files and pass it with `--file <file>`.
- Check `BUILDIN_TOKEN` first. Credential precedence is `--token`, then
  `BUILDIN_TOKEN`, then saved login credentials.
- Do not print or save bearer tokens outside the Buildin CLI credential store.
- Prefer domain commands over `api call`; `buildin api --docs` names a
  recommended domain command when one exists.
- Do not call the Buildin V2 API with `curl`.
- Before write operations, confirm IDs, file paths, URLs, and body files come
  from user-authorized input.

## Useful commands

- Pages: `page get/create/update`, `page property get`
- Blocks: `block get/children/append/update/append-file`
- Databases: `database get/query/create/update`
- Markdown: `markdown get/put`
- Search: `search text`, `search semantic`
- Files: `file upload`
- Fallback: `buildin --json api call ...`

For fallback API work, use this lookup sequence before constructing a request:

```bash
buildin api ls
buildin api --docs /v2/blocks/{block_id}/children -X PATCH
buildin api --spec /v2/blocks/{block_id}/children -X PATCH
buildin --json api call PATCH /v2/blocks/:block_id/children --param block_id=<block_id> --body body.json
```

Use `buildin api ls --plain` when you need a compact list of request fields for
operations such as `updateBlock` or `appendBlockChildren`. Use `--spec` when
the full OpenAPI schema is needed.

