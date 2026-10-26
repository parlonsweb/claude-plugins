# learn

Shared plugin that reviews the current session and saves useful context to the Claude Code auto-memory system.

## Skills

### `/learn`

Run it at the end of a session or any time the conversation has surfaced something worth keeping. The skill scans the exchange for four types of information:

- **Feedback** — corrections you gave Claude ("don't do X", "use Y instead") and approaches you confirmed worked ("yes exactly", accepting an unusual choice)
- **User context** — your role, expertise, stated preferences, or things to avoid
- **Project context** — decisions and their reasons, deadlines, constraints, architectural choices
- **References** — pointers to external systems (cloud console projects, GitOps apps, password-manager vaults, GitHub repos, dashboards)

It reads your existing memory index first, updates entries that already cover the topic, and only creates new files for genuinely new information. At the end it reports what was saved.

## Install

```
/plugin install learn@parlonsweb
```

## Usage

```
/learn
/learn focus on the Terraform discussion
```

The optional argument narrows the scan to a specific part of the session.
