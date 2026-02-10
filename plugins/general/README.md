# General Plugin

Language-agnostic agents that work across all technologies and programming languages.

## Available Agents

### Architecture & Design

- **architect.md**: Software Architecture Agent specializing in system design, architectural decisions, and technical planning. Provides guidance on architecture patterns, technology selection, and system structure regardless of the implementation language.

## Usage

General agents are technology-agnostic and can be used in any project:

```bash
# Install the architect agent
./scripts/sync-agents.sh
# Select: architect
```

These agents complement technology-specific agents by providing high-level guidance and planning before diving into implementation details.

## When to Use General Agents

Use general plugin agents when:
- Planning system architecture before implementation
- Making high-level technical decisions
- Designing system structure and component interactions
- Evaluating architectural patterns and approaches
- Need guidance that applies across programming languages

## Organization

General agents are kept separate from technology-specific plugins because:
- They don't depend on specific programming languages or frameworks
- They can be used alongside any technology plugin
- They focus on conceptual and architectural concerns
- They provide value at the planning and design phases
