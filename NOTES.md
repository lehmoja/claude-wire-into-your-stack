# NOTES

## Server (MCP)
Connected the `filesystem` server (`@modelcontextprotocol/server-filesystem`) at project scope, committed in `.mcp.json`, pointed at `.` (the repo root). It's useful here because the course work is largely about reading and cross-checking files in this repo (docs, config, source) — having Claude reach the filesystem through a dedicated server rather than ad hoc shell commands.

My permission rule in `.claude/settings.json` allows only the read-only tools: `read_text_file`, `read_multiple_files`, `list_directory`, `list_directory_with_sizes`, `directory_tree`, `search_files`, `get_file_info`, `list_allowed_directories`. `write_file`, `edit_file`, `move_file`, and `create_directory` are not allowed — the server can look, not touch. Used it to list `docs/` and inspect file metadata (`list_directory` + `get_file_info`) to sort documents by last-modified date.

## Skill
The repeated way of working: whenever someone wants a rundown of the project's docs, freshest first. Captured as `.claude/skills/open_docs_folder/SKILL.md`.

Description: "Use the filesystem MCP server to list the project's docs folder, sorted by last-modified date, descending." Worded around the concrete action (list docs, sorted by date) rather than a vague topic, so it fires on phrasing like "what documents exist in this project, newest first" without naming the skill — confirmed this triggers correctly.

## Command
Not yet added.

## Hook
`PostToolUse` on matcher `Edit|Write` in `.claude/settings.json`: runs `eslint --fix` on the edited file if it's a `.js` file outside `node_modules`. It reacts rather than prevents — it doesn't block the edit, it cleans up after it, so every JS edit stays lint-clean automatically for anyone who pulls the repo.

## Headless run
Not yet done.
