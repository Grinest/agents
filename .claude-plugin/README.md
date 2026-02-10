# Claude Agents Marketplace

This is a plugin marketplace for Claude Code containing specialized agents and skills for development workflows.

## Installation

Add this marketplace to your Claude Code:

```bash
/plugin marketplace add juanpaconpa/claude-agents
```

## Available Plugins

### 🏗️ general
Language-agnostic agents for software architecture and system design.

**Install:**
```bash
/plugin install general@claude-agents
```

**Contains:**
- `architect` - Software architecture specialist for system design and planning

---

### 🐍 python-development
Python backend development agents and skills with Clean Architecture, FastAPI, and Celery.

**Install:**
```bash
/plugin install python-development@claude-agents
```

**Contains:**
- `backend-py` - Backend Python development with Clean Architecture
- `qa-backend-py` - QA and testing specialist for Python backend
- `reviewer-backend-py` - Code review agent for Python backend PRs
- `reviewer-library-py` - Code review agent for Python library projects
- `backend-py-celery` (skill) - FastAPI routes and Celery tasks development

---

### 📱 flutter-development
Flutter and Dart development agents for mobile app code review.

**Install:**
```bash
/plugin install flutter-development@claude-agents
```

**Contains:**
- `reviewer-flutter-app` - Code review agent for Flutter application PRs

---

## Usage

After installing plugins, agents and skills become available in Claude Code:

### Using Agents
Agents are automatically available based on your project context. Simply describe your task and Claude will use the appropriate agent.

### Using Skills
Skills can be invoked with the `/` prefix:

```bash
/backend-py-celery Create a new API endpoint for user authentication
```

## Browse Plugins

List all available plugins from this marketplace:

```bash
/plugin list
```

Show details of a specific plugin:

```bash
/plugin show python-development@claude-agents
```

## Updates

Check for plugin updates:

```bash
/plugin update python-development@claude-agents
```

Update all plugins from this marketplace:

```bash
/plugin update --marketplace claude-agents
```

## Contributing

To add new plugins to this marketplace, see [CONTRIBUTING.md](../CONTRIBUTING.md).

## License

MIT License - See [LICENSE](../LICENSE) for details.
