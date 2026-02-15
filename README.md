# Engineering Team Agent Skills

Reusable [Claude Code](https://claude.com/claude-code) slash-command agents that form a complete engineering team. Drop them into any project's `.claude/commands/` directory and customize the `{{PLACEHOLDERS}}`.

## The Team

| File | Slash Command | Role |
|------|--------------|------|
| `jira-officer.md` | `/jira-officer` | Ticket creation, lifecycle, documentation, compliance audits |
| `github-officer.md` | `/github-officer` | Branching, commits, pushes, PRs, code safety |
| `api-engineer.md` | `/api-engineer` | API design, contracts, backward compatibility, frontend sync |
| `db-engineer.md` | `/db-engineer` | Schema design, indexes, migrations, query optimization |
| `code-reviewer.md` | `/code-reviewer` | Quality standards, security, library currency (Context7) |
| `build-test.md` | `/build-test` | Build validation, test execution, pre-commit gate |
| `team.md` | `/team` | Orchestrator — coordinates all agents for end-to-end delivery |
| `wiki-sync.md` | `/wiki-sync` | Pushes agent definitions to a local Wiki.js knowledge base |
| `lessons-learned.md` | (reference doc) | Living document of past mistakes — all agents read before acting |

## Quick Start

```bash
# 1. Copy into your project's .claude/commands/
mkdir -p .claude/commands
cp /path/to/skills/*.md .claude/commands/

# 2. Find and replace placeholders
# Search for {{...}} in each file and fill in your project values
```

## Placeholders to Customize

Each file uses `{{PLACEHOLDER}}` markers for project-specific values:

| Placeholder | Example | Where Used |
|-------------|---------|------------|
| `{{PROJECT_NAME}}` | My App | All files |
| `{{PROJECT_KEY}}` | MYAPP | Jira officer, GitHub officer, team |
| `{{JIRA_PROJECT_ID}}` | 10708 | Jira officer |
| `{{JIRA_SITE}}` | yoursite.atlassian.net | Jira officer |
| `{{JIRA_EMAIL}}` | you@company.com | Jira officer |
| `{{JIRA_BUG_TYPE_ID}}` | 10005 | Jira officer |
| `{{GITHUB_OWNER}}` | your-username | GitHub officer |
| `{{GITHUB_REPO}}` | my-project | GitHub officer |
| `{{DEFAULT_BRANCH}}` | main | GitHub officer |
| `{{DB_PORT}}` | 5432 | DB engineer |
| `{{DB_NAME}}` | myapp_dev | DB engineer |
| `{{DB_USER}}` | myapp_admin | DB engineer |
| `{{DB_PASSWORD}}` | dev_password | DB engineer |
| `{{WIKI_PORT}}` | 3001 | Wiki sync |
| `{{WIKI_DB}}` | myapp_wiki | Wiki sync |

## Pipeline Workflow

When used together via `/team`, the agents follow this pipeline:

```
1. Jira Officer    -> creates/finds ticket, moves to In Progress
2. API Engineer    -> designs API contract
3. DB Engineer     -> designs schema changes
4. Developer (you) -> implements the feature
5. Code Reviewer   -> reviews code quality, security
6. Build & Test    -> validates builds and tests pass
7. GitHub Officer  -> commits and pushes
8. Jira Officer    -> adds resolution comment, closes ticket
```

## Key Features

- **Full autonomy** — agents act without stopping to ask permission
- **Lessons learned** — living document prevents repeated mistakes
- **Build gate** — builds must pass before any commit
- **Context7 integration** — code reviewer checks library versions automatically
- **Wiki.js sync** — optional local knowledge base for agent definitions

## Customization Tips

1. **lessons-learned.md** — delete the example entries and start fresh, or keep relevant ones
2. **code-reviewer.md** — update the "Project Standards" section for your tech stack
3. **db-engineer.md** — update "Established Patterns" for your ORM and database
4. **build-test.md** — update build commands for your package manager and workspaces
5. **api-engineer.md** — update "Project API Architecture" for your framework

## Prerequisites

- [Claude Code](https://claude.com/claude-code) CLI
- MCP servers configured: `atlassian` (Jira), `github`, optionally `context7`
- `gh` CLI authenticated for GitHub operations

## License

MIT — use these in any project.
