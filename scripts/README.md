# Claude Agents Scripts

Utility scripts for Claude Code agents and workflows management.

## 📦 Available Scripts

### validate-agents.sh

Validates the structure and format of agent files in the repository.

**Purpose**: Ensure all agents meet quality standards before publishing.

**Usage**:
```bash
./scripts/validate-agents.sh
```

**What it validates**:
- ✅ Plugin directory structure exists
- ✅ Agent files have YAML frontmatter
- ✅ Required fields: name, description, model, color
- ✅ Name follows kebab-case convention
- ✅ File encoding is UTF-8
- ✅ No excessively long lines

**Output**:
- Passes: ✓ Green checkmarks
- Fails: ✗ Red errors
- Warnings: ⚠ Yellow warnings
- Summary report with counts

**Used in CI/CD**: This script runs automatically in GitHub Actions on pull requests.

---

### sync-workflows.sh

Synchronizes GitHub Actions workflows from this repository to your projects.

**Purpose**: Install reusable workflows for automated code review.

**Usage**:
```bash
# Interactive mode
./scripts/sync-workflows.sh

# From remote repository
./scripts/sync-workflows.sh https://github.com/your-org/workflows.git

# With environment variable
WORKFLOWS_REPO=https://github.com/company/workflows.git ./scripts/sync-workflows.sh
```

**What it does**:
1. Lists available workflows (Python backend review, Flutter app review, etc.)
2. Lets you select which workflows to install
3. Copies workflows to `.github/workflows/` in your project
4. Shows configuration instructions (secrets, permissions)

**Available workflows**:
- `code-review-backend-py.yml` - Automated Python backend PR reviews
- `code-review-flutter-app.yml` - Automated Flutter app PR reviews

---

## 🗑️ Removed Scripts

### ~~sync-agents.sh~~ (REMOVED)

**Status**: ❌ Removed in favor of modern plugin system

**Migration**: Use Claude Code's built-in plugin system instead:

```bash
# Old way (removed)
./scripts/sync-agents.sh

# New way (2026)
/plugin marketplace add Grinest/agents
/plugin install python-development@agents
```

**See**: [MIGRATION.md](../MIGRATION.md) for complete migration guide.

---

## 🏗️ Plugin System (Recommended)

As of 2026, agent installation uses Claude Code's native plugin system:

### Installation
```bash
# Add marketplace
/plugin marketplace add Grinest/agents

# Install plugins
/plugin install general@agents
/plugin install python-development@agents
/plugin install flutter-development@agents
```

### Benefits over bash scripts
- ✅ Version control and auto-updates
- ✅ One-command installation
- ✅ Namespace isolation
- ✅ Team configuration via `.claude/settings.json`
- ✅ No manual file copying

### Documentation
- [Plugin System Guide](./../.claude-plugin/README.md)
- [Migration Guide](../MIGRATION.md)
- [Main README](../README.md)

---

## 🛠️ Development

### Running Validation Locally

Before submitting a PR, validate your changes:

```bash
./scripts/validate-agents.sh
```

Fix any errors or warnings before committing.

### Adding New Workflows

1. Create workflow in `git-workflows/[technology]/`
2. Add documentation in `git-workflows/README.md`
3. Test workflow in a sample project
4. Update `sync-workflows.sh` if needed

### CI/CD Integration

The validation script runs automatically in GitHub Actions:

```yaml
# .github/workflows/validate-agents.yml
- name: Validate agents
  run: ./scripts/validate-agents.sh
```

This ensures all agents meet quality standards before merging.

---

## 📚 Additional Resources

- [Main README](../README.md) - Complete project documentation
- [Plugin README](../plugins/README.md) - Plugin architecture guide
- [Workflows README](../git-workflows/README.md) - GitHub Actions workflows
- [Migration Guide](../MIGRATION.md) - Migrate from bash scripts to plugins

---

## 🐛 Troubleshooting

### Validation fails on valid agent

Check that your agent file has:
- Proper YAML frontmatter with `---` delimiters
- All required fields: name, description, model, color
- Valid model value: `inherit`, `sonnet`, `opus`, or `haiku`
- kebab-case name format

### Workflow sync script doesn't find workflows

Ensure:
- You're in the repository root
- `git-workflows/` directory exists
- Workflow files have `.yml` extension

### Permission denied when running scripts

Make scripts executable:
```bash
chmod +x scripts/validate-agents.sh
chmod +x scripts/sync-workflows.sh
```

---

## 📄 License

MIT License - See [LICENSE](../LICENSE) for details.
