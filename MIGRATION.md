# Migration Guide: Bash Scripts to Plugin System

This guide helps you migrate from the old bash script installation method to the modern Claude Code plugin system.

## 📅 Timeline

- **Before**: Used `./scripts/sync-agents.sh` to copy `.md` files
- **Now (2026)**: Use `/plugin` commands for modern installation

## 🚨 Breaking Changes

### Removed

- ❌ `scripts/sync-agents.sh` - No longer available
- ❌ Manual file copying workflow

### Added

- ✅ `.claude-plugin/marketplace.json` - Marketplace catalog
- ✅ `.claude-plugin/plugin.json` in each plugin
- ✅ Plugin-based installation via `/plugin` commands

## 🔄 Migration Steps

### Step 1: Remove Old Installations

If you previously used the bash scripts, clean up old installations:

```bash
# Backup existing agents (optional)
mv .claude/agents .claude/agents.backup

# Or just remove them
rm -rf .claude/agents
```

### Step 2: Add New Marketplace

```bash
/plugin marketplace add juanpaconpa/claude-agents
```

### Step 3: Install Plugins

Replace your old installation with modern plugins:

#### Old Way ❌
```bash
git clone https://github.com/juanpaconpa/claude-agents.git
cd claude-agents
./scripts/sync-agents.sh
# Select agents: 1 2 3
```

#### New Way ✅
```bash
/plugin install general@claude-agents
/plugin install python-development@claude-agents
/plugin install flutter-development@claude-agents
```

### Step 4: Update Team Configuration

If your team had custom configurations, migrate them:

#### Old Way ❌
```bash
# .bashrc or .zshrc
export AGENTS_REPO="https://github.com/empresa/agents.git"
alias sync-agents="~/.claude-agents/scripts/sync-agents.sh"
```

#### New Way ✅
```json
// .claude/settings.json (commit this to repo)
{
  "plugin_marketplaces": ["empresa/agents"],
  "plugins": [
    "python-development@agents",
    "company-standards@agents"
  ]
}
```

### Step 5: Verify Installation

```bash
# List installed plugins
/plugin list

# List available agents
/agents list

# List available skills
/skills list
```

## 📋 Command Mapping

| Old Command | New Command |
|------------|-------------|
| `./scripts/sync-agents.sh` | `/plugin marketplace add owner/repo` |
| Select agents from menu | `/plugin install plugin-name@marketplace` |
| Update agents | `/plugin update plugin-name@marketplace` |
| Check installed agents | `/plugin list` |

## 🎯 Benefits of Migration

### Before (Bash Scripts)
- ❌ Manual cloning required
- ❌ No version control
- ❌ No auto-updates
- ❌ File conflicts possible
- ❌ Team setup inconsistent

### After (Plugin System)
- ✅ One-command installation
- ✅ Semantic versioning
- ✅ Auto-update support
- ✅ Namespace isolation
- ✅ Automatic team setup via `.claude/settings.json`

## 🏢 Enterprise Migration

### Scenario: Company with Private Agents

#### Old Setup
```bash
# Each developer had to:
git clone git@github.com:empresa/private-agents.git
cd private-agents
./scripts/sync-agents.sh
export AGENTS_REPO="git@github.com:empresa/private-agents.git"
```

#### New Setup
```bash
# One-time: Create company marketplace
# Fork juanpaconpa/claude-agents to empresa/agents
# Add company-specific plugins

# In each project: .claude/settings.json (committed)
{
  "plugin_marketplaces": ["empresa/agents"],
  "plugins": ["company-standards@agents"]
}

# Developers just clone and work - plugins install automatically
```

## 📦 Custom Plugin Migration

If you created custom agents in your own fork:

### Step 1: Add Plugin Metadata

```bash
# For each plugin directory
mkdir -p plugins/my-plugin/.claude-plugin
```

Create `plugins/my-plugin/.claude-plugin/plugin.json`:
```json
{
  "name": "my-plugin",
  "description": "Custom agents for my needs",
  "version": "1.0.0",
  "agents": ["agents/my-agent.md"],
  "skills": ["skills/my-skill.md"]
}
```

### Step 2: Create Marketplace Catalog

Create `.claude-plugin/marketplace.json` at repository root:
```json
{
  "name": "my-agents",
  "description": "My custom agent collection",
  "owner": {
    "name": "Your Name"
  },
  "plugins": [
    {
      "name": "my-plugin",
      "source": "plugins/my-plugin",
      "description": "Custom agents",
      "version": "1.0.0"
    }
  ]
}
```

### Step 3: Use Your Custom Marketplace

```bash
/plugin marketplace add your-username/your-repo
/plugin install my-plugin@your-repo
```

## ❓ FAQ

### Q: Can I still copy files manually?

A: Yes, but not recommended. You lose versioning, auto-updates, and namespace isolation.

### Q: Do I need to delete my fork?

A: No! Convert your fork to use the plugin system. See "Custom Plugin Migration" above.

### Q: What about private repositories?

A: Plugin marketplaces work with private repos. Configure Git authentication (SSH keys or tokens).

### Q: Can I use both public and private marketplaces?

A: Yes! You can add multiple marketplaces:
```bash
/plugin marketplace add juanpaconpa/claude-agents  # Public
/plugin marketplace add company/private-agents     # Private
```

### Q: How do I update my plugins?

A: Use `/plugin update`:
```bash
/plugin update python-development@claude-agents
/plugin update --marketplace claude-agents  # Update all from marketplace
```

### Q: What if a plugin breaks my workflow?

A: Pin to a specific version in `plugin.json` or roll back:
```bash
/plugin uninstall python-development@claude-agents
/plugin install python-development@claude-agents@1.0.0  # Specific version
```

## 📞 Support

- **Documentation**: See [README.md](./README.md) for full plugin documentation
- **Issues**: Report problems at https://github.com/juanpaconpa/claude-agents/issues
- **Questions**: Open a discussion on GitHub

## 📚 Additional Resources

- [Plugin System Documentation](./.claude-plugin/README.md)
- [Plugin Development Guide](./plugins/README.md)
- [Claude Code Plugin Docs](https://code.claude.com/docs/en/plugins.md)
