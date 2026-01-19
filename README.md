# Claude Code Archetypes

Role-based configuration system for Claude Code that loads different rules and permissions based on your current task.

## Roles

### Engineer (`claude-as engineer`)
Senior Software Engineer / Architect focused on implementation.

**Can do:**
- Full git workflow (add, commit, push to feature branches, create PRs)
- Edit any source code files
- Run builds, tests, and linters
- Create database migrations

**Cannot do:**
- Deploy directly (`fly deploy`)
- Modify infrastructure configs
- Push to main/master

### Analyst (`claude-as analyst`)
Business Analyst / Planner focused on requirements and documentation.

**Can do:**
- Read any files in the codebase
- Edit markdown files only
- Web search for research
- View git history (read-only)

**Cannot do:**
- Modify source code
- Git commits or pushes
- Run builds or tests

### DevOps (`claude-as devops`)
DevOps Engineer focused on monitoring and CI/CD.

**Can do:**
- View fly.io status, logs, releases
- Monitor GitHub Actions workflows
- Edit Dockerfile, fly.toml, workflow files
- Diagnostic commands (curl, dig)

**Cannot do:**
- Deploy (`fly deploy`)
- Set secrets (`fly secrets set`)
- Modify application source code
- Run database migrations

## Installation

```bash
# Clone or copy files to ~/.claude
cp -r archetypes ~/.claude/
cp CLAUDE.base.md ~/.claude/
cp bin/claude-as ~/.claude/bin/
chmod +x ~/.claude/bin/claude-as

# Add to PATH (add to ~/.bashrc or ~/.zshrc)
export PATH="$HOME/.claude/bin:$PATH"
```

## Usage

```bash
# Start Claude as an engineer (default)
claude-as engineer

# Start as business analyst
claude-as analyst

# Start as devops engineer
claude-as devops

# Pass additional arguments to claude
claude-as engineer --model opus

# List available roles
claude-as --list

# Show help
claude-as --help
```

## How It Works

When you run `claude-as <role>`:

1. Combines `CLAUDE.base.md` (universal safety rules) with `archetypes/<role>/context.md`
2. Writes the result to `~/.claude/CLAUDE.md`
3. Copies `archetypes/<role>/permissions.json` to `~/.claude/settings.json`
4. Launches Claude Code with the new configuration

## File Structure

```
~/.claude/
├── CLAUDE.base.md           # Universal rules (always included)
├── CLAUDE.md                # Active config (generated)
├── settings.json            # Active permissions (generated)
├── archetypes/
│   ├── engineer/
│   │   ├── context.md       # Engineer-specific rules
│   │   └── permissions.json # Engineer permissions
│   ├── analyst/
│   │   ├── context.md       # Analyst-specific rules
│   │   └── permissions.json # Analyst permissions
│   └── devops/
│       ├── context.md       # DevOps-specific rules
│       └── permissions.json # DevOps permissions
└── bin/
    └── claude-as            # Activation script
```

## Adding New Roles

1. Create a new directory: `mkdir ~/.claude/archetypes/myrole`
2. Add `context.md` with role-specific instructions
3. Add `permissions.json` with allowed bash commands
4. Run `claude-as myrole`

## License

MIT
